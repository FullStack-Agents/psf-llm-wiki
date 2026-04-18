# Block

**Summary**: A block is a group of transactions bundled together and committed to the blockchain. It contains a single coinbase transaction followed by zero or more standard transactions.

**Sources**: block.md

**Last updated**: 2026-04-18

---

A block serves as a container for transactions on the Bitcoin Cash network. While the transactions within a block are generally unrelated, they are grouped by the time of their submission and the miner's selection.

## Block Headers
Blocks are uniquely identified by the SHA-256 hash of their header. This hash is the definitive ID of the block and is dependent on:
- The block's meta-information.
- The full contents of all included transactions, as the header contains the root of a [Merkle Tree](merkle-tree.md) of those transactions.

## Coinbase Transaction
Every block contains exactly one coinbase transaction, which is created by the miner. Unlike standard transactions, the coinbase input does not consume existing satoshis; instead, it creates new value from two sources:
1. **Block Reward**: A decreasing incentive for miners that starts at 50 BCH and halves every 210,000 blocks.
2. **Transaction Fees**: Satoshis from the transactions in the block that are not consumed by their respective outputs.

### Coinbase Requirements
- **Single Input**: Every coinbase transaction must have exactly one input.
- **Coinbase Message**: Miners can include arbitrary data (the "coinbase message") in the unlocking script.
- **Block Height**: Since the implementation of BIP-34 (version 2 blocks), the unlocking script must begin with the block height encoded as a variable-length, little-endian integer.
- **Size Limit**: The unlocking script for a coinbase transaction must be $\le 100$ bytes.

## Block Size and Limits
- **Maximum Size**: The maximum size for a block is 32MB ($32 \times 1000 \times 1000$ bytes).
- **Transaction Capacity**: The number of transactions is limited by this 32MB cap (minimum transaction size is 100 bytes) and other network rules, such as the total number of signature operations (sigops) allowed per block.

## Related pages

- [mining](mining.md)
- [merkle-tree](merkle-tree.md)
- [coinbase-transaction](coinbase-transaction.md)
- [blockchain-data-structure](blockchain-data-structure.md)
