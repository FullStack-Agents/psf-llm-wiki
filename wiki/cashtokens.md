# cashtokens

**Summary**: Overview of the CashTokens system on Bitcoin Cash, including its design for fungibility, unique assets, and smart contract interactions.

**Sources**: cashtokens-intro.md

**Last updated**: 2026-04-18

---

CashTokens provides a framework for issuing and managing digital assets directly on the [bitcoin-cash](bitcoin-cash.md) network. Unlike some token standards that operate as separate layers, CashTokens is a built-in, optional feature of the network (source: cashtokens-intro.md).

## Core Characteristics
- **Counterfeit-Proof**: Tokens cannot be counterfeited and their authenticity can be easily verified by wallets.
- **Non-Destructive**: Tokens cannot be accidentally destroyed by software that is not "token-aware".
- **Scalable**: By utilizing non-fungible tokens to allow contracts to communicate, Bitcoin Cash can support complex [decentralized applications](https://read.cash/@TomZ/scaling-bitcoin-cash-be8344a6) that scale to millions of users without fee spikes (source: cashtokens-intro.md).

## Comparison with SLP
While [simple-ledger-protocol](simple-ledger-protocol.md) (SLP) also provides tokenization on Bitcoin Cash, CashTokens represents a different architectural approach as a built-in feature with specific focus on contract-to-contract communication via non-fungible commitments.

## Related pages

- [cashtokens-intro](cashtokens-intro.md)
- [bitcoin-cash](bitcoin-cash.md)
- [simple-ledger-protocol](simple-ledger-protocol.md)
