# Get all notifications

`GET /v1/notification/inbox/notifications`

**Authentication:** RWA

**Rate limit:** 10 requests per 60 seconds

## Description

Returns notification records for the user.

Use `type` to filter the categories returned.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `type` | query | string | No | Filter notifications by type: `TRADE` or `SYSTEM`. |
| `page` | query | number | No | start from 1 |
| `size` | query | number | No | Number of notifications to return per page. |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/notification/inbox/notifications{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.rows` | array<object> | Yes | — |
| `data.rows[].id` | integer | No | Unique ID of the notification. Example: `12345` |
| `data.rows[].message_type` | string | No | Internal message type of the notification payload. Example: `ORDER_FILLED` |
| `data.rows[].email` | string | No | Email address bound to the account, when available. Example: `test@rwaperp.xyz` |
| `data.rows[].application_id` | string | No | Wallet address associated with the account. Example: `0x0f29bfb4c1bc9fea3f3be46bab6d795e22a6272354b136fde05f6b80cfcad546` |
| `data.rows[].title` | string | No | Notification title shown to the user. Example: ` Your order has been filled` |
| `data.rows[].type` | string | No | Notification category. Supported values are `TRADE` and `SYSTEM`. Example: `TRADE` |
| `data.rows[].level` | string | No | Notification priority level. Supported values are `GENERAL` and `IMPORTANT`. Example: `GENERAL` |
| `data.rows[].content_summary` | string | No | Short summary shown in notification lists. Example: `Your order to buy 1 NEAR-PERP has been filled: 0.5/1 at 1.9876.` |
| `data.rows[].content` | string | No | Full notification content, which may include HTML formatting. Example: `<p>Your order to buy 1 NEAR-PERP has been filled: 0.5/1 at 1.9876.</p>` |
| `data.rows[].content_raw` | object | No | — |
| `data.rows[].content_raw.symbol` | string | Yes | Example: `PERP_NEAR_USDC` |
| `data.rows[].content_raw.side` | string | Yes | Example: `BUY` |
| `data.rows[].content_raw.order_id` | integer | Yes | Example: `1` |
| `data.rows[].content_raw.executed_price` | number | Yes | Example: `1.9876` |
| `data.rows[].content_raw.executed_quantity` | number | Yes | Example: `0.5` |
| `data.rows[].content_raw.executed_timestamp` | integer | Yes | Example: `1567382401000` |
| `data.rows[].mark_read` | integer | No | Read state of the notification. `1` means read and `0` means unread. Example: `1` |
| `data.rows[].operator` | integer | No | Internal operator identifier associated with the notification event. Example: `1` |
| `data.rows[].created_time` | integer | No | Timestamp when the notification was created in milliseconds. Example: `1670425970373` |
| `data.rows[].announcement_id` | integer | No | Related announcement ID when the notification comes from an announcement. |
| `data.meta` | object | Yes | — |
| `data.meta.total` | integer | Yes | Example: `9` |
| `data.meta.records_per_page` | integer | Yes | Example: `25` |
| `data.meta.current_page` | integer | Yes | start from 1 Example: `1` |
