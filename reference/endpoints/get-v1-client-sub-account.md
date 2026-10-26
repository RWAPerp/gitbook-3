# Get sub account list

`GET /v1/client/sub_account`

**Authentication:** RWA

**Rate limit:** 10 requests per second

## Description

Only the main account is allowed to call this API.

## Parameters

No fields are defined in the published schema.

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/client/sub_account{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.main_account_id` | string | Yes | Account ID of the main account that owns the listed sub accounts. Example: `0x7ecc7eb7dc60d7fb5c5ea9cc637da1a46e265a744efda327b9914d7a21725bbf` |
| `data.rows` | array<object> | Yes | Sub-accounts under the main account. |
| `data.rows[].sub_account_id` | string | Yes | Account ID of the sub account. Example: `0x86987799a1433266cacd80c817b670336d6779468f69defd6f8dc384a07b6457` |
| `data.rows[].description` | string | Yes | User-defined label for the sub account. Example: `abc` |
