# GAZYAVA — token launch blueprint (working draft)

**Status:** planning document only. Nothing here is a promise, final token allocation, sale offer, or guarantee of value. Token name/ticker, chain, supply, launch date, jurisdiction, and legal structure remain undecided.

## 1. Product principles

1. The tap game remains playable without buying a token.
2. Game points are an off-chain gameplay score, not a token, deposit, claim, or promise of conversion.
3. Do not publish a fixed points-to-token rate before anti-abuse rules, eligibility, snapshot dates, supply, and legal review are complete.
4. No paid gameplay advantage that makes rewards depend on spending.
5. Publish allocation, vesting, treasury wallets, unlock schedule, and material changes before any token distribution.

## 2. Current game baseline (database snapshot, 2026-11-18)

- Registered players: 20
- Players updated in the last 7 days: 20
- Aggregate game points: 31,973
- Highest individual balance: 25,204

These are a small, early-stage sample, not a reliable basis for setting token supply or an airdrop conversion. The concentration of points in one account also means raw points should not be the only eligibility criterion.

## 3. Illustrative allocation model — discussion only

A possible starting framework for community feedback; percentages are not approved:

| Bucket | Illustrative share | Intended use |
|---|---:|---|
| Community & player rewards | 40% | Season rewards, quests, referral and ecosystem campaigns |
| Liquidity | 20% | Initial and ongoing liquidity, subject to a published policy |
| Ecosystem & development | 15% | Integrations, product development, grants |
| Core contributors | 10% | Long-term contributor incentives with vesting |
| Treasury / reserve | 10% | Audited, governed future needs |
| Marketing & partnerships | 5% | Disclosed campaigns and partnerships |
| **Total** | **100%** | |

Before approval, define the fully diluted supply, vesting dates, wallet controls, governance and reporting. Contributor tokens should have a cliff and linear vesting rather than being fully unlocked at launch.

## 4. Fair player-reward design

Use a multi-signal eligibility model rather than a simple balance conversion:

- Verified Telegram account and account-age / activity checks.
- Meaningful gameplay across multiple days, not just one burst of taps.
- Referral quality checks; exclude self-referrals, duplicate identities and suspicious clusters.
- Completed daily tasks and streak participation as supporting signals.
- A published snapshot window and dispute process.
- Per-account caps or diminishing returns to reduce whale concentration.
- Anti-bot review and a documented appeals process.

A future season points score may inform a reward pool, but the formula and snapshot must be announced before the season starts. Never retroactively change a published formula.

## 5. Launch gates

- [ ] Choose chain after considering wallet UX, fees, ecosystem, security and compliance.
- [ ] Obtain legal advice for target jurisdictions, token classification, marketing, sanctions and distribution restrictions.
- [ ] Finalize token utility that exists beyond speculative trading; do not promise profit or price appreciation.
- [ ] Approve supply, allocation, vesting, emissions and treasury policy.
- [ ] Publish smart-contract source and obtain an independent security audit before mainnet deployment.
- [ ] Establish multisig custody, role separation, emergency pause policy and public wallet disclosures.
- [ ] Define airdrop eligibility, snapshot, Sybil review, claim window, unclaimed-token handling and support process.
- [ ] Test claim flow and wallet recovery/support on testnet.
- [ ] Publish risks, terms, privacy notice and a clear statement that game points are not tokens.

## 6. Decisions still required

- Token ticker and final name
- Chain and contract standard
- Fixed supply vs. capped / emissions-based supply
- Actual utility and governance scope
- Jurisdictions and eligible / excluded regions
- Whether player rewards are an airdrop, season-based claims, or another compliant mechanism
- Launch timing and liquidity policy

## 7. Immediate next implementation step

Do not mint or promise token balances yet. First add a transparent season system to the game: season start/end, eligible activity metrics, anti-abuse flags, immutable snapshot record, and a public rules page. Keep the game-point ledger separate from any future token claim ledger.
