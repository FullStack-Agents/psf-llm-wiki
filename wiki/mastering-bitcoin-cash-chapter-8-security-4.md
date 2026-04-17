# Mastering [[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) Chapter 8 Security 4

**Summary**: Analysis of the "Root of Trust" architecture, explaining how [[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) replaces traditional trusted cores with a decentralized public ledger based on the genesis block.

**Sources**: mastering-bitcoin-cash_chapter-8-bitcoin-cash-security_4.md

**Last updated**: 2026-04-17

---

## Traditional Root of Trust
Traditional security architecture is built on a "root of trust"—a trusted core that serves as the foundation for the entire system. Security is extended outward in concentric circles, with each layer relying on more trusted inner layers through the use of signatures, encryption, and controls. This model aims to place the most trust in the least complex parts of the system, which are theoretically less vulnerable to attack (source: mastering-bitcoin-cash_chapter-8-bitcoin-cash-security_4.md).

## [[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) Root of Trust
[[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) fundamentally alters this model by implementing a decentralized consensus system. The root of trust is not a centralized entity or core, but the [genesis block](genesis-block.md), extending through the chain up to the current block to create a trusted public ledger (source: mastering-bitcoin-cash_chapter-8-bitcoin-cash-security_4.md).

When designing applications, developers should use the [blockchain](blockchain.md) itself as the root of trust rather than any other component. Trust should only be explicitly placed in a fully validated [blockchain](blockchain.md) (source: mastering-bitcoin-cash_chapter-8-bitcoin-cash-security_4.md).

## Evaluating Security Architecture
To evaluate the security of a [[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) application, one should consider the impact of individual component compromises. A correctly designed application should be resilient to the compromise of its peripheral components and only be vulnerable if the underlying [[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) consensus mechanism itself is compromised (source: mastering-bitcoin-cash_chapter-8-bitcoin-cash-security_4.md).

## Related pages

- [genesis-block](genesis-block.md)
- [decentralization](decentralization.md)
- [mastering-bitcoin-cash-chapter-8-security-3](mastering-bitcoin-cash-chapter-8-security-3.md)
