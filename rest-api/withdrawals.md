# Withdrawals

`POST /v1/withdraw_request` is **not** an ordinary RWA endpoint. It requires both:

1. **RWA headers** (the same as order placement)
2. **A wallet EIP-712 signature** (`primaryType = Withdraw`) that uses a **different domain** from account opening and key binding

| EIP-712 Domain | Account opening / key binding | Withdrawal (this endpoint) |
|----------------|-------------------------------|----------------------------|
| `name` | `DexDomain` | `Orderly` (protocol-required; not a product brand) |
| `version` | `1` | `1` |
| `chainId` | `196` | `196` |
| `verifyingContract` | `0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC` | **`0x6F7a338F2aA472838dEFD3283eB360d4Dff5D203`** |

Do not use the account-opening `0xCcCC…` address or a per-chain vault address for this signature domain. An incorrect address returns `code=29` with `Verify contract is invalid`.

> **Production transaction:** A successful request initiates a real withdrawal. Verify the receiver, token, amount, nonce, signing domain, and account before submission.

**Steps**

1. `GET /v1/withdraw_nonce` (RWA) → `data.withdraw_nonce`
2. Sign the EIP-712 `Withdraw` message with your wallet (when signing, `amount` is a **uint256 integer**; USDC has 6 decimals, so `1 USDC = 1000000`)
3. `POST /v1/withdraw_request`: RWA headers + JSON. On submission `amount` must be a **string**, and `message` carries an additional `"chainType":"EVM"` field (not part of the EIP-712 payload)

**EIP-712 message**

```
brokerId: string          # rwaperp_xyz
chainId: uint256          # 196
receiver: address         # must equal the account-opening wallet
token: string             # USDC
amount: uint256           # smallest unit
withdrawNonce: uint64
timestamp: uint64         # milliseconds
```

**Get the withdrawal nonce**

```http
GET /v1/withdraw_nonce
```

**Submit the withdrawal**

```http
POST /v1/withdraw_request
```

**Request body**

```json
{
  "message": {
    "brokerId": "rwaperp_xyz",
    "chainId": 196,
    "receiver": "0xYourWallet",
    "token": "USDC",
    "amount": "1000000",
    "withdrawNonce": 1,
    "timestamp": 1787130000000,
    "chainType": "EVM"
  },
  "signature": "0x...",
  "userAddress": "0xYourWallet",
  "verifyingContract": "0x6F7a338F2aA472838dEFD3283eB360d4Dff5D203"
}
```

The POST body string must be byte-for-byte identical to what the RWA signature covers. Funds are transferred after on-chain confirmation. A successful response from this endpoint means only that the withdrawal request has been accepted.

```python
import time
from eth_account import Account
from eth_account.messages import encode_typed_data

LEDGER = "0x6F7a338F2aA472838dEFD3283eB360d4Dff5D203"
WITHDRAW = [
    {"name": "brokerId", "type": "string"},
    {"name": "chainId", "type": "uint256"},
    {"name": "receiver", "type": "address"},
    {"name": "token", "type": "string"},
    {"name": "amount", "type": "uint256"},
    {"name": "withdrawNonce", "type": "uint64"},
    {"name": "timestamp", "type": "uint64"},
]

def withdraw_usdc(client, evm_pk: str, qty_raw: int = 1_000_000):
    """qty_raw: USDC smallest unit. Requires a B2BClient with signed / public methods."""
    user = Account.from_key(evm_pk).address
    nonce = int(client.signed("GET", "/v1/withdraw_nonce")["data"]["withdraw_nonce"])
    ts = int(time.time() * 1000)
    sign_msg = {
        "brokerId": "rwaperp_xyz", "chainId": 196, "receiver": user,
        "token": "USDC", "amount": qty_raw, "withdrawNonce": nonce, "timestamp": ts,
    }
    typed = {
        "types": {
            "EIP712Domain": [
                {"name": "name", "type": "string"}, {"name": "version", "type": "string"},
                {"name": "chainId", "type": "uint256"}, {"name": "verifyingContract", "type": "address"},
            ],
            "Withdraw": WITHDRAW,
        },
        "primaryType": "Withdraw",
        "domain": {"name": "Orderly", "version": "1", "chainId": 196, "verifyingContract": LEDGER},  # protocol-required domain name
        "message": sign_msg,
    }
    sig = "0x" + Account.from_key(evm_pk).sign_message(encode_typed_data(full_message=typed)).signature.hex()
    body = {
        "message": {**sign_msg, "amount": str(qty_raw), "chainType": "EVM"},
        "signature": sig, "userAddress": user, "verifyingContract": LEDGER,
    }
    return client.signed("POST", "/v1/withdraw_request", body)
```

**Common errors**

| code | message | Cause |
|------|---------|-------|
| `29` | `Verify contract is invalid` | `verifyingContract` is not the on-chain domain address in the table above |
| `5` | `Amount error` | Invalid amount or insufficient withdrawable USDC |
