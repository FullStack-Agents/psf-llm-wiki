# block-level-validation-rules

**Summary**: Overview of the absolute consensus rules that define what transactions and blocks are permitted in the Bitcoin Cash blockchain, contrasting with network-level "standardness" rules.

**Sources**: block-level-validation-rules.md

**Last updated**: 2026-04-18

---

Block-level validation rules, also known as **consensus rules**, are absolute requirements for any block or transaction to be included in the blockchain. Any violation of these rules results in the immediate rejection of the block or transaction. 

These differ from [network-level validation rules](transaction-validation.md) (standardness rules), which provide recommended behavior for nodes. While nodes usually follow standardness rules when relaying, miners can choose to include non-standard transactions in a block as long as they do not violate consensus rules.

## Transaction Context and UTXOs

Transaction validation is context-dependent. A transaction must be validated relative to a specific block or a hypothetical "next" block (such as those in the mempool). 

The most critical validation rule is that **transaction inputs must be UTXOs** ([Unspent Transaction Outputs](utxo.md)). A transaction must spend outputs created by a prior transaction that have not yet been spent in the target block's history. This means that nodes on different blockchain forks may disagree on whether a transaction is valid if the transaction depends on a UTXO created in a block that only exists on one of the forks.

## Consensus Rules

The following rules must be strictly adhered to for a transaction or block to be considered valid:

### Spending and Value
- **Double-Spend Validation**: An input may only be spent once on a given blockchain fork. If two transactions attempt to spend the same input, only one can be valid.
- **Value Conservation**: The total value of a transaction's outputs may not exceed the total value of its inputs, except in the case of [coinbase transactions](coinbase-transaction.md).

### Coinbase Transactions
- **Reward Validation**: The coinbase transaction must collect the correct reward corresponding to the block height.
- **Coinbase Maturity**: Outputs from coinbase transactions cannot be spent until 100 blocks have passed (e.g., a reward from block 1,000 is spendable at block 1,100).
- **Block Height Requirement**: The coinbase unlocking script must start with a push operation that pushes the height of the block containing the transaction (introduced in BIP-34 to ensure uniqueness).

### Signature Checks (SigChecks)
Introduced in [HF-20200515](/protocol/forks/hf-20200515], SigChecks replaced the old SigOps system. The number of signature checks is limited to prevent Denial-of-Service (DoS) attacks:
- **Transaction Limit**: No more than 3,000 signature checks per transaction.
- **Block Limit**: The total signature checks in a block may not exceed the maximum block size divided by 141 (currently 226,950).

**Counting Rules**:
- `OP_CHECKSIG`, `OP_CHECKSIGVERIFY`, `OP_CHECKDATASIG`, and `OP_CHECKDATASIGVERIFY` increment the count by **+1** if the signature is non-NULL, and **+0** if it is NULL.
- `OP_CHECKMULTISIG` and `OP_CHECKMULTISIGVERIFY` increment by:
    - **+0** if all M signatures are NULL.
    - **+M** if at least one signature is non-NULL and verification is in Schnorr mode.
    - **+N** if at least one signature is non-NULL and verification is in ECDSA mode.

## Related pages

- [transaction-validation](transaction-validation.md)
- [utxo](utxo.md)
- [coinbase-transaction](coinbase-transaction.md)
- [blockchain](blockchain.md)
