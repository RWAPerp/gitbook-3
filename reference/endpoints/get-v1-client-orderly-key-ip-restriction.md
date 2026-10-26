# Get API key IP restriction

`GET /v1/client/orderly_key_ip_restriction`

**Authentication:** RWA

**Rate limit:** See platform limits

## Description

**Limit 10 requests per 60 seconds**

Retrieves the current IP restriction of a particular API key.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `orderly_key` | query | string | Yes | The API key to query the IP restriction list |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/client/orderly_key_ip_restriction{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.account_id` | string | Yes | Account ID that owns the API key. Example: `0x0f29bfb4c1bc9fea3f3be46bab6d795e22a6272354b136fde05f6b80cfcad546` |
| `data.orderly_key` | string | Yes | API key whose IP restrictions are returned. Example: `ed25519:8tm7dnKYkSc3FzgPuJaw1wztr79eeZpN35nHW5pL5XhX` |
| `data.ip_restriction_list` | array<string> | Yes | List of allowed IP addresses or IP ranges for the key. |
| `data.tag` | string | Yes | Optional tag associated with the API key. This field can be `null`. |
