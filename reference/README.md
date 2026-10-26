# REST API reference

Base URL: `https://api-trade.rwaperp.xyz` (default). Dedicated VIP REST: `https://api-vip.rwaperp.xyz` (same paths and `RWA-*` signing). **To-B partners:** contact RWA Perp to obtain a dedicated Base URL before using `api-trade`, `api-vip`, or any custom host. This reference contains **147** endpoints grouped by domain. Open an endpoint from the tables below to view its parameters, request body, response fields, authentication requirement, and rate limit.

Schemas are adapted from the published API specification supplied for this integration. RWA Perp's base URL, `RWA-*` authentication headers, X Layer restriction, and RWA-specific signing flows are authoritative for this document.

Three RWA-specific operations—`POST /v1/public/query`, `POST /v1/register_dex_account`, and `POST /v1/dex_api_key`—are documented in the local integration guides.

General request and response conventions are documented in the [REST API overview](../rest-api/README.md).

- **Auth = None**: call directly
- **Auth = RWA**: see [request signing](../authentication/request-signing.md)
- **Auth = Wallet**: `register_dex_account` / `dex_api_key`
- **Auth = Wallet + RWA**: `withdraw_request` ([Withdrawals](../rest-api/withdrawals.md))

| Section | Count |
|---------|-------|
| [Public market data](public-market-data.md) | 33 |
| [Candles and TradingView](candles-tradingview.md) | 5 |
| [Trading and orders](trading-orders.md) | 28 |
| [Positions and leverage](positions-leverage.md) | 14 |
| [Account](account.md) | 15 |
| [Funds and settlement](funds-settlement.md) | 18 |
| [Account registration and API keys](registration-api-keys.md) | 2 |
| [Strategy Vault](strategy-vault.md) | 6 |
| [Staking and Valor](staking-valor.md) | 11 |
| [Volume statistics](volume-statistics.md) | 3 |
| [Notifications](notifications.md) | 4 |
| [Liquidator](liquidator.md) | 1 |
| [Other endpoints](other.md) | 7 |
| [Out of scope](out-of-scope.md) | — |

For public GET endpoints, replace `{symbol}` with a value such as `PERP_ETH_USDC`.
