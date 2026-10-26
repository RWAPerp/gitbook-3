# Batch cancel orders

`DELETE /v1/batch-order`

**Authentication:** RWA (`trading` scope)

**Rate limit:** 10 requests per 1 second

| Base | URL |
|------|-----|
| Default REST | `https://api-trade.rwaperp.xyz` |
| VIP REST | `https://api-vip.rwaperp.xyz` |

Same path, same `RWA-*` signing on both hosts. Prefer VIP when your integration is provisioned for the dedicated REST endpoint. **To-B partners:** contact RWA Perp to obtain a dedicated Base URL before using `api-trade`, `api-vip`, or any custom host.

## Description

`DELETE /v1/batch-order?order_ids={order_id1},{order_id2}`

Cancel a list of orders by `order_ids`. The maximum orders that can be cancelled within 1 batch cancel request is 10. 

This endpoint will return invalid order_id error if 0 order_ids are given or all of the given order_ids are invalid. 

Note: This endpoint requires `trading` scope in API key.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `order_ids` | query | string | Yes | List of order_ids, comma-separated, with a maximum of 10 order ids per request. |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}DELETE/v1/batch-order{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.status` | string | Yes | Example: `CANCEL_ALL_SENT` |
