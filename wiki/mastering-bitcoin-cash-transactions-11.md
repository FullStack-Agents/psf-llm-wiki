# mastering-bitcoin-cash-transactions-11

**Summary**: Explanation of the practical execution process of unlocking and locking scripts during transaction validation, including a step-by-step example of P2PKH validation.

**Sources**: mastering-bitcoin-cash_transactions_11.md

**Last updated**: 2026-04-17

---

## Script Execution Process

When a [Bitcoin Cash](bitcoin-cash.md) node validates a transaction, it executes the unlocking and locking scripts in a specific sequence (source: mastering-bitcoin-cash_transactions_11.md):

1. **Unlocking Script Execution**: The unlocking script is executed first. If it executes without errors, the main stack is copied for the next step.
2. **Locking Script Execution**: The locking script is then executed using the state of the stack left by the unlocking script.
3. **Validation Result**: If the final result on top of the stack is `TRUE`, the unlocking script has successfully satisfied the conditions, and the transaction input is considered valid (source: mastering-bitcoin-cash_transactions_11.md).

## Practical Example: P2PKH Validation

In a Pay-to-Public-Key-Hash (P2PKH) transaction, the combined execution sequence looks like this:
`<Signature> <Public Key> OP_DUP OP_HASH160 <Public Key Hash> OP_EQUAL OP_CHECKSIG` (source: mastering-bitcoin-cash_transactions_11.md).

### Step-by-Step Execution:
1. **Signature**: The signature is pushed onto the stack.
2. **Public Key**: The [public key](addresses.md) is pushed onto the stack.
3. **Duplicate**: `OP_DUP` duplicates the [public key](addresses.md) on the stack.
4. **Hashing**: `OP_HASH160` hashes the [public key](addresses.md).
5. **Locking Hash**: The [public key](addresses.md) hash from the locking script is pushed onto the stack.
6. **Comparison**: `OP_EQUAL` compares the two hashes for equality.
7. **Verification**: `OP_CHECKSIG` verifies the signature against the [public key](addresses.md) (source: mastering-bitcoin-cash_transactions_11.md).

This systematic approach ensures that funds can only be spent by parties who provide valid signatures that match the specific conditions defined in the locking script.

## Related pages

- [transaction-scripts](transaction-scripts.md)
- [transaction-validation](transaction-validation.md)
- [standard-transaction-types](standard-transaction-types.md)
- [mastering-bitcoin-cash-transactions-10](mastering-bitcoin-cash-transactions-10.md)
