# Get open interests for all symbols

`GET /v1/public/market_info/traders_open_interests`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Return the long/short Open Interests for all symbols (mm accounts are excluded).

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
| `data.rows[].long_oi` | number | No | Example: `31000` |
| `data.rows[].short_oi` | number | No | Example: `31000` |
