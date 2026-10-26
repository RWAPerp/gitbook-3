# Get order by client_order_id

`GET /v1/client/order/{client_order_id}`

**Authentication:** RWA

**Rate limit:** 10 requests per 1 second

## Description

Get details of a single order by `client_order_id`.

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
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/client/order/{client_order_id}{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.order_id` | number | Yes | Example: `78151` |
| `data.user_id` | number | Yes | Example: `12345` |
| `data.price` | number | Yes | Example: `0.67772` |
| `data.type` | string | Yes | Example: `LIMIT` |
| `data.quantity` | number | Yes | Example: `20` |
| `data.amount` | number | Yes | Example: `10` |
| `data.executed_quantity` | number | No | Example: `20` |
| `data.total_executed_quantity` | number | Yes | Example: `20` |
| `data.visible_quantity` | number | Yes | Example: `1` |
| `data.visible` | number | No | Example: `1` |
| `data.symbol` | string | Yes | Example: `PERP_WOO_USDC` |
| `data.side` | string | Yes | Example: `BUY` |
| `data.status` | string | Yes | NEW / FILLED / PARTIAL_FILLED / CANCELLED Example: `FILLED` |
| `data.total_fee` | number | Yes | Aggregate fee across executed trades, including any custom trading fees. Use trade-level fields for reconciliation; this value is not a builder or affiliate payout basis. Example: `0.5` |
| `data.fee_asset` | string | Yes | Example: `WOO` |
| `data.client_order_id` | number | Yes | Example: `1` |
| `data.average_executed_price` | number | Yes | Example: `0.67772` |
| `data.created_time` | number | Yes | Example: `1653563963000` |
| `data.updated_time` | number | Yes | Example: `1653564213000` |
| `data.realized_pnl` | number | Yes | Example: `0.0` |
| `data.executed` | number | No | Example: `20` |
| `data.reduce_only` | boolean | No | — |
| `data.order_tag` | string | No | Full tag stored on the order. Current custom-fee tags use `enum:<owning_broker_id>:<enum_id>`. Historical orders may contain a legacy `enum:<enum_id>` tag; do not rewrite it.
 Example: `enum:broker_b:GRID_PRO` |
| `data.margin_mode` | string | No | Example: `CROSS` |
