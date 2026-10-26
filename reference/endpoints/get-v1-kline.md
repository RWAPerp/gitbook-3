# Get kline

`GET /v1/kline`

**Authentication:** None

**Rate limit:** 10 requests per 1 second

## Description

Get the latest klines (OHLC) of the specified symbol.

Please note that for symbols with low trading activity, the kline might be generated through the mid price of the orderbook in addition to any executed trades on the platform.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `symbol` | query | string | Yes | — |
| `type` | query | string | Yes | 1m/5m/15m/30m/1h/4h/12h/1d/1w/1mon/1y |
| `limit` | query | number | No | Numbers of klines. Maximum of 1000 klines. |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.rows` | array<object> | Yes | — |
| `data.rows[].open` | number | Yes | Example: `66166.23` |
| `data.rows[].close` | number | Yes | Example: `66124.56` |
| `data.rows[].low` | number | Yes | Example: `66038.06` |
| `data.rows[].high` | number | Yes | Example: `66176.97` |
| `data.rows[].volume` | number | Yes | Example: `23.45528526` |
| `data.rows[].amount` | number | Yes | Example: `1550436.21725288` |
| `data.rows[].symbol` | string | Yes | Example: `PERP_BTC_USDC` |
| `data.rows[].type` | string | Yes | Example: `1m` |
| `data.rows[].start_timestamp` | integer | Yes | Unix epoch time in milliseconds Example: `1636388220000` |
| `data.rows[].end_timestamp` | integer | Yes | Unix epoch time in milliseconds Example: `1636388280000` |
