# Choose an endpoint

## Core endpoints

| Endpoint | Request | Response `data` |
|----------|---------|-----------------|
| `GET /v1/public/info` | None | `{ rows: [{ symbol, base_tick, quote_tick, min_notional, ... }] }` |
| `GET /v1/public/market_trades` | query: `symbol`, `limit` | `{ rows: [{ side, executed_price, executed_quantity, ... }] }` |
| `POST /v1/public/query` | body: `{ type, ... }` | See [Public Query API](public-query.md) |
| `GET /v1/orders` | RWA; `symbol`, `status` (`NEW` returns resting orders only; use `FILLED`/`COMPLETED` for filled ones) | `{ rows, meta }` |
| `PUT /v1/order` | `order_price` / `order_quantity` only; cancel and re-place to change anything else | `{ status }` |
| `POST /v1/client/leverages` | RWA; `{ symbol, leverage }` | Leverage info |
| `GET /v1/asset/history` | RWA; `token`, `page`, `size` | `{ rows, meta }` |
| `POST /v1/withdraw_request` | Wallet + RWA, see [withdrawals](withdrawals.md) | Withdrawal acceptance result |

For a guided example of the primary trading operations, see the [trading workflow](trading-workflow.md).

---

## Endpoints by scenario

| Scenario | Method | Path | Auth |
|----------|--------|------|------|
| Look up account_id | GET | `/v1/get_account?address=&broker_id=rwaperp_xyz` | None |
| Bind API key | POST | `/v1/dex_api_key` | Wallet |
| Trading rules | GET | `/v1/public/info` | None |
| Market snapshot | GET | `/v1/public/futures` | None |
| Real-time market data | WS | Public stream + `subscribe` | None |
| Balance | GET | `/v1/client/holding` | RWA |
| Positions | GET | `/v1/positions` | RWA |
| Open orders | GET | `/v1/orders?status=NEW` | RWA |
| Filled orders | GET | `/v1/orders?status=FILLED` or `COMPLETED` | RWA |
| Individual fills | GET | `/v1/trades` | RWA |
| Place / cancel order | POST/DELETE | `/v1/order` | RWA (use VIP REST base `https://api-vip.rwaperp.xyz` when provisioned; To-B partners contact RWA Perp for a dedicated Base URL) |
| Change price or quantity | DELETE then POST | `/v1/order` | RWA (recommended). `PUT /v1/order` can only change `order_price` / `order_quantity` |
| Execution reports | WS | `executionreport` | RWA |
| Asset history | GET | `/v1/asset/history` | RWA |
| Withdrawal | GET + POST | `/v1/withdraw_nonce` → `/v1/withdraw_request` | RWA + wallet, see [withdrawals](withdrawals.md) |
| Change leverage | POST | `/v1/client/leverages` | RWA |
| Aggregated read-only | POST | `/v1/public/query` | None |

For request and response details, see the [trading workflow](trading-workflow.md).
