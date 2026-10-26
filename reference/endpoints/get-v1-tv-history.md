# Get tradingview history bars

`GET /v1/tv/history`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

`GET /v1/tv/history?symbol={}&resolution={}&from={}&to={}`

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `symbol` | query | string | Yes | — |
| `resolution` | query | string | Yes | — |
| `from` | query | string | Yes | — |
| `to` | query | string | Yes | — |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `s` | string | Yes | — |
| `t` | array<integer> | Yes | — |
| `o` | array<object> | Yes | — |
| `h` | array<number> | Yes | — |
| `l` | array<number> | Yes | — |
| `c` | array<number> | Yes | — |
| `v` | array<number> | Yes | — |
