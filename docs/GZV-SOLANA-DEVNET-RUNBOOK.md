# GZV — Solana Devnet preparation runbook

**Status (19 November 2026): preparation only.** This runbook is for a disposable Devnet rehearsal. It does not authorize a Mainnet mint, public distribution, sale, liquidity deployment, or marketing claim.

## Confirmed working baseline

- Project / proposed token name: Gazyava-Coin
- Proposed ticker: GZV
- Target network: Solana
- Proposed initial supply: 1,000,000,000 GZV
- Working allocation: 40% community/player rewards, 20% liquidity, 15% ecosystem/development, 10% contributors, 10% treasury, 5% marketing
- No token has been created; game points are not tokens and do not promise conversion.

## Decisions required before a Devnet mint

Record these in a reviewed change to the launch plan before running the mint commands:

1. Token program: classic SPL Token or Token-2022. Prefer the simplest program that meets the product requirements; do not select Token-2022 features without a concrete need and review.
2. Decimals: choose and document the value. Nine decimals is a common Solana convention, not an approved GZV setting.
3. Mint authority: decide whether to revoke it immediately after minting the full test supply, or retain it temporarily for controlled test iterations. Devnet only.
4. Freeze authority: decide whether the token needs freeze functionality at all. If not, create without a freeze authority or revoke it after tests. Understand that revocation is irreversible.
5. Metadata: decide who can update name, symbol, URI and image, and when metadata update authority will be relinquished.
6. Test distribution: choose test wallets and small transfer amounts. Never use production treasury or user wallets for Devnet.

## Local tooling and wallet isolation

Install the official Solana CLI and SPL Token CLI from their official documentation. Check versions before use:

```sh
solana --version
spl-token --version
```

Create a dedicated Devnet-only keypair. Do not import a Mainnet wallet or reuse a production key:

```sh
solana-keygen new --outfile ~/.config/solana/gazyava-devnet.json
solana config set --url https://api.devnet.solana.com
solana config set --keypair ~/.config/solana/gazyava-devnet.json
solana address
solana airdrop 2
solana balance
```

The keypair file is secret. Keep it only on the local machine, protect it with OS disk encryption, and never paste its contents into chat, a repository, a website, or a server. Devnet airdrops are test funds with no monetary value.

## Devnet rehearsal — only after the decisions above

The following is a rehearsal outline, not a command to execute until the token program, decimals and authority policy are written down. Start with a disposable Devnet keypair:

```sh
# Example only: replace <DECIMALS> with the reviewed decision.
spl-token create-token --decimals <DECIMALS>
```

Save the returned mint address in a local test log. Verify the mint on the Solana Devnet Explorer. Then create a test token account and mint only the proposed test supply on Devnet:

```sh
spl-token create-account <DEVNET_MINT_ADDRESS>
spl-token mint <DEVNET_MINT_ADDRESS> 1000000000
spl-token supply <DEVNET_MINT_ADDRESS>
spl-token accounts
```

Do not copy these commands to Mainnet. Do not use a Mainnet RPC URL or production keypair in this rehearsal.

## Acceptance checklist

- [ ] Dedicated Devnet keypair used; no production key material involved.
- [ ] Token program and decimals match the reviewed decision.
- [ ] Devnet mint address and program ID recorded.
- [ ] Mint supply equals the test target shown by the CLI and explorer.
- [ ] Transfers between two test wallets succeed.
- [ ] Balances and supply reconcile after transfers.
- [ ] Mint and freeze authority states are inspected and recorded.
- [ ] Metadata renders correctly and its update authority is understood.
- [ ] A second reviewer checks the recorded mint address and configuration.
- [ ] No Mainnet action, public sale, liquidity deployment, or player claim is performed.

## Mainnet stop conditions

Mainnet remains blocked until qualified Netherlands/EU legal counsel has reviewed the intended activities and disclosures; token utility, allocation vesting, recipient and treasury policies are final; multisig custody and signer controls are established; independent security review is complete; and all public documentation is consistent. Devnet success is not legal approval or a security audit.

Never send seed phrases or private keys to anyone. No project contributor or support agent needs them.
