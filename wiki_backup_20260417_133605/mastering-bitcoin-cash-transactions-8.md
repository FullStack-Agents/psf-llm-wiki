# mastering-bitcoin-cash-transactions-8

**Summary**: Introduction to the [[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) transaction script language, its stack-based nature, and the intentional limitations placed on its design.

**Sources**: mastering-bitcoin-cash_transactions_8.md

**Last updated**: 2026-04-17

---

## The Script Language

[[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) utilizes a specific scripting system for all transactions. The language is **stack-based** and resembles **Forth**, designed specifically to be limited in scope and capable of running on simple hardware (source: mastering-bitcoin-cash_transactions_8.md).

This language is used to write both the **locking script** (the encumbrance on a [[utxo](utxo.md)](utxo.md)) and the **unlocking script** used to spend that [[utxo](utxo.md)](utxo.md).

## Execution Process

During transaction validation, the unlocking script in an input is executed in conjunction with the corresponding locking script to verify if spending conditions are satisfied (source: mastering-bitcoin-cash_transactions_8.md).

The execution follows a stack-based model:
- **Data Constants**: Numbers are pushed onto the stack.
- **Operators**: Operators act upon items on the stack. 
- *Example*: `OP_ADD` pops the top two items from the stack, adds them, and pushes the resulting sum back onto the stack (source: mastering-bitcoin-cash_transactions_8.md).

## Design Limitations

The script language is deliberately constrained to protect the network:
1. **Not Turing-complete**: It lacks loops and complex flow control (source: mastering-bitcoin-cash_transactions_8.md).
2. **Stateless**: There is no state preserved before or after the execution of a script (source: mastering-bitcoin-cash_transactions_8.md).

These limitations ensure that execution times are predictable and prevent the possibility of infinite loops that could be used in denial-of-service attacks against the network (source: mastering-bitcoin-cash_transactions_8.md).

## Related pages

- [transaction-scripts](transaction-scripts.md)
- [transaction-validation](transaction-validation.md)
- [mastering-bitcoin-cash-transactions-7](mastering-bitcoin-cash-transactions-7.md)
- [utxo](utxo.md)
