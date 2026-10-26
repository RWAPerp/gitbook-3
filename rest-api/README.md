# REST API overview

Use the REST API for market data, account queries, order management, and withdrawals.

## Request and response conventions

Most REST responses use the following JSON envelope. Clients should still inspect the HTTP status and `Content-Type`, because some error responses may be returned as plain text.

**Success**

```json
{"success": true, "data": {}, "timestamp": 1781628474510}
```

Some endpoints use `ts` instead of `timestamp`:

```json
{"success": true, "data": {}, "ts": 1781628475491}
```

**Failure**

```json
{"success": false, "code": -1002, "message": "Error description"}
```

| Field | Description |
|-------|-------------|
| `success` | Whether the business operation succeeded |
| `data` | Payload; usually omitted on failure |
| `code` / `message` | Error code and description on failure |
| `timestamp` / `ts` | Server time in milliseconds |

### Request construction

| Method | Request | Signed path includes |
|--------|---------|----------------------|
| GET / DELETE | URL **query** (`?symbol=...&status=NEW`) | The query string |
| POST / PUT | **JSON body** (`Content-Type: application/json`) | The body string exactly as sent |
| Path parameters | Substitute `{symbol}`, `{order_id}`, etc. | The expanded path |

Private endpoints additionally carry `RWA-*` headers; see [Request signing](../authentication/request-signing.md) for the rules. **The POST body must be byte-for-byte identical to what was signed.**

### Response `data` shapes

Common `data` shapes include:

| Shape | Structure | Typical endpoints |
|-------|-----------|-------------------|
| **Single object** | `{ field: value, ... }` | `GET /v1/public/futures/{symbol}`, `GET /v1/client/info` |
| **List** | `{ "rows": [ ... ] }` | `GET /v1/public/info`, `GET /v1/positions` |
| **Paged list** | `{ "rows": [ ... ], "meta": { ... } }` or `"next_cursor"` | `GET /v1/orders`, `GET /v1/trades`, order queries under `public/query` |

Use the [REST API reference](../reference/README.md) for endpoint-specific parameters, request bodies, response fields, authentication requirements, and rate limits. For the primary trading operations, see the [trading workflow](trading-workflow.md).
