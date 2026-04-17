# Merkle Tree

**Summary**: A binary hash tree used to efficiently summarize and verify large sets of data, such as transactions in a block.

**Sources**: mastering-bitcoin-cash_chapter-6-the-[blockchain](blockchain.md)_4.md, mastering-bitcoin-cash_chapter-6-the-[blockchain](blockchain.md)_5.md

**Last updated**: 2026-04-17

---

A Merkle Tree is a data structure where leaf nodes (transaction hashes) are recursively paired and hashed until a single root is reached.

## Technical Implementation in [BCH](bitcoin-cash.md)
- **Hashing Algorithm**: Double-SHA256 (SHA256 applied twice).
- **Balancing**: If there's an odd number of leaf nodes, the last node is duplicated to ensure a balanced binary tree.
- **Verification Complexity**: The complexity to verify a transaction's inclusion is $O(\log N)$, specifically $2 \cdot \log_2(N)$ calculations for $N$ transactions (source: mastering-bitcoin-cash_chapter-6-the-[blockchain](blockchain.md)_4.md).

## Merkle Paths
A **merkle path** (or authentication path) consists of the minimal set of hashes required to reconstruct the [merkle-root](merkle-root.md) starting from a specific transaction hash. Because the path size grows logarithmically, verification remains efficient even as block sizes increase (source: mastering-bitcoin-cash_chapter-6-the-[blockchain](blockchain.md)_5.md).

## Related pages
- [merkle-root](merkle-root.md)
- [mastering-bitcoin-cash-chapter-6-4](mastering-bitcoin-cash-chapter-6-4.md)
- [mastering-bitcoin-cash-chapter-6-5](mastering-bitcoin-cash-chapter-6-5.md)
- [[blockchain](blockchain.md)-data-structure]([blockchain](blockchain.md)-data-structure.md)
