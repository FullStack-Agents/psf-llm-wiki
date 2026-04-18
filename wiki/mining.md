# Mining

**Summary**: The process of modifying a proposed block's header until its hash meets a specific target, thereby securing the network and adding new blocks to the [blockchain](blockchain.md).

**Sources**: mining.md, mastering-bitcoin-cash_transactions_1.md

**Last updated**: 2026-04-18

---

Mining is the process of verifying transactions and bundling them into blocks. A miner seeks to alter a proposed block until its hash, when interpreted as a number, is below a calculated [target](proof-of-work.md) (source: mining.md, mastering-bitcoin-cash_transactions_1.md).

### The Mining Process
To achieve a hash below the target, miners modify the [block header](block-header.md) in the following ways (source: mining.md):
1. **Nonce**: The `nonce` field is modified, cycling through its $2^{32}$ possible values.
2. **Extra Nonce**: If the nonce is exhausted, the merkle root is changed by modifying the [coinbase transaction](coinbase-transaction.md) to include an "extra nonce" (source: proof-of-work.md).
3. **Timestamp**: The block timestamp is updated occasionally to keep the block current.

Once a suitable hash is found, the block is broadcast to the network.

### Types of Mining
Miners use various hardware techniques to maximize hashing power and profit (source: mining.md):
- **CPU Mining**: The initial method, using a computer's processor. Multi-threading is used to increase candidate block throughput.
- **GPU Mining**: Utilizing Graphics Processing Units, which are better suited for parallel processing, significantly increasing hashing power.
- **ASIC Mining**: Using Application-Specific Integrated Circuits—purpose-built devices designed specifically for mining as fast as physically possible. These devices require significant power and cooling solutions (source: [asic](asic.md)).

## Related pages

- [proof-of-work](proof-of-work.md)
- [block-header](block-header.md)
- [coinbase-transaction](coinbase-transaction.md)
- [asic](asic.md)
- [blockchain](blockchain.md)
- [bitcoin-cash-transactions](bitcoin-cash-transactions.md)
