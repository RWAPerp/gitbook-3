# Get supported collateral info

`GET /v1/public/token`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Retrieves the available tokens to be used as collateral within RWA Perp.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `chain_id` | query | string | No | Filter results by chain_id |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.rows` | array<object> | Yes | — |
| `data.rows[].token` | string | No | name of token Example: `ETH` |
| `data.rows[].base_weight` | number | No | 1 for usdc Example: `0.8` |
| `data.rows[].discount_factor` | number | No | null for usdc Example: `0.02` |
| `data.rows[].haircut` | number | No | 0 for usdc Example: `0.95` |
| `data.rows[].user_max_qty` | number | No | -1 = infinity > usdc Example: `111` |
| `data.rows[].is_collateral` | boolean | No | True, the asset can be collateral, users are allowed to manually swap, and we will do auto-swap Example: `True` |
| `data.rows[].decimals` | number | No | precision of the token Example: `6` |
| `data.rows[].minimum_withdraw_amount` | number | No | Example: `1e-06` |
| `data.rows[].on_chain_swap` | boolean | No | True, the asset is eligible for on-chain swaps on at least one supported blockchain Example: `True` |
| `data.rows[].token_hash` | string | No | Example: `0xd6aca1be9729c13d677335161321649cccae6a591554772516700f986f942eaa` |
| `data.rows[].chain_details` | array<object> | No | — |
| `data.rows[].chain_details[].chain_id` | integer | No | Example: `43113` |
| `data.rows[].chain_details[].contract_address` | string | No | Example: `0x5d64c9cfb0197775b4b3ad9be4d3c7976e0d8dc3` |
| `data.rows[].chain_details[].cross_chain_withdrawal_fee` | integer | No | Example: `0` |
| `data.rows[].chain_details[].decimals` | integer | No | Example: `18` |
| `data.rows[].chain_details[].withdraw_fee` | number | No | Example: `2` |
| `data.rows[].chain_details[].display_name` | string | No | `USDC.e` for `Mantle` chain Example: `ETH` |
| `data.rows[].chain_details[].exclusive_deposit_supported` | boolean | No | Whether this token on this chain supports deposit via exclusive receiver address. Example: `False` |
