# mastering-bitcoin-cash-transactions-4

**Summary**: Introduction to Unspent Transaction Outputs (UTXOs) as the fundamental building block of [Bitcoin Cash](bitcoin-cash.md) transactions.

**Sources**: mastering-bitcoin-cash_transactions_4.md

**Last updated**: 2026-04-17

---

## What is a [UTXO](utxo.md)?

An [Unspent Transaction Output](utxo.md) ([UTXO](utxo.md)) is an indivisible chunk of currency locked to specific owners and recognized as a currency unit by the entire network (source: mastering-bitcoin-cash_transactions_4.md). When a user receives [Bitcoin Cash](bitcoin-cash.md), it is recorded as a [UTXO](utxo.md) in the blockchain.

## Account-less Model

[Bitcoin Cash](bitcoin-cash.md) does not utilize accounts or balances. Instead, a user's "balance" is calculated by scanning the blockchain and aggregating all UTXOs that belong to that user (source: mastering-bitcoin-cash_transactions_4.md).

## [UTXO](utxo.md) Characteristics

- **Indivisibility**: Once created, a [UTXO](utxo.md) is indivisible. It cannot be partially spent (source: mastering-bitcoin-cash_transactions_4.md).
- **Value**: UTXOs can have any value, denominated in satoshis (where 1 [BCH](bitcoin-cash.md) = 100,000,000 satoshis) (source: mastering-bitcoin-cash_transactions_4.md).
- **Consumption and Change**: Because UTXOs are indivisible, if a [UTXO](utxo.md) is larger than the amount required for a payment, it must be consumed entirely. The excess is returned to the sender as "change".
    - *Example*: Spending 1 [BCH](bitcoin-cash.md) from a 20 [BCH](bitcoin-cash.md) [UTXO](utxo.md) requires two outputs: one for 1 [BCH](bitcoin-cash.md) (recipient) and one for 19 [BCH](bitcoin-cash.md) (sender's change) (source: mastering-bitcoin-cash_transactions_4.md).

## Related pages

- [utxo](utxo.md)
- [bitcoin-cash-transactions](bitcoin-cash-transactions.md)
- [mastering-bitcoin-cash-transactions-3](mastering-bitcoin-cash-transactions-3.md)
