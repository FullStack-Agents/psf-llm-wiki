# mastering-bitcoin-cash-chapter-6-1

**Summary**: Introduction to the [blockchain](blockchain.md) data structure, describing it as an ordered, back-linked list of blocks starting from a genesis block.

**Sources**: mastering-bitcoin-cash_chapter-6-the-[blockchain](blockchain.md)_1.md

**Last updated**: 2026-04-17

---

The [blockchain](blockchain.md) is an ordered, back-linked list of blocks containing transactions. It is stored by nodes as a flat file or in a database, such as [google-leveldb](google-leveldb.md) used by Bitcoin ABC (source: mastering-bitcoin-cash_chapter-6-the-[blockchain](blockchain.md)_1.md).

## Structure and Terminology
- **Genesis Block**: The first block in the chain.
- **Height**: The distance of a block from the genesis block.
- **Tip**: The most recently added block in the chain.

## Block Identification and Linking
Each block is uniquely identified by a SHA256 cryptographic hash of its header. A block references its parent via the "previous block hash" field. While a block has only one parent, it can have multiple children during a [fork](fork.md) (source: mastering-bitcoin-cash_chapter-6-the-[blockchain](blockchain.md)_1.md).

## Immutability
The parent-child relationship ensures immutability. Because each block contains the hash of its parent, any change to a parent block changes its hash, which cascades through all subsequent child blocks. This makes changing deep history computationally infeasible (source: mastering-bitcoin-cash_chapter-6-the-[blockchain](blockchain.md)_1.md).

## Related pages
- [data-structure](data-structure.md)
- [fork](fork.md)
- [google-leveldb](google-leveldb.md)
