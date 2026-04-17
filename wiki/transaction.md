# Transaction

**Summary**: The fundamental mechanism for transferring value (BCH and tokens) on the [blockchain](blockchain.md), consisting of inputs spent and outputs created.

**Sources**: transaction.md

**Last updated**: 2026-04-17

---

A [transaction](bitcoin-cash-transactions.md) is a set of [transaction-inputs](transaction-anatomy.md) (debits) spent to create a set of [transaction-outputs](transaction-anatomy.md) (credits). Nodes verify each transaction against blockchain rules before it is admitted to a block.

## Verification Rules
For a transaction to be valid:
- Inputs must not have been previously spent.
- Total input value $\ge$ total output value.
- The transaction must be syntactically and cryptographically valid.
- The [locking-scripts](transaction-scripts.md) of the spent outputs must be correctly unlocked by the [unlocking-scripts](transaction-scripts.md) in the inputs.

## Transaction Format
| Field | Length | Format | Description |
|--|--|--|--|
| version | 4 bytes | unsigned int (LE) | Transaction format version (currently `0x02000000`). |
| input count | variable | varint | Number of inputs. |
| transaction inputs | variable | - | Serialized inputs. |
| output count | variable | varint | Number of outputs. |
| transaction outputs | variable | - | Serialized outputs. |
| lock-time | 4 bytes | unsigned int (LE) | Block height or timestamp after which the transaction is valid. |

### Lock-time and Median-Time-Past (MTP)
- **Interpretation**: If lock-time $< 500,000,000$, it is a block height. Otherwise, it is a Unix timestamp.
- **MTP**: To prevent issues with non-monotonic timestamps, time-based locking is compared to the Median-Time-Past (the median timestamp of the 11 preceding blocks). This introduces an average delay of one hour after the lock-time is reached (source: transaction.md).

## Transaction Input
Inputs reference a **PrevOut** (a [utxo](utxo.md) from a prior transaction) and provide proof of ownership.
- **Format**: includes the previous transaction hash, output index, unlocking script, and a sequence number.
- **Relative Lock-time**: Since BIP-68, the sequence number can act as a relative lock-time, preventing mining until a certain time or block depth has passed since the output was created (source: transaction.md).

## Transaction Output
Outputs specify the amount of satoshis and the requirements (locking script) to spend them.
- **Format**: Includes value (satoshis) and the locking script.
- **Token Output Format**: Since HF-20230515, outputs can encode token state (category, NFT commitment, and fungible amount) using a "token prefix" before the locking bytecode (source: transaction.md).
- **Token Bitfield**: A bitfield determines if the output contains an NFT, an amount of fungible tokens, and the capability of the NFT (immutable, mutable, or minting).

## Fees and Burning
- **Transaction Fees**: The difference between total input value and total output value is collected by the miner as a fee.
- **Token Burning**: Any extra tokens from inputs not accounted for in outputs are implicitly burned (source: transaction.md).

## Related pages

- [transaction-anatomy](transaction-anatomy.md)
- [transaction-scripts](transaction-scripts.md)
- [utxo](utxo.md)
- [bitcoin-cash-transactions](bitcoin-cash-transactions.md)
- [transaction-fees](transaction-fees.md)
- [blockchain](blockchain.md)
