# Reset API key IP restriction

`POST /v1/client/reset_orderly_key_ip_restriction`

**Authentication:** RWA

**Rate limit:** 10 requests per 60 seconds

## Description

Reset the IP restriction of a particular API key under the account.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `orderly_key` | query | string | Yes | The API key whose IP restriction will be reset. |
| `reset_mode` | query | string | Yes | Reset mode to apply. Use `ALLOW_ALL_IPS` to remove all IP restrictions, or `DISALLOW_ALL_IPS` to block all IPs for this key. |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}POST/v1/client/reset_orderly_key_ip_restriction{body}` → URL-safe Base64 without trailing `=` |
| `Content-Type` | Yes | `application/json` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
