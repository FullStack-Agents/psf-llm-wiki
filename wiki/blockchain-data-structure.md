# Blockchain Data Structure

**Summary**: The fundamental organization of the blockchain as a linked list of blocks.

**Sources**: mastering-bitcoin-cash_chapter-6-the-blockchain_1.md

**Last updated**: 2026-04-17

---

The blockchain is a sequential ledger where each block points to its predecessor. This creates a chain back to the [genesis-block](genesis-block.md). 

Key characteristics include:
- **Ordered sequence**: Blocks are added one after another.
- **Back-linking**: Each block header contains the hash of the previous block.
- **Immutability**: The recursive hashing of block headers ensures that any modification to an old block would require re-mining all subsequent blocks.

## Related pages
- [mastering-bitcoin-cash-chapter-6-1](mastering-bitcoin-cash-chapter-6-1.md)
- [genesis-block](genesis-block.md)
