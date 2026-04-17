# Mastering [Bitcoin Cash](bitcoin-cash.md) Chapter 5 Part 2

**Summary**: Exploration of node types and their roles within the [Bitcoin Cash](bitcoin-cash.md) network, including full nodes, lightweight (SPV) nodes, and mining nodes.

**Sources**: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_2.md

**Last updated**: 2026-04-17

---

A [Bitcoin Cash](bitcoin-cash.md) node consists of several core functions: routing, blockchain database management, mining, and wallet services. Every node must implement routing to participate in the network, which involves validating/propagating blocks and transactions and maintaining peer connections (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_2.md).

## Node Specializations

Nodes are categorized by their capabilities and roles:

### Full Nodes
Full nodes maintain a complete, up-to-date copy of the blockchain. This allows them to verify any transaction authoritatively without relying on external sources (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_2.md).

### Lightweight (SPV) Nodes
Lightweight nodes use **Simplified Payment Verification (SPV)** and only store a subset of the blockchain. These are typically used on resource-constrained devices like smartphones (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_2.md).

### Mining Nodes
Mining nodes solve the proof-of-work algorithm to create new blocks. Some are full nodes, while others are lightweight nodes participating in pool mining (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_2.md).

### Edge Routers
Large companies (e.g., exchanges or payment processors) often run full nodes that do not mine or provide wallet services, instead acting as network edge routers for their services (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_2.md).

## Related pages

- [bitcoin-cash-network](bitcoin-cash-network.md)
- [mining](mining.md)
- [proof-of-work](proof-of-work.md)
- [digital-wallets](digital-wallets.md)
