# bch-consumer

**Summary**: A JavaScript library that provides a JSON RPC interface for interacting with the `ipfs-bch-wallet-consumer` back end.

**Sources**: [minimal-slp-wallet](minimal-slp-wallet.md)

**Last updated**: 2026-04-17

---

`bch-consumer` is a JavaScript library used as an interface for Web 3 infrastructure in the [Cash Stack](cash-stack-layers.md) (source: [minimal-slp-wallet](minimal-slp-wallet.md).

### Role in the [Cash Stack](cash-stack-layers.md)
Within the [Cash Stack](cash-stack-layers.md), `bch-consumer` sits at the **Interface Library** layer. It is specifically used when `[minimal-slp-wallet](minimal-slp-wallet.md)` is configured with the `consumer-api` interface to communicate with `ipfs-bch-wallet-consumer` via JSON RPC (source: [minimal-slp-wallet](minimal-slp-wallet.md).

### Comparison with [bch-js](bch-js.md)
While [bch-js](bch-js.md) is used for REST API interactions (Web 2), `bch-consumer` is the corresponding interface for the Web 3 (IPFS-based) back end (source: [minimal-slp-wallet](minimal-slp-wallet.md).

## Related pages
- [minimal-slp-wallet](minimal-slp-wallet.md)
- [ipfs-bch-wallet-consumer](ipfs-bch-wallet-consumer.md)
- [cash-stack-layers](cash-stack-layers.md)
- [bch-js](bch-js.md)
