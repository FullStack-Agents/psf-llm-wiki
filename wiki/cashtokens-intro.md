# cashtokens-intro

**Summary**: Introduction to CashTokens, a built-in feature of Bitcoin Cash (BCH) that allows for the creation and use of fungible and non-fungible tokens on the network.

**Sources**: cashtokens-intro.md

**Last updated**: 2026-05-21

---

CashTokens are digital assets that can be created and used on the global, decentralized [bitcoin-cash](bitcoin-cash.md) network. Issued by any person, organization, or decentralized application, they are designed to be counterfeit-proof, verifiable by wallets, and safe from accidental destruction (source: cashtokens.org/docs/intro.md).

## Contract-Issued Commitments

Before CashTokens, Bitcoin Cash contracts could only issue commitments through transaction signatures (requiring a private key) or data signatures (via `OP_CHECKDATASIG`). Because contracts cannot hold private keys, they relied on trusted external entities for verifiable messages. CashTokens solves this by providing a commitment primitive usable directly by contracts, enabling **decentralized oracles** and cross-contract communication without increasing validation costs (source: CHIP-2022-02-CashTokens).

## Cross-Contract Interfaces

Using NFTs as authenticated commitments, contracts can create **impersonation-proof messages** read by other contracts. This allows behavior to be broken into smaller, coordinating contracts — reducing transaction sizes. Covenants can communicate over **public interfaces**, allowing diverse ecosystems of compatible covenants to work together even when developed separately. Critically, this is achieved within Bitcoin Cash's stateless UTXO model, retaining its >1000x efficiency advantage over account-based models (source: CHIP-2022-02-CashTokens).

## Token Types

### Fungible Tokens
Fungible tokens have a total supply where each unit is identical to any other unit. They can be merged and divided, making them suitable for representing:
- Off-chain assets: Stocks, bonds, stablecoins, regional currencies, and loyalty points.
- On-chain assets: Voting shares, utility tokens, and collateralized loans.
- Coordination tasks: Liquidity pooling, auctions, and mergers (source: cashtokens-intro.md).

### Non-Fungible Tokens (NFTs)
Non-fungible tokens are unique units that cannot be merged or divided. In CashTokens, they are authenticated messages belonging to a **token category**. They allow contracts to attest to a **commitment** in an impersonation-proof way, enabling covenants to design public interfaces for other contracts (source: cashtokens-intro.md).

## Decentralized Applications (dApps)
Non-fungible tokens enable contracts to "call" other contracts while maintaining the high performance of Bitcoin Cash (which can handle 25,000 transactions per second on modest hardware). Because BCH covenants do not rely on miners for transaction ordering, dApps can scale to millions of users without increasing transaction fees (source: cashtokens-intro.md).

## Opt-In Support
CashTokens are an optional feature. Token-supporting wallets use unique payment addresses or query parameters to signal their capability. This ensures that BCH-only wallets remain compatible and can continue to operate without needing to support token functionality (source: cashtokens-intro.md).

## Related pages

- [bitcoin-cash](bitcoin-cash.md)
- [simple-ledger-protocol](simple-ledger-protocol.md)
- [slp-nft-1](slp-nft-1.md)
