# Create internal transfer with wallet signature

`POST /v2/internal_transfer`

**Authentication:** RWA

**Rate limit:** 10 requests per 1 second

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `signature` | body | string | No | — |
| `userAddress` | body | string | No | — |
| `verifyingContract` | body | string | No | — |
| `message` | body | object | No | — |
| `message.receiver` | body | string | No | — |
| `message.token` | body | string | No | — |
| `message.amount` | body | integer | No | Example: `123` |
| `message.transferNonce` | body | string | No | — |
| `message.chainId` | body | string | No | Example: `1` |
| `message.chainType` | body | string | No | Example: `SOL` |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}POST/v2/internal_transfer{body}` → URL-safe Base64 without trailing `=` |
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
