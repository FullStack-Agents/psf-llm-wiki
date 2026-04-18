# slp-token-indexer

**Summary**: A [blockchain](blockchain.md) indexer that tracks [SLP](slp-token-protocol.md) token transactions according to Type 1 and NFT1 specifications, providing the necessary data for token-related operations in the [Cash Stack](cash-stack-layers.md).

**Sources**: slp-indexer-software.md

**Last updated**: 2026-04-17

---

The **[SLP](slp-token-protocol.md) Token Indexer** crawls the [blockchain](blockchain.md) to index [SLP](slp-token-protocol.md) token transactions, similar to how the [fulcrum-indexer](fulcrum-indexer.md) indexes [BCH](bitcoin-cash.md) addresses and balances (source: slp-indexer-software.md). It specifically tracks tokens following the Type 1 and NFT1 specifications (source: slp-indexer-software.md).

Together with the [bchn-full-node](bchn-full-node.md) and the [fulcrum-indexer](fulcrum-indexer.md), it forms the core back-end infrastructure of the [Cash Stack](cash-stack-layers.md) (source: slp-indexer-software.md).

## Architecture

To prevent real-time transaction processing from being stalled by large blocks (due to JavaScript's single-threaded nature), the indexer is split into three separate Docker containers that communicate via a REST API (source: slp-indexer-software.md):

1. **psf-slp-db**: A [LevelDB](https://github.com/google/leveldb) database wrapped in a REST API. It manages the actual storage of all indexed data (source: slp-indexer-software.md).
2. **Block Indexer**: Handles the Initial Block Download (IBD) starting from the [SLP](slp-token-protocol.md) Genesis (block ~543,000). Once IBD is complete, it monitors the full node's ZMQ interface for new blocks and creates periodic database backups (source: slp-indexer-software.md).
3. **TX Indexer**: Monitors the full node's ZMQ interface for new unconfirmed transactions and indexes them in real time after the Block Indexer has completed IBD (source: slp-indexer-software.md).

## Deployment and Operation

### Requirements and Syncing
The [SLP](slp-token-protocol.md) indexer requires a fully synced [bchn-full-node](bchn-full-node.md) to operate (source: slp-indexer-software.md). A full sync from SLP Genesis can take **two to three weeks** (source: slp-indexer-software.md). 

To accelerate this, users can download a pre-synced database snapshot from `fullstack.cash/cashstrap` and restore it into the `current/` directory of the LevelDB storage (source: slp-indexer-software.md).

### Critical Configuration
Once fully synced and running at the chain tip, it is recommended to set `EXIT_ON_MISSING_BACKUP=true` in both the block-indexer and slp-db `.env` files. This prevents the system from accidentally rolling back to Genesis if a backup is missing during a restart (source: slp-indexer-software.md).

## Related pages

- [bchn-full-node](bchn-full-node.md)
- [fulcrum-indexer](fulcrum-indexer.md)
- [psf-bch-api](psf-bch-api.md)
- [cash-stack-layers](cash-stack-layers.md)
- [permissionless-software-foundation](permissionless-software-foundation.md)
