# Get market trades

`GET /v1/public/market_trades`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Get the latest market trades.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `symbol` | query | string | Yes | Symbol to query, for example `PERP_BTC_USDC`. |
| `limit` | query | integer | No | Numbers of trades want to query. |

## Responses

### HTTP 200

Success

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.rows` | array<object> | Yes | — |
| `data.rows[].symbol` | string | Yes | Example: `PERP_ETH_USDC` |
| `data.rows[].side` | string | Yes | Example: `BUY` |
| `data.rows[].executed_price` | number | Yes | Example: `2050` |
| `data.rows[].executed_quantity` | number | Yes | Example: `1` |
| `data.rows[].executed_timestamp` | number | Yes | Example: `1683878609166` |
