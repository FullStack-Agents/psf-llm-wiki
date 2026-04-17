# mastering-bitcoin-cash-chapter-6-4

**Summary**: Explanation of Merkle trees, their construction, and their utility in efficient transaction verification in [Bitcoin Cash](bitcoin-cash.md).

**Sources**: mastering-bitcoin-cash_chapter-6-the-blockchain_4.md

**Last updated**: 2026-04-17

---

Merkle trees (binary hash trees) are used in [Bitcoin Cash](bitcoin-cash.md) to summarize and verify large sets of data, specifically all transactions within a block (source: mastering-bitcoin-cash_chapter-6-the-blockchain_4.md).

## Construction Process
Merkle trees are built bottom-up using double-SHA256 hashing:
1. **Leaf Nodes**: Each transaction is hashed using double-SHA256 to create the initial leaf nodes.
2. **Pairing**: Pairs of leaf nodes are concatenated and hashed together to form parent nodes.
3. **Root Generation**: This process continues recursively until only a single 32-byte hash remains: the [merkle-root](merkle-root.md).
4. **Odd Number Handling**: If there is an odd number of transactions, the last transaction hash is duplicated to ensure a balanced binary tree (source: mastering-bitcoin-cash_chapter-6-the-blockchain_4.md).

## Efficiency and Verification
The primary benefit of Merkle trees is the efficiency of verification. To verify if a transaction is included in a block containing $N$ transactions, only $2 \cdot \log_2(N)$ calculations are required. This significantly reduces the amount of data needed to prove a transaction's presence in a block.

## Related pages
- [merkle-root](merkle-root.md)
- [blockchain-data-structure](blockchain-data-structure.md)
- [mastering-bitcoin-cash-chapter-6-2](mastering-bitcoin-cash-chapter-6-2.md)
- [mastering-bitcoin-cash-chapter-6-4](mastering-bitcoin-cash-chapter-6-4.md)
