# mastering-bitcoin-cash-transactions-7

**Summary**: Explanation of transaction chaining, parent-child relationships, and the handling of orphan transactions in the Bitcoin Cash network.

**Sources**: mastering-bitcoin-cash_transactions_7.md

**Last updated**: 2026-04-17

---

## Transaction Chaining

Transactions in Bitcoin Cash form chains. A transaction that spends the outputs of a previous transaction is considered a **child**, while the transaction whose outputs are being spent is the **parent** (source: mastering-bitcoin-cash_transactions_7.md). 

In some cases, entire chains of interdependent transactions can be created simultaneously to support complex workflows (source: mastering-bitcoin-cash_transactions_7.md).

## Orphan Transactions

An **orphan transaction** occurs when a child transaction arrives at a node before its parent transaction has arrived (source: mastering-bitcoin-cash_transactions_7.md).

### Handling Orphan Transactions
1. **Orphan Transaction Pool**: Nodes store these child transactions in a temporary pool until the parent transaction arrives (source: mastering-bitcoin-cash_transactions_7.md).
2. **Release and Revalidation**: Once the parent transaction arrives, the orphans referencing its outputs are released, revalidated, and the chain is processed (source: mastering-bitcoin-cash_transactions_7.md).
3. **Purpose**: This mechanism prevents valid transactions from being rejected due to network delays in parent transaction propagation (source: mastering-bitcoin-cash_transactions_7.md).

### Security and Limits
To prevent denial-of-service (DoS) attacks, nodes have a limit on the number of orphan transactions they can store in memory, defined as `MAX_ORPHAN_TRANSACTIONS` (source: mastering-bitcoin-cash_transactions_7.md). If this limit is reached, randomly selected orphan transactions are evicted from the pool (source: mastering-bitcoin-cash_transactions_7.md).

## Related pages

- [transaction-chaining](transaction-chaining.md)
- [orphan-transactions](orphan-transactions.md)
- [transaction-validation](transaction-validation.md)
- [mastering-bitcoin-cash-transactions-6](mastering-bitcoin-cash-transactions-6.md)
