# mastering-bitcoin-cash-transactions-6

**Summary**: Explanation of transaction fees in [[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md), how they are calculated, and their role in network security.

**Sources**: mastering-bitcoin-cash_transactions_6.md

**Last updated**: 2026-04-17

---

## Transaction Fees Calculation

Transaction fees are not explicitly stated in a transaction but are implied. They are calculated as the difference between the total value of all inputs and the total value of all outputs:

`Fees = Sum(Inputs) – Sum(Outputs)` (source: mastering-bitcoin-cash_transactions_6.md)

## Purpose of Fees

Fees serve two primary purposes in the [[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) network:
1. **Incentive**: They compensate miners for the work of securing the network and including transactions in blocks (source: mastering-bitcoin-cash_transactions_6.md).
2. **Spam Prevention**: They act as a disincentive against network spam (source: mastering-bitcoin-cash_transactions_6.md).

## Fee Determination and Prioritization

Fees are based on the **transaction size in kilobytes**, rather than the transaction's value in [[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) (source: mastering-bitcoin-cash_transactions_6.md). 

Miners prioritize transactions that offer sufficient fees. Transactions with insufficient fees may experience delays or may not be processed at all (source: mastering-bitcoin-cash_transactions_6.md).

## The Importance of Change Outputs

When creating a transaction, it is critical to account for the full value of all consumed [utxo](utxo.md)s. If a user consumes a large [[utxo](utxo.md)](utxo.md) but only specifies a small output to the recipient without a change output, the remaining balance is automatically treated as a transaction fee for the miner (source: mastering-bitcoin-cash_transactions_6.md).

*Example*: Consuming a 20 [BCH](bitcoin-cash.md) [[utxo](utxo.md)](utxo.md) for a 1 [BCH](bitcoin-cash.md) payment without a change output results in a 19 [BCH](bitcoin-cash.md) fee (source: mastering-bitcoin-cash_transactions_6.md).

## Related pages

- [transaction-fees](transaction-fees.md)
- [utxo](utxo.md)
- [mining](mining.md)
- [mastering-bitcoin-cash-transactions-5](mastering-bitcoin-cash-transactions-5.md)
