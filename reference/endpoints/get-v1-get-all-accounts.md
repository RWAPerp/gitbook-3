# Check account details of an address

`GET /v1/get_all_accounts`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Returns all accounts associated with the provided wallet address and builder ID.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `address` | query | string | Yes | The address of the user wallet |
| `broker_id` | query | string | Yes | Builder ID whose accounts should be returned. |
| `chain_type` | query | string | No | `EVM` or `SOL` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.rows` | array<object> | Yes | — |
| `data.rows[].user_id` | integer | Yes | Internal user ID associated with the account. Example: `24` |
| `data.rows[].account_id` | string | Yes | Account ID returned for the wallet and builder combination. Example: `0xb129e074a17dfba8d652ae1eca21c7d6bb6904f1aa693f4886d50db170933a46` |
| `data.rows[].broker_id` | string | Yes | Builder ID associated with the account. Example: `aden` |
| `data.rows[].chain_type` | string | Yes | Chain type of the account. Supported values are `EVM` or `SOL`. Example: `EVM` |
| `data.rows[].user_type` | string | Yes | Account role. Supported values are `SUB`, `MAIN`, `SP`, `PV`, and `UV`. Example: `SUB` |
