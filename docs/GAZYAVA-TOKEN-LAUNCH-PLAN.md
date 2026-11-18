# GAZYAVA — GZV token launch plan

**Status (19 November 2026): approved working baseline.** The project has selected Solana, the GZV ticker, a proposed fixed supply of 1,000,000,000 GZV, and the allocation split below for further design. This is not a deployed token, final legal disclosure, sale offer, or promise of value. Mainnet minting and public distribution are on hold until all legal, security, custody, and operational launch gates are completed.

## 1. Product principles

1. The tap game remains playable without buying a token.
2. Game points are an off-chain gameplay score, not a token, deposit, claim, or promise of conversion.
3. No fixed points-to-token conversion rate is promised. Any community distribution needs separately published eligibility, snapshot, anti-abuse, and legal rules.
4. No paid gameplay advantage that makes rewards depend on spending.
5. Publish allocation, vesting, treasury wallets, unlock schedule, and material changes before any token distribution.

## 2. Approved working token parameters

| Parameter | Working decision |
|---|---|
| Project / token name | Gazyava-Coin |
| Ticker | GZV |
| Network | Solana |
| Proposed total supply | 1,000,000,000 GZV |
| Supply model | Fixed initial supply; no discretionary ongoing emissions intended |
| Status | Not created / not launched |

The exact Solana token program (classic SPL Token or Token-2022), decimals, metadata authority, mint authority and freeze authority policy still require technical review. Do not assume any authority has been revoked until verified on-chain.

## 3. Approved working allocation baseline

The following split is approved as the working baseline. It remains subject to legal, tax, liquidity, custody, and operational review before minting or distribution.

| Allocation | Share | Amount at proposed supply | Intended use |
|---|---:|---:|---|
| Community & player rewards | 40% | 400,000,000 GZV | Season rewards, quests and ecosystem campaigns |
| Liquidity | 20% | 200,000,000 GZV | Initial and ongoing liquidity under a published policy |
| Ecosystem & development | 15% | 150,000,000 GZV | Product development, integrations and grants |
| Core contributors | 10% | 100,000,000 GZV | Long-term contributor incentives with vesting |
| Treasury / reserve | 10% | 100,000,000 GZV | Disclosed, governed future needs |
| Marketing & partnerships | 5% | 50,000,000 GZV | Disclosed campaigns and partnerships |
| **Total** | **100%** | **1,000,000,000 GZV** | |

These are allocation budgets, not existing balances, wallet reserves, or circulating supply. Before launch, publish recipient / wallet policy, vesting and cliff schedules, liquidity deployment policy, multisig signers and thresholds, treasury reporting, and treatment of unclaimed community allocations. Contributor tokens should have a cliff and linear vesting rather than being fully unlocked at launch.

## 4. Fair player-reward design

Use a multi-signal eligibility model rather than a simple balance conversion:

- Verified Telegram account and account-age / activity checks.
- Meaningful gameplay across multiple days, not just one burst of taps.
- Referral quality checks; exclude self-referrals, duplicate identities and suspicious clusters.
- Completed daily tasks and streak participation as supporting signals.
- A published snapshot window and dispute process.
- Per-account caps or diminishing returns to reduce concentration.
- Anti-bot review and a documented appeals process.

A future season points score may inform a reward pool, but the formula and snapshot must be announced before the qualifying season starts. Never retroactively change a published formula. Game points remain separate from any future token claim ledger.

## 5. Launch gates

- [x] Select Solana as the target network for the working design.
- [x] Approve GZV as the working ticker.
- [x] Approve the 1,000,000,000 GZV working supply target.
- [x] Approve the 40 / 20 / 15 / 10 / 10 / 5 working allocation split.
- [ ] Confirm final legal name, metadata and ticker availability.
- [ ] Select classic SPL Token vs. Token-2022 after feature and security review.
- [ ] Confirm decimals and exact mint / freeze authority policy.
- [ ] Obtain Netherlands / EU legal advice on MiCA, white-paper and notification requirements, marketing, consumer disclosures, sanctions, tax, and geographic restrictions. Do not assume an exemption applies.
- [ ] Finalize token utility, vesting, treasury policy and recipient wallet rules; do not promise profit or price appreciation.
- [ ] Establish hardware-wallet-backed multisig custody, role separation and public wallet disclosures.
- [ ] Publish smart-contract / program configuration and obtain an independent security review before mainnet deployment.
- [ ] Define community reward eligibility, snapshot, Sybil review, claim window, unclaimed-token handling and appeals process.
- [ ] Test mint, transfers, authority changes and any claim flow on devnet.
- [ ] Publish risk disclosures, terms, privacy notice and a clear statement that game points are not tokens.

## 6. Execution sequence

1. Reconcile all public tokenomics references and retire outdated allocation drafts.
2. Obtain qualified legal advice for the intended jurisdictions before any public offer, promotion, distribution or admission to trading.
3. Finalize token metadata, token program, decimals, supply, mint / freeze authority handling, and an independently reviewed creation runbook.
4. Set up hardware-wallet-backed multisig custody for treasury and liquidity. Never put seed phrases or private keys in source code, GitHub, chat, or a hosted backend.
5. Publish community reward eligibility, anti-Sybil process, snapshot timing, claims and appeals before the qualifying period begins.
6. Prepare and execute the disposable Devnet rehearsal using the [GZV Solana Devnet runbook](./GZV-SOLANA-DEVNET-RUNBOOK.md); test mint, transfers, authority states and any claim flow, then obtain an independent security review.
7. Only after all gates are signed off, create the mainnet mint, verify it on a Solana explorer, publish the mint address and authority state, and execute liquidity under the disclosed policy.

**No mainnet token has been created by this plan.** Never share seed phrases or private keys with anyone, including project contributors or support staff.
