# Mastering [Bitcoin Cash](bitcoin-cash.md) Chapter 5 Part 4

**Summary**: Explanation of the blockchain synchronization process for new or returning nodes, focusing on block height comparison and the `getblocks` / `inv` / `getdata` workflow.

**Sources**: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_4.md

**Last updated**: 2026-04-17

---

When a full node first joins the network or returns from being offline, it must synchronize its local blockchain to match the network's current state (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_4.md).

## The Synchronization Workflow

The process starts by comparing blockchain heights across peers using the `BestHeight` field in the initial `version` message (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_4.md).

### Step-by-Step Sync Process
1. **Identify Missing Blocks**: The node sends a `getblocks` message containing the hash of its current top block. Peers with a longer chain identify which blocks are missing (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_4.md).
2. **Inventory Advertisement**: The peer sends an `inv` (inventory) message containing hashes of the first 500 blocks the node needs (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_4.md).
3. **Data Retrieval**: The node sends `getdata` messages to request the full block data for those hashes (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_4.md).
4. **Incremental Addition**: As blocks are received, they are added to the local blockchain, and the process repeats until the node reaches the current network height (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_4.md).

## Load Distribution
To avoid overwhelming any single peer, the node distributes `getdata` requests across multiple connected peers and tracks the number of blocks "in transit" per connection (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_4.md).

## Related pages

- [blockchain](blockchain.md)
- [bitcoin-cash-network](bitcoin-cash-network.md)
- [network-discovery](network-discovery.md)
- [mastering-bitcoin-cash-chapter-5-4](mastering-bitcoin-cash-chapter-5-4.md)
