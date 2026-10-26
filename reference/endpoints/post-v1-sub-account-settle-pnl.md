# Settle sub account PnL

`POST /v1/sub_account_settle_pnl`

**Authentication:** RWA

**Rate limit:** 10 requests per second

## Description

Main account’s API key can control sub accounts.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `settle_nonce` | body | number | Yes | — |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}POST/v1/sub_account_settle_pnl{body}` → URL-safe Base64 without trailing `=` |
| `Content-Type` | Yes | `application/json` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.settle_pnl_id` | integer | Yes | Example: `1` |
