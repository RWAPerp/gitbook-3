# End-to-end trading script

Save this example as `trading-mainline.py`. Complete [account onboarding](../authentication/onboarding.md) first, then provide `RWA_ACCOUNT_ID`, `RWA_API_KEY`, and `RWA_SECRET_B58` through environment variables. By default, the script runs read-only queries.

> **Production environment:** Default REST is `https://api-trade.rwaperp.xyz`. Set `B2B_API_BASE=https://api-vip.rwaperp.xyz` for the VIP host (same paths and `RWA-*` signing). **To-B partners:** contact RWA Perp to obtain a dedicated Base URL before using either host. Passing `--with-order` submits and cancels a real order and requires sufficient USDC for the symbol's current `min_notional`.

For an existing trading account, the script also accepts `EVM_PRIVATE_KEY` as a fallback when the `RWA_*` variables are absent. This fallback binds a newly generated API key for the current process; it does not create an account or persist the generated credentials.

```python
#!/usr/bin/env python3
"""RWA Perp B2B trading workflow."""

from __future__ import annotations

import argparse
import base64
import json
import os
import sys
import time
import urllib.error
import urllib.parse
import urllib.request
import uuid
from decimal import Decimal, ROUND_UP
from typing import Any

try:
    import base58
    from nacl.signing import SigningKey
except ImportError as e:
    raise SystemExit("pip install base58 pynacl") from e

API_BASE = os.environ.get("B2B_API_BASE", "https://api-trade.rwaperp.xyz").rstrip("/")
WS_BASE = API_BASE.replace("https://", "wss://")
BROKER_ID = "rwaperp_xyz"
DEFAULT_SYMBOL = "PERP_ETH_USDC"


class B2BClient:
    def __init__(self, account_id: str, api_key: str, secret_b58: str) -> None:
        self.account_id = account_id
        self.api_key = api_key
        self._signing = SigningKey(base58.b58decode(secret_b58))

    @classmethod
    def from_env(cls) -> B2BClient:
        account_id = os.environ.get("RWA_ACCOUNT_ID", "")
        api_key = os.environ.get("RWA_API_KEY", "")
        secret_b58 = os.environ.get("RWA_SECRET_B58", "")
        if account_id and api_key and secret_b58:
            return cls(account_id, api_key, secret_b58)
        evm_pk = os.environ.get("EVM_PRIVATE_KEY", "")
        if not evm_pk:
            raise SystemExit("Set RWA_ACCOUNT_ID+RWA_API_KEY+RWA_SECRET_B58 or EVM_PRIVATE_KEY")
        # X Layer (196) only; any other chainId will fail API-key binding
        return cls.from_wallet(evm_pk, int(os.environ.get("CHAIN_ID", "196")))

    @classmethod
    def from_wallet(cls, evm_pk: str, chain_id: int) -> B2BClient:
        from cryptography.hazmat.primitives.asymmetric.ed25519 import Ed25519PrivateKey
        from eth_account import Account
        from eth_account.messages import encode_typed_data

        verifying = "0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC"
        domain_fields = [
            {"name": "name", "type": "string"},
            {"name": "version", "type": "string"},
            {"name": "chainId", "type": "uint256"},
            {"name": "verifyingContract", "type": "address"},
        ]
        user = Account.from_key(evm_pk).address

        def api(method: str, path: str, body: dict | None = None) -> dict:
            data = json.dumps(body).encode() if body is not None else None
            req = urllib.request.Request(
                f"{API_BASE}{path}",
                data=data,
                headers={"Content-Type": "application/json"} if data else {},
                method=method,
            )
            with urllib.request.urlopen(req, timeout=30) as resp:
                return json.loads(resp.read())

        res = api("GET", f"/v1/get_account?address={user}&broker_id={BROKER_ID}")
        if not res.get("success"):
            raise SystemExit(f"get_account failed; complete account onboarding first: {res}")
        account_id = res["data"]["account_id"]

        priv = Ed25519PrivateKey.generate()
        public_key = "ed25519:" + base58.b58encode(priv.public_key().public_bytes_raw()).decode()
        secret_b58 = base58.b58encode(priv.private_bytes_raw()).decode()

        ts = int(time.time() * 1000)
        sign_msg = {
            "brokerId": BROKER_ID,
            "key": public_key,
            "scope": "read,trading",
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
        typed = {
            "types": {"EIP712Domain": domain_fields, "AddDexApiKey": fields},
            "primaryType": "AddDexApiKey",
            "domain": {
                "name": "DexDomain",
                "version": "1",
                "chainId": chain_id,
                "verifyingContract": verifying,
            },
            "message": sign_msg,
        }
        sig = "0x" + Account.from_key(evm_pk).sign_message(encode_typed_data(full_message=typed)).signature.hex()
        bind = api(
            "POST",
            "/v1/dex_api_key",
            {"message": {**sign_msg, "chainType": "EVM"}, "signature": sig, "userAddress": user},
        )
        if not bind.get("success"):
            raise SystemExit(f"dex_api_key failed: {bind}")
        print(f"[onboard] wallet={user} account_id={account_id[:18]}...")
        return cls(account_id, public_key, secret_b58)

    def public_get(self, path: str) -> dict:
        with urllib.request.urlopen(f"{API_BASE}{path}", timeout=30) as resp:
            return json.loads(resp.read())

    def signed(self, method: str, path: str, body: dict | None = None) -> dict:
        body_str = json.dumps(body, separators=(",", ":")) if body is not None else ""
        ts = str(int(time.time() * 1000))
        sig = base64.urlsafe_b64encode(
            self._signing.sign(f"{ts}{method.upper()}{path}{body_str}".encode()).signature
        ).decode().rstrip("=")
        data = body_str.encode() if body_str and method.upper() in ("POST", "PUT", "DELETE") else None
        req = urllib.request.Request(
            f"{API_BASE}{path}",
            data=data,
            headers={
                "RWA-Account-Id": self.account_id,
                "RWA-Api-Key": self.api_key,
                "RWA-Timestamp": ts,
                "RWA-Signature": sig,
                "Content-Type": "application/json",
            },
            method=method.upper(),
        )
        try:
            with urllib.request.urlopen(req, timeout=30) as resp:
                return json.loads(resp.read())
        except urllib.error.HTTPError as e:
            raw = e.read().decode()
            try:
                return json.loads(raw)
            except json.JSONDecodeError:
                raise SystemExit(f"{method} {path} -> HTTP {e.code}: {raw}") from e

    def private_ws_url(self) -> str:
        ts = str(int(time.time() * 1000))
        sign = base64.urlsafe_b64encode(self._signing.sign(ts.encode()).signature).decode().rstrip("=")
        q = urllib.parse.urlencode({"rwa_api_key": self.api_key, "rwa_timestamp": ts, "rwa_sign": sign})
        return f"{WS_BASE}/ws/private/v2/ws/private/stream/{self.account_id}?{q}"


def round_step(value: float, step: float) -> float:
    d, s = Decimal(str(value)), Decimal(str(step))
    return float((d / s).to_integral_value(rounding=ROUND_UP) * s)


def ok(name: str, res: dict) -> None:
    if not res.get("success"):
        raise SystemExit(f"[FAIL] {name}: {json.dumps(res, ensure_ascii=False)[:400]}")
    print(f"[OK] {name}")


def step_ws_public(client: B2BClient, symbol: str) -> None:
    import websocket

    url = f"{WS_BASE}/ws/public/ws/stream/{client.account_id}"
    ws = websocket.create_connection(url, timeout=15)
    ws.settimeout(10)
    try:
        ws.send(json.dumps({"event": "subscribe", "topic": f"{symbol}@ticker"}))
        ticker_data = None
        for _ in range(8):
            msg = json.loads(ws.recv())
            if msg.get("event") == "ping":
                ws.send(json.dumps({"event": "pong"}))
                continue
            if msg.get("event") == "subscribe":
                if not msg.get("success"):
                    raise SystemExit(f"[FAIL] WS public subscribe: {msg}")
                continue
            if msg.get("topic") == f"{symbol}@ticker" and "data" in msg:
                ticker_data = msg["data"]
                break
        if ticker_data is None:
            raise SystemExit("[FAIL] WS public: no ticker data")
        print(f"[OK] WS public {symbol}@ticker close={ticker_data.get('close')}")
    finally:
        ws.close()


def step_ws_private(client: B2BClient) -> None:
    import websocket

    ws = websocket.create_connection(client.private_ws_url(), timeout=15)
    ws.settimeout(10)
    try:
        ws.send(json.dumps({"event": "subscribe", "topic": "executionreport"}))
        subscribed = False
        for _ in range(8):
            msg = json.loads(ws.recv())
            if msg.get("event") == "ping":
                ws.send(json.dumps({"event": "pong"}))
                continue
            if msg.get("event") == "subscribe":
                if not msg.get("success"):
                    raise SystemExit(f"[FAIL] WS private subscribe: {msg}")
                subscribed = True
                break
        if not subscribed:
            raise SystemExit("[FAIL] WS private: no subscribe ack")
        print("[OK] WS private executionreport")
    finally:
        ws.close()


def step_order_cycle(client: B2BClient, symbol: str, market: dict[str, Any]) -> None:
    info = client.public_get("/v1/public/info")
    ok("GET /v1/public/info", info)
    row = next(r for r in info["data"]["rows"] if r["symbol"] == symbol)
    holding = client.signed("GET", "/v1/client/holding")
    ok("GET /v1/client/holding (pre-order)", holding)
    usdc = next((h for h in holding["data"]["holding"] if h["token"] == "USDC"), None)
    free = float(usdc["holding"]) if usdc else 0.0
    min_notional = float(row["min_notional"])
    if free < min_notional:
        raise SystemExit(
            f"[SKIP] --with-order needs free USDC >= {min_notional} (have {free:.4f})"
        )
    mark = float(market["mark_price"])
    price = round_step(mark * 0.5, row["quote_tick"])
    qty = round_step(max(float(row["base_min"]), min_notional / price * 1.05), row["base_tick"])
    order_body = {
        "symbol": symbol,
        "side": "BUY",
        "order_type": "POST_ONLY",
        "order_price": price,
        "order_quantity": qty,
        "client_order_id": f"rwa-mainline-{uuid.uuid4().hex[:12]}",
    }
    place = client.signed("POST", "/v1/order", order_body)
    ok("POST /v1/order", place)
    order_id = place["data"]["order_id"]
    ok("GET /v1/orders?status=NEW", client.signed("GET", f"/v1/orders?symbol={symbol}&status=NEW"))
    cancel_path = f"/v1/order?symbol={symbol}&order_id={order_id}"
    ok(f"DELETE {cancel_path}", client.signed("DELETE", cancel_path))


def main() -> int:
    p = argparse.ArgumentParser(description="RWA Perp B2B trading workflow")
    p.add_argument("--symbol", default=os.environ.get("B2B_SYMBOL", DEFAULT_SYMBOL))
    p.add_argument("--with-order", action="store_true")
    args = p.parse_args()
    client = B2BClient.from_env()
    symbol = args.symbol
    print(f"[info] account_id={client.account_id[:18]}... symbol={symbol}")
    evm_pk = os.environ.get("EVM_PRIVATE_KEY")
    if evm_pk:
        from eth_account import Account
        addr = Account.from_key(evm_pk).address
        ok("GET /v1/get_account", client.public_get(f"/v1/get_account?address={addr}&broker_id={BROKER_ID}"))
    ok("GET /v1/client/info", client.signed("GET", "/v1/client/info"))
    market = client.public_get(f"/v1/public/futures/{symbol}")
    ok(f"GET /v1/public/futures/{symbol}", market)
    market = market["data"]
    step_ws_public(client, symbol)
    ok("GET /v1/client/holding", client.signed("GET", "/v1/client/holding"))
    ok("GET /v1/positions", client.signed("GET", "/v1/positions"))
    ok("GET /v1/orders", client.signed("GET", f"/v1/orders?symbol={symbol}&status=NEW"))
    step_ws_private(client)
    if args.with_order:
        step_order_cycle(client, symbol, market)
    else:
        print("[skip] order/cancel (pass --with-order; requires sufficient USDC for min_notional)")
    print("\n=== trading workflow OK ===")
    return 0


if __name__ == "__main__":
    sys.exit(main())
```
