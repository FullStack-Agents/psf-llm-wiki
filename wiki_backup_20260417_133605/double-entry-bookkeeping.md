# Double-Entry Bookkeeping

**Summary**: The accounting model used by [[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) to ensure the integrity and conservation of coins during transfers.

**Sources**: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_11.md

**Last updated**: 2026-04-17

---

[[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md)'s transaction structure is essentially a distributed double-entry bookkeeping system. 

### Mechanics
- **Debits**: Transaction inputs represent the funds being moved.
- **Credits**: Transaction outputs represent the destination of the funds.
- **Balance**: The sum of inputs must exactly balance with the sum of outputs plus any transaction fees.

This model ensures that coins are neither created nor destroyed in regular transactions; they only change ownership.

## Related pages

- [coinbase-transaction](coinbase-transaction.md)
- [auditability](auditability.md)
