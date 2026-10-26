# Get tradingview symbol info

`GET /v1/tv/symbol_info`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `group` | query | string | Yes | — |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `s` | string | Yes | — |
| `symbol` | array<string> | Yes | — |
| `description` | array<string> | Yes | — |
| `currency` | array<string> | Yes | — |
| `base-currency` | array<object> | Yes | — |
| `exchange-listed` | array<string> | Yes | — |
| `exchange-traded` | array<string> | Yes | — |
| `minmovement` | array<integer> | Yes | — |
| `minmovement2` | array<integer> | Yes | — |
| `fractional` | array<boolean> | Yes | — |
| `pricescale` | array<integer> | Yes | — |
| `root` | array<object> | Yes | — |
| `root-description` | array<object> | Yes | — |
| `has-intraday` | array<boolean> | Yes | — |
| `has-no-volume` | array<boolean> | Yes | — |
| `type` | array<string> | Yes | — |
| `is-cfd` | array<boolean> | Yes | — |
| `ticker` | array<string> | Yes | — |
| `timezone` | array<string> | Yes | — |
| `session-regular` | array<string> | Yes | — |
| `session-extended` | array<string> | Yes | — |
| `session-premarket` | array<object> | Yes | — |
| `session-postmarket` | array<object> | Yes | — |
| `supported-resolutions` | array<array<string>> | Yes | — |
| `has-daily` | array<boolean> | Yes | — |
| `intraday-multipliers` | array<array<string>> | Yes | — |
| `has-weekly-and-monthly` | array<boolean> | Yes | — |
| `pointvalue` | array<object> | Yes | — |
| `expiration` | array<object> | Yes | — |
| `bar-source` | array<string> | Yes | — |
| `bar-transform` | array<string> | Yes | — |
| `bar-fillgaps` | array<string> | Yes | — |
| `isin` | array<string> | Yes | — |
| `wkn` | array<string> | Yes | — |
