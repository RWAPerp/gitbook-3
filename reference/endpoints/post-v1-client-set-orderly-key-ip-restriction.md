# Set API key IP restriction

`POST /v1/client/set_orderly_key_ip_restriction`

**Authentication:** RWA

**Rate limit:** 10 requests per 60 seconds

## Description

Set the IP restrictions of a particular API key under the account.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `orderly_key` | query | string | Yes | The API key to set the IP restriction list. |
| `ip_restriction_list` | query | string | Yes | List of IP addresses or IP ranges, comma separated, that are allowed to use the `orderly_key`. |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}POST/v1/client/set_orderly_key_ip_restriction{body}` → URL-safe Base64 without trailing `=` |
| `Content-Type` | Yes | `application/json` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.ip_restriction_list` | array<string> | Yes | — |
