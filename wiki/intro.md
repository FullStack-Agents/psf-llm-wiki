# Introduction to the [Cash Stack](cash-stack-layers.md)

**Summary**: Overview of the [Cash Stack](cash-stack-layers.md) framework for building [blockchain](blockchain.md)-based applications, focusing on [[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) ([BCH](bitcoin-cash.md)) and the goals of the Permissionless Software Foundation (PSF).

**Sources**: intro.md

**Last updated**: 2026-04-17

---

The [Cash Stack](cash-stack-layers.md) is a framework designed for building [blockchain](blockchain.md)-based web and phone applications. It enables "web2" applications to utilize "web3" primitives such as money transfer via [[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) ([BCH](bitcoin-cash.md)), tokenization (NFTs/fungible tokens), file hosting via IPFS, encrypted messaging, and social media via Nostr (source: intro.md).

The framework emphasizes:
- **Censorship Resistance**: Avoiding state or corporate tampering (source: intro.md).
- **Self Sufficiency**: Reducing third-party dependencies (source: intro.md).
- **Technology Stack**: Uses JavaScript exclusively, Docker Compose for orchestration, and targeting Ubuntu Linux (source: intro.md).

The [Cash Stack](cash-stack-layers.md) is maintained by the [permissionless-software-foundation](permissionless-software-foundation.md) (source: intro.md). It is designed to be efficient, where a single standard desktop ($400 USD, 32GB RAM, 1TB SSD) can serve 1,000 to 10,000 users (source: intro.md).

## The [Cash Stack](cash-stack-layers.md) Model

Inspired by the OSI model, the [Cash Stack](cash-stack-layers.md) is divided into layers to isolate networking and technical issues (source: intro.md):

1. **Application**: End-user software (UI) and application libraries containing business logic.
2. **Interface Library**: Libraries like `[bch-js](bch-js.md)` or `bch-consumer` used by application libraries.
3. **API**: REST API or JSON RPC servers providing a single interface to backend services.
4. **Indexers**: Search engines for [blockchain](blockchain.md) data (e.g., [Fulcrum](fulcrum-indexer.md) for balances/[utxo](utxo.md)s, `psf-slp-indexer` for [SLP](slp-token-protocol.md) tokens).
5. **Full Nodes**: Basic [blockchain](blockchain.md) software for broadcasting and verifying blocks.

The [psf-bch-api]([psf-bch-api](psf-bch-api.md).md) serves as the central REST API server connecting the [blockchain](blockchain.md) infrastructure (Full node, [Fulcrum](fulcrum-indexer.md), [SLP](slp-token-protocol.md) Token Indexer) to the web interface (source: intro.md).

## Related pages

- [permissionless-software-foundation](permissionless-software-foundation.md)
- [psf-bch-api]([psf-bch-api](psf-bch-api.md).md)
- [cash-stack-layers](cash-stack-layers.md)
- [bitcoin-cash](bitcoin-cash.md)
