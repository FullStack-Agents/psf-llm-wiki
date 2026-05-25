# cashtokens

**Summary**: Overview of the CashTokens system on Bitcoin Cash, including its design for fungibility, unique assets, and smart contract interactions.

**Sources**: cashtokens-intro.md

**Last updated**: 2026-04-18

---

CashTokens provides a framework for issuing and managing digital assets directly on the [bitcoin-cash](bitcoin-cash.md) network. Unlike some token standards that operate as separate layers, CashTokens is a built-in, optional feature of the network — activated in the **May 2023 Bitcoin Cash upgrade** (source: cashtokens.org/docs/intro.md).

## Core Characteristics
- **Counterfeit-Proof**: Tokens cannot be counterfeited and their authenticity can be easily verified by wallets.
- **Non-Destructive**: Tokens cannot be accidentally destroyed by software that is not "token-aware".
- **Scalable**: By utilizing non-fungible tokens to allow contracts to communicate, Bitcoin Cash can support complex [decentralized applications](https://read.cash/@TomZ/scaling-bitcoin-cash-be8344a6) that scale to millions of users without fee spikes (source: cashtokens.org/docs/intro.md).

## Design Principles
- **Fungible vs. Non-Fungible**: The specification cleanly separates these two primitives, recognizing that token fungibility and token commitments are conceptually incompatible (source: CHIP-2022-02-CashTokens).
- **Opt-In**: Token-aware wallets use distinct CashAddress types, preventing tokens from being sent to incompatible wallets (source: CHIP-2022-02-CashTokens).
- **Stateless Contract Interoperability**: NFTs enable covenants to authenticate each other without shared global state, preserving Bitcoin Cash's massive parallel validation advantage (source: CHIP-2022-02-CashTokens).

## Ecosystem Support
The CashTokens CHIP received widespread approval from the Bitcoin Cash ecosystem:
- **Nodes**: BCHN, Bitcoin Verde, Bitcoin Unlimited, Flowee, Knuth, BCHD
- **Wallets**: Electron Cash, Paytaca, Cashual, Melis, Flowee Pay, Guarda, Verde Wallet, Zapit
- **Projects**: Chaingraph, Libauth, CashScript, AnyHedge, Fulcrum, Bitauth IDE, [FullStack.Cash](https://fullstack.cash/), and the [Permissionless Software Foundation](https://psfoundation.cash/)
- **Industry**: Antpool, Bitcoin.com (neutral), and many exchanges
(source: CHIP-2022-02-CashTokens)

## Comparison with SLP
While [simple-ledger-protocol](simple-ledger-protocol.md) (SLP) also provides tokenization on Bitcoin Cash, CashTokens represents a different architectural approach as a built-in feature with specific focus on contract-to-contract communication via non-fungible commitments.

## Related pages

- [cashtokens-intro](cashtokens-intro.md)
- [cashtokens-spec](cashtokens-spec.md)
- [cashtoken-rationale](cashtoken-rationale.md)
- [cashtoken-alternatives](cashtoken-alternatives.md)
- [cashtoken-stakeholders](cashtoken-stakeholders.md)
- [token-examples](token-examples.md)
- [bcmr-spec](bcmr-spec.md)
- [bcmr-examples](bcmr-examples.md)
- [bitcoin-cash](bitcoin-cash.md)
- [simple-ledger-protocol](simple-ledger-protocol.md)
