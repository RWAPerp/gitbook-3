# Get current API key info

`GET /v1/client/key_info`

**Authentication:** RWA

**Rate limit:** See platform limits

## Description

**Limit 10 requests per 60 seconds**

Retrieves all registered API keys under the account.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `key_status` | query | string | No | Filter by API key status. Supported values: `ACTIVE`, `REMOVING`, or `REMOVED`. |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/client/key_info{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.rows` | array<object> | Yes | — |
| `data.rows[].orderly_key` | string | No | API key registered under the account. Example: `ed25519:B4yEc8xMjoqdUiKT5ZT1b2cUy5cggZrbMPvCrqyjkQhf` |
| `data.rows[].key_status` | string | No | Current key status. Supported values are `ACTIVE`, `REMOVING`, and `REMOVED`. Example: `ACTIVE` |
| `data.rows[].ip_restriction_list` | array<string> | No | List of IP addresses or ranges allowed to use the key. |
| `data.rows[].ip_restriction_status` | string | No | IP restriction mode for the key. Supported values are `ALLOW_RESTRICTION_LIST`, `ALLOW_ALL_IPS`, and `DISALLOW_ALL_IPS`. Example: `ALLOW_ALL_IPS` |
| `data.rows[].expiration` | integer | No | Expiration timestamp of the API key in milliseconds. Example: `1689086651947` |
| `data.rows[].scope` | string | No | Scopes granted to the API key. Example: `read,trading` |
| `data.rows[].tag` | string | No | Optional tag associated with the API key. |
