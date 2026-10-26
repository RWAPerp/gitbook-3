# Get IP info

`GET /v1/ip_info`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Returns the detected IP address and location metadata for the calling client.

## Parameters

No fields are defined in the published schema.

## Responses

### HTTP 200

Success

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.city` | string | No | Detected city for the calling IP address. Example: `Toronto` |
| `data.ip` | string | No | Detected public IP address of the calling client. Example: `192.192.192.0` |
| `data.checked` | boolean | No | Example: `False` |
| `data.region` | string | No | Detected region or country for the calling IP address. Example: `Canada` |
