# mastering-bitcoin-cash-transactions-4

**Summary**: Introduction to Unspent Transaction Outputs (UTXOs) as the fundamental building block of Bitcoin Cash transactions.

**Sources**: mastering-bitcoin-cash_transactions_4.md

**Last updated**: 2026-04-17

---

## What is a UTXO?

An Unspent Transaction Output (UTXO) is an indivisible chunk of currency locked to specific owners and recognized as a currency unit by the entire network (source: mastering-bitcoin-cash_transactions_4.md). When a user receives Bitcoin Cash, it is recorded as a UTXO in the blockchain.

## Account-less Model

Bitcoin Cash does not utilize accounts or balances. Instead, a user's "balance" is calculated by scanning the blockchain and aggregating all UTXOs that belong to that user (source: mastering-bitcoin-cash_transactions_4.md).

## UTXO Characteristics

- **Indivisibility**: Once created, a UTXO is indivisible. It cannot be partially spent (source: mastering-bitcoin-cash_transactions_4.md).
- **Value**: UTXOs can have any value, denominated in satoshis (where 1 BCH = 100,000,000 satoshis) (source: mastering-bitcoin-cash_transactions_4.md).
- **Consumption and Change**: Because UTXOs are indivisible, if a UTXO is larger than the amount required for a payment, it must be consumed entirely. The excess is returned to the sender as "change".
    - *Example*: Spending 1 BCH from a 20 BCH UTXO requires two outputs: one for 1 BCH (recipient) and one for 19 BCH (sender's change) (source: mastering-bitcoin-cash_transactions_4.md).

## Related pages

- [[utxo]]
- [[bitcoin-cash-transactions]]
- [[mastering-bitcoin-cash-transactions-3]]
