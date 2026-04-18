# Proof of Work

**Summary**: A cryptographic system used by Bitcoin Cash to secure the network, determine block production, and achieve consensus via a Hashcash-like SHA-256 algorithm.

**Sources**: proof-of-work.md, mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-([BCH](bitcoin-cash.md))_4.md

**Last updated**: 2026-04-18

---

Proof-of-Work (PoW) is a cryptographic mechanism used to achieve network consensus and prevent [double-spending](double-spending.md) by requiring computational effort to validate new blocks (source: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-([BCH](bitcoin-cash.md))_4.md). 

### Mechanism
Bitcoin Cash uses a Hashcash-like algorithm. The [block header](block-header.md) is hashed; if the resulting hash is not below the current **target**, the nonce is changed and the process is repeated (source: proof-of-work.md). Because SHA-256 is computationally expensive to invert, this process serves as a "quasi-random" election for:
1. Determining which transactions are included in a block.
2. Claiming the block reward.
3. Claiming transaction fees (source: proof-of-work.md).

The probability of successfully mining a block is directly proportional to the miner's hashing power (source: proof-of-work.md).

### Target and Difficulty
The **target** is a value that the block hash must be below to be considered valid. It is deterministically calculated using the difficulties and timestamps of prior blocks to maintain an average block time of 10 minutes (source: proof-of-work.md).

**Difficulty** is often used as a more human-readable representation of the target, typically calculated as a base target (like the [genesis block](genesis-block.md) target) divided by the current target (source: proof-of-work.md).

### Chainwork
**Chainwork** represents the total cumulative work performed throughout a block's entire history. It is the expected number of hashes required to re-solve every block in the chain (source: proof-of-work.md).

### Extra Nonce
Because the 4-byte nonce and 4-byte timestamp in the block header may not provide enough variability to reach the target, miners use an "extra nonce." This is placed within the [coinbase transaction](coinbase-transaction.md) to allow for efficient re-calculation of the [merkle root](merkle-root.md) (source: proof-of-work.md).

## Related pages

- [mining](mining.md)
- [block-header](block-header.md)
- [genesis-block](genesis-block.md)
- [coinbase-transaction](coinbase-transaction.md)
- [merkle-root](merkle-root.md)
- [byzantine-generals-problem](byzantine-generals-problem.md)
- [double-spending](double-spending.md)
- [bitcoin-cash](bitcoin-cash.md)
