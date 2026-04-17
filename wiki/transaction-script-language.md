# Transaction Script Language

**Summary**: The stack-based, non-Turing-complete language used to define locking and unlocking conditions in [Bitcoin Cash](bitcoin-cash.md).

**Sources**: mastering-bitcoin-cash_transactions_8.md

**Last updated**: 2026-04-17

---

The [Bitcoin Cash](bitcoin-cash.md) script language is a Forth-like, stack-based language used to implement the conditions required to spend UTXOs (source: mastering-bitcoin-cash_transactions_8.md).

### Operation
The language operates by pushing data (constants) onto a stack and using operators to manipulate that data. For instance, `OP_ADD` pops two values and pushes their sum (source: mastering-bitcoin-cash_transactions_8.md). Both [transaction-scripts](transaction-scripts.md) (locking and unlocking) are written in this language.

### Key Constraints
To maintain network security and predictability, the language is designed with specific limitations:
- **No Loops**: Because it is not Turing-complete, it prevents infinite loops that could crash nodes (source: mastering-bitcoin-cash_transactions_8.md).
- **Statelessness**: Every script execution is independent, with no state carried over from previous executions (source: mastering-bitcoin-cash_transactions_8.md).

## Related pages

- [transaction-scripts](transaction-scripts.md)
- [mastering-bitcoin-cash-transactions-8](mastering-bitcoin-cash-transactions-8.md)
- [transaction-validation](transaction-validation.md)
- [utxo](utxo.md)
