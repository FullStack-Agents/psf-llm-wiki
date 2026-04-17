# [BCH](bitcoin-cash.md) Node Configuration

**Summary**: Configuration options for controlling the behavior of a [[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) node.

**Sources**: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_11.md

**Last updated**: 2026-04-17

---

While [[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) nodes typically manage peer connections automatically, users can override this behavior for specialized configurations.

### Manual Peer Connection
The `-connect=<IPAddress>` option can be used to force a node to connect only to specific IP addresses. This disables the automatic peer discovery and maintenance mechanisms in favor of a fixed set of peers (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_11.md).

## Related pages

- [bch-peer-management](bch-peer-management.md)
- [mastering-bitcoin-cash-chapter-5-network-resilience](mastering-bitcoin-cash-chapter-5-network-resilience.md)
