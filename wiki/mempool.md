# Memory Pool

**Summary**: A temporary staging area in Bitcoin Cash nodes for valid transactions awaiting inclusion in a block.

**Sources**: memory-pool.md

**Last updated**: 2026-04-17

---

The memory pool, commonly referred to as the **mempool**, serves as a cache for valid [transactions](bitcoin-cash-transactions.md) received from the network. Transactions remain in the mempool until they are mined into a block on the [blockchain](blockchain.md) or are removed due to invalidity or node policy (source: memory-pool.md).

## Purpose and Incentives
- **Responsiveness**: Mempools allow nodes to accept and validate transactions immediately, rather than waiting for the average 10-minute block interval.
- **Mining Incentives**: Mining nodes use mempools to aggregate transactions and maximize the collection of transaction fees for each block mined (source: memory-pool.md).

## Transaction Management
- **Virtual Block Application**: Transactions in the mempool are treated as if they belong to an imaginary block following the current tip. This allows nodes to apply policies regarding double-spending and maximum block size.
- **Transaction Chaining**: Nodes track parent-child relationships (where a child transaction spends an output of a parent). If a parent transaction is removed from the mempool, its dependent children are also removed to prevent invalidity (source: memory-pool.md).

## Rejection Criteria
Valid transactions may be rejected from entering the mempool if they:
- Fail to meet the node's minimum transaction fee (often occurs when the mempool is near capacity or if the transaction is considered "dust").
- Attempt to double-spend inputs of another transaction already in the mempool.
- Are considered "non-standard" by the node's rules (source: memory-pool.md).

## Removal Criteria
Transactions already in the mempool may be removed if:
- **Blockchain Reorg**: A reorganization renders the transaction invalid (e.g., it now double-spends or is time-locked due to block height changes).
- **Block Arrival**: The transaction is included in a newly received block, or it double-spends a transaction in the new block.
- **Capacity/Performance**: The node reaches its capacity limit, often leading to the removal of transactions with the lowest fees (source: memory-pool.md).

## Related pages

- [bitcoin-cash-transactions](bitcoin-cash-transactions.md)
- [blockchain](blockchain.md)
- [transaction-validation](transaction-validation.md)
- [blockchain-data-structure](blockchain-data-structure.md)
- [transaction-fees](transaction-fees.md)
- [blockchain-fork](blockchain-fork.md)
