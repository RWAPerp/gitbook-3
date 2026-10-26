# Get supported chains per builder

`GET /v1/public/chain_info`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Returns the chains supported by the specified builder. When `broker_id` is omitted, the response includes all supported chains.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `broker_id` | query | string | No | Filter results to a specific broker ID. |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.rows` | array<object> | Yes | Chains available for the requested builder scope. |
| `data.rows[].name` | string | Yes | Human-readable chain name. Example: `Arbitrum` |
| `data.rows[].public_rpc_url` | string | Yes | Public RPC endpoint for the chain. Example: `https://arb1.arbitrum.io/rpc` |
| `data.rows[].chain_id` | string | Yes | Chain ID used for deposits and withdrawals. Example: `42161` |
| `data.rows[].currency_symbol` | string | Yes | Native gas token symbol for the chain. Example: `ETH` |
| `data.rows[].currency_decimal` | number | No | Number of decimals used by the native gas token. Example: `18` |
| `data.rows[].explorer_base_url` | string | Yes | Base URL of the chain explorer. Example: `https://arbiscan.io` |
| `data.rows[].vault_address` | string | Yes | RWA Perp vault address on the chain. Example: `0x816f722424B49Cf1275cc86DA9840Fbd5a6167e9` |
| `data.rows[].broker_ids` | array<string> | No | Builders available on the chain. |
