# Merkle Tree

**Summary**: A binary hash tree used to efficiently summarize and verify large sets of data, such as transactions in a block.

**Sources**: mastering-bitcoin-cash_chapter-6-the-[blockchain](blockchain.md)_4.md, mastering-bitcoin-cash_chapter-6-the-[blockchain](blockchain.md)_5.md, merkle-tree.md

**Last updated**: 2026-04-18

---

A Merkle Tree is a data structure where leaf nodes (transaction hashes) are recursively paired and hashed until a single root is reached.

## Purpose in Bitcoin Cash
In Bitcoin Cash, the transactions in a [block](block.md) are organized into a Merkle Tree. The resulting **Merkle Root** is a single hash representing all transactions in that block and is stored in the [block-header](block-header.md). This ensures that any change to a single transaction will change the Merkle Root and, consequently, the block hash.

### Key Advantages
- **Efficient Updates**: When mining a block, new transactions can be added without re-hashing the entire dataset. Only a small number of hashes on the path to the root need to be recalculated.
- **Partial Block Transfer**: Merkle Trees allow a node to verify that a specific transaction exists in a block without needing to download the entire block (by using a Merkle Path).

## Technical Implementation in [BCH](bitcoin-cash.md)
- **Hashing Algorithm**: Double-SHA256 (SHA256 applied twice).
- **Balancing**: If there's an odd number of leaf nodes, the last node is duplicated to ensure a balanced binary tree.
- **Verification Complexity**: The complexity to verify a transaction's inclusion is $O(\log N)$, specifically $2 \cdot \log_2(N)$ calculations for $N$ transactions (source: mastering-bitcoin-cash_chapter-6-the-blockchain_4.md).

## Merkle Paths
A **merkle path** (or authentication path) consists of the minimal set of hashes required to reconstruct the [merkle-root](merkle-root.md) starting from a specific transaction hash. Because the path size grows logarithmically, verification remains efficient even as block sizes increase (source: mastering-bitcoin-cash_chapter-6-the-blockchain_5.md).

## Related pages
- [merkle-root](merkle-root.md)
- [block](block.md)
- [block-header](block-header.md)
