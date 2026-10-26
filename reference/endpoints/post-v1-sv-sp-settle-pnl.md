# Request SP PnL settlement

`POST /v1/sv/sp_settle_pnl`

**Authentication:** Wallet

**Rate limit:** 1 request per second

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `message` | body | object | No | — |
| `message.contract` | body | string | No | — |
| `message.brokerId` | body | string | No | — |
| `message.chainId` | body | number | No | — |
| `message.settleNonce` | body | string | No | — |
| `message.timestamp` | body | number | No | — |
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
