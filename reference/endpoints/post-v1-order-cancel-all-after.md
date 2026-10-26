# Cancel all after

`POST /v1/order/cancel_all_after`

**Authentication:** RWA

**Rate limit:** 1 request per 1 second

| Base | URL |
|------|-----|
| Default REST | `https://api-trade.rwaperp.xyz` |
| VIP REST | `https://api-vip.rwaperp.xyz` |

Same path, same `RWA-*` signing on both hosts. Prefer VIP when your integration is provisioned for the dedicated REST endpoint. **To-B partners:** contact RWA Perp to obtain a dedicated Base URL before using `api-trade`, `api-vip`, or any custom host.

## Description

Cancels all of the user's ordinary and algo orders after being called (dead man switch).

Note: Users must apply for access before using this endpoint.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `trigger_after` | body | number | Yes | Timeout in milliseconds. 
Min timeout is 5000.
Max timeout can be set to 900000. 
To cancel this timer, set timeout to 0.
 Example: `5000` |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}POST/v1/order/cancel_all_after{body}` → URL-safe Base64 without trailing `=` |
| `Content-Type` | Yes | `application/json` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.expected_trigger_time` | number | No | Example: `1711534302938` |
