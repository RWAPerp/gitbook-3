# Check if account exists

`GET /v1/public/account`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Check if provided account account is registered with RWA Perp and it's respective builder.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `account_id` | query | string | No | — |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.address` | string | Yes | Example: `0xfcc17f2b240380d56f0615e8f654e4ae3cee8957` |
| `data.broker_id` | string | Yes | Example: `woofi_pro` |
