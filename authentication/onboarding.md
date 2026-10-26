# Account onboarding

## Onboarding checklist

1. Open an account → `POST /v1/register_dex_account` (or use "Enable Trading" on the web UI)
2. Look up `account_id` → `GET /v1/get_account?address=0x...&broker_id=rwaperp_xyz`
3. Generate an Ed25519 key pair → bind it with `POST /v1/dex_api_key`
4. Verify → `GET /v1/client/info` returns `success: true`
5. Run the trading example → save the returned API credentials, then follow the [trading workflow](../rest-api/trading-workflow.md)

```bash
pip install eth-account base58 cryptography pynacl websocket-client
export EVM_PRIVATE_KEY="0x..." CHAIN_ID=196   # X Layer only; do not change to another chainId
python3 onboard-b2b.py
```

**Chain restriction: X Layer only (`chainId = 196`). No other chain is supported.** Do not use Avalanche, Arbitrum, Base or any other `CHAIN_ID` when opening an account or binding a key.

---

## One-time onboarding script

Save as `onboard-b2b.py`. The script generates the key pair itself and prints `RWA_ACCOUNT_ID` / `RWA_API_KEY` / `RWA_SECRET_B58` when it finishes.

> **Credential security:** Run this script in a trusted environment. It reads the wallet private key and prints the generated API private key. Store the output securely, and do not include either private key in logs, source control, or support requests.

**Account-opening / key-binding endpoints** (the public-key field is **`key`**):

| Operation | Endpoint | EIP-712 `primaryType` | Notes |
|-----------|----------|----------------------|-------|
| Open account | `POST /v1/register_dex_account` | `Registration` | `chainType` is not part of the signature |
| Bind key | `POST /v1/dex_api_key` | `AddDexApiKey` | Public-key field is **`key`** |

When submitting, the message carries an **additional** `"chainType": "EVM"` field (not included in the signature). Domain: `DexDomain` + **`chainId: 196` (X Layer, the only supported chain)** + `verifyingContract: 0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC`.

```python
#!/usr/bin/env python3
"""RWA Perp B2B: register (if needed) + bind API key + verify REST."""

from __future__ import annotations

import argparse
import base64
import json
import os
import time
import urllib.request

try:
    import base58
    from cryptography.hazmat.primitives.asymmetric.ed25519 import Ed25519PrivateKey
    from eth_account import Account
    from eth_account.messages import encode_typed_data
    from nacl.signing import SigningKey
except ImportError as e:
    raise SystemExit("pip install eth-account base58 cryptography pynacl") from e

BROKER_ID = "rwaperp_xyz"
# Default REST. VIP: export B2B_API_BASE=https://api-vip.rwaperp.xyz
# To-B partners: contact RWA Perp to obtain a dedicated Base URL first.
API_BASE = os.environ.get("B2B_API_BASE", "https://api-trade.rwaperp.xyz")
VERIFYING = "0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC"
CHAIN_TYPE = "EVM"
SCOPE = "read,trading"
EIP712_DOMAIN = [
    {"name": "name", "type": "string"},
    {"name": "version", "type": "string"},
    {"name": "chainId", "type": "uint256"},
    {"name": "verifyingContract", "type": "address"},
]


def api(method: str, path: str, body: dict | None = None) -> dict:
    data = json.dumps(body).encode() if body is not None else None
    req = urllib.request.Request(
        f"{API_BASE.rstrip('/')}{path}",
        data=data,
        headers={"Content-Type": "application/json"} if data else {},
        method=method,
    )
    with urllib.request.urlopen(req, timeout=30) as resp:
        return json.loads(resp.read())


def dex_domain(chain_id: int) -> dict:
    return {"name": "DexDomain", "version": "1", "chainId": chain_id, "verifyingContract": VERIFYING}


def sign_eip712(primary_type: str, field_types: list, message: dict, chain_id: int, evm_pk: str) -> str:
    typed = {
        "types": {"EIP712Domain": EIP712_DOMAIN, primary_type: field_types},
        "primaryType": primary_type,
        "domain": dex_domain(chain_id),
        "message": message,
    }
    signed = Account.from_key(evm_pk).sign_message(encode_typed_data(full_message=typed))
    return "0x" + signed.signature.hex()


def post_wallet(endpoint: str, sign_msg: dict, api_msg: dict, signature: str, user_address: str) -> dict:
    return api("POST", endpoint, {
        "message": {**api_msg, "chainType": CHAIN_TYPE},
        "signature": signature,
        "userAddress": user_address,
    })


def get_account_id(address: str) -> str | None:
    res = api("GET", f"/v1/get_account?address={address}&broker_id={BROKER_ID}")
    return res.get("data", {}).get("account_id") if res.get("success") else None


def register_account(chain_id: int, evm_pk: str, user_address: str) -> str:
    nonce_res = api("GET", "/v1/registration_nonce")
    if not nonce_res.get("success"):
        raise SystemExit(f"registration_nonce failed: {nonce_res}")
    nonce = int(nonce_res["data"]["registration_nonce"])
    server_ts = int(nonce_res["timestamp"])
    sign_msg = {
        "brokerId": BROKER_ID,
        "chainId": chain_id,
        "timestamp": server_ts,
        "registrationNonce": nonce,
    }
    fields = [
        {"name": "brokerId", "type": "string"},
        {"name": "chainId", "type": "uint256"},
        {"name": "timestamp", "type": "uint64"},
        {"name": "registrationNonce", "type": "uint256"},
    ]
    sig = sign_eip712("Registration", fields, sign_msg, chain_id, evm_pk)
    res = post_wallet("/v1/register_dex_account", sign_msg, sign_msg, sig, user_address)
    if not res.get("success"):
        raise SystemExit(f"register_dex_account failed: {res}")
    return res["data"]["account_id"]


def gen_api_key() -> tuple[str, str]:
    priv = Ed25519PrivateKey.generate()
    seed = priv.private_bytes_raw()
    pub = priv.public_key().public_bytes_raw()
    return "ed25519:" + base58.b58encode(pub).decode(), base58.b58encode(seed).decode()


def bind_api_key(public_key: str, chain_id: int, evm_pk: str, user_address: str) -> dict:
    ts = int(time.time() * 1000)
    sign_msg = {
        "brokerId": BROKER_ID,
        "key": public_key,
        "scope": SCOPE,
        "chainId": chain_id,
        "timestamp": ts,
        "expiration": ts + 365 * 24 * 60 * 60 * 1000,
    }
    fields = [
        {"name": "brokerId", "type": "string"},
        {"name": "chainId", "type": "uint256"},
        {"name": "key", "type": "string"},
        {"name": "scope", "type": "string"},
        {"name": "timestamp", "type": "uint64"},
        {"name": "expiration", "type": "uint64"},
    ]
    sig = sign_eip712("AddDexApiKey", fields, sign_msg, chain_id, evm_pk)
    return post_wallet("/v1/dex_api_key", sign_msg, sign_msg, sig, user_address)


def signed_get(account_id: str, secret_b58: str, path: str) -> dict:
    signing = SigningKey(base58.b58decode(secret_b58))
    pub = "ed25519:" + base58.b58encode(signing.verify_key.encode()).decode()
    ts = str(int(time.time() * 1000))
    sig = base64.urlsafe_b64encode(signing.sign(f"{ts}GET{path}".encode()).signature).decode().rstrip("=")
    req = urllib.request.Request(
        API_BASE + path,
        headers={
            "RWA-Account-Id": account_id,
            "RWA-Api-Key": pub,
            "RWA-Timestamp": ts,
            "RWA-Signature": sig,
        },
        method="GET",
    )
    with urllib.request.urlopen(req, timeout=30) as resp:
        return json.loads(resp.read())


def main() -> None:
    p = argparse.ArgumentParser(description="RWA Perp B2B onboarding")
    p.add_argument("--evm-private-key", default=os.environ.get("EVM_PRIVATE_KEY"))
    # X Layer (196) only; any other chainId will fail account opening / key binding
    p.add_argument("--chain-id", type=int, default=int(os.environ.get("CHAIN_ID", "196")))
    p.add_argument("--skip-bind", action="store_true", help="Only register / resolve account_id")
    args = p.parse_args()
    if not args.evm_private_key:
        raise SystemExit("Set EVM_PRIVATE_KEY or pass --evm-private-key")

    user = Account.from_key(args.evm_private_key).address
    print(f"wallet: {user}")

    account_id = get_account_id(user)
    if account_id:
        print(f"account_id (existing): {account_id}")
    else:
        print("registering...")
        account_id = register_account(args.chain_id, args.evm_private_key, user)
        print(f"account_id (new): {account_id}")

    if args.skip_bind:
        return

    public_key, secret_b58 = gen_api_key()
    print(f"binding API key: {public_key}")
    bind_res = bind_api_key(public_key, args.chain_id, args.evm_private_key, user)
    if not bind_res.get("success"):
        raise SystemExit(f"dex_api_key failed: {bind_res}")

    info = signed_get(account_id, secret_b58, "/v1/client/info")
    if not info.get("success"):
        raise SystemExit(f"verify failed: {info}")

    print("\n=== credentials (store securely) ===")
    print(f"RWA_ACCOUNT_ID={account_id}")
    print(f"RWA_API_KEY={public_key}")
    print(f"RWA_SECRET_B58={secret_b58}")
    print("\nREST verify: success")


if __name__ == "__main__":
    main()
```
