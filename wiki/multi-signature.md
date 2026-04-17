# Multi-signature

**Summary**: A security mechanism that requires multiple independent private keys to authorize a transaction, eliminating single points of failure.

**Sources**: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets-8.md, mastering-bitcoin-cash_chapter-8-bitcoin-cash-security_9.md

**Last updated**: 2026-04-17

---

## Mechanism
Multi-signature (multi-sig) addresses require a predefined number of signatures from a set of authorized keys to spend funds. For example, in a "2-of-3" setup, any two of the three designated keyholders must sign the transaction for it to be valid (source: mastering-bitcoin-cash_chapter-8-bitcoin-cash-security_9.md).

## Applications
- **Corporate Security**: Keys can be distributed among different executives to prevent a single individual from stealing funds or losing the only copy of a key (source: mastering-bitcoin-cash_chapter-8-bitcoin-cash-security_9.md).
- **Escrow Services**: A 2-of-3 setup can involve a buyer, a seller, and an independent arbitrator.
- **Redundancy**: Users can store backup keys in different geographic locations to ensure they can recover funds if one key is lost.

## Comparison to Single-sig
Unlike standard addresses where one key has total control, multi-sig distributes the security responsibility across different people and locations, providing robust protection for high-value holdings (source: mastering-bitcoin-cash_chapter-8-bitcoin-cash-security_9.md).

## Related pages

- [private-keys](private-keys.md)
- [digital-wallets](digital-wallets.md)
- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-8](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-8.md)
- [mastering-bitcoin-cash-chapter-8-security-9](mastering-bitcoin-cash-chapter-8-security-9.md)
