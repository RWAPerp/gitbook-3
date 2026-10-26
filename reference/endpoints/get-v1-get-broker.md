# Check if address is registered

`GET /v1/get_broker`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Checks whether an address is already registered and returns the associated builder IDs.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `address` | query | string | Yes | Wallet address to check. |
| `chain_type` | query | string | No | `EVM` or `SOL` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.broker_id` | array<string> | No | Broker IDs associated with the queried wallet address. |
