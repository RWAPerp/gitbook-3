# RWA Perp B2B API

Integrate with RWA Perp through its REST and WebSocket APIs. Start with the [quick start](getting-started/README.md), then use the authentication, REST API, WebSocket, and API reference sections as needed.

> Default REST: `https://api-trade.rwaperp.xyz` · VIP REST: `https://api-vip.rwaperp.xyz` (same paths and `RWA-*` signing)  
> **To-B partners:** Contact RWA Perp to obtain a dedicated Base URL before using `api-trade`, `api-vip`, or any custom host.  
> **X Layer only** (`chainId = 196`). No other chain is supported.  
> Complete [account onboarding](authentication/onboarding.md) first. Then use the [trading example](rest-api/mainline-script.md) with your API credentials. For signing details, see [Authentication](authentication/README.md).

| Section | Purpose |
|---------|---------|
| [Quick start](getting-started/README.md) | Install dependencies and run the trading example |
| [Authentication](authentication/README.md) | Open an account, bind an API key, and sign requests |
| [REST API](rest-api/README.md) | Request and response conventions, trading, and withdrawals |
| [WebSocket](websocket/README.md) | Public market streams and private account streams |
| [REST API reference](reference/README.md) | Parameters, request bodies, responses, authentication, and rate limits grouped by domain |
