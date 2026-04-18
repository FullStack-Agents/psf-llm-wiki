# Script

Bitcoin Cash transactions make use of a scripting language to authorize and secure transfers.
While, colloquially, there is a tendency to refer to transactions as "sending" Bitcoin Cash to "an address", that is merely an abstraction.
In fact, the only thing that permits the spending of existing [UTXOs](/protocol/blockchain/transaction#transaction-output) is the successful execution of a script.
The only thing preventing the spending of newly created UTXOs is the difficulty of producing a successfully executing script.
Through the use of cryptographic signatures and hash functions, such scripts are often designed specifically to be difficult to produce unless you are the intended spender of a given UTXO, though that need not necessarily be the case.

For more information on how Transactions are commonly secured, see [Locking Script](/protocol/blockchain/transaction/locking-script).

This page will focus on how the scripts are run, what they are capable of, and what limitations they have.

## Script Execution

Scripts are executed using a stack-based memory model and have an intentionally restricted set of available operations.
Unlike the common general-purpose programming languages your are probably aware of, Script (the term for the language itself) does not allow for loops, persistent state/memory across script executions, or the definition of functions.
Instead, scripts are expected to contain whatever data they need and use the available operations to prove transaction validity.

### Features

In addition to the primary stack ("the stack"), there is a secondary stack, referred to as the "alt-stack", which data can be moved to temporarily.
Any data left on the alt-stack is lost when a given sub-script finishes execution.
In effect, any data moved to the alt-stack by an unlocking script is not present when the locking script runs.

There are a large number of op-codes that support everything from simple stack-manipulation, to mathematical calculations, to complex cryptographic processes.  In terms of control structures there are only basic conditional branching (IF/ELSE) operations available.

### Transaction Validation

Scripts are run when validating transactions, and successful execution of all of the scripts defined by the transaction is a necessary, but not sufficient, condition for transaction validity.
See [Transaction Validation](/protocol/blockchain/transaction-validation) for more details.

As a part of validating a transaction, a script is built for each input spent by the transaction.
Each script is the sequential execution (carrying over the same stack, but not alt-stack) of the [unlocking script](/protocol/blockchain/transaction/unlocking-script) provided with the input definition (which is used that the beginning of the script) and the locking script provided by the [previous output](/protocol/blockchain/transaction#transaction-output) being referenced.
The exception to this is [pay to script hash](/protocol/blockchain/transaction/locking-script#standard-scripts), which has an altered execution workflow.
In general, though, this combined unlocking/locking script is then executed and considered successful if and only if the following conditions are met:

 - **Non-Zero Value** - after execution the top of the stack must contain a non-zero (TRUE) value.
 - **No Stack Overflows** - no operation should attempt to pop a value from the stack when the stack is empty.  An overflow of the alt-stack is also disallowed.
 - **Clean Stack** - after execution the stack must only contain a single value, which must be non-zero (TRUE).  Added in [HF-20181115](/protocol/forks/hf-20181115).  The alt-stack is exempt from this.

Additionally, in order for the combined script to be valid, the following must be true:

 - **Non-Empty Scripts** - both the locking and unlocking scripts must be non-empty.
 - **Max Script Length** - the locking and unlocking script, when executed, must each be less than the max script length of 10,000 bytes (for a combined script maximum of 20,000 bytes).
 - **Contained Control Flow** - an IF/ELSE block cannot start in the unlocking script and end in the locking script, the script must be in the top-level scope when the locking script execution begins.
 - **Permitted Operations Only** - the locking script must not include operations that are disallowed and must not execute operations that are disabled..
 - **Push Only** - the unlocking script must contain only push operations (i.e. those with op codes 0x60 or less).  Added in [HF-20181115](/protocol/forks/hf-20181115).

NOTE: violations of the above rules does not necessarily make a transaction invalid.
For example, a locking script may be longer than 10,000 bytes, but it would be unspendable, since the max script length is only checked when the scripts are combined before execution.

## Operation codes (opcodes)

<style>
	table th:first-child,
	table td:first-child
	{
		width: fit-content;
	}

	table th,
	table td
	{
		font-size: smaller;
	}

	table a
	{
		font-size: inherit;
	}
</style>

The table below lists the currently allocated op codes.  Op codes marked with **(ignored)** are permitted but will do nothing when executed.
Op codes marked with **(disabled)** are permitted in scripts so long as they are not executed.
Op codes marked with **(do not use)** are disallowed and will make a transaction invalid merely be being present.

### Constants

| Codepoint   | Opcode          | Input | Output | Cost         | Description                                                 |
| ----------- | --------------- | ----- | ------ | ------------ | ----------------------------------------------------------- |
| 0x00        | OP_0, OP_FALSE  |       | 0      | 100          | An empty array of bytes is pushed onto the stack. See also [OP_X](/protocol/blockchain/script/op-codes/op-x) |
| 0x01 - 0x4b | OP_PUSHBYTES_N  |       |        | 100 + N      | The next *value* bytes is data to be pushed onto the stack. See also [OP_DATA_X](/protocol/blockchain/script/op-codes/op-data-x) |
| 0x4c        | OP_PUSHDATA1    |       |        | 100 + Length | The next byte contains the number of bytes to be pushed onto the stack. |
| 0x4d        | OP_PUSHDATA2    |       |        | 100 + Length | The next two bytes contain the number of bytes to be pushed onto the stack in little endian order. |
| 0x4e        | OP_PUSHDATA4    |       |        | 100 + Length | The next four bytes contain the number of bytes to be pushed onto the stack in little endian order. |
| 0x4f        | OP_1NEGATE      |       | -1     | 100 + 1      | The number -1 is pushed onto the stack.                     |
| 0x51        | OP_1, OP_TRUE   |       | 1      | 100 + 1      | The number 1 is pushed onto the stack.                      |
| 0x52 - 0x60 | OP_2 - OP_16    |       | 2-16   | 100 + 1      | The number (2-16) is pushed onto the stack.                 |


### Flow control

| Codepoint  | Opcode      | Input                                  | Output           | Cost | Description                |
| ---- | --------- | -------------------------------------- | ---------------- | ---- | -------------------------- |
| 0x61 | OP_NOP    |                                        |                  | 100  | Does nothing.              |
| 0x63 | OP_IF     | IF [statements] ENDIF                  |                  | 100  | If the top stack value is not False, the statements are executed. The top stack value is removed. |
| 0x64 | OP_NOTIF  | NOTIF [statements] ENDIF               |                  | 100  | If the top stack value is False, the statements are executed. The top stack value is removed. |
| 0x67 | OP_ELSE   | IF/NOTIF [...] ELSE [statements] ENDIF |                  | 100  | If the preceding OP_IF or OP_NOTIF or OP_ELSE was not executed then these statements are and if the preceding OP_IF or OP_NOTIF or OP_ELSE was executed then these statements are not. |
| 0x68 | OP_ENDIF  | IF [statements] ENDIF                  |                  | 100  | Ends an if/else block. All blocks must end, or the transaction is **marked as invalid**. An OP_ENDIF without OP_IF earlier is also **invalid**. |
| 0x69 | OP_VERIFY | true / false                           | Nothing / *fail* | 100  | **Marks transaction as invalid** if top stack value is not true. The top stack value is removed. |
| 0x6a | OP_RETURN |                                        | *fail*           | 100  | **Marks the output as unspendable**. Since [Bitcoin Core 0.9](https://bitcoin.org/en/release/v0.9.0#opreturn-and-data-in-the-block-chain), a standard way of attaching extra data to transactions is to add a zero-value output with a scriptPubKey consisting of OP_RETURN followed by data. Such outputs are provably unspendable and specially discarded from storage in the UTXO set, reducing their cost to the network. Current [standard relay rules](https://reference.cash/protocol/blockchain/transaction-validation/network-level-validation-rules/) on the Bitcoin Cash network allow any number of outputs with OP_RETURN, that contains any sequence of push statements (or OP_RESERVED) after the OP_RETURN provided the total scriptPubKey length is at most 223 bytes. |


### Stack

| Codepoint  | Opcode            | Input               | Output                 | Cost                                 | Description                           |
| ---- | --------------- | ------------------- | ---------------------- | ------------------------------------ | ------------------------------------- |
| 0x6b | OP_TOALTSTACK   | a                   | (alt) a                | 100                                  | Puts the input onto the top of the alt stack. Removes it from the main stack. |
| 0x6c | OP_FROMALTSTACK | (alt) a             | a                      | 100 + a.length                       | Puts the input onto the top of the main stack. Removes it from the alt stack. |
| 0x73 | OP_IFDUP        | a                   | a &#124; a a           | 100 &#124; 100 + a.length            | If the top stack value is not 0, duplicate it. |
| 0x74 | OP_DEPTH        |                     | depth                  | 100 + depth.length                   | Puts the number of stack items onto the stack. |
| 0x75 | OP_DROP         | a                   |                        | 100                                  | Removes the top stack item.           |
| 0x76 | OP_DUP          | a                   | a a                    | 100 + a.length                       | Duplicates the top stack item.        |
| 0x77 | OP_NIP          | a b                 | b                      | 100                                  | Removes the second-to-top stack item. |
| 0x78 | OP_OVER         | a b                 | a b a                  | 100 + a.length                       | Copies the second-to-top stack item to the top. |
| 0x79 | OP_PICK         | xn ... x2 x1 x0 n   | xn ... x2 x1 x0 xn     | 100 + a.length                       | The item *n* back in the stack is copied to the top. |
| 0x7a | OP_ROLL         | xn ... x2 x1 x0 n   | x(n-1) ... x2 x1 x0 xn | 100 + a.length + depth.length        | The item *n* back in the stack is moved to the top. |
| 0x7b | OP_ROT          | a b c               | b c a                  | 100                                  | The top three items on the stack are rotated to the left. |
| 0x7c | OP_SWAP         | a b                 | b a                    | 100                                  | The top two items on the stack are swapped. |
| 0x7d | OP_TUCK         | a b                 | b a b                  | 100 + b.length                       | The item at the top of the stack is copied and inserted below the second-to-top item. |
| 0x6d | OP_2DROP        | a b                 |                        | 100                                  | Removes the top two stack items.      |
| 0x6e | OP_2DUP         | a b                 | a b a b                | 100 + a.length + b.length            | Duplicates the top two stack items.   |
| 0x6f | OP_3DUP         | a b c               | a b c a b c            | 100 + a.length + b.length + c.length | Duplicates the top three stack items. |
| 0x70 | OP_2OVER        | a b c d             | a b c d a b            | 100 + a.length + b.length            | Copies the pair of items two spaces back in the stack to the front. |
| 0x71 | OP_2ROT         | a b c d e f         | c d e f a b            | 100 + a.length + b.length            | The fifth and sixth items back are moved to the top of the stack. |
| 0x72 | OP_2SWAP        | a b c d             | c d a b                | 100                                  | Swaps the top two pairs of items.     |


### Splice

| Codepoint  | Opcode            | Input         | Output     | Cost                      | Description                                                       |
| ---------- | ----------------- | ------------- | ---------- | ------------------------- | ----------------------------------------------------------------- |
| 0x7e       | OP_CAT            | a b           | c          | 100 + a.length + b.length | Concatenates two byte sequences                                   |
| 0x7f       | OP_SPLIT          | x n           | x1 x2      | 100 + a.length + b.length | Splits byte sequence *x* at position *n*. Known as OP_SUBSTR before 2018-05-15. |
| 0x80       | OP_NUM2BIN        | a b           | c          | 100 + b.length            | Converts numeric value *a* into byte sequence of length *b*. Known as OP_LEFT before 2018-05-15. |
| 0x81       | OP_BIN2NUM        | a             | b          | 100 + b.length            | Converts byte sequence *x* into a numeric value. Known as OP_RIGHT before 2018-05-15. |
| 0x82       | OP_SIZE           | a             | a b        | 100 + b.length            | Pushes the byte length of the top element of the stack (without popping it). |
| 0xbc       | OP_REVERSEBYTES   | a             | b          | 100 + b.length            | Reverses the order of the bytes in byte sequence *x* so that the first byte is now its last byte, the second is now its second-to-last, and so forth. Enabled in [HF-20200515](/protocol/forks/hf-20200515). |


### Bitwise logic

| Codepoint  | Opcode            | Input         | Output                | Cost               | Description                                                      |
| ---------- | ----------------- | ------------- | --------------------- | ------------------ | ----------------------------------------------------------------- |
| 0x83       | OP_INVERT         | N/A           | N/A                   | 0                  | **DISABLED**                                                     |
| 0x84       | OP_AND            | a b           | c                     | 100 + c.length     | Boolean *AND* between each bit of the inputs                      |
| 0x85       | OP_OR             | a b           | c                     | 100 + c.length     | Boolean *OR* between each bit of the inputs.                      |
| 0x86       | OP_XOR            | a b           | c                     | 100 + c.length     | Boolean *EXCLUSIVE OR* between each bit of the inputs.            |
| 0x87       | OP_EQUAL          | a b           | true &#124; false     | 100 &#124; 100 + 1 | Returns 1 if the inputs are exactly equal, 0 otherwise.           |
| 0x88       | OP_EQUALVERIFY    | a b           | Nothing &#124; *fail* | 100 + 1            | Same as OP_EQUAL, but runs OP_VERIFY afterward.                   |


### Arithmetic

Numeric opcodes (OP_1ADD, etc.) are restricted to operating on 8-byte signed "Script Number" integers, enabled in [HF-20220515](/protocol/forks/hf-20220515).
This excludes the value `-9223372036854775808` that fits in 8-byte two's complement encoding, but does not fit in an 8-byte Script Number encoding used by the Script VM.
If an operation [overflows or underflows](protocol/forks/chips/2022-05-bigger-script-integers#arithmetic-operation-overflows), the operation must immediately fail evaluation.

| Codepoint  | Opcode                 | Input         | Output                | Cost                                          | Description                                          |
| ---------- | ---------------------- | ------------- | --------------------- | --------------------------------------------- | ---------------------------------------------------- |
| 0x8b       | OP_1ADD                | a             | b                     | 100 + (2 * b.length)                          | 1 is added to the input.                             |
| 0x8c       | OP_1SUB                | a             | b                     | 100 + (2 * b.length)                          | 1 is subtracted from the input.                      |
| 0x8d       | OP_2MUL                | a             | b                     | 0                                             | The input is multiplied by 2. **DISABLED**           |
| 0x8e       | OP_2DIV                | a             | b                     | 0                                             | The input is divided by 2. **DISABLED**              |
| 0x8f       | OP_NEGATE              | a             | b                     | 100 + (2 * b.length)                          | The sign of the input is flipped.                    |
| 0x90       | OP_ABS                 | a             | b                     | 100 + (2 * b.length)                          | The input is made positive.                          |
| 0x91       | OP_NOT                 | a             | true &#124; false     | 100 &#124; 100 + 1                            | If the input is 0 or 1, it is flipped. Otherwise the output will be 0. |
| 0x92       | OP_0NOTEQUAL           | a             | true &#124; false     | 100 &#124; 100 + 1                            | Returns 0 if the input is 0. 1 otherwise.            |
| 0x93       | OP_ADD                 | a b           | c                     | 100 + (2 * c.length)                          | *a* is added to *b*.                                 |
| 0x94       | OP_SUB                 | a b           | c                     | 100 + (2 * c.length)                          | *b* is subtracted from *a*.                          |
| 0x95       | OP_MUL                 | a b           | c                     | 100 + (2 * c.length) + (a.length * b.length)  | *a* is multiplied by *b*. Enabled in [HF-20220515](/protocol/forks/hf-20220515). |
| 0x96       | OP_DIV                 | a b           | c                     | 100 + (2 * c.length) + (a.length * b.length)  | *a* is [divided](/protocol/blockchain/script/integer-division) by *b*. |
| 0x97       | OP_MOD                 | a b           | c                     | 100 + (2 * c.length) + (a.length * b.length)  | Returns the remainder after *a* is [divided](/protocol/blockchain/script/integer-division) by *b*. |
| 0x98       | OP_LSHIFT              | a b           | c                     | 0                                             | Shifts *a* left *b* bits, preserving sign. **DISABLED** |
| 0x99       | OP_RSHIFT              | a b           | c                     | 0                                             | Shifts *a* right *b* bits, preserving sign. **DISABLED** |
| 0x9a       | OP_BOOLAND             | a b           | true &#124; false     | 100 &#124; 100 + 1                            | If both *a* and *b* are not 0, the output is 1. Otherwise 0. |
| 0x9b       | OP_BOOLOR              | a b           | true &#124; false     | 100 &#124; 100 + 1                            | If *a* or *b* is not 0, the output is 1. Otherwise 0. |
| 0x9c       | OP_NUMEQUAL            | a b           | true &#124; false     | 100 &#124; 100 + 1                            | Returns 1 if the numbers are equal, 0 otherwise.      |
| 0x9d       | OP_NUMEQUALVERIFY      | a b           | Nothing &#124; *fail* | 100 + 1                                       | Same as OP_NUMEQUAL, but runs OP_VERIFY afterward.    |
| 0x9e       | OP_NUMNOTEQUAL         | a b           | true &#124; false     | 100 &#124; 100 + 1                            | Returns 1 if the numbers are not equal, 0 otherwise.  |
| 0x9f       | OP_LESSTHAN            | a b           | true &#124; false     | 100 &#124; 100 + 1                            | Returns 1 if *a* is less than *b*, 0 otherwise.       |
| 0xa0       | OP_GREATERTHAN         | a b           | true &#124; false     | 100 &#124; 100 + 1                            | Returns 1 if *a* is greater than *b*, 0 otherwise.    |
| 0xa1       | OP_LESSTHANOREQUAL     | a b           | true &#124; false     | 100 &#124; 100 + 1                            | Returns 1 if *a* is less than or equal to *b*, 0 otherwise. |
| 0xa2       | OP_GREATERTHANOREQUAL  | a b           | true &#124; false     | 100 &#124; 100 + 1                            | Returns 1 if *a* is greater than or equal to *b*, 0 otherwise. |
| 0xa3       | OP_MIN                 | a b           | c                     | 100 + (2 * c.length)                          | Returns the smaller of a and b.                       |
| 0xa4       | OP_MAX                 | a b           | c                     | 100 + (2 * c.length)                          | Returns the larger of a and b.                        |
| 0xa5       | OP_WITHIN              | a min max     | true &#124; false     | 100 &#124; 100 + 1                            | Returns 1 if *a* is within the specified range (left-inclusive), 0 otherwise. |


### Cryptography

| Codepoint  | Opcode                 | Input                           | Output                | Cost                                                                        | Description                                   |
| ---------- | ---------------------- | ------------------------------- | --------------------- | --------------------------------------------------------------------------- | --------------------------------------------- |
| 0xa6       | OP_RIPEMD160           | a                               | b                     | 100 + (iterations * 192) + b.length                                         | Hashes input with RIPEMD-160.                 |
| 0xa7       | OP_SHA1                | a                               | b                     | 100 + (iterations * 192) + b.length                                         | Hashes input with SHA-1.                      |
| 0xa8       | OP_SHA256              | a                               | b                     | 100 + (iterations * 192) + b.length                                         | Hashes input with SHA-256.                    |
| 0xa9       | OP_HASH160             | a                               | b                     | 100 + ((iterations + 1) * 192) + b.length                                   | Hashes input with SHA-256 and then with RIPEMD-160. |
| 0xaa       | OP_HASH256             | a                               | b                     | 100 + ((iterations + 1) * 192) + b.length                                   | Hashes input twice with SHA-256.              |
| 0xab       | OP_CODESEPARATOR       |                                 |                       | 100                                                                         | Makes `OP_CHECK(MULTI)SIG(VERIFY)` use the subset of the script of everything after the most recently-executed OP_CODESEPARATOR when computing the sighash. |
| 0xac       | OP_CHECKSIG            | sig pubkey                      | true &#124; false     | 100 + 26000 + (iterations * 192) + 1 or 100 for null signature checks       | The last byte (=sighash type) of the signature is removed. The sighash for this input is calculated based on the sighash type. The truncated signature used by OP_CHECKSIG must be a valid ECDSA or Schnorr signature for this hash and public key. If it is valid, 1 is returned, if it is empty, 0 is returned, otherwise the operation fails. |
| 0xad       | OP_CHECKSIGVERIFY      | sig pubkey                      | nothing &#124; *fail* | 100 + 26000 + (iterations * 192) + 1                                        | Same as OP_CHECKSIG, but OP_VERIFY is executed afterward. |
| 0xae       | OP_CHECKMULTISIG       | [dummy] [signatures] m [keys] n | true &#124; false     | 100 + (26000 * [m for schnorr, n for ecdsa]) + (iterations * 192) + 1 or 100 for null signature checks | Signatures are checked against public keys. Signatures must be placed in the unlocking script using the same order as their corresponding public keys were placed in the locking script or redeem script. If all signatures are valid, 1 is returned, 0 otherwise. All elements are removed from the stack. For more information on the execution of this opcode, see [Multisignature](/protocol/blockchain/cryptography/multisignature). |
| 0xaf       | OP_CHECKMULTISIGVERIFY | [dummy] [signatures] m [keys] n | nothing &#124; *fail* | 100 + (26000 * [m for schnorr, n for ecdsa]) + (iterations * 192) + 1                                  | Same as OP_CHECKMULTISIG, but OP_VERIFY is executed afterward. |
| 0xba       | OP_CHECKDATASIG        | sig msg pubkey                  | true &#124; false     | 100 + 26000 + (iterations * 192) + 1 or 100 for null signature checks       | Check if signature is valid for message and a public key. [See spec](/protocol/forks/op_checkdatasig) |
| 0xbb       | OP_CHECKDATASIGVERIFY  | sig msg pubkey                  | nothing &#124; *fail* | 100 + 26000 + (iterations * 192)                                            | Same as OP_CHECKDATASIG, but runs OP_VERIFY afterward. |


### Locktime

| Codepoint  | Opcode                 | Input | Output          | Cost | Description                                     |
| ---------- | ---------------------- | ----- | --------------- | ---- | ----------------------------------------------- |
| 0xb1       | OP_CHECKLOCKTIMEVERIFY | a     | a &#124; *fail* | 100  | Marks transaction as invalid if the top stack item is greater than the transaction's nLockTime field, otherwise script evaluation continues as though an OP_NOP was executed. Transaction is also invalid if 1. the stack is empty; or 2. the top stack item is negative; or 3. the top stack item is greater than or equal to 500000000 while the transaction's nLockTime field is less than 500000000, or vice versa; or 4. the input's nSequence field is equal to 0xffffffff. The precise semantics are described in [BIP65](/protocol/forks/bip-0065). |
| 0xb2       | OP_CHECKSEQUENCEVERIFY | a     | a &#124; *fail* | 100  | Marks transaction as invalid if the relative lock time of the input (enforced by BIP68 with nSequence) is not equal to or longer than the value of the top stack item. The precise semantics are described in [BIP112](/protocol/forks/bip-0112). |


### Introspection

| Codepoint  | Opcode                   | Input | Output | Cost           | Description                                            |
| ---------- | ------------------------ | ----- | ------ | -------------- | ------------------------------------------------------ |
| 0xc0       | OP_INPUTINDEX            |       | a      | 100 + a.length | Push the index of the input being evaluated to the stack as a Script Number. |
| 0xc1       | OP_ACTIVEBYTECODE        |       | a      | 100 + a.length | Push the bytecode currently being evaluated, beginning after the last executed OP_CODESEPARATOR, to the stack1. For Pay-to-Script-Hash (P2SH) evaluations, this is the redeem bytecode of the Unspent Transaction Output (UTXO) being spent; for all other evaluations, this is the locking bytecode of the UTXO being spent. |
| 0xc2       | OP_TXVERSION             |       | a      | 100 + a.length | Push the version of the current transaction to the stack as a Script Number. |
| 0xc3       | OP_TXINPUTCOUNT          |       | a      | 100 + a.length | Push the count of inputs in the current transaction to the stack as a Script Number. |
| 0xc4       | OP_TXOUTPUTCOUNT         |       | a      | 100 + a.length | Push the count of outputs in the current transaction to the stack as a Script Number. |
| 0xc5       | OP_TXLOCKTIME            |       | a      | 100 + a.length | Push the locktime of the current transaction to the stack as a Script Number. |
| 0xc6       | OP_UTXOVALUE             | a     | b      | 100 + b.length | Pop the top item from the stack as an input index (Script Number). Push the value (in satoshis) of the Unspent Transaction Output (UTXO) spent by that input to the stack as a Script Number. |
| 0xc7       | OP_UTXOBYTECODE          | a     | b      | 100 + b.length | Pop the top item from the stack as an input index (Script Number). Push the full locking bytecode of the Unspent Transaction Output (UTXO) spent by that input to the stack. |
| 0xc8       | OP_OUTPOINTTXHASH        | a     | b      | 100 + b.length | Pop the top item from the stack as an input index (Script Number). From that input, push the outpoint transaction hash – the hash of the transaction which created the Unspent Transaction Output (UTXO) which is being spent – to the stack in OP_HASH256 byte order. |
| 0xc9       | OP_OUTPOINTINDEX         | a     | b      | 100 + b.length | Pop the top item from the stack as an input index (Script Number). From that input, push the outpoint index – the index of the output in the transaction which created the Unspent Transaction Output (UTXO) which is being spent – to the stack as a Script Number. |
| 0xca       | OP_INPUTBYTECODE         | a     | b      | 100 + b.length | Pop the top item from the stack as an input index (Script Number). Push the unlocking bytecode of the input at that index to the stack. |
| 0xcb       | OP_INPUTSEQUENCENUMBER   | a     | b      | 100 + b.length | Pop the top item from the stack as an input index (Script Number). Push the sequence number of the input at that index to the stack as a Script Number. |
| 0xcc       | OP_OUTPUTVALUE           | a     | b      | 100 + b.length | Pop the top item from the stack as an output index (Script Number). Push the value (in satoshis) of the output at that index to the stack as a Script Number. |
| 0xcd       | OP_OUTPUTBYTECODE        | a     | b      | 100 + b.length | Pop the top item from the stack as an output index (Script Number). Push the locking bytecode of the output at that index to the stack. |
| 0xce       | OP_UTXOTOKENCATEGORY     | a     | b      | 100 + b.length | Pop the top item from the stack as an input index (VM Number). If the Unspent Transaction Output (UTXO) spent by that input includes no tokens, push a 0 (VM Number) to the stack. If the UTXO does not include a non-fungible token with a capability, push the UTXO's token category, otherwise, push the concatenation of the token category and capability, where the mutable capability is represented by 1 (VM Number) and the minting capability is represented by 2 (VM Number). |
| 0xcf       | OP_UTXOTOKENCOMMITMENT   | a     | b      | 100 + b.length | Pop the top item from the stack as an input index (VM Number). Push the token commitment of the Unspent Transaction Output (UTXO) spent by that input to the stack. If the UTXO does not include a non-fungible token, or if it includes a non-fungible token with a zero-length commitment, push a 0 (VM Number). |
| 0xd0       | OP_UTXOTOKENAMOUNT       | a     | b      | 100 + b.length | Pop the top item from the stack as an input index (VM Number). Push the fungible token amount of the Unspent Transaction Output (UTXO) spent by that input to the stack as a VM Number. If the UTXO includes no fungible tokens, push a 0 (VM Number). |
| 0xd1       | OP_OUTPUTTOKENCATEGORY   | a     | b      | 100 + b.length | Pop the top item from the stack as an output index (VM Number). If the output at that index includes no tokens, push a 0 (VM Number) to the stack. If the output does not include a non-fungible token with a capability, push the output's token category, otherwise, push the concatenation of the token category and capability, where the mutable capability is represented by 1 (VM Number) and the minting capability is represented by 2 (VM Number). |
| 0xd2       | OP_OUTPUTTOKENCOMMITMENT | a     | b      | 100 + b.length | Pop the top item from the stack as an output index (VM Number). Push the token commitment of the output at that index to the stack. If the output does not include a non-fungible token, or if it includes a non-fungible token with a zero-length commitment, push a 0 (VM Number). |
| 0xd3       | OP_OUTPUTTOKENAMOUNT     | a     | b      | 100 + b.length | Pop the top item from the stack as an output index (VM Number). Push the fungible token amount of the output at that index to the stack as a VM Number. If the output includes no fungible tokens, push a 0 (VM Number). |


### Reserved

| Codepoint       | Opcode           | Input | Output | Cost | Description                                                              |
| --------------- | ---------------- | ----- | ------ | ---- | ------------------------------------------------------------------------ |
| 0xb0            | OP_NOP1          |       |        | 0    | Previously reserved for OP_EVAL (BIP12).                                 |
| 0xb3-0xb9       | OP_NOP4-OP_NOP10 |       |        | 0    | Ignored. Does not mark transaction as invalid.                           |


### Uncategorized

Please help improve this article by categorizing and describing the following op codes.

| Codepoint | Opcode           | Input | Output | Cost | Description                                                              |
| --------- | ---------------- | ----- | ------ | ---- | ------------------------------------------------------------------------ |
| 0x50      | OP_RESERVED      |       |        | 0    | **(disabled)**                                                           |
| 0x62      | OP_VER           |       |        | 0    | **(disabled)**                                                           |
| 0x65      | OP_VERIF         |       |        | 0    | **(do not use)**                                                         |
| 0x66      | OP_VERNOTIF      |       |        | 0    | **(do not use)**                                                         |
| 0x89      | OP_RESERVED1     |       |        | 0    | **(do not use)**                                                         |
| 0x8a      | OP_RESERVED2     |       |        | 0    | **(do not use)**                                                         |
| 0xbd-0xff | Unused           |       |        | 0    | **(disabled)**                                                           |

