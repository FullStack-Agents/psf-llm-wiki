# Transaction Fees

**Summary**: The mechanism for compensating miners and preventing spam in [bitcoin-cash](bitcoin-cash.md).

**Sources**: mastering-bitcoin-cash_transactions_6.md

**Last updated**: 2026-04-17

---

Transaction fees are the difference between the total amount of inputs and the total amount of outputs in a transaction (source: mastering-bitcoin-cash_transactions_6.md).

### Key Principles
- **Calculation**: `Fees = Sum(Inputs) – Sum(Outputs)` (source: mastering-bitcoin-cash_transactions_6.md).
- **Basis**: Fees are determined by the **size of the transaction (KB)**, not its monetary value (source: mastering-bitcoin-cash_transactions_6.md).
- **Incentives**: Fees reward [mining](mining.md) nodes for securing the network and discourage the broadcasting of spam transactions (source: mastering-bitcoin-cash_transactions_6.md).
- **Prioritization**: Miners tend to prioritize transactions with higher fees for inclusion in blocks (source: mastering-bitcoin-cash_transactions_6.md).

### Warning on Change
Failure to create a change output for the unused portion of a consumed [utxo](utxo.md) will result in that remaining balance being collected as a fee by the miner (source: mastering-bitcoin-cash_transactions_6.md).

## Related pages

- [mastering-bitcoin-cash-transactions-6](mastering-bitcoin-cash-transactions-6.md)
- [mining](mining.md)
- [utxo](utxo.md)
- [bitcoin-cash-transactions](bitcoin-cash-transactions.md)
