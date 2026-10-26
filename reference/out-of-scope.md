# Out of scope

| Capability | Notes |
|------------|-------|
| On-chain deposits | The wallet calls the contract directly; this is not a REST operation |
| On-chain withdrawal settlement | REST initiation is covered in [Withdrawals](../rest-api/withdrawals.md); settlement depends on on-chain confirmation |
| Broker admin / rebates | `/v1/admin/*`, `/v1/broker/*`, `/v1/referral/*` |
| Strategy Vault public queries | `/v1/public/strategy_vault/*` is not available through this B2B API base URL |
| Upstream account registration | Use [Account onboarding](../authentication/onboarding.md) (`/v1/register_dex_account`, `/v1/dex_api_key`) instead of upstream register/key endpoints |

This sync excluded **85** published paths (admin, referral, campaign, faucet, alternate data hosts, and upstream registration).
