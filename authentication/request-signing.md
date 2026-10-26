# Request signing

| | REST | Private WS |
|---|------|------------|
| String to sign | `{timestamp}{METHOD}{path}{body}` | `{timestamp}` |
| Sent as | `RWA-*` headers | `rwa_api_key` / `rwa_timestamp` / `rwa_sign` query parameters |
| Notes | `path` includes the query string; body is `""` for GET/DELETE; the POST body must match the signed bytes exactly | On receiving `{"event":"ping"}` you must reply `{"event":"pong"}` |

```python
import base64, json, time, urllib.parse, urllib.request, base58, websocket
from nacl.signing import SigningKey

ACCOUNT_ID, SECRET_B58 = "0x...", "..."
# Default REST. VIP: "https://api-vip.rwaperp.xyz" (same paths and RWA-* signing).
# To-B partners: contact RWA Perp to obtain a dedicated Base URL first.
BASE = "https://api-trade.rwaperp.xyz"
# WS host can be the same edge host as REST (default or VIP).
WS_BASE = BASE.replace("https://", "wss://")

signing = SigningKey(base58.b58decode(SECRET_B58))
pub = "ed25519:" + base58.b58encode(signing.verify_key.encode()).decode()

def signed_request(method: str, path: str, body: str = ""):
    ts = str(int(time.time() * 1000))
    sig = base64.urlsafe_b64encode(
        signing.sign(f"{ts}{method.upper()}{path}{body}".encode()).signature
    ).decode().rstrip("=")
    req = urllib.request.Request(
        BASE + path,
        data=body.encode() if body and method.upper() in ("POST", "PUT") else None,
        headers={"RWA-Account-Id": ACCOUNT_ID, "RWA-Api-Key": pub,
                 "RWA-Timestamp": ts, "RWA-Signature": sig, "Content-Type": "application/json"},
        method=method.upper(),
    )
    with urllib.request.urlopen(req, timeout=30) as resp:
        return json.loads(resp.read())

def private_ws_url(account_id: str) -> str:
    ts = str(int(time.time() * 1000))
    sign = base64.urlsafe_b64encode(signing.sign(ts.encode()).signature).decode().rstrip("=")
    q = urllib.parse.urlencode({"rwa_api_key": pub, "rwa_timestamp": ts, "rwa_sign": sign})
    return f"{WS_BASE}/ws/private/v2/ws/private/stream/{account_id}?{q}"

# signed_request("GET", "/v1/client/info")
# ws = websocket.create_connection(f"{WS_BASE}/ws/public/ws/stream/{ACCOUNT_ID}")
# ws.send(json.dumps({"event": "subscribe", "topic": "PERP_ETH_USDC@ticker"}))
```

