# Get vault balance

`GET /v1/public/vault_balance`

**Authentication:** None

**Rate limit:** See platform limits

## Description

Returns the current vault balance by chain and token. Use `chain_id` and `token` to narrow the result set.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `chain_id` | query | string | No | Chain ID to query. Use `900900900` for Solana. |
| `token` | query | string | No | Token symbol to query, for example `USDC`. If omitted, returns all supported tokens. |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.rows` | array<object> | Yes | Vault balance entries that match the requested filters. |
| `data.rows[].chain_id` | integer | No | Chain ID for the reported balance. Example: `80001` |
| `data.rows[].token` | string | No | Token symbol for the reported balance. Example: `USDC` |
| `data.rows[].balance` | number | No | Available vault balance for the token on the chain. Example: `1000.12345` |
