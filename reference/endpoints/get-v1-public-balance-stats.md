# Get TVL by builder

`GET /v1/public/balance/stats`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Returns TVL (total balance plus unsettled PnL), optionally filtered by broker ID.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `broker_id` | query | string | No | When omitted, returns TVL for all brokers. |

## Responses

### HTTP 200

Success

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.total_holding` | number | No | Total balance across the selected scope. Example: `100` |
| `data.total_unsettled_balance` | number | No | Total unsettled PnL across the selected scope. Example: `21` |
| `data.last_update_time` | number | No | Timestamp of the most recent TVL update in milliseconds. Example: `1702989203989` |
