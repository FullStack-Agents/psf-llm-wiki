# [blockchain](blockchain.md) Synchronization

**Summary**: The process by which a full node downloads and verifies missing blocks to catch up with the current state of the [bitcoin-cash](bitcoin-cash.md) network.

**Sources**: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_4.md

**Last updated**: 2026-04-17

---

[blockchain](blockchain.md) synchronization is essential for any full node to operate authoritatively. It occurs during the initial boot-up (Initial Block Download) and every time a node returns from being offline (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_4.md).

### The Sync Protocol
The synchronization utilizes a request-response pattern using specific P2P messages:

1. **Height Comparison**: Nodes use the `BestHeight` field in the `version` handshake to find peers with a longer chain (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_4.md).
2. **Discovery of Missing Blocks**:
   - The node sends `getblocks` requesting blocks after its current top hash.
   - The peer responds with `inv` (inventory) messages containing lists of block hashes (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_4.md).
3. **Fetching Data**:
   - The node requests the actual block data using `getdata` messages (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_4.md).
   - Data is requested from multiple peers to balance the network load (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_4.md).

### Recovery
Whether a node is missing one block or a million, the process remains identical: compare height $\rightarrow$ request hashes $\rightarrow$ fetch data (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_4.md).

## Related pages

- [blockchain](blockchain.md)
- [bitcoin-cash-network](bitcoin-cash-network.md)
- [mastering-bitcoin-cash-chapter-5-4](mastering-bitcoin-cash-chapter-5-4.md)
