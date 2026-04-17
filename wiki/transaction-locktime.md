# Transaction Locktime

**Summary**: The mechanism used to delay the validity of a [Bitcoin Cash](bitcoin-cash.md) transaction.

**Sources**: mastering-bitcoin-cash_transactions_3.md

**Last updated**: 2026-04-17

---

The locktime field (`nLockTime`) determines the earliest time or block height at which a transaction becomes valid (source: mastering-bitcoin-cash_transactions_3.md).

### Interpretation of Values
- **Zero**: The transaction is valid immediately.
- **< 500 Million**: The value represents a block height.
- **$\ge$ 500 Million**: The value represents a Unix timestamp.

This functionality allows transactions to act like postdated checks, where they must be held until the specified time or height is reached (source: mastering-bitcoin-cash_transactions_3.md).

## Related pages

- [mastering-bitcoin-cash-transactions-3](mastering-bitcoin-cash-transactions-3.md)
- [bitcoin-cash-transactions](bitcoin-cash-transactions.md)
