# Get lite positions info

`GET /v1/positions_lite`

**Authentication:** RWA

**Rate limit:** 10 requests per 1 second

## Description

Get lightweight positions information.

## Parameters

No fields are defined in the published schema.

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/positions_lite{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.rows` | array<object> | Yes | — |
| `data.rows[].IMR_withdraw_orders` | number | No | Example: `0.1` |
| `data.rows[].MMR_with_orders` | number | No | Example: `0.05` |
| `data.rows[].average_open_price` | number | No | Example: `27908.14386047` |
| `data.rows[].cost_position` | number | No | Example: `-139329.358492` |
| `data.rows[].est_liq_price` | number | No | Example: `117335.92899428` |
| `data.rows[].fee_24_h` | number | No | Example: `0` |
| `data.rows[].imr` | number | No | Example: `0.1` |
| `data.rows[].last_sum_unitary_funding` | number | No | Example: `70.38` |
| `data.rows[].mark_price` | number | No | Example: `27794.9` |
| `data.rows[].mmr` | number | No | Example: `0.05` |
| `data.rows[].pending_long_qty` | number | No | Example: `0` |
| `data.rows[].pending_short_qty` | number | No | Example: `0` |
| `data.rows[].pnl_24_h` | number | No | Example: `0` |
| `data.rows[].position_qty` | number | No | Example: `-5` |
| `data.rows[].settle_price` | number | No | Example: `27865.8716984` |
| `data.rows[].symbol` | string | No | Example: `PERP_BTC_USDC` |
| `data.rows[].margin_mode` | string | No | Example: `CROSS` |
| `data.rows[].margin` | number | No | Example: `5` |
| `data.rows[].timestamp` | number | No | Example: `1685429350571` |
| `data.rows[].updated_time` | number | No | Example: `1685429350571` |
| `data.rows[].unsettled_pnl` | number | No | Example: `354.858492` |
| `data.rows[].leverage` | integer | No | Example: `10` |
