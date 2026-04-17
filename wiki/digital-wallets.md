# Digital Wallets

**Summary**: Software or hardware used to store cryptographic keys for managing Bitcoin Cash and managing the construction of transactions.

**Sources**: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-(BCH)_1.md, mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_8.md

**Last updated**: 2026-04-16

---

Digital wallets are used to store the cryptographic keys required to prove ownership of Bitcoin Cash. The [[private-keys]] stored within the wallet are the essential requirement to unlock and spend bitcoins (source: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-(BCH)_1.md). 

Wallets are independent of the Bitcoin Cash protocol and can be generated without an internet connection or blockchain access (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_2.md).

### Functionality
Wallets vary in how they manage keys:
- **Nondeterministic (JBOK)**: Each key is random and must be backed up individually (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_8.md).
- **Deterministic**: All keys are derived from a single seed; backing up the seed recovers all keys (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_8.md).
- **Hierarchical Deterministic (HD)**: Keys are organized in a tree structure (BIP0032/BIP0044), often backed up using mnemonic phrases (BIP0039) of 12-24 words (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_8.md). HD wallets use a Child Key Derivation (CKD) function and can utilize "hardened" derivation to prevent compromised child keys from revealing other keys in the tree (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_9.md).

Contrary to a physical wallet, a digital wallet does not store "coins" but rather manages the keys and tracks [[utxo]] (Unspent Transaction Outputs) associated with those keys to identify available funds (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_8.md).

When a user initiates a payment, the wallet application automatically handles the complexities of the [[transaction-process]], including:
- Selecting appropriate inputs.
- Creating outputs.
- Calculating change.
- Applying digital signatures.

### Offline Transactions
A key feature of Bitcoin Cash wallets is the ability to construct transactions offline. A transaction can be signed and created while disconnected from the network and transmitted to the peer-to-peer network once connectivity is available (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_8.md).

## Related pages

- [[bitcoin-cash]]
- [[private-keys]]
- [[utxo]]
- [[transaction-process]]
- [[mastering-bitcoin-cash-chapter-1]]
- [[mastering-bitcoin-cash-chapter-2]]
