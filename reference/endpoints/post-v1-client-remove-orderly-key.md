# Remove API key

`POST /v1/client/remove_orderly_key`

**Authentication:** RWA

**Rate limit:** 10 requests per 1 second per IP address

## Description

Removes an API key from an account and deactivates it for future use.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `orderly_key` | body | string | Yes | The API key to be removed from the account |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}POST/v1/client/remove_orderly_key{body}` → URL-safe Base64 without trailing `=` |
| `Content-Type` | Yes | `application/json` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
