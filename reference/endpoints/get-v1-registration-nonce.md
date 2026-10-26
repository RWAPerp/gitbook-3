# Get registration nonce

`GET /v1/registration_nonce`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Retrieve a nonce used for registering an account on RWA Perp. The validity of the nonce value is `2` minutes. Each nonce can only be used once (ie for one account).

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
| `data.registration_nonce` | string | Yes | Registration nonce used to sign account registration requests. Example: `194528949540` |
