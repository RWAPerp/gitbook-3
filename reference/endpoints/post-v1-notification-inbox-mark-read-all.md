# Set read status of all notifications

`POST /v1/notification/inbox/mark_read_all`

**Authentication:** RWA

**Rate limit:** 10 requests per 60 seconds

## Description

Set the read status on all notifications for a user.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `flag` | query | number | Yes | The value of the read flag, where 1 = READ and 0 = UNREAD |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}POST/v1/notification/inbox/mark_read_all{body}` → URL-safe Base64 without trailing `=` |
| `Content-Type` | Yes | `application/json` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
