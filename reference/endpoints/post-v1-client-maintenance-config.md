# Configure auto-cancel during maintenance

`POST /v1/client/maintenance_config`

**Authentication:** RWA

**Rate limit:** 10 requests per 60 seconds

## Description

Set the user config for whether the system should automatically cancel the user's pending orders during maintenance.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `maintenance_cancel_order_flag` | body | boolean | Yes | if true, system will cancel all of user's pending orders during maintenance. |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}POST/v1/client/maintenance_config{body}` → URL-safe Base64 without trailing `=` |
| `Content-Type` | Yes | `application/json` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.success_alter` | string | Yes | Example: `Success! Your change has been saved!` |
