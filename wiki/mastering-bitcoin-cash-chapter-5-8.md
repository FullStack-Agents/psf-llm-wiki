# Mastering [bitcoin-cash](bitcoin-cash.md) Chapter 5 Part 8

**Summary**: Detailed explanation of the transaction pool ([mempool](mempool.md)) and orphan pool, explaining how unconfirmed transactions are tracked and reconstructed.

**Sources**: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_8.md

**Last updated**: 2026-04-17

---

Most [bitcoin-cash](bitcoin-cash.md) nodes maintain a temporary storage area for transactions that have been broadcast to the network but not yet included in a block, known as the **memory pool ([mempool](mempool.md))** or **transaction pool** (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_8.md).

## The Transaction Pool (Mempool)
The [mempool](mempool.md) is used by nodes to:
- Track unconfirmed transactions.
- Monitor incoming payments that lack confirmation (crucial for wallet-holding nodes).
- Relay verified transactions to neighboring nodes for network-wide propagation (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_8.md).

## The Orphan Pool
Some nodes maintain a separate **orphan pool** for transactions that reference parent transactions not yet known to the node (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_8.md).

### Orphan Reconstruction Process
1. **Arrival**: A transaction arrives whose inputs reference an unknown parent; it is placed in the orphan pool.
2. **Parent Arrival**: When the missing parent transaction is eventually received and added to the transaction pool, the system checks the orphan pool for any "children" (transactions referencing that parent).
3. **Promotion**: Valid matching orphans are moved from the orphan pool to the main transaction pool.
4. **Cascade**: This process can trigger a recursive cascade, reconstructing entire interdependent chains of transactions as parents are reunited with children (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_8.md).

## Storage Characteristics
- **Volatility**: Both the transaction pool and orphan pool are stored in local memory and are not persistent.
- **Initialization**: Both pools start empty upon node startup and are populated dynamically via network messages (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_8.md).

## Related pages

- [transaction-broadcasting](transaction-broadcasting.md)
- [orphan-transactions](orphan-transactions.md)
- [bitcoin-cash-network](bitcoin-cash-network.md)
- [mastering-bitcoin-cash-chapter-5-8](mastering-bitcoin-cash-chapter-5-8.md)
