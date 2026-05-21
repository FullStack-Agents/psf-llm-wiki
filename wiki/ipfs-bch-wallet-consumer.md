# ipfs-bch-wallet-consumer

**Summary**: A Web 3 back-end infrastructure component that provides a JSON RPC interface for [bitcoin-cash](bitcoin-cash.md) wallet operations, often delivered via IPFS.

**Sources**: ipfs-bch-wallet-consumer.md, minimal-slp-wallet.md

**Last updated**: 2026-05-21

---

`ipfs-bch-wallet-consumer` is a back-end infrastructure component that enables Web 3 connectivity for [bitcoin-cash](bitcoin-cash.md) applications (source: [minimal-slp-wallet](minimal-slp-wallet.md).

### Role in the [Cash Stack](cash-stack-layers.md)
In the [Cash Stack](cash-stack-layers.md), `ipfs-bch-wallet-consumer` resides at the REST API / JSON RPC layer. It is a REST API server based on [Koa](https://koajs.com/), serving as a localized mirror of `[ipfs-bch-wallet-service](ipfs-bch-wallet-service.md)`. Where the service is coupled to `[psf-bch-api](psf-bch-api.md)`, the consumer provides a localized REST API for consuming blockchain services (source: ipfs-bch-wallet-consumer.md).

It starts an IPFS node, connects to an `ipfs-bch-wallet-service` server over IPFS, and pipes that connection over its own localized REST API. This REST API is primarily consumed by the [bch-consumer](bch-consumer.md) JavaScript library, which is embedded in [minimal-slp-wallet](minimal-slp-wallet.md) (source: ipfs-bch-wallet-consumer.md).

### Deployment and Access
It is often provided by community volunteers as "Free Community Servers." These servers are generally faster than the free Web 2 REST API servers but may have different uptime guarantees (source: minimal-slp-wallet.md).

### Interface
The component is accessed via the [bch-consumer](bch-consumer.md) interface library when using the `consumer-api` configuration in [minimal-slp-wallet](minimal-slp-wallet.md) (source: minimal-slp-wallet.md).

## Related pages
- [bch-consumer](bch-consumer.md)
- [minimal-slp-wallet](minimal-slp-wallet.md)
- [psf-bch-api](psf-bch-api.md)
- [cash-stack-layers](cash-stack-layers.md)
