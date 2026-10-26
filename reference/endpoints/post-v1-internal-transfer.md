# Create internal transfer

`POST /v1/internal_transfer`

**Authentication:** RWA

**Rate limit:** 10 requests per 1 second

## Description

This endpoint will return internal transfer is not available for Delegate Signer account if the `from` is a Delegate Signer account.

Scenarios where internal transfers are allowed:

a. Main and sub accounts

b. Accounts within the same wallet group

c. Same address across all brokers.

d. A whitelisted `account_id` can be used as `from address`

e. If 2 `account_id` are under the same broker_id and the broker_id is whitelisted.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `token` | body | string | No | Example: `USDC` |
| `receiver_list` | body | array<object> | No | Maximum 50 receivers per request, transferring to yourself will lead to request failure.  |
| `receiver_list[].account_id` | body | string | No | Example: `0x0000000` |
| `receiver_list[].amount` | body | number | No | Example: `100` |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}POST/v1/internal_transfer{body}` → URL-safe Base64 without trailing `=` |
| `Content-Type` | Yes | `application/json` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | No | — |
| `data.internal_transfer_request_id` | integer | No | Example: `123` |
