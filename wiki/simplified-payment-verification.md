# Simplified Payment Verification (SPV)

**Summary**: A lightweight method for verifying transactions without needing the full blockchain's transaction data.

**Sources**: mastering-bitcoin-cash_chapter-6-the-blockchain_6.md

**Last updated**: 2026-04-17

---

Simplified Payment Verification (SPV) is a protocol that allows "lightweight" clients to verify that a transaction is included in a block without needing to download the entire blockchain.

## How it Works
SPV nodes store only the 80-byte block headers. To verify a transaction, they rely on the [merkle-tree](merkle-tree.md) structure of blocks:
1. They receive a [merkle-path](merkle-tree.md) from a full node.
2. They use this path to verify the transaction's hash against the [merkle-root](merkle-root.md) stored in the block header.
3. They verify the block header's validity based on the chain of headers.

This process reduces the data required for verification from megabytes (full block) to less than a kilobyte (header + path) (source: mastering-bitcoin-cash_chapter-6-the-blockchain_6.md).

## Requirements
- **Block Headers**: The node must have a copy of all block headers.
- **Trusted/Reliable Peers**: The node relies on full nodes to provide the necessary merkle paths and match the addresses of interest via [bloom-filters](bloom-filters.md).

## Related pages
- [merkle-tree](merkle-tree.md)
- [bloom-filters](bloom-filters.md)
- [mastering-bitcoin-cash-chapter-6-6](mastering-bitcoin-cash-chapter-6-6.md)
