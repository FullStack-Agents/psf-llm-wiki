# Transaction Validation

**Summary**: The process by which nodes verify the validity of a transaction before propagating it.

**Sources**: mastering-bitcoin-cash_transactions_2.md

**Last updated**: 2026-04-17

---

When a transaction reaches a node, it undergoes validation. If the transaction is valid, the node propagates it to other connected nodes, resulting in a "flooding effect" where the transaction spreads exponentially across the network (source: mastering-bitcoin-cash_transactions_2.md).

Each node validates transactions independently, which serves as a security measure to prevent malformed transactions from spreading beyond the initial node (source: mastering-bitcoin-cash_transactions_2.md).

## Related pages

- [transaction-broadcasting](transaction-broadcasting.md)
- [bitcoin-cash-transactions](bitcoin-cash-transactions.md)
- [mastering-bitcoin-cash-transactions-2](mastering-bitcoin-cash-transactions-2.md)
