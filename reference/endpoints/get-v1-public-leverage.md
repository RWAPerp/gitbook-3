# Get max leverage setting

`GET /v1/public/leverage`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Get max leverage setting

## Parameters

No fields are defined in the published schema.

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | No | — |
| `data.max_futures_leverage` | string | No | Example: `100` |
