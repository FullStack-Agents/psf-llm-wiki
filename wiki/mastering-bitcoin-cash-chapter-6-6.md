# mastering-bitcoin-cash-chapter-6-6

**Summary**: Explanation of Simplified Payment Verification (SPV), how it leverages Merkle trees and bloom filters for lightweight transaction verification.

**Sources**: mastering-bitcoin-cash_chapter-6-the-blockchain_6.md

**Last updated**: 2026-04-17

---

Simplified Payment Verification (SPV) allows nodes to validate transactions without downloading entire blocks, enabling lightweight clients to operate on devices with limited storage and bandwidth (source: mastering-bitcoin-cash_chapter-6-the-blockchain_6.md).

## SPV Node Architecture
SPV nodes do not store the full blockchain. Instead, they store only the **block headers** (80 bytes each). This drastically reduces the storage requirement compared to full nodes (source: mastering-bitcoin-cash_chapter-6-the-blockchain_6.md).

## Verification Workflow
When an SPV node needs to verify a transaction, it performs the following steps:
1. **Interest Specification**: It sets up a [bloom-filter](bloom-filters.md) with its peers to specify which addresses it is interested in.
2. **Data Retrieval**: A peer finds a matching transaction and sends a `merkleblock` message.
3. **Path Validation**: This message includes the block header and a [merkle-path](merkle-tree.md) that links the transaction to the [merkle-root](merkle-root.md).
4. **Root Verification**: The SPV node uses the merkle path to verify that the transaction is indeed included in the block.
5. **Chain Verification**: The node uses the block header to confirm the block is part of the canonical blockchain (source: mastering-bitcoin-cash_chapter-6-the-blockchain_6.md).

## Efficiency
The amount of data required for verification is less than a kilobyte (block header + merkle path), whereas a full block can be 1MB or larger. This is what makes BCH wallets viable on mobile phones (source: mastering-bitcoin-cash_chapter-6-the-blockchain_6.md).

## Related pages
- [merkle-tree](merkle-tree.md)
- [merkle-root](merkle-root.md)
- [bloom-filters](bloom-filters.md)
- [mastering-bitcoin-cash-chapter-6-6](mastering-bitcoin-cash-chapter-6-6.md)
