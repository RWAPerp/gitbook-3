# Get algo order by client_order_id

`GET /v1/algo/client/order/{client_order_id}`

**Authentication:** RWA

**Rate limit:** 10 requests per 1 second

## Description

Get details of a single algo order by `client_order_id`.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `client_order_id` | path | string | Yes | client_order_id of the order |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/algo/client/order/{client_order_id}{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.algo_order_id` | number | Yes | Example: `168400010` |
| `data.algo_status` | string | Yes | Example: `NEW` |
| `data.algo_type` | string | Yes | Example: `STOP` |
| `data.fee_asset` | string | Yes | Example: `USDC` |
| `data.is_triggered` | string | Yes | Example: `false` |
| `data.order_tag` | string | Yes | Full tag stored on the algo order. Current custom-fee tags use `enum:<owning_broker_id>:<enum_id>`. Historical orders may contain a legacy `enum:<enum_id>` tag; do not rewrite it.
 Example: `enum:broker_b:GRID_PRO` |
| `data.parent_algo_order_id` | number | Yes | Example: `0` |
| `data.quantity` | number | Yes | Example: `5.5` |
| `data.root_algo_order_id` | number | Yes | Example: `168400010` |
| `data.root_algo_order_status` | string | Yes | Example: `NEW` |
| `data.side` | string | Yes | Example: `BUY` |
| `data.symbol` | string | Yes | Example: `PERP_NEAR_USDC` |
| `data.margin_mode` | string | No | Example: `CROSS` |
| `data.executed_quantity` | number | No | Example: `0` |
| `data.total_executed_quantity` | number | Yes | Example: `0` |
| `data.total_fee` | number | Yes | Aggregate fee across executed trades, including any custom trading fees. Use trade-level fields for reconciliation; this value is not a builder or affiliate payout basis. Example: `0` |
| `data.trigger_price` | number | Yes | Example: `2.5` |
| `data.trigger_price_type` | string | Yes | Example: `MARK_PRICE` |
| `data.type` | string | Yes | Example: `MARKET` |
| `data.created_time` | string | Yes | Example: `1702871974317` |
| `data.updated_time` | string | Yes | Example: `1702871974317` |
| `data.visible_quantity` | number | Yes | Example: `5.5` |
| `data.realized_pnl` | number | No | Example: `0.0` |
| `data.child_orders` | array<object> | No | Array of `AlgoOrder` |
