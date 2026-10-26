# Add SP API key

`POST /v1/sv/sp_orderly_key`

**Authentication:** Wallet

**Rate limit:** 10 requests per second per IP address

## Description

Adds an RWA Perp access key to a SP account

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `message` | body | object | No | — |
| `message.contract` | body | string | Yes | — |
| `message.brokerId` | body | string | Yes | — |
| `message.chainId` | body | number | Yes | — |
| `message.orderlyKey` | body | string | Yes | — |
| `message.scope` | body | string | Yes | — |
| `message.timestamp` | body | number | Yes | — |
| `message.expiration` | body | number | Yes | — |
| `message.subAccountId` | body | string | No | If subAccountId is not null, create the api key for the input subAccountId |
| `signature` | body | string | No | — |
| `userAddress` | body | string | No | — |

## Responses

### HTTP 200

Success

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
