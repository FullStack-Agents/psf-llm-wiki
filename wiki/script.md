# script

**Summary**: A detailed technical overview of the Bitcoin Cash scripting language, its execution model, validation rules, and a comprehensive list of operation codes (opcodes).

**Sources**: script.md

**Last updated**: 2026-04-18

---

Bitcoin Cash transactions use a specialized scripting language to authorize and secure transfers. While commonly described as "sending" funds to an "address," this is an abstraction; spending an [UTXO](utxo.md) requires the successful execution of a script.

## Script Execution

The language, known as **Script**, utilizes a stack-based memory model and is intentionally restricted. Unlike general-purpose languages, it does not support loops, persistent state across executions, or function definitions.

### Memory Model
- **The Stack**: The primary memory structure where data is pushed and popped.
- **The Alt-Stack**: A secondary stack used for temporary data storage. Data on the alt-stack is lost when a sub-script finishes execution.

### Transaction Validation
Scripts are executed during the validation of transactions. For each input spent, a script is constructed by sequentially executing the **unlocking script** (provided with the input) followed by the **locking script** (provided by the referenced previous output).

A combined script is considered successful if:
- **Non-Zero Value**: The top of the stack contains a non-zero (TRUE) value after execution.
- **No Stack Overflows**: No operation pops from an empty stack.
- **Clean Stack**: After execution, the stack contains exactly one non-zero value (added in [HF-20181115](/protocol/forks/hf-20181115)).

### Validation Constraints
- **Non-Empty**: Both locking and unlocking scripts must be non-empty.
- **Length**: Each script must be under 10,000 bytes (combined total < 20,000 bytes).
- **Control Flow**: IF/ELSE blocks cannot span across the boundary of the unlocking and locking scripts.
- **Push Only**: The unlocking script must contain only push operations (opcodes $\le$ 0x60), added in [HF-20181115](/protocol/forks/hf-20181115).

## Operation Codes (Opcodes)

The scripting language consists of a wide array of opcodes categorized by their functionality.

### Constants and Flow Control
- **Constants**: Opcodes like `OP_0` (FALSE), `OP_1` (TRUE), and `OP_PUSHBYTES_N` to push data onto the stack.
- **Flow Control**: Basic conditional branching using `OP_IF`, `OP_ELSE`, and `OP_ENDIF`. `OP_VERIFY` marks a transaction as invalid if the top stack value is not true.

### Stack and Splice Operations
- **Stack Manipulation**: Includes `OP_DUP` (duplicate), `OP_DROP` (remove), `OP_SWAP` (swap top two), and `OP_ROT` (rotate top three).
- **Alt-Stack**: `OP_TOALTSTACK` and `OP_FROMALTSTACK` move data between the primary and alternative stacks.
- **Splicing**: `OP_CAT` (concatenate), `OP_SPLIT` (substring), and `OP_REVERSEBYTES` (introduced in [HF-20200515](/protocol/forks/hf-20200515)).

### Logic and Arithmetic
- **Bitwise Logic**: `OP_AND`, `OP_OR`, `OP_XOR`, and `OP_EQUAL`.
- **Arithmetic**: Basic math operations (`OP_ADD`, `OP_SUB`, `OP_MUL`, `OP_DIV`, `OP_MOD`). Since [HF-20220515](/protocol/forks/hf-20220515), these operate on 8-byte signed "Script Number" integers. Overflow or underflow results in immediate failure.

### Cryptography and Locktime
- **Hashing**: Support for RIPEMD-160, SHA-1, SHA-256, and combined hashes (`OP_HASH160`, `OP_HASH256`).
- **Signatures**: `OP_CHECKSIG` and `OP_CHECKMULTISIG` verify ECDSA or Schnorr signatures.
- **Locktime**: `OP_CHECKLOCKTIMEVERIFY` (CLTV) and `OP_CHECKSEQUENCEVERIFY` (CSV) allow for time-locked spending conditions.

### Introspection
Introspection opcodes allow scripts to reference data from the transaction or the blockchain itself:
- **Transaction Data**: `OP_TXVERSION`, `OP_TXINPUTCOUNT`, `OP_TXLOCKTIME`.
- **UTXO Data**: `OP_UTXOVALUE`, `OP_UTXOBYTECODE`, `OP_OUTPOINTTXHASH`.
- **Token Data**: Opcodes to retrieve token categories, commitments, and amounts for both inputs and outputs (e.g., `OP_UTXOTOKENAMOUNT`, `OP_OUTPUTTOKENCATEGORY`).

## Related pages

- [locking-script](locking-script.md)
- [transaction-script-language](transaction-script-language.md)
- [transaction-validation](transaction-validation.md)
- [utxo](utxo.md)
