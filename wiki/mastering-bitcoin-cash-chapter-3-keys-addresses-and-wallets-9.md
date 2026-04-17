# mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-9

**Summary**: This document provides a technical explanation of Hierarchical Deterministic (HD) wallets, their child key derivation (CKD) mechanism, hardened derivation, and the BIP0044 standard for key path organization.

**Sources**: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_9.md

**Last updated**: 2026-04-17

---

HD wallets enable the organization of keys into a tree structure, allowing a single root seed to generate an infinite number of child keys.

### Child Key Derivation (CKD)
Child keys are created by combining a parent key (private or public), a 256-bit chain code, and a 32-bit index number using **HMAC-SHA512**. 
- The resulting 512-bit hash is split:
    - **Right 256 bits**: Become the child's chain code.
    - **Left 256 bits**: Combined with the parent [private key](private-keys.md) to produce the child [private key](private-keys.md).

### Hardened Derivation
To increase security, HD wallets use "hardened" derivation (denoted by a prime symbol, e.g., $m/0'$). This breaks the mathematical link between a parent [public key](addresses.md) and child chain codes, ensuring that a compromised child key cannot be used to reveal other keys in the tree.

### BIP0044 Standard
BIP0044 defines a standardized path for HD wallets to ensure interoperability:
`m / purpose' / coin_type' / account' / change / address_index`

For [Bitcoin Cash](bitcoin-cash.md), the `coin_type` is `145'`. For example, the path `M/44'/145'/0'/0/2` represents the third receiving [address](addresses.md) for the primary account.

## Related pages

- [digital-wallets](digital-wallets.md)
- [private-keys](private-keys.md)
- [transaction-scripts](transaction-scripts.md)
