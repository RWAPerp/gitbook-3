# Get price info for all symbols

`GET /v1/public/market_info/price_changes`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Return the current price and the price 5m, 30m, 1h, 24h, 3d, 7d, 30d ago for all symbols

Examples:

- Now: 11:06:30 (2024-07-11)  

- 5m: 11:01:00 (2024-07-11)

- 30m: 10:36:00 (2024-07-11)

- 1h: 10:06:00 (2024-07-11)

- 4h: 07:06:00 (2024-07-11)

- 24h: 11:06:00 (2024-07-10)

- 3d: 00:00:00 (2024-07-08)

- 7d: 00:00:00 (2024-07-04)

- 30d: 00:00:00 (2024-06-11)

## Parameters

No fields are defined in the published schema.

## Responses

### HTTP 200

Success

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.rows` | array<object> | Yes | — |
| `data.rows[].symbol` | string | No | Example: `PERP_BTC_USDC` |
| `data.rows[].last_price` | number | No | Example: `31000` |
| `data.rows[].5m` | number | No | Example: `31000` |
| `data.rows[].30m` | number | No | Example: `31000` |
| `data.rows[].1h` | number | No | Example: `31000` |
| `data.rows[].4h` | number | No | Example: `31000` |
| `data.rows[].24h` | number | No | Example: `31000` |
| `data.rows[].3d` | number | No | Example: `31000` |
| `data.rows[].7d` | number | No | Example: `31000` |
| `data.rows[].30d` | number | No | — |
