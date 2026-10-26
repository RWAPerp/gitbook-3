# Public streams

**Request** (use an `account_id` returned by `GET /v1/get_account` in the path)

```
wss://api-trade.rwaperp.xyz/ws/public/ws/stream/{account_id}
# VIP edge (same feed): wss://api-vip.rwaperp.xyz/ws/public/ws/stream/{account_id}
# To-B partners: contact RWA Perp to obtain a dedicated Base URL first.
→ {"event":"subscribe","topic":"PERP_ETH_USDC@ticker"}
```

**Response**

Subscription acknowledgment:

```json
{"event":"subscribe","success":true,"ts":1781628477334}
```

Ticker update:

```json
{"topic":"PERP_ETH_USDC@ticker","ts":1781628478000,"data":{"symbol":"PERP_ETH_USDC","open":1840.86,"close":1777.67,"high":1844.78,"low":1758.29,"volume":15117.5,"count":16769}}
```
