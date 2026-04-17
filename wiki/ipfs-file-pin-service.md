# ipfs-file-pin-service

**Summary**: An optional Cash Stack component that provides paid IPFS file pinning, implementing the PSF File Pinning Protocol (PS010) to create censorship-resistant, redundant file storage.

**Sources**: ipfs-file-pin-service.md

**Last updated**: 2026-04-17

---

`ipfs-file-pin-service` is a specialized server that bridges the [bitcoin-cash](bitcoin-cash.md) blockchain with the Inter-Planetary File System (IPFS). It runs an embedded Helia IPFS node and a REST API to automate the pinning of files based on blockchain-validated payments.

## Role in the Cash Stack

The service sits at the top of the Cash Stack and integrates several lower-layer components:

- **[slp-token-indexer](slp-token-indexer.md)**: Detects "Pin Claim" transactions on the blockchain and notifies `ipfs-file-pin-service` via a webhook.
- **[psf-bch-api](psf-bch-api.md)**: Used to verify proof-of-burn transactions and validate that the correct amount of PSF tokens was destroyed.
- **Helia IPFS Node**: Handles the actual storage and retrieval of content using CIDs.

## Core Workflow

When a Pin Claim is detected:
1. **Validation**: The service verifies the Proof-of-Burn (PoB) of PSF tokens.
2. **Verification**: It ensures the burn amount meets the required cost based on the file size (as determined by the [PSF Minting Council](https://PSFoundation.cash)).
3. **Pinning**: It downloads the content from IPFS and pins it to the local node.
4. **Availability**: The pinned content is then served via HTTP endpoints for direct download and viewing.

By having multiple independent nodes running this service worldwide, the network achieves **redundant hosting**, eliminating central points of failure.

## Key Features

### Hybrid API Interface
- **REST API**: Exposed over HTTP (default port `5031`) for standard web integration and webhook processing.
- **JSON-RPC API**: Exposed over IPFS using `helia-coord`, allowing for decentralized access without direct HTTP connections.

### Infrastructure Reliability
- **Automatic Retry Queue**: Failed downloads are retried with a concurrent queue to ensure reliability.
- **Dynamic Pricing**: The service fetches the current write price from the blockchain at startup to stay in sync with token valuation.
- **Maintenance Timers**: Automated controllers handle pin processing (every 10m), usage cleanup (every 1h), and restarts (every 6h).

## Technical Architecture

The project follows **Clean Architecture** principles to separate concerns:
- **Adapters**: Interfaces for external services (IPFS/Helia, MongoDB, Wallet).
- **Controllers**: Input handlers for REST API, JSON-RPC, and timer-based tasks.
- **Entities**: Business logic and validation.
- **Use-Cases**: Application-specific business rules.

## Related pages
- [decentralized-file-hosting](decentralized-file-hosting.md)
- [decentralized-file-storage](decentralized-file-storage.md)
- [slp-token-indexer](slp-token-indexer.md)
- [psf-bch-api](psf-bch-api.md)
- [bitcoin-cash](bitcoin-cash.md)
