# Get API key

`GET /v1/get_orderly_key`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Check the validity of an RWA Perp access key attached to the account.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `account_id` | query | string | Yes | The account id of the user. |
| `orderly_key` | query | string | Yes | The public key of the RWA Perp access key. |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.orderly_key` | string | Yes | API key associated with the account. Example: `ed25519:7tEoJo5hMBKBrQsqmc8yw1xNfoQCFQBVwQT1eFafRNRf` |
| `data.scope` | string | Yes | Scopes granted to the API key. Example: `read,trading` |
| `data.expiration` | integer | Yes | Expiration timestamp of the API key in milliseconds. Example: `1689086651947` |
| `data.tag` | string | No | Optional tag associated with the API key. |
