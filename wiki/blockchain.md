# Blockchain

**Summary**: A linear collection of blocks that forms the authoritative ledger of the Bitcoin Cash network, secured by proof-of-work and cryptographic chaining.

**Sources**: blockchain.md

**Last updated**: 2026-04-17

---

A [blockchain](blockchain.md) is a sequential record of [blocks](blockchain-data-structure.md), where each block contains a set of [transactions](bitcoin-cash-transactions.md). The state of the network is derived by executing these transactions in order. This process creates the overall [blockchain-ledger](blockchain-ledger.md).

## Structure and Security
- **Cryptographic Chaining**: Each block includes the [hash](hash.md) of the previous block. This ensures that any modification to a past block would require rebuilding all subsequent blocks, making the history immutable provided sufficient work is required. This is conceptually similar to Git commits.
- **Proof-of-Work (PoW)**: To create a block, a node must perform a specific amount of computational work ([proof-of-work](proof-of-work.md)). This prevents instant block creation and secures the chain against history rewriting (source: blockchain.md).

## Block Height and Sibling Blocks
- **Block Height**: The distance of a block from the [genesis-block](genesis-block.md). The genesis block has a height of `0`.
- **Contentious/Sibling Blocks**: Two blocks sharing the same height. This occurs when two miners find valid blocks nearly simultaneously before the network can propagate them.
- **Resolution**: One block eventually becomes orphaned as the network reaches consensus (usually when a subsequent block is mined on top of one of the contentious blocks).
- **BIP-34**: This update ensured that block height is included within the [coinbase-transaction](coinbase-transaction.md) (source: blockchain.md).

## Work and Consensus
- **Main Chain**: The longest valid chain with the most total proof-of-work is generally accepted as the main chain.
- **Chainwork**: The summation of all work done on each block up to a specific point. Since HF-20171113, chainwork is used to calculate the new block's difficulty adjustment starting from block height 504,032 (source: blockchain.md).

## Blockchain Reorganization (Reorg)
A "reorg" occurs when a node switches from one chain to another after discovering a chain with more work.
- **Impact**: Transactions on the abandoned chain may become invalid if the same [utxo](utxo.md) was spent on the winning chain.
- **Recovery**: Valid transactions from the orphaned chain are typically migrated back into the [mempool](mempool.md) if they remain valid (source: blockchain.md, memory-pool.md).

## The Genesis Block
The first block in the chain, with a hard-coded hash: `000000000019D6689C085AE165831E934FF763AE46A2A6C172B3F1B60A8CE26F`.
- **Coinbase Transaction**: Contains a single transaction with an unlocking script including the text: *"The Times 03/Jan/2009 Chancellor on brink of second bailout for banks"*.
- **Technical Details**: The genesis block's merkle tree consists of only this single coinbase transaction (source: blockchain.md).

## Related pages

- [blockchain-data-structure](blockchain-data-structure.md)
- [proof-of-work](proof-of-work.md)
- [genesis-block](genesis-block.md)
- [hash](hash.md)
- [coinbase-transaction](coinbase-transaction.md)
- [mempool](mempool.md)
- [utxo](utxo.md)
- [blockchain-ledger](blockchain-ledger.md)
