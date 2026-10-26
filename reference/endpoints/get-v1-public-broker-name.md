# Get builder list

`GET /v1/public/broker/name`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

`GET /v1/public/broker/name?broker_id={broker_id}`

Returns the list of builders currently onboarded to RWA Perp. Use `broker_id` to retrieve a single builder entry.

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
| `data.rows` | array<object> | Yes | Builders that match the requested filters. |
| `data.rows[].broker_id` | string | Yes | Unique broker ID for the builder. Example: `woofi_pro` |
| `data.rows[].broker_name` | string | Yes | Display name of the builder. Example: `WOOFi Pro` |
