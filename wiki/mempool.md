# Mempool

**Summary**: The local storage on a node for unconfirmed transactions awaiting inclusion in a block.

**Sources**: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_8.md

**Last updated**: 2026-04-17

---

The mempool (memory pool) is a temporary storage area where nodes keep track of valid transactions that have been broadcast to the network but not yet included in a block by a miner.

### Key Functions
- **Queueing**: Acts as a waiting room for transactions.
- **Prioritization**: Miners typically select transactions from their mempool based on fee value or arrival time.
- **Orphan Handling**: Transactions that reference a non-existent input are stored separately until the parent transaction arrives (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_8.md).

## Related pages

- [transaction-pools](transaction-pools.md)
- [orphan-transactions](orphan-transactions.md)
- [mining](mining.md)
