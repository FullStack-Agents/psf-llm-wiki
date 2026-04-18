# Simplified Payment Verification (SPV)

**Summary**: A lightweight method for verifying transactions without needing the full [blockchain](blockchain.md)'s transaction data, reducing resource requirements for mobile wallets and low-performance environments.

**Sources**: mastering-bitcoin-cash_chapter-6-the-[blockchain](blockchain.md)_6.md, spv.md

**Last updated**: 2026-04-18

---

Simplified Payment Verification (SPV) is a protocol that allows "lightweight" clients to verify that a transaction is included in a block without needing to download the entire [blockchain](blockchain.md). This significantly reduces the storage space, computational power, and network traffic required for operation (source: spv.md).

## Theory
The validity of transactions can be demonstrated through the fact that they have been accepted by the Bitcoin Cash network and admitted into the blockchain. SPV clients keep their own copy of the [block-header](block-header.md) chain and query other network nodes for proof that the blocks containing specific transactions are valid. As the number of confirmations increases, the confidence in the transaction's validity grows due to the increased difficulty of forging additional blocks (source: spv.md).

## How it Works
SPV nodes store only the block headers. To verify a transaction, they rely on the [merkle-tree](merkle-tree.md) structure of blocks:
1. They receive a merkle-path from a full node.
2. They use this path to verify the transaction's hash against the [merkle-root](merkle-root.md) stored in the block header.
3. They verify the block header's validity based on the chain of headers.

This process reduces the data required for verification from megabytes (full block) to less than a kilobyte (header + path) (source: mastering-bitcoin-cash_chapter-6-the-blockchain_6.md).

## Network Implementation (BIP-37)
SPV implementation is based on BIP-37. Clients use specific P2P messages to interact with full nodes:
- **Bloom Filters**: Clients use `filterload` and `filteradd` messages to request that peers install a [bloom-filter](bloom-filters.md) on the connection. This allows peers to send only the transactions and blocks that match the client's interests.
- **Inventory/Transactions**: Peers send `inv` messages for matching data, and transactions are transmitted via `tx` messages.
- **Merkle Blocks**: When blocks are requested, they are sent as `merkleblock` messages, which provide the partial merkle trees serving as proof of inclusion.
- **Cleanup**: The `filterclear` message can be used to revert the connection to its typical state (source: spv.md).

## Trade-offs

### Advantages
- **Resource Efficiency**: Ideal for mobile wallets or metered networks due to low storage and bandwidth requirements (source: spv.md).
- **Verification Core**: Still allows verification of the block header chain.

### Disadvantages
- **Confirmation Time**: Typically requires more confirmations to build confidence.
- **Security Risks**: Cannot detect fabricated transactions if an attacker overpowers the network.
- **Privacy/Stability**: Known flaws can weaken client privacy and potentially allow denial-of-service attack vectors on full nodes that support SPV (source: spv.md).

## Related pages
- [merkle-tree](merkle-tree.md)
- [bloom-filters](bloom-filters.md)
- [p2p-network-messages](p2p-network-messages.md)
- [block-header](block-header.md)
- [mastering-bitcoin-cash-chapter-6-6](mastering-bitcoin-cash-chapter-6-6.md)

