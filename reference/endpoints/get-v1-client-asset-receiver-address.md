# Get receiver address

`GET /v1/client/asset/receiver_address`

**Authentication:** RWA

**Rate limit:** 10 requests per 1 second

## Description

Returns the exclusive receiver address for the authenticated account. Users can deposit supported tokens by transferring directly to this address without wallet connection or gas.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `chain_id` | query | integer | Yes | Chain ID to get the receiver address for. Supported chains: Arbitrum (`42161`), BNB Chain (`56`), ADI (`36900`). |
| `token` | query | string | No | Token symbol. Supported tokens: `USDC`, `USDT`. Defaults to `USDC` if omitted. |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/client/asset/receiver_address{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | No | — |
| `data.receiver_address` | string | No | The unique deposit address for this account. Example: `0x13a8f4736c001fed44731177c95302055a0a6df0` |
| `data.token_address` | string | No | The token contract address on the specified chain. Example: `0xaf88d065e77c8cC2239327C5EDb3A432268e5831` |
| `data.minimum_deposit` | number | No | Minimum deposit amount. Transfers below this are treated as dust and cannot be recovered. Example: `5` |
