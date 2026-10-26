# Check if wallet is registered

`GET /v1/get_account`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Check whether a wallet has a registered account with the provided builder ID.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `address` | query | string | Yes | The address of the user wallet |
| `broker_id` | query | string | Yes | Builder ID to check for the wallet address. |
| `chain_type` | query | string | No | `EVM` or `SOL` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.user_id` | integer | Yes | Internal user ID associated with the wallet and builder. Example: `24` |
| `data.account_id` | string | Yes | Account ID associated with the wallet and builder. Example: `0xb129e074a17dfba8d652ae1eca21c7d6bb6904f1aa693f4886d50db170933a46` |
