# Get orders

`GET /v1/orders`

**Authentication:** RWA

**Rate limit:** 10 requests per 1 second

| Base | URL |
|------|-----|
| Default REST | `https://api-trade.rwaperp.xyz` |
| VIP REST | `https://api-vip.rwaperp.xyz` |

Same path, same `RWA-*` signing on both hosts. Prefer VIP when your integration is provisioned for the dedicated REST endpoint. **To-B partners:** contact RWA Perp to obtain a dedicated Base URL before using `api-trade`, `api-vip`, or any custom host.

## Description

Get orders by customized filters.

For filter by status, one can reference special bundled statuses below for ease of access of Open (ie `INCOMPLETE`) orders or `COMPLETED` orders.

- `INCOMPLETE` = `NEW` + `PARTIAL_FILLED`
- `COMPLETED` = `CANCELLED` + `FILLED`

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `symbol` | query | string | No | — |
| `side` | query | string | No | `BUY`/`SELL` |
| `order_type` | query | string | No | `LIMIT`/`MARKET` |
| `status` | query | string | No | `NEW`/`CANCELLED`/`PARTIAL_FILLED`/`FILLED`/`REJECTED`/`INCOMPLETE`/`COMPLETED` |
| `order_tag` | query | string | No | Filter by the full stored order tag, including a current-format `enum:<owning_broker_id>:<enum_id>` tag. |
| `start_t` | query | number | No | start time range that wish to query, noted the time stamp is 13-digits timestamp. |
| `end_t` | query | number | No | end time range that wish to query, noted the time stamp is 13-digits timestamp. |
| `page` | query | number | No | the page you wish to query. start from 1 |
| `size` | query | number | No | the page size you wish to query (max: 500) |
| `sort_by` | query | string | No | If empty:

Descending order by updated_time if user passed update_start_t or update_end_t; descending order by order_id if updated_time are the same;

Otherwise descending order by created_time; descending order by order_id if created_time are the same;


If not empty:

If sort_by == `CREATED_TIME_DESC`, descending order by created_time. Descending order by order_id if created_time are same;

If sort_by == `CREATED_TIME_ASC`, ascending order by created_time. Ascending order by order_id if created_time are same;

If sort_by == `UPDATED_TIME_DESC`, descending order by updated_time. Descending order by order_id if updated_time are same;

If sort_by == `UPDATED_TIME_ASC`, ascending order by updated_time. Ascending order by order_id if updated_time are same;
 |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/orders{body}` → URL-safe Base64 without trailing `=` |

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
| `data.rows[].order_id` | number | Yes | Example: `78151` |
| `data.rows[].user_id` | number | Yes | Example: `12345` |
| `data.rows[].price` | number | Yes | Example: `0.67772` |
| `data.rows[].type` | string | Yes | Example: `LIMIT` |
| `data.rows[].quantity` | number | Yes | Example: `20` |
| `data.rows[].amount` | number | Yes | Example: `10` |
| `data.rows[].executed_quantity` | number | No | Example: `20` |
| `data.rows[].total_executed_quantity` | number | Yes | Example: `20` |
| `data.rows[].visible_quantity` | number | Yes | Example: `1` |
| `data.rows[].visible` | number | No | Example: `1` |
| `data.rows[].symbol` | string | Yes | Example: `PERP_WOO_USDC` |
| `data.rows[].side` | string | Yes | Example: `BUY` |
| `data.rows[].status` | string | Yes | NEW / FILLED / PARTIAL_FILLED / CANCELLED Example: `FILLED` |
| `data.rows[].total_fee` | number | Yes | Aggregate fee across executed trades, including any custom trading fees. Use trade-level fields for reconciliation; this value is not a builder or affiliate payout basis. Example: `0.5` |
| `data.rows[].fee_asset` | string | Yes | Example: `WOO` |
| `data.rows[].client_order_id` | number | Yes | Example: `1` |
| `data.rows[].average_executed_price` | number | Yes | Example: `0.67772` |
| `data.rows[].created_time` | number | Yes | Example: `1653563963000` |
| `data.rows[].updated_time` | number | Yes | Example: `1653564213000` |
| `data.rows[].realized_pnl` | number | Yes | Example: `0.0` |
| `data.rows[].executed` | number | No | Example: `20` |
| `data.rows[].reduce_only` | boolean | No | — |
| `data.rows[].order_tag` | string | No | Full tag stored on the order. Current custom-fee tags use `enum:<owning_broker_id>:<enum_id>`. Historical orders may contain a legacy `enum:<enum_id>` tag; do not rewrite it.
 Example: `enum:broker_b:GRID_PRO` |
| `data.rows[].margin_mode` | string | No | Example: `CROSS` |
