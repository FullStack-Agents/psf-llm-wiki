# mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-10

**Summary**: This document explains Pay-to-Script-Hash (P2SH) addresses and multi-signature (multi-sig) configurations, allowing for complex spending conditions beyond a single public key owner.

**Sources**: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_10.md

**Last updated**: 2026-04-17

---

Bitcoin Cash supports advanced address types that allow for flexible spending conditions.

### Pay-to-Script-Hash (P2SH)
P2SH addresses (which historically began with "3") designate the beneficiary as the hash of a **script** rather than a public key. This allows for the implementation of complex spending logic.

To create a P2SH address, the same double-hash function (SHA256 followed by RIPEMD160) is applied to a script instead of a public key.

### Multi-Signature (Multi-sig)
The most common use of P2SH is the **multi-signature** address, which requires a specific number of signatures from a set of available keys to authorize a spend.
- **M-of-N Multi-sig**: Requires $M$ signatures from a total of $N$ keys.
- **Examples**:
    - **1-of-2**: Either of two keys can authorize the spend (analogous to a joint bank account).
    - **2-of-3**: At least two of three keys must authorize the spend, providing distributed control and redundancy.

This system provides enhanced security for businesses, shared funds, and organizational control by distributing signing authority across multiple parties.

## Related pages

- [addresses](addresses.md)
- [transaction-scripts](transaction-scripts.md)
- [private-keys](private-keys.md)
