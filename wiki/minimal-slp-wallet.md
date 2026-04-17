# minimal-slp-wallet

**Summary**: A high-level JavaScript wallet engine for building web, mobile, and Node.js applications on [bitcoin-cash](bitcoin-cash.md) ([BCH](bitcoin-cash.md)), providing a simplified API for common wallet operations.

**Sources**: minimal-slp-wallet.md

**Last updated**: 2026-04-17

---

`minimal-slp-wallet` is a JavaScript library maintained by the [Permissionless Software Foundation](permissionless-software-foundation.md) that provides a high-level API for creating wallets, sending/receiving [BCH](bitcoin-cash.md), and managing [SLP](slp-token-protocol.md) tokens and NFTs (source: minimal-slp-wallet.md).

### Role in the [Cash Stack](cash-stack-layers.md)
It operates at the **Application Library** layer of the [Cash Stack](cash-stack-layers.md). It is positioned one level above interface libraries like [bch-js](bch-js.md). While `[bch-js](bch-js.md)` is a low-level tool requiring deep Bitcoin knowledge, `minimal-slp-wallet` simplifies these operations for developers (source: minimal-slp-wallet.md).

### Key Features
- **High-Level API**: Simplifies common tasks such as sending [BCH](bitcoin-cash.md) (`wallet.send()`), checking balances, and listing tokens, reducing the need to manually build transactions (source: minimal-slp-wallet.md).
- **Token Awareness**: Built-in support for all [SLP](slp-token-protocol.md) tokens and NFTs, including tools to retrieve metadata using IPFS CIDs and supporting specifications like PS002 and PS007 (source: minimal-slp-wallet.md).
- **Dual Infrastructure Support**: Can connect to both Web 2 (via [psf-bch-api](psf-bch-api.md) REST API) and Web 3 (via `ipfs-bch-wallet-consumer` JSON RPC) back ends (source: minimal-slp-wallet.md).
- **Embedded [bch-js](bch-js.md)**: Includes an instance of [bch-js](bch-js.md), allowing developers to access low-level functions when fine-grained control is required (source: minimal-slp-wallet.md).
- **Wallet Management**: Supports [HD wallet](digital-wallets.md) creation via mnemonics, mnemonic encryption for secure storage, and wallet optimization to consolidate [[utxo](utxo.md)s](utxo.md) (source: minimal-slp-wallet.md).

### Comparison: minimal-slp-wallet vs [bch-js](bch-js.md)
| Feature | minimal-slp-wallet | [bch-js](bch-js.md) |
|---|---|---|
| **Primary Use** | Most apps and wallets | Custom, advanced transactions |
| **API Style** | High-level (Simplified) | Low-level (Manual) |
| **Web 3 Support** | Yes (via `consumer-api`) | No (REST API only) |
| **Browser Ready** | Yes (via Browserify) | No (Node.js only) |
| **Token Support** | Built-in | Manual (OP_RETURN scripts) |
(source: minimal-slp-wallet.md)

### Configuration and Connectivity
The wallet can be configured for different back-end environments:
1. **[x402](x402-bch.md) Pay-Per-Call (Web 2)**: Uses [x402-bch]([x402](x402-bch.md)-bch.md) for automatic micro-payments.
2. **Free Community Servers (Web 3)**: Connects to community-provided `ipfs-bch-wallet-consumer` instances.
3. **Free Public REST API (Web 2)**: Connects to the public `[psf-bch-api](psf-bch-api.md)` (rate-limited).
4. **Private Infrastructure (Web 2)**: Uses Bearer token authentication for private deployments (source: minimal-slp-wallet.md).

## Related pages
- [bch-js](bch-js.md)
- [psf-bch-api](psf-bch-api.md)
- [cash-stack-layers](cash-stack-layers.md)
- [slp-token-protocol](slp-token-protocol.md)
- [x402-bch]([x402](x402-bch.md)-bch.md)
- [utxo](utxo.md)
- [permissionless-software-foundation](permissionless-software-foundation.md)
