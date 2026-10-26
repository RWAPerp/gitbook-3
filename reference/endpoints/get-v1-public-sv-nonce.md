# Get strategy vault nonce for account transaction

`GET /v1/public/sv_nonce`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

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
| `data.nonce` | number | No | Example: `14001212121234` |
