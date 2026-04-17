# fulcrum-indexer

**Summary**: A [blockchain](blockchain.md) indexer that functions like a search engine for the [bitcoin-cash](bitcoin-cash.md) [blockchain](blockchain.md), tracking [address](addresses.md) balances, [utxo](utxo.md)s, and transaction histories.

**Sources**: fulcrum-indexer.md

**Last updated**: 2026-04-17

---

The **Fulcrum Indexer** is a critical component of the [Cash Stack](cash-stack-layers.md) that complements the [BCHN](bchn-full-node.md) [Full Node](bchn-full-node.md) (source: fulcrum-indexer.md). While the full node tracks transactions, it does not track high-level data such as [address](addresses.md) balances or [utxo](utxo.md)s; Fulcrum fills this gap by crawling the [blockchain](blockchain.md) and indexing this metadata into a database (source: fulcrum-indexer.md).

## Technical Implementation

Fulcrum implements the [Electrum protocol](https://electrumx.readthedocs.io/en/latest/protocol.html) (source: fulcrum-indexer.md). To make this data accessible to web2 applications, the Permissionless Software Foundation (PSF) provides Docker containers that wrap the Electrum protocol into a REST API, which then interfaces with [psf-bch-api](psf-bch-api.md) (source: fulcrum-indexer.md).

## Deployment and Requirements

Fulcrum requires a fully synced [BCHN Full Node](bchn-full-node.md) to be running before it can operate (source: fulcrum-indexer.md).

### Key Operational Details:
- **Hardware Versions**: Deployment configurations vary by hardware, with specific versions for standard x86-amd64 desktops/laptops and rpi-arm64 Raspberry Pi devices (source: fulcrum-indexer.md).
- **Database Storage**: Fulcrum saves its indexed metadata in a `[blockchain](blockchain.md)` directory (source: fulcrum-indexer.md).
- **Security**: Internal communication between the Fulcrum indexer and its REST API wrapper is secured using SSL certificates (source: fulcrum-indexer.md).
- **Sync Time**: Full synchronization typically takes between 2 hours and 2 days, depending on the hardware (source: fulcrum-indexer.md).

## Related pages

- [bchn-full-node](bchn-full-node.md)
- [psf-bch-api](psf-bch-api.md)
- [cash-stack-layers](cash-stack-layers.md)
- [permissionless-software-foundation](permissionless-software-foundation.md)
