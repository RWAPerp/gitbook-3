# Get liquidated positions by liquidator

`GET /v1/client/liquidator_liquidations`

**Authentication:** RWA

**Rate limit:** 10 requests per 1 second per IP address

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `symbol` | query | string | No | — |
| `start_t` | query | number | No | — |
| `end_t` | query | number | No | — |
| `page` | query | number | No | start from 1 |
| `size` | query | number | No | — |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/client/liquidator_liquidations{body}` → URL-safe Base64 without trailing `=` |

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
| `data.rows[].liquidation_id` | integer | No | Example: `1728` |
| `data.rows[].timestamp` | number | No | Example: `1685154032762` |
| `data.rows[].type` | string | No | Example: `liquidated` |
| `data.rows[].assigned` | number | No | 1 assigned to SPV or MM; 0 means claimed Example: `1` |
| `data.rows[].positions_by_perp` | array<object> | No | — |
| `data.rows[].positions_by_perp[].symbol` | string | No | Example: `PERP_BTC_USDC` |
| `data.rows[].positions_by_perp[].abs_liquidator_fee` | number | No | Example: `1.152279` |
| `data.rows[].positions_by_perp[].cost_position_transfer` | number | No | Example: `21.002786` |
| `data.rows[].positions_by_perp[].liquidator_fee` | number | No | Example: `0.006` |
| `data.rows[].positions_by_perp[].position_qty` | number | No | Example: `0.00017` |
| `data.rows[].positions_by_perp[].transfer_price` | number | No | Example: `123545.8` |
