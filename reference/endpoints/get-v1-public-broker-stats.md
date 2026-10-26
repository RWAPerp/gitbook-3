# Get builder stats

`GET /v1/public/broker/stats`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

`GET /v1/public/broker/stats?broker_id={broker_id}`

Returns statistics for builders on RWA Perp. Use `broker_id` to limit the response to a single builder.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `broker_id` | query | string | No | Filter results to a specific broker ID. |

## Responses

### HTTP 200

Success

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.rows` | array<object> | Yes | Statistics for the requested builders. |
| `data.rows[].connected_user` | integer | Yes | Number of connected users for the builder. Example: `274148` |
