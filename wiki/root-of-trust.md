# Root of Trust

**Summary**: The foundational security principle where trust is placed in the smallest and least complex part of a system to ensure overall integrity.

**Sources**: mastering-bitcoin-cash_chapter-8-bitcoin-cash-security_4.md

**Last updated**: 2026-04-17

---

## Concept Overview
A "root of trust" is a trusted core that serves as the foundation for an entire security system. In traditional architectures, security is extended outward in concentric circles, where each layer relies on the integrity of a more trusted inner layer via signatures and encryption (source: mastering-bitcoin-cash_chapter-8-bitcoin-cash-security_4.md).

## Root of Trust in [Bitcoin Cash](bitcoin-cash.md)
[Bitcoin Cash](bitcoin-cash.md) replaces centralized trusted cores with a decentralized consensus system. The root of trust in [BCH](bitcoin-cash.md) is the [genesis-block](genesis-block.md). By verifying the chain of blocks from the genesis block to the current tip, users can establish a trusted public ledger without needing to trust a third party (source: mastering-bitcoin-cash_chapter-8-bitcoin-cash-security_4.md).

## Implementation Guideline
When designing [BCH](bitcoin-cash.md) applications, the blockchain itself should be used as the root of trust. Trust should only be placed in a fully validated blockchain rather than in peripheral software components (source: mastering-bitcoin-cash_chapter-8-bitcoin-cash-security_4.md).

## Related pages

- [genesis-block](genesis-block.md)
- [decentralization](decentralization.md)
- [mastering-bitcoin-cash-chapter-8-security-4](mastering-bitcoin-cash-chapter-8-security-4.md)
