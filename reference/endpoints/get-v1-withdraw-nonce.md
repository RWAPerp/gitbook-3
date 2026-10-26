# Get withdrawal nonce

`GET /v1/withdraw_nonce`

**Authentication:** RWA

**Rate limit:** See platform limits

## Description

**Limit 10 requests per 1 seconds**

Retrieves a nonce required to sign a withdrawal request. Each nonce can only be used once.

## Parameters

No fields are defined in the published schema.

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/withdraw_nonce{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.withdraw_nonce` | integer | Yes | Nonce used to sign a withdrawal request. Example: `1` |
