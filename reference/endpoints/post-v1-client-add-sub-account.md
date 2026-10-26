# Add sub account

`POST /v1/client/add_sub_account`

**Authentication:** RWA

**Rate limit:** 10 requests per second

## Description

Only the main account is allowed to call this API.

Main account’s API key can control sub accounts.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `description` | body | string | No | — |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}POST/v1/client/add_sub_account{body}` → URL-safe Base64 without trailing `=` |
| `Content-Type` | Yes | `application/json` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.sub_account_id` | number | Yes | Example: `123` |
| `data.description` | string | Yes | Example: `abc` |
