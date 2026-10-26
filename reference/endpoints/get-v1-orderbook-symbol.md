# Orderbook snapshot

`GET /v1/orderbook/{symbol}`

**Authentication:** RWA

**Rate limit:** 10 requests per 1 second

| Base | URL |
|------|-----|
| Default REST | `https://api-trade.rwaperp.xyz` |
| VIP REST | `https://api-vip.rwaperp.xyz` |

Same path, same `RWA-*` signing on both hosts. Prefer VIP when your integration is provisioned for the dedicated REST endpoint. **To-B partners:** contact RWA Perp to obtain a dedicated Base URL before using `api-trade`, `api-vip`, or any custom host.

## Description

Snapshot of the current orderbook. Price of asks/bids are in descending order.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `symbol` | path | string | Yes | — |
| `max_level` | query | integer | No | the levels wish to show on both side. |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/orderbook/{symbol}{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.asks` | array<object> | Yes | — |
| `data.asks[].price` | number | Yes | Example: `10669.4` |
| `data.asks[].quantity` | number | Yes | Example: `1.56263218` |
| `data.bids` | array<object> | Yes | — |
| `data.bids[].price` | number | Yes | Example: `10669.4` |
| `data.bids[].quantity` | number | Yes | Example: `1.56263218` |
| `data.timestamp` | integer | Yes | Unix epoch time in milliseconds |
