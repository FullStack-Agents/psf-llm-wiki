# transaction-validation

**Summary**: Overview of the transaction validation process in Bitcoin Cash, categorized by script execution, block-level rules, and network-level rules.

**Sources**: transaction-validation.md

**Last updated**: 2026-04-18

---

Transaction validation in Bitcoin Cash consists of various checks that determine how a node handles a received transaction. While some transactions are rejected as outright invalid, others may be valid for some nodes but not others. Ultimately, network consensus is achieved through the [blockchain](blockchain.md), where any ambiguity regarding a transaction's validity is resolved as new blocks are mined.

## Validation Categories

Transaction validation is divided into three primary categories:

1. **Script Execution Rules**: Determine whether the inputs of a transaction are considered spendable (see [script](script.md)).
2. **Block-Level Validation Rules**: Determine if a transaction is valid within a specific blockchain context, such as a particular block and its associated history.
3. **Network-Level Validation Rules**: Determine whether a transaction is relayed from one node to another.

These categories are closely intertwined and lead to different outcomes when rules are violated.

## Miscellaneous Validation Rules

Bitcoin Cash includes several specific exceptions and rules:

### Genesis Block Coinbase
- The coinbase transaction of the genesis block is unspendable.
- Its output is not treated as an Unspent Transaction Output ([UTXO](utxo.md)).

### Coinbase Constraints
- Coinbase transactions are restricted to exactly one transaction input.
- The unlocking script for any coinbase transaction must be 100 bytes or less in size.

## Related pages

- [script](script.md)
- [blockchain](blockchain.md)
- [utxo](utxo.md)
- [coinbase-transaction](coinbase-transaction.md)
