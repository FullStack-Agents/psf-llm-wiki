# Transaction Pools

**Summary**: The temporary storage mechanisms (mempools and orphan pools) used by nodes to manage unconfirmed transactions.

**Sources**: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_8.md

**Last updated**: 2026-04-17

---

Transaction pools are essential for the flow of transactions between the time they are created and the time they are mined into a block.

### The Mempool
The **memory pool**, or mempool, is a local, volatile list of unconfirmed transactions. Nodes use this pool to:
- **Relay**: Propagate transactions to peers to ensure network-wide coverage.
- **Monitor**: Allow wallets to see "unconfirmed" funds that have been sent but not yet included in the blockchain (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_8.md).

### Orphan Handling
An **orphan transaction** is one that arrives at a node before its parent transaction has been seen. To handle this, nodes use an **orphan pool**:
- Orphans are held temporarily in a separate pool.
- Once the parent transaction arrives, the child is "promoted" to the main mempool.
- This can trigger a cascade where multiple layers of descendant transactions are reconstructed in sequence (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_8.md).

### Operational Details
Mempools and orphan pools exist only in RAM. When a node restarts, these pools are cleared and must be repopulated through network traffic (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_8.md).

## Related pages

- [transaction-broadcasting](transaction-broadcasting.md)
- [orphan-transactions](orphan-transactions.md)
- [bitcoin-cash-network](bitcoin-cash-network.md)
- [mastering-bitcoin-cash-chapter-5-8](mastering-bitcoin-cash-chapter-5-8.md)
