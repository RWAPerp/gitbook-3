# Get kline history

`GET /v1/tv/kline_history`

**Authentication:** None

**Rate limit:** 5 request per 10 second per IP address

## Description

Get the historical klines of the specified symbol

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `symbol` | query | string | Yes | Symbol name |
| `resolution` | query | string | Yes | `1m/5m/15m/30m/1h/4h/12h/1d/1w/1mon` |
| `from` | query | string | No | If the range from from to to contains 1200 klines, only 1000 klines will be returned, starting from to and moving backward (due to the limit). |
| `to` | query | string | No | If the range from from to to contains only 500 klines, then all 500 will be returned, starting from to and moving backward. |
| `limit` | query | number | No | Numbers of klines you want to query.  Maximum of 1000 klines allowed. |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `s` | string | Yes | Example: `ok` |
| `o` | array<number> | Yes | Example: `[2.105, 2.155, 2.105, 2.0285, 1.8, 2.55, 2.55]` |
| `c` | array<number> | Yes | Example: `[2.1, 2.155, 2.057, 1.86, 1.8, 2.55, 2.48]` |
| `h` | array<number> | Yes | Example: `[2.155, 2.155, 2.105, 2.0285, 1.8, 2.55, 3.175]` |
| `l` | array<number> | Yes | Example: `[2.1, 2.155, 2.02, 1.85, 1.8, 2.55, 2.48]` |
| `v` | array<number> | Yes | Example: `[22.0, 0.0, 2.0, 3000.0, 26.0, 0.0, 2.0]` |
| `a` | array<number> | Yes | Example: `[46.2, 0.0, 4.114, 5635.0, 46.8, 0.0, 6.1]` |
| `t` | array<integer> | Yes | Example: `[1761955200, 1762041600, 1762128000, 1762214400, 1762300800, 1762646400, 1762732800]` |
