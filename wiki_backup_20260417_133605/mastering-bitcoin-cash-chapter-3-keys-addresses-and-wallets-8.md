# mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-8

**Summary**: This document explains different types of [[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) wallets, detailing the evolution from nondeterministic (JBOK) wallets to deterministic and Hierarchical Deterministic (HD) wallets.

**Sources**: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_8.md

**Last updated**: 2026-04-17

---

Wallets serve as secure containers for private keys. The architecture of how keys are stored and generated varies by wallet type:

### Wallet Types
- **Nondeterministic (JBOK - "Just a Bunch Of Keys")**: Type-0 wallets where keys are randomly generated and have no relationship to one another. Every new key must be backed up separately.
- **Deterministic (Seeded) Wallets**: Keys are derived from a single common seed via one-way hash functions. Backing up the seed is sufficient to recover all keys.
- **Hierarchical Deterministic (HD) Wallets (BIP0032/BIP0044)**: Keys are organized in a tree structure. Parent keys can derive child keys, allowing for organized key management and [public key](addresses.md) derivation without private keys.

### Mnemonic Phrases (BIP0039)
HD wallets typically use a mnemonic phrase (12-24 English words) to represent the random root seed, making it easier for humans to write down and backup the seed value.

## Related pages

- [digital-wallets](digital-wallets.md)
- [private-keys](private-keys.md)
