# Get leverage configuration

`GET /v1/public/config`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Returns the leverage configuration available to users on RWA Perp.

## Parameters

No fields are defined in the published schema.

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.available_futures_leverage` | string | Yes | Comma-separated list of leverage values available for futures trading. Example: `1,2,3,4,5,10,15,20` |
