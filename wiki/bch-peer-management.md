# [BCH](bitcoin-cash.md) Peer Management

**Summary**: How [bitcoin-cash](bitcoin-cash.md) nodes discover, maintain, and bootstrap connections to other peers.

**Sources**: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_11.md

**Last updated**: 2026-04-17

---

Nodes in the [bitcoin-cash](bitcoin-cash.md) network manage their connections to ensure diverse paths into the network and reliable connectivity.

### Peer Discovery and Bootstrapping
- **Bootstrapping**: For initial entry or after a failure of known peers, nodes use seed nodes to bootstrap their connection list (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_11.md).
- **Persistence**: Nodes maintain a memory of their most recent successful peer connections, which allows for rapid re-establishment of the network after a reboot.

### Connection Diversity
Nodes typically maintain connections to multiple peers simultaneously to avoid single points of failure and ensure a diverse set of network paths.

## Related pages

- [bch-network-resilience](bch-network-resilience.md)
- [network-discovery](network-discovery.md)
- [mastering-bitcoin-cash-chapter-5-network-resilience](mastering-bitcoin-cash-chapter-5-network-resilience.md)
