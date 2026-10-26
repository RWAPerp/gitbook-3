# Get position history

`GET /v1/position_history`

**Authentication:** RWA

**Rate limit:** 10 requests per 1 second per user

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `symbol` | query | string | No | — |
| `limit` | query | number | Yes | — |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/position_history{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.rows` | array<object> | No | — |
| `data.rows[].position_id` | number | No | Example: `1` |
| `data.rows[].status` | string | No | Example: `closed` |
| `data.rows[].type` | string | No | Example: `liquidated` |
| `data.rows[].symbol` | string | No | Example: `PERP_ETH_USDC` |
| `data.rows[].avg_open_price` | number | No | Example: `61016.1` |
| `data.rows[].avg_close_price` | number | No | Example: `61016.1` |
| `data.rows[].max_position_qty` | number | No | Example: `56.6` |
| `data.rows[].closed_position_qty` | number | No | Example: `56.6` |
| `data.rows[].side` | string | No | Example: `LONG` |
| `data.rows[].trading_fee` | number | No | Example: `0.015` |
| `data.rows[].accumulated_funding_fee` | number | No | Example: `0.11` |
| `data.rows[].insurance_fund_fee` | number | No | Example: `0` |
| `data.rows[].liquidator_fee` | number | No | Example: `0` |
| `data.rows[].liquidation_id` | number | No | — |
| `data.rows[].realized_pnl` | number | No | Example: `-9.09691927314905` |
| `data.rows[].open_timestamp` | number | No | Example: `1685429350571` |
| `data.rows[].close_timestamp` | number | No | Example: `1685429350571` |
| `data.rows[].last_update_timestamp` | number | No | Example: `1685429350571` |
| `data.rows[].leverage` | integer | No | Example: `10` |
| `data.rows[].margin_mode` | string | No | Example: `CROSS` |
