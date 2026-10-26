# Get historical price list for all symbols

`GET /v1/public/market_info/history_charts`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Return the close price for all symbols

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `time_interval` | query | string | No | — |

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
| `data.rows[].price_list` | array<object> | No | — |
| `data.rows[].price_list[].ts` | number | No | Example: `1702989203989` |
| `data.rows[].price_list[].price` | number | No | Example: `31000` |
