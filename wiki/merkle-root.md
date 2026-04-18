# Merkle Root

**Summary**: A cryptographic hash that summarizes all transactions within a block, allowing for efficient verification.

**Sources**: mastering-bitcoin-cash_chapter-6-the-[blockchain](blockchain.md)_2.md, mastering-bitcoin-cash_chapter-6-the-[blockchain](blockchain.md)_4.md

**Last updated**: 2026-04-17

---

The Merkle Root is a field in the 80-byte block header. It serves as a cryptographic summary of all transactions included in that block (source: mastering-bitcoin-cash_chapter-6-the-[blockchain](blockchain.md)_2.md).

## Construction and Merkle Trees
The root is the final result of a [merkle-tree](merkle-tree.md) structure, built bottom-up by recursively hashing pairs of transactions using double-SHA256 (source: mastering-bitcoin-cash_chapter-6-the-[blockchain](blockchain.md)_4.md).

## Role in Block Identification
Because the Merkle Root is part of the block header, any change to a single transaction in the block would change the Merkle Root, which in turn changes the overall block hash.

## Related pages
- [mastering-bitcoin-cash-chapter-6-2](mastering-bitcoin-cash-chapter-6-2.md)
- [mastering-bitcoin-cash-chapter-6-4](mastering-bitcoin-cash-chapter-6-4.md)
- [data-structure](data-structure.md)
