# cauldron-intro

**Summary**: Introduction to Cauldron DEX, a decentralized exchange on Bitcoin Cash (BCH) for swapping and providing liquidity to native CashTokens, developed by Riften Labs.

**Sources**: docs.riftenlabs.com

**Last updated**: 2026-05-31

---

Cauldron DEX is a decentralized exchange on the [bitcoin-cash](bitcoin-cash.md) network that enables users to swap [cashtokens](cashtokens.md) and provide liquidity. Developed by the Norwegian company **Riften Labs AS**, Cauldron operates as a non-custodial automated liquidity protocol emphasizing openness, transparency, and user accessibility (source: docs.riftenlabs.com).

## Motivation

Cauldron was created to bring DeFi to Bitcoin Cash, addressing several key goals (source: docs.riftenlabs.com):
- Bring DeFi functionality to the BCH ecosystem
- Increase liquidity on the BCH network
- Grow the [cashtokens](cashtokens.md) ecosystem
- Onboard DeFi users and liquidity
- Pull coins from centralized exchange markets into BCH's Total Value Locked (TVL)

## How It Works

Cauldron DEX utilizes the **Automated Market Maker (AMM)** model. It consists of a series of smart contracts that standardize the processes for creating liquidity pools and swapping CashTokens. All fungible CashTokens are compatible, and Cauldron recognizes both **BCMR** ([bcmr-spec](bcmr-spec.md)) and **CRC20** token metadata (source: docs.riftenlabs.com).

### User Interface

Users can interact with Cauldron via the web application at [app.cauldron.quest](https://app.cauldron.quest) by connecting a Bitcoin Cash wallet via WalletConnect or creating a new in-browser Cauldron wallet (source: docs.riftenlabs.com).

## Liquidity Provision

### Micro-Pools

Liquidity provisioning on Cauldron works through **micro-pools** — individual liquidity pools that anyone can set up for any token pair. Liquidity providers (LPs) retain full ownership of their pool and earn fees from trades that occur through it (source: docs.riftenlabs.com).

### Fees
- **LP Fee**: 0.3% per swap, paid entirely to the liquidity provider
- **Cauldron Fee**: None — Cauldron takes no trade fee
- **Slippage**: Any slippage also goes to LP earnings
- **Network Fee**: Standard Bitcoin Cash network fee applies

### Impermanent Loss

Impermanent loss is the difference between holding tokens in a wallet versus staking them in a liquidity pool. It occurs when the price ratio of tokens in a DEX pool changes from when they were deposited. It becomes permanent if assets are withdrawn while prices remain diverged (source: docs.riftenlabs.com).

### Yield Calculation

LP rewards are not shown as a separate balance — they are reflected in the growth of the pool's value over time. The Cauldron interface shows an **APY (Annual Percentage Yield)** based on the growth of √K over time, where K is the constant product of the pool's reserves (source: docs.riftenlabs.com).

When users swap through a micro-pool, the 0.3% fee is added to the pool's reserves, increasing the pool's constant product (K). The difference between the current K and the initial K represents the earned yield.

## Supported Tokens

All fungible [cashtokens](cashtokens.md) are compatible with Cauldron DEX. The platform recognizes BCMR and CRC20 token metadata registries for token identification and display (source: docs.riftenlabs.com).

## Links

- **Website**: [cauldron.quest](https://cauldron.quest)
- **App**: [app.cauldron.quest](https://app.cauldron.quest)
- **Docs**: [docs.riftenlabs.com](https://docs.riftenlabs.com/cauldron/)
- **Twitter**: [@cauldronswap](https://twitter.com/cauldronswap)
- **TVL**: [Cauldron on DefiLlama](https://defillama.com/protocol/cauldron)
- **Contact**: hello@cauldron.quest

## Related pages

- [cashtokens](cashtokens.md)
- [cashtokens-intro](cashtokens-intro.md)
- [cauldron-api](cauldron-api.md)
- [bcmr-spec](bcmr-spec.md)
- [bitcoin-cash](bitcoin-cash.md)
