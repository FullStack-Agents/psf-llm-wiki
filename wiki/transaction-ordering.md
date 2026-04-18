# Transaction Ordering

**Summary**: Describes the rules governing the sequence of transactions within a block, transitioning from topological ordering to the current canonical lexicographical ordering.

**Sources**: transaction-ordering.md

**Last updated**: 2026-04-18

---

Transactions within a block are inherently ordered. The [coinbase transaction](coinbase-transaction.md) must always be the first transaction in the block. The ordering of subsequent transactions has evolved over the history of the Bitcoin Cash network.

## Canonical Transaction Ordering (CTOR)
Since block height 556766 (activating around median-time-past 1542300000), Bitcoin Cash uses **Canonical Transaction Ordering**, also known as **Lexicographical Transaction Ordering (LTOR)**.

- **The Rule**: All transactions following the coinbase transaction must be sorted in lexicographical order by their transaction hash.
- **Implementation**: The transaction hash is interpreted as little-endian during the sorting process.
- **Enforcement**: Blocks that do not adhere to CTOR are rejected by the network.

This rule was introduced as part of [HF20181115](/protocol/forks/HF20181115) to standardize block construction.

## Topological Transaction Ordering (Legacy)
Before the activation of CTOR, blocks followed **Topological Transaction Ordering**.

- **The Rule**: If transaction B spends an output created by transaction A, then transaction A must appear before transaction B in the block.
- **Flexibility**: Other transactions that did not have such a dependency could appear in any order.

## Technical Context
The final order of transactions is captured in the [Merkle Tree](merkle-tree.md), which is then summarized as the Merkle Root in the [block-header](block-header.md).

## Related pages

- [block](block.md)
- [coinbase-transaction](coinbase-transaction.md)
- [merkle-tree](merkle-tree.md)
- [block-header](block-header.md)
