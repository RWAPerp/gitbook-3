# Get index price source

`GET /v1/public/index_price_source`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Retrieves the configured index price sources for each symbol.

The `sources` array lists configured sources; it does not indicate which sources
actually participated in the index price calculation at that moment. Actual
participation depends on price availability, price validity, and effective weight.

## Parameters

No fields are defined in the published schema.

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.rows` | array<object> | Yes | — |
| `data.rows[].symbol` | string | No | SPOT symbol name Example: `SPOT_BNB_USDC` |
| `data.rows[].updated_time` | number | No | Example: `1710382176255` |
| `data.rows[].sources` | array<string> | No | Configured index price sources for this symbol. This list does not
indicate which sources actually participated in the calculation at
that moment; participation depends on price availability, price
validity, and effective weight.
 Example: `['gateio', 'kucoin', 'binance', 'okx', 'huobi', 'bybit', 'mexc']` |
