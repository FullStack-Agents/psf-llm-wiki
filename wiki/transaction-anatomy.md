# Transaction Anatomy

**Summary**: The structural composition of Bitcoin Cash transactions, including inputs, outputs, cryptographic signatures, and different transaction types.

**Sources**: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_2.md

**Last updated**: 2026-04-16

---

Transactions are the fundamental units of value transfer in the Bitcoin Cash system, functioning as a chain of ownership where value moves from one address to another (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_2.md).

### Structure of a Transaction
A transaction consists of two primary components:
- **Inputs (Debits)**: These refer to outputs from previous transactions that the sender is now spending.
- **Outputs (Credits)**: These define the amount of BCH and the address of the recipient(s).

The difference between the total value of the inputs and the total value of the outputs creates an implied **transaction fee**, which is collected by the miner who includes the transaction in a block (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_2.md).

### Authorization and Chain of Ownership
To spend BCH, a user must provide a digital signature as cryptographic proof of ownership. This signature authorizes the transfer of value from a previous transaction output to a new address, continuing the chain of ownership.

### Common Transaction Types
- **Simple Payments with Change**: Typically consists of one input and two outputs (one for the recipient and one returning the "change" to the sender).
- **Aggregating Transactions**: Combines multiple inputs into a single output.
- **Distributing Transactions**: Splits a single input into multiple outputs for various recipients.

## Related pages

- [[transaction-process]]
- [[private-keys]]
- [[mining]]
- [[bitcoin-cash]]
- [[mastering-bitcoin-cash-chapter-2]]
