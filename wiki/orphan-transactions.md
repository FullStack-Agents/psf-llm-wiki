# Orphan Transactions

**Summary**: Child transactions that arrive at a node before their parent transactions.

**Sources**: mastering-bitcoin-cash_transactions_7.md

**Last updated**: 2026-04-17

---

An orphan transaction is a child transaction that arrives at a node before its corresponding parent transaction has been received (source: mastering-bitcoin-cash_transactions_7.md).

### Process of Handling Orphans
- **Storage**: Nodes place orphan transactions in a temporary "orphan transaction pool" (source: mastering-bitcoin-cash_transactions_7.md).
- **Trigger**: When the parent transaction eventually arrives, the orphan is released and revalidated (source: mastering-bitcoin-cash_transactions_7.md).
- **Goal**: This ensures that valid transactions are not rejected due to network propagation delays (source: mastering-bitcoin-cash_transactions_7.md).

### Memory Constraints
To mitigate denial-of-service (DoS) attacks, the number of orphan transactions stored in memory is capped by `MAX_ORPHAN_TRANSACTIONS`. If the limit is exceeded, transactions are randomly evicted from the pool (source: mastering-bitcoin-cash_transactions_7.md).

## Related pages

- [[transaction-chaining]]
- [[transaction-validation]]
- [[mastering-bitcoin-cash-transactions-7]]
