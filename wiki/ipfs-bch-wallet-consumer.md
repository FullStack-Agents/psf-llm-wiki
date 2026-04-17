# ipfs-bch-wallet-consumer

**Summary**: A Web 3 back-end infrastructure component that provides a JSON RPC interface for [bitcoin-cash](bitcoin-cash.md) wallet operations, often delivered via IPFS.

**Sources**: [minimal-slp-wallet](minimal-slp-wallet.md).md

**Last updated**: 2026-04-17

---

`ipfs-bch-wallet-consumer` is a back-end infrastructure component that enables Web 3 connectivity for [bitcoin-cash](bitcoin-cash.md) applications (source: [minimal-slp-wallet](minimal-slp-wallet.md).md).

### Role in the [Cash Stack](cash-stack-layers.md)
In the [Cash Stack](cash-stack-layers.md), `ipfs-bch-wallet-consumer` resides at the REST API / JSON RPC layer. It serves as an alternative to `[psf-bch-api](psf-bch-api.md)`, allowing the [minimal-slp-wallet](minimal-slp-wallet.md) application library to interact with the [blockchain](blockchain.md) via a JSON RPC interface rather than a REST API (source: [minimal-slp-wallet](minimal-slp-wallet.md).md).

### Deployment and Access
It is often provided by community volunteers as "Free Community Servers." These servers are generally faster than the free Web 2 REST API servers but may have different uptime guarantees (source: [minimal-slp-wallet](minimal-slp-wallet.md).md).

### Interface
The component is accessed via the [bch-consumer](bch-consumer.md) interface library when using the `consumer-api` configuration in `[minimal-slp-wallet](minimal-slp-wallet.md)` (source: [minimal-slp-wallet](minimal-slp-wallet.md).md).

## Related pages
- [bch-consumer](bch-consumer.md)
- [minimal-slp-wallet](minimal-slp-wallet.md)
- [psf-bch-api](psf-bch-api.md)
- [cash-stack-layers](cash-stack-layers.md)
