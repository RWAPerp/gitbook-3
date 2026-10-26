# Get valor2 redeem info

`GET /v1/staking/valor2/redeem`

**Authentication:** RWA

**Rate limit:** 10 requests per 1 second per IP address

## Description

The redeemed VALOR amount may come from multiple batches

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `address` | query | string | Yes | — |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/staking/valor2/redeem{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | No | — |
| `data.redeeming_valor_amount` | number | No | Example: `1000` |
| `data.redeeming_valor_list` | array<object> | No | The redeemed VALOR amount may come from multiple batches, so redeeming_valor_list provides a per-batch breakdown for users to identify each batch. |
| `data.redeeming_valor_list[].batch_id` | number | No | Example: `13` |
| `data.redeeming_valor_list[].redeem_amount` | number | No | Example: `2000` |
| `data.pending_esorder` | number | No | Example: `5000` |
| `data.available_esorder` | number | No | Example: `1500` |
