# Get aggregate positions

`GET /v1/client/aggregate/positions`

**Authentication:** RWA

**Rate limit:** 1 request per 60 seconds

## Description

Only the main account is allowed to call this API.

## Parameters

No fields are defined in the published schema.

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/client/aggregate/positions{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | No | Example: `[{'account_id': '0x11111', 'IMR_withdraw_orders': 0.1, 'MMR_with_orders': 0.05, 'average_open_price': 27908.14386047, 'cost_position': -139329.358492, 'est_liq_price': 117335.92899428, 'fee_24_h': 0, 'imr': 0.1, 'last_sum_unitary_funding': 70.38, 'mark_price': 27794.9, 'mmr': 0.05, 'pending_long_qty': 0, 'pending_short_qty': 0, 'pnl_24_h': 0, 'position_qty': -5, 'settle_price': 27865.8716984, 'symbol': 'PERP_BTC_USDC', 'seq': 1730181536341943600, 'timestamp': 1685429350571, 'updated_time': 1685429350571, 'unsettled_pnl': 354.858492, 'leverage': 10}, {'account_id': '0x22222', 'IMR_withdraw_orders': 0.12, 'MMR_with_orders': 0.06, 'average_open_price': 28000.123456, 'cost_position': -100000.56789, 'est_liq_price': 120000.654321, 'fee_24_h': 5.5, 'imr': 0.12, 'last_sum_unitary_funding': 50.12, 'mark_price': 27794.9, 'mmr': 0.06, 'pending_long_qty': 1, 'pending_short_qty': 0, 'pnl_24_h': 150.75, 'position_qty': -3, 'settle_price': 27950.6789, 'symbol': 'PERP_BTC_USDC', 'seq': 1730181536341943601, 'timestamp': 1685429350572, 'updated_time': 1685429350571, 'unsettled_pnl': 354.858492, 'leverage': 10}]` |
| `data.rows` | array<object> | No | Aggregate position records for the main account and its sub accounts. |
| `data.rows[].account_id` | string | No | Account ID that owns the position. |
| `data.rows[].IMR_withdraw_orders` | number | No | Initial margin ratio after accounting for pending withdraw orders. |
| `data.rows[].MMR_with_orders` | number | No | Maintenance margin ratio after accounting for open orders. |
| `data.rows[].average_open_price` | number | No | Average entry price of the position. |
| `data.rows[].cost_position` | number | No | Cost basis of the position. |
| `data.rows[].est_liq_price` | number | No | Estimated liquidation price of the position. |
| `data.rows[].fee_24_h` | number | No | Trading fees paid over the last 24 hours for the position. |
| `data.rows[].imr` | number | No | Current initial margin ratio of the position. |
| `data.rows[].last_sum_unitary_funding` | number | No | Latest cumulative unit funding value applied to the position. |
| `data.rows[].mark_price` | number | No | Current mark price of the symbol. |
| `data.rows[].mmr` | number | No | Current maintenance margin ratio of the position. |
| `data.rows[].pending_long_qty` | number | No | Pending long order quantity for the symbol. |
| `data.rows[].pending_short_qty` | number | No | Pending short order quantity for the symbol. |
| `data.rows[].pnl_24_h` | number | No | Profit and loss over the last 24 hours. |
| `data.rows[].position_qty` | number | No | Current position quantity. |
| `data.rows[].settle_price` | number | No | Latest settlement price of the symbol. |
| `data.rows[].symbol` | string | No | Trading symbol of the position. |
| `data.rows[].seq` | number | No | Sequence number of the latest position update. |
| `data.rows[].timestamp` | number | No | Timestamp of the position snapshot in milliseconds. |
| `data.rows[].updated_time` | number | No | Timestamp of the latest position update in milliseconds. |
| `data.rows[].unsettled_pnl` | number | No | Unrealized PnL that has not been settled. |
| `data.rows[].leverage` | integer | No | Effective leverage applied to the position. |
| `data.rows[].margin_mode` | string | No | Margin mode used by the position. |
| `data.rows[].margin` | number | No | Margin currently allocated to the position. |
| `data.rows[].accrued_funding_fee` | number | No | Funding fee accrued by the position. |
