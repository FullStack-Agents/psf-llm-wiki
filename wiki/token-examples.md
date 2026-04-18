# token-examples

**Summary**: Practical examples and high-level constructions enabled by CashTokens, including identity tokens, advanced voting mechanisms, and multithreaded covenants.

**Sources**: token-examples.md

**Last updated**: 2026-04-18

---

CashTokens enable a variety of advanced contract constructions on Bitcoin Cash that were previously impossible or inefficient. These include mechanisms for identity management, decentralized governance, and highly scalable application architectures (source: token-examples.md).

## Identity and Covenant Management

### Identity Tokens
Identity tokens are non-fungible tokens (NFTs) that prove control of a represented identity. Unlike static public keys, identity tokens can be moved independently of the contracts that verify them. This allows users to rotate keys or upgrade to multisig wallets without having to re-create every contract they interact with (source: token-examples.md).

### Covenant-Tracking Identity Tokens
A covenant can be associated with a "tracking" identity token. This provides:
- **Public Interfaces**: Other contracts can authenticate a particular covenant instance using its tracking token.
- **State Optimization**: A covenant's internal state can be stored in the tracking token's `commitment`, allowing the locking bytecode to remain constant across transactions (source: token-examples.md).

### Depository Child Covenants
These are covenants that hold tokens on behalf of a parent covenant. By requiring that the depository be spent only in transactions with the parent, a parent covenant can manage unlimited token portfolios despite the limit of one token prefix per output (source: token-examples.md).

## Decentralized Governance (Voting)

Fungible tokens allow for sophisticated on-chain voting without hindering the ability to trade or divide shares during the voting period (source: token-examples.md).

### Voting Strategies
- **Token Category Migration**: Covenants can migrate to new categories based on vote outcomes. This allows post-vote tokens to reflect market prices for different outcomes immediately.
- **Voting Receipts**: Covenants can issue NFT "receipts" in exchange for deposited fungible tokens, allowing voters to reclaim their shares after the period ends.
- **Sealed Voting**: Voters mint a "sealed vote NFT" containing a hash of their vote and a salt. This keeps votes secret until the unsealing period, where results are aggregated (source: token-examples.md).

## Multithreaded Covenants

To avoid "spend races" (where multiple users attempt to spend the same UTXO), CashTokens enable **multithreaded covenants**.

### Threading Architecture
A parent covenant can offload logic to "thread" sub-covenants. Users interact with multiple UTXOs in parallel, and results are "checked in" to the parent in batches. This allows Bitcoin Cash to maintain its high-parallelism advantage while providing a consistent user experience (source: token-examples.md).

### Thread Management
- **Lifetimes and Heartbeats**: Threads can have fixed lifetimes or renewing "heartbeats" to prevent DOS attacks and ensure periodic check-in windows.
- **Managed Threads**: High-activity threads can require authorization from specific keys or NFTs to order transactions without contention (source: token-examples.md).

## Demonstrated Applications
The **Joint-Execution Decentralized Exchange (Jedex)** serves as a technical demonstration of these concepts, implementing a multi-covenant DEX supporting trades between fungible tokens and BCH (source: token-examples.md).

## Related pages

- [cashtokens](cashtokens.md)
- [cashtokens-spec](cashtokens-spec.md)
- [bitcoin-cash](bitcoin-cash.md)
