# mastering-bitcoin-cash-chapter-6-2

**Summary**: Detailed breakdown of block structure, including the block header, size, and identifiers (hash and height).

**Sources**: mastering-bitcoin-cash_chapter-6-the-[blockchain](blockchain.md)_2.md

**Last updated**: 2026-04-17

---

A block is a container that aggregates transactions. A full 32MB [bitcoin-cash](bitcoin-cash.md) block can contain nearly 128,000 transactions (source: mastering-bitcoin-cash_chapter-6-the-blockchain_2.md).

## Block Anatomy
A block consists of the following components:
- **Block Size (4 bytes)**: The size of the block in bytes.
- **Block Header (80 bytes)**: Metadata containing the [previous-block-hash](mastering-bitcoin-cash-chapter-6-1.md), mining data, and the [merkle-root](merkle-root.md).
- **Transaction Counter (1-9 bytes)**: Number of transactions following.
- **Transactions**: The bulk of the block's data.
- **Sequence Number (4 bytes)**: Currently unused (set to 0xFFFFFFFF).

## Block Header Metadata
The 80-byte header includes:
1. Reference to the previous block hash.
2. Mining competition data: includes the timestamp, difficulty, and nonce.
3. The **[Merkle Tree](merkle-tree.md) Root**: A summary of all transactions in the block (source: mastering-bitcoin-cash_chapter-6-the-blockchain_2.md).

## Block Identification
Blocks are identified in two ways:
- **Block Hash**: A unique cryptographic fingerprint derived from the header. This is the only truly unique identifier.
- **Block Height**: The position in the chain. Note that during [blockchain-forks](blockchain-fork.md), multiple blocks can exist at the same height (source: mastering-bitcoin-cash_chapter-6-the-blockchain_2.md).

## Related pages
- [data-structure](data-structure.md)
- [merkle-root](merkle-root.md)
- [fork](fork.md)
- [mastering-bitcoin-cash-chapter-6-1](mastering-bitcoin-cash-chapter-6-1.md)
