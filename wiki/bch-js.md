# bch-js

**Summary**: A JavaScript npm library for building web and mobile applications that interact with the [bitcoin-cash](bitcoin-cash.md) ([BCH](bitcoin-cash.md)) [blockchain](blockchain.md). It serves as the Interface Library layer in the [Cash Stack](cash-stack-layers.md).

**Sources**: bch-js.md, [psf-bch-api](psf-bch-api.md)

**Last updated**: 2026-04-17

---

`bch-js` is a JavaScript library maintained by the [Permissionless Software Foundation](permissionless-software-foundation.md) that provides a developer-friendly API for communicating with the [psf-bch-api](psf-bch-api.md) REST API server (source: bch-js.md).

### Role in the [Cash Stack](cash-stack-layers.md)
It sits at the **Interface Library** layer of the [Cash Stack](cash-stack-layers.md), bridging the gap between application code (e.g., wallets, bots) and the back-end REST API. For most web applications, `[minimal-slp-wallet](minimal-slp-wallet.md)` is used instead, as it embeds `bch-js` and provides a higher-level interface (source: bch-js.md).

### Key Features
- **Wallet Management**: Supports creating HD wallets using [BIP39](digital-wallets.md) and [BIP44](digital-wallets.md) standards (source: bch-js.md).
- **[blockchain](blockchain.md) Interaction**: Tools for checking balances, listing [[utxo](utxo.md)s](utxo.md), and building/broadcasting [BCH](bitcoin-cash.md) transactions (source: bch-js.md).
- **[SLP](slp-token-protocol.md) & [NFT](slp-token-protocol.md) Support**: Full support for the [Simple Ledger Protocol](slp-token-protocol.md) ([SLP](slp-token-protocol.md)), including creating and managing fungible tokens and NFTs according to the NFT1 specification (source: bch-js.md).
- **Cryptographic Utilities**: Capabilities for message signing and verification, as well as [address](addresses.md) conversion between Cash Address, legacy, and [SLP](slp-token-protocol.md) formats (source: bch-js.md).
- **Integration Testing**: Used for end-to-end testing of `[psf-bch-api](psf-bch-api.md)` installations to verify connectivity to [BCHN](bchn-full-node.md) Full Nodes, [Fulcrum](fulcrum-indexer.md) Indexers, and [SLP](slp-token-protocol.md) Token Indexers (source: [psf-bch-api](psf-bch-api.md).

### Configuration and Authentication
`bch-js` can be configured via constructor options or environment variables. It supports three primary connection modes (source: bch-js.md):
1. **[x402](x402-bch.md) Pay-Per-Call**: Uses [x402-bch](x402-bch.md) to handle micro-payments per API call automatically using a WIF [private key](private-keys.md).
2. **Free Public Server**: Rate-limited access via a public server.
3. **Private Infrastructure**: Uses Bearer token authentication for private `[psf-bch-api](psf-bch-api.md)` deployments.

## Related pages
- [psf-bch-api](psf-bch-api.md)
- [cash-stack-layers](cash-stack-layers.md)
- [x402-bch](x402-bch.md)
- [slp-token-protocol](slp-token-protocol.md)
- [permissionless-software-foundation](permissionless-software-foundation.md)
- [utxo](utxo.md)
