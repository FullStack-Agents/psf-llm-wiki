# token-examples

**Summary**: Practical examples and high-level constructions enabled by CashTokens, including identity tokens, advanced voting mechanisms, and multithreaded covenants.

**Sources**: CHIP-2022-02-CashTokens (cashtokens.org/docs/spec/examples.md)

**Last updated**: 2026-05-25

---

CashTokens enable a variety of advanced contract constructions on Bitcoin Cash that were previously impossible or inefficient. These include mechanisms for identity management, decentralized governance, and highly scalable application architectures (source: CHIP-2022-02-CashTokens examples.md).

## Identity and Covenant Management

### Identity Tokens
Identity tokens are non-fungible tokens (NFTs) that prove control of a represented identity. Unlike static public keys, identity tokens can be moved independently of the contracts that verify them. This allows users to rotate keys or upgrade to multisig wallets without having to re-create every contract they interact with (source: CHIP-2022-02-CashTokens examples.md).

### Covenant-Tracking Identity Tokens
A covenant can be associated with a **"tracking" identity token**, requiring that spends always re-associate the identity token with the covenant. This provides:
- **Public Interfaces**: Other contracts can authenticate a particular covenant instance using its tracking token.
- **State Optimization**: A covenant's internal state can be stored in the tracking token's `commitment`, **allowing the locking bytecode of covenants to remain unchanged across transactions**.
- **Mutually-Aware Contracts**: Because token category IDs can be known prior to their creation, ecosystems of mutually-aware contracts are straightforward to design (source: CHIP-2022-02-CashTokens examples.md).

### Depository Child Covenants
These are covenants that hold tokens on behalf of a parent covenant. By requiring that the depository be spent only in transactions with the parent, a parent covenant can manage unlimited token portfolios despite the limit of one token prefix per output. This creates a parent-child strategy offering contracts practically unlimited flexibility in holding portfolios of both fungible and non-fungible tokens (source: CHIP-2022-02-CashTokens examples.md).

## Decentralized Governance (Voting)

Fungible tokens allow for sophisticated on-chain voting without hindering the ability to trade or divide shares during the voting period (source: CHIP-2022-02-CashTokens examples.md).

### Voting Strategies
- **Token Category Migration**: Covenants can migrate to new categories based on vote outcomes — shareholders trade pre-vote shares for post-vote shares, incrementing their chosen result. This reveals additional consensus strategies:
  - **Vote-dependent, post-vote token categories**: Different post-vote categories can be issued for different outcomes, allowing trading even before the voting period ends. Differences are immediately reflected in market prices.
  - **Covenant spin-offs**: Participants can choose between receiving shares in a new covenant or alternative compensation (source: CHIP-2022-02-CashTokens examples.md).
- **Voting Receipts**: Covenants can issue NFT "receipts" in exchange for deposited fungible tokens, allowing voters to reclaim their shares after the period ends.
- **Single-use voting tokens**: Covenants issue multiple batches of single-use tokens for deposits. Redeeming the original deposit may require returning a subset of these tokens.
- **Off-chain voting**: Votes can be conducted via [Bitauth signature](https://github.com/bitauth/bitauth-cli) from any output holding fungible tokens at a previously-announced block height (source: CHIP-2022-02-CashTokens examples.md).

### Sealed Voting
Voters cast a **sealed vote** — a message containing the number of share-votes cast and a hash of their vote with a salt — by minting a **sealed vote NFT** from the vote-taking covenant. After the voting period ends, participants re-submit sealed vote NFTs to aggregate results. This construction can be augmented with:
- **Voting quorum**: Requiring minimum percentage of sealed votes
- **Unsealing quorum**: Requiring minimum percentage to be unsealed before results are final
- **Sealing deposits**: Requiring deposits with sealed votes
- **Enforced vote secrecy**: Allowing proofs that another voter divulged their vote early, penalizing them (a strategy developed for [Truthcoin](https://bitcoinhivemind.com/papers/truthcoin-whitepaper.pdf)) (source: CHIP-2022-02-CashTokens examples.md).

## Multithreaded Covenants

To avoid "spend races" (where multiple users attempt to spend the same UTXO), CashTokens enable **multithreaded covenants**.

### Threading Architecture
A parent covenant can offload logic to "thread" sub-covenants. Users interact with multiple UTXOs in parallel, and results are "checked in" to the parent in batches. This allows Bitcoin Cash to maintain its high-parallelism advantage while providing a consistent user experience (source: CHIP-2022-02-CashTokens examples.md).

### Thread Management
- **Lifetimes and Heartbeats**: Threads can have fixed lifetimes (decrementing counters) or renewing "heartbeats" (renewed via locktime/sequence numbers) to prevent DOS attacks and ensure periodic check-in windows.
- **Proof-of-work**: Some threads may rate-limit by requiring preimages with required hash prefixes (though fees/deposits are more uniform).
- **Managed Threads**: High-activity threads can require authorization from specific keys or NFTs to order transactions without contention. Given typical propagation speed (99% at 2 seconds), multithreaded apps can expect minimal contention when thread count exceeds 2 per interaction per second (source: CHIP-2022-02-CashTokens examples.md).

## Demonstrated Applications
The **Joint-Execution Decentralized Exchange (Jedex)** serves as a technical demonstration of these concepts, implementing a multi-covenant DEX supporting trades between fungible tokens and BCH. A full [list of demonstrated concepts](https://github.com/bitjson/jedex#demonstrated-concepts) and the [application-specific token API](https://github.com/bitjson/jedex#jedex-token-api) are documented in the Jedex repository (source: CHIP-2022-02-CashTokens examples.md).

## Related pages

- [cashtokens](cashtokens.md)
- [cashtokens-spec](cashtokens-spec.md)
- [cashtoken-rationale](cashtoken-rationale.md)
- [bitcoin-cash](bitcoin-cash.md)
- [script](script.md)
