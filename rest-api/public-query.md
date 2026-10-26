# Public Query API

Send `POST /v1/public/query` with a body in the form `{"type":"<query_type>", ...}`. Authentication is not required.

**Request example**

```bash
# Default host. VIP: https://api-vip.rwaperp.xyz (same path).
# To-B partners: contact RWA Perp to obtain a dedicated Base URL first.
curl -s -X POST "https://api-trade.rwaperp.xyz/v1/public/query" \
  -H "Content-Type: application/json" \
  -d '{"type":"marketDetail","symbol":"PERP_ETH_USDC"}'
```

The response `data` includes the requested symbol and the following datasets:

| Field | Included fields |
|-------|-----------------|
| `market_info` | `mark_price`, `index_price`, `24h_volume`, `open_interest` |
| `orderbook` | `asks`, `bids`; each entry contains price and quantity |
| `recent_trades` | `side`, `executed_price`, `executed_quantity` |
| `candles` | `open`, `high`, `low`, `close`, `volume`, `timestamp` |

**Account-state request body**

```json
{"type":"accountState","address":"0x...","broker_id":"rwaperp_xyz"}
```

Authentication is not required. The response `data` contains `address` and an `accounts` array with fields including `account_id`, `free_collateral`, and `margin_ratio`.

| type | Additional request fields | Response `data` highlights |
|------|---------------------------|----------------------------|
| `marketSummary` | Optional `symbols[]` | Snapshot across multiple pairs |
| `marketDetail` | `symbol` | Market data + depth + trades + candles bundle |
| `orderbook` / `candles` / `marketTrades` | `symbol` + per-type parameters | The requested dataset |
| `accountState` | `address`, `broker_id` | Account summary |
| `openOrders` / `historicalOrders` | `address`, `broker_id` | `{ rows, next_cursor }` |
| `positionContext` | `address`, `broker_id`, `symbol` | `{ position, open_orders, market, account_summary }` |
| `agentContext` | `address`, ... | Account + positions + market data bundle |
| `rateLimitStatus` | None | Quota for this IP |
