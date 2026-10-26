# Get predicted funding rate for one market

`GET /v1/public/funding_rate/{symbol}`

**Authentication:** None

**Rate limit:** 30 requests per 1 second per IP address

## Description

Get latest funding rate for one market.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `symbol` | path | string | Yes | — |

## Responses

### HTTP 200

Success

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.symbol` | string | Yes | Example: `PERP_ETH_USDC` |
| `data.est_funding_rate` | integer | Yes | Example: `0` |
| `data.est_funding_rate_timestamp` | integer | Yes | Example: `1683880020000` |
| `data.last_funding_rate` | number | Yes | Example: `0.0001` |
| `data.last_funding_rate_timestamp` | integer | Yes | Example: `1683878400000` |
| `data.next_funding_time` | integer | Yes | Example: `1683907200000` |
| `data.sum_unitary_funding` | number | Yes | Example: `521.367` |
