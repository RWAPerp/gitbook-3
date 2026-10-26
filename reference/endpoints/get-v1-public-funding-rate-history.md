# Get funding rate history for one market

`GET /v1/public/funding_rate_history`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Get funding rate history for one market.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `symbol` | query | string | Yes | — |
| `start_t` | query | number | No | start time range that you wish to query, noted that the time stamp is a 13-digits timestamp. |
| `end_t` | query | number | No | end time range that you wish to query, noted that the time stamp is a 13-digits timestamp. |
| `page` | query | number | No | the page you wish to query. start from 1 |
| `size` | query | number | No | Default: 60 |

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
| `data.rows[].funding_rate` | number | Yes | Example: `0.0001` |
| `data.rows[].funding_rate_timestamp` | integer | Yes | Example: `1684224000000` |
| `data.rows[].next_funding_time` | integer | Yes | Example: `1684252800000` |
| `data.meta` | object | Yes | — |
| `data.meta.total` | integer | Yes | Example: `9` |
| `data.meta.records_per_page` | integer | Yes | Example: `25` |
| `data.meta.current_page` | integer | Yes | start from 1 Example: `1` |
