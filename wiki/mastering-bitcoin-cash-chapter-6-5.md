# mastering-bitcoin-cash-chapter-6-5

**Summary**: Analysis of the efficiency of Merkle paths for verifying transaction inclusion, showing logarithmic growth relative to block size.

**Sources**: mastering-bitcoin-cash_chapter-6-the-blockchain_5.md

**Last updated**: 2026-04-17

---

The primary utility of the [merkle-tree](merkle-tree.md) is the ability to prove a transaction's inclusion in a block without needing the entire block data. This is achieved through a **merkle path** (or authentication path) (source: mastering-bitcoin-cash_chapter-6-the-blockchain_5.md).

## Merkle Path Efficiency
The size of the merkle path grows logarithmically relative to the number of transactions $N$. This allows for extremely compact proofs:

| Number of Transactions | Approx. Block Size | Path Size (hashes) | Path Size (bytes) |
| :--------------------- | :----------------- | :----------------- | :---------------- |
| 16 Tx                  | 4 Kilobytes        | 4 hashes           | 128 bytes         |
| 512 Tx                 | 128 Kilobytes      | 9 hashes           | 288 bytes         |
| 2048 Tx                | 512 Kilobytes      | 11 hashes          | 352 bytes         |
| 65,535 Tx              | 16 megabytes       | 16 hashes          | 512 bytes         |

*(Source: mastering-bitcoin-cash_chapter-6-the-blockchain_5.md)*

## Verification Process
To verify that a specific transaction is included in a block, a node requires only three pieces of information:
1. The **transaction hash**.
2. The **merkle path** (the sequence of hashes needed to reconstruct the root).
3. The **block header** (to obtain the [merkle-root](merkle-root.md)).

The node hashes the transaction hash with the hashes in the merkle path until it reaches a final hash. If this final hash matches the merkle root in the block header, the transaction is proven to be part of that block (source: mastering-bitcoin-cash_chapter-6-the-blockchain_5.md).

## Related pages
- [merkle-tree](merkle-tree.md)
- [merkle-root](merkle-root.md)
- [mastering-bitcoin-cash-chapter-6-4](mastering-bitcoin-cash-chapter-6-4.md)
- [mastering-bitcoin-cash-chapter-6-5](mastering-bitcoin-cash-chapter-6-5.md)
