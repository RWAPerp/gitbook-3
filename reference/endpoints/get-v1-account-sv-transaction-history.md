# Get account’s strategy vault transaction history

`GET /v1/account_sv_transaction_history`

**Authentication:** None

**Rate limit:** See platform limits

## Description

Get account transaction history with strategy vaults

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `vault_id` | query | string | No | if vault_id is empty, it will return all vaults |
| `start_t` | query | string | No | start time range that you wish to query, noted that the time stamp is a 13-digits timestamp. |
| `end_t` | query | string | No | end time range that you wish to query, noted that the time stamp is a 13-digits timestamp. |
| `page` | query | string | No | the page you wish to query. start from 1 |
| `size` | query | string | No | Default: 60 |
| `type` | query | string | No | deposit/withdraw, if empty = return all |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.rows` | array<object> | Yes | Aggregate position records for the main account and its sub accounts. |
| `data.rows[].vault_id` | string | Yes | — |
| `data.rows[].created_time` | integer | Yes | Example: `1734652800000` |
| `data.rows[].type` | string | Yes | Example: `withdrawal` |
| `data.rows[].status` | string | Yes | `pending` / `completed` / `failed` Example: `pending` |
| `data.rows[].asset` | string | No | Example: `USDC` |
| `data.rows[].amount_change` | integer | Yes | All values are positive. When type = `deposit`, `amount_change` is shown normally. 
When type = `withdrawal`, only when status == `completed` return `amount_change` value, all other status return null.
 Example: `100.0` |
| `data.rows[].shares_change` | integer | No | All values are positive. When type = `withdrawal`, `shares_change` is shown normally. 
When type = `deposit`, only when status == `completed` return `shares_change` value, all other status return null.
 Example: `88.009` |
| `data.meta` | object | Yes | — |
| `data.meta.total` | integer | Yes | Example: `9` |
| `data.meta.records_per_page` | integer | Yes | Example: `25` |
| `data.meta.current_page` | integer | Yes | start from 1 Example: `1` |
