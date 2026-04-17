# Forging and Consensus

**Summary**: The cryptographic process of creating a valid block (forging) and the mechanism by which the network reaches consensus on the authoritative chain.

**Sources**: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_9.md

**Last updated**: 2026-04-16

---

In [Bitcoin Cash](bitcoin-cash.md), the process of adding a new block to the blockchain is often referred to as "forging." This is a computational competition where miners strive to create a block that meets the network's difficulty requirements (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_9.md).

### The Forging Process
To forge a block, a miner must:
1. Collect a set of valid transactions from the [mempool](mempool.md).
2. Create a block header.
3. Solve the PoW puzzle by finding a nonce that, when hashed with the header using SHA-256, results in a value below the target threshold.

### Network Consensus
Consensus is the process by which all nodes in the decentralized network agree on a single version of the blockchain.

- **Propagation**: When a miner finds a valid block, they broadcast it to the network.
- **Validation**: Other nodes verify the block's PoW and the validity of the included transactions.
- **The Longest Chain Rule**: In the event of a conflict (e.g., two miners finding a block at nearly the same time), nodes follow the "longest chain" (or more accurately, the chain with the most cumulative proof-of-work). This ensures that the network eventually converges on a single, authoritative history of transactions (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_9.md).

## Related pages

- [mining](mining.md)
- [proof-of-work](proof-of-work.md)
- [blockchain](blockchain.md)
- [decentralization](decentralization.md)
- [mastering-bitcoin-cash-chapter-2](mastering-bitcoin-cash-chapter-2.md)
