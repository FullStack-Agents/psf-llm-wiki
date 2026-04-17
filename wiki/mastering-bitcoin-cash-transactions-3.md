# mastering-bitcoin-cash-transactions-3

**Summary**: Description of the [Bitcoin Cash](bitcoin-cash.md) transaction data structure and the function of the locktime field.

**Sources**: mastering-bitcoin-cash_transactions_3.md

**Last updated**: 2026-04-17

---

## Transaction Data Structure

A [Bitcoin Cash](bitcoin-cash.md) transaction is a data structure consisting of the following fields:

| Size | Field | Description |
| :--- | :--- | :--- |
| 4 bytes | Version | Specifies which rules this transaction follows |
| 1–9 bytes (VarInt) | Input Counter | How many inputs are included |
| Variable | Inputs | One or more transaction inputs |
| 1–9 bytes (VarInt) | Output Counter | How many outputs are included |
| Variable | Outputs | One or more transaction outputs |
| 4 bytes | Locktime | A Unix timestamp or block number |

(source: mastering-bitcoin-cash_transactions_3.md)

## Locktime (nLockTime)

The `nLockTime` field defines the earliest time a transaction is considered valid (source: mastering-bitcoin-cash_transactions_3.md).

- **Immediate Processing**: If set to zero, the transaction can be processed immediately.
- **Block Height**: Values below 500 million are interpreted as block heights.
- **Unix Timestamp**: Values 500 million or higher are interpreted as Unix timestamps.

Transactions with future locktimes are held until they become valid, behaving similarly to a postdated check (source: mastering-bitcoin-cash_transactions_3.md).

## Related pages

- [bitcoin-cash-transactions](bitcoin-cash-transactions.md)
- [transaction-locktime](transaction-locktime.md)
- [mastering-bitcoin-cash-transactions-2](mastering-bitcoin-cash-transactions-2.md)
