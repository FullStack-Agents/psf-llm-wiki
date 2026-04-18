# network-level-validation-rules

**Summary**: Overview of "standardness" rules in Bitcoin Cash, which determine whether nodes relay a transaction to their peers, contrasting with absolute consensus rules.

**Sources**: network-level-validation-rules.md

**Last updated**: 2026-04-18

---

Network-level validation rules, also known as **standardness rules**, define the recommended behavior for nodes on the network. Unlike [block-level validation rules](block-level-validation-rules.md) (consensus rules), which are absolute, standardness rules can be configured per node. A node may receive a transaction that is technically valid according to consensus rules but choose not to relay it to its peers if it is considered "non-standard."

Miners may still choose to include non-standard transactions in a block, as they do not violate consensus. Because these rules can vary between node implementations, it is often advisable to broadcast transactions to multiple nodes.

## Standard Transactions

A transaction is considered "standard" if it meets the following criteria:

### Structural Requirements
- **Size**: Total transaction size must be below 100,000 bytes.
- **Version**: Must be version 1 or [version 2](/protocol/forks/bip-0068/).
- **Input Scripts**: Must contain only push operations and be $\le$ 1,650 bytes in length.
- **Locking Scripts**: Outputs must use [standard locking scripts](locking-script.md).
- **Multisig**: For multisig outputs, there must be at most 3 parties and at least 1 required party (1-of-1 through 3-of-3).

### Data and Value Constraints
- **Data Outputs**: The total size of [data output](locking-script.md) locking scripts must not exceed 223 bytes. Since [HF-20210515](/protocol/forks/hf-20210515), this limit applies to the sum of all data outputs in the transaction.
- **Dust Limit**: All non-data outputs must be above the "dust" threshold.
- **Signature Checks**: Each input must require no more than `((scriptLength + 60) / 43)` [SigChecks](block-level-validation-rules.md).

## The Dust Threshold

To prevent the network from being bogged down by transactions with very small amounts that are expensive to spend (relative to their value), nodes reject "dust" outputs.

### Definition of Dust
Dust is generally defined as an output where the cost to spend it would be more than 1/3 of the minimum relay fee. While implementations vary, the common default threshold is **546 satoshis**. 

**Exception**: Provably unspendable outputs (such as data outputs using `OP_RETURN`) have a dust threshold of zero.

### implementation Variations
- **bchd & Bitcoin ABC**: Calculate dust based on the `minFreeTxRelayFee` (typically resulting in 546 satoshis).
- **Bitcoin Unlimited**: Uses a static threshold of 546 satoshis.
- **Bitcoin Verde**: Similar to ABC, but adjusts input size to 180 bytes for uncompressed addresses and uses a fixed 34-byte output length.

## Related pages

- [block-level-validation-rules](block-level-validation-rules.md)
- [transaction-validation](transaction-validation.md)
- [locking-script](locking-script.md)
- [script](script.md)
