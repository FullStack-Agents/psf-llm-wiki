# fulcrum-indexer

**Summary**: A blockchain indexer that functions like a search engine for the Bitcoin Cash blockchain, tracking address balances, UTXOs, and transaction histories.

**Sources**: fulcrum-indexer.md

**Last updated**: 2026-04-17

---

The **Fulcrum Indexer** is a critical component of the Cash Stack that complements the BCHN Full Node (source: fulcrum-indexer.md). While the full node tracks transactions, it does not track high-level data such as address balances or UTXOs; Fulcrum fills this gap by crawling the blockchain and indexing this metadata into a database (source: fulcrum-indexer.md).

## Technical Implementation

Fulcrum implements the [Electrum protocol](https://electrumx.readthedocs.io/en/latest/protocol.html) (source: fulcrum-indexer.md). To make this data accessible to web2 applications, the Permissionless Software Foundation (PSF) provides Docker containers that wrap the Electrum protocol into a REST API, which then interfaces with [psf-bch-api](psf-bch-api.md) (source: fulcrum-indexer.md).

## Deployment and Requirements

Fulcrum requires a fully synced [BCHN Full Node](bchn-full-node.md) to be running before it can operate (source: fulcrum-indexer.md).

### Key Operational Details:
- **Hardware Versions**: Deployment configurations vary by hardware, with specific versions for standard x86-amd64 desktops/laptops and rpi-arm64 Raspberry Pi devices (source: fulcrum-indexer.md).
- **Database Storage**: Fulcrum saves its indexed metadata in a `blockchain` directory (source: fulcrum-indexer.md).
- **Security**: Internal communication between the Fulcrum indexer and its REST API wrapper is secured using SSL certificates (source: fulcrum-indexer.md).
- **Sync Time**: Full synchronization typically takes between 2 hours and 2 days, depending on the hardware (source: fulcrum-indexer.md).

## Related pages

- [bchn-full-node](bchn-full-node.md)
- [psf-bch-api](psf-bch-api.md)
- [cash-stack-layers](cash-stack-layers.md)
- [permissionless-software-foundation](permissionless-software-foundation.md)
