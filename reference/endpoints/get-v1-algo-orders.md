# Get algo orders

`GET /v1/algo/orders`

**Authentication:** RWA

**Rate limit:** 5 requests per 1 second

## Description

Get algo order details by customized filters.

For filter by status, one can reference special bundled statuses below for ease of access of Open (i.e `INCOMPLETE`) orders or `COMPLETED` orders.

`INCOMPLETE` = `NEW` + `PARTIAL_FILLED`


`COMPLETED` = `CANCELLED` + `FILLED`

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `symbol` | query | string | No | — |
| `order_type` | query | string | No | `LIMIT`/`MARKET` |
| `status` | query | string | No | `NEW`/`CANCELLED`/`PARTIAL_FILLED`/`FILLED`/`REJECTED`/`INCOMPLETE`/`COMPLETED` |
| `order_tag` | query | string | No | Filter by the full stored order tag, including a current-format `enum:<owning_broker_id>:<enum_id>` tag. |
| `start_t` | query | number | No | start time range that wish to query, noted the time stamp is 13-digits timestamp. |
| `end_t` | query | number | No | end time range that wish to query, noted the time stamp is 13-digits timestamp. |
| `page` | query | number | No | the page you wish to query. start from 1 |
| `size` | query | number | No | the page size you wish to query (max: 500) |
| `side` | query | string | No | `BUY`/`SELL` |
| `algo_type` | query | string | No | Supported types are `STOP`, `TPSL`, `positional_TPSL` |
| `is_triggered` | query | string | No | — |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/algo/orders{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.meta` | object | Yes | — |
| `data.meta.total` | integer | Yes | Example: `9` |
| `data.meta.records_per_page` | integer | Yes | Example: `25` |
| `data.meta.current_page` | integer | Yes | start from 1 Example: `1` |
| `data.rows` | array<object> | Yes | — |
| `data.rows[].algo_order_id` | number | Yes | Example: `168400010` |
| `data.rows[].algo_status` | string | Yes | Example: `NEW` |
| `data.rows[].algo_type` | string | Yes | Example: `STOP` |
| `data.rows[].fee_asset` | string | Yes | Example: `USDC` |
| `data.rows[].is_triggered` | string | Yes | Example: `false` |
| `data.rows[].order_tag` | string | Yes | Full tag stored on the algo order. Current custom-fee tags use `enum:<owning_broker_id>:<enum_id>`. Historical orders may contain a legacy `enum:<enum_id>` tag; do not rewrite it.
 Example: `enum:broker_b:GRID_PRO` |
| `data.rows[].parent_algo_order_id` | number | Yes | Example: `0` |
| `data.rows[].quantity` | number | Yes | Example: `5.5` |
| `data.rows[].root_algo_order_id` | number | Yes | Example: `168400010` |
| `data.rows[].root_algo_order_status` | string | Yes | Example: `NEW` |
| `data.rows[].side` | string | Yes | Example: `BUY` |
| `data.rows[].symbol` | string | Yes | Example: `PERP_NEAR_USDC` |
| `data.rows[].margin_mode` | string | No | Example: `CROSS` |
| `data.rows[].executed_quantity` | number | No | Example: `0` |
| `data.rows[].total_executed_quantity` | number | Yes | Example: `0` |
| `data.rows[].total_fee` | number | Yes | Aggregate fee across executed trades, including any custom trading fees. Use trade-level fields for reconciliation; this value is not a builder or affiliate payout basis. Example: `0` |
| `data.rows[].trigger_price` | number | Yes | Example: `2.5` |
| `data.rows[].trigger_price_type` | string | Yes | Example: `MARK_PRICE` |
| `data.rows[].type` | string | Yes | Example: `MARKET` |
| `data.rows[].created_time` | string | Yes | Example: `1702871974317` |
| `data.rows[].updated_time` | string | Yes | Example: `1702871974317` |
| `data.rows[].visible_quantity` | number | Yes | Example: `5.5` |
| `data.rows[].realized_pnl` | number | No | Example: `0.0` |
| `data.rows[].child_orders` | array<object> | No | Array of `AlgoOrder` |
