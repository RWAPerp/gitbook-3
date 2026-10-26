# Create strategy vault deposit/withdrawal request with account

`POST /v1/sv_operation_request`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Deposit into a strategy vault with account balance / withdraw from a strategy vault into your account balance

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `message` | body | object | No | — |
| `message.payloadType` | body | number | No | LP_DEPOSIT=0/LP_WITHDRAW=1/SP_DEPOSIT=2/SP_WITHDRAW=3 |
| `message.nonce` | body | string | No | — |
| `message.receiver` | body | string | No | — |
| `message.amount` | body | string | No | — |
| `message.vaultId` | body | string | No | — |
| `message.token` | body | string | No | — |
| `message.dexBrokerId` | body | string | No | — |
| `message.chainId` | body | number | No | — |
| `message.chainType` | body | string | No | — |
| `signature` | body | string | No | — |
| `userAddress` | body | string | No | — |
| `verifyingContract` | body | string | No | — |

## Responses

### HTTP 200

Success

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
