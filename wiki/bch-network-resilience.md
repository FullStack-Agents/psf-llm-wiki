# BCH Network Resilience

**Summary**: Analysis of the mechanisms that ensure the stability and availability of the Bitcoin Cash P2P network.

**Sources**: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_11.md

**Last updated**: 2026-04-17

---

Resilience in the Bitcoin Cash network is achieved through dynamic adaptation to the availability of peers.

### Connection Maintenance
Nodes periodically send messages to maintain activity on existing connections. If a connection shows no activity for more than 90 minutes, the node presumes it is disconnected and seeks a new peer (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_11.md).

This approach allows the network to grow and shrink organically, adapting to network problems and transient nodes without requiring a central coordinator.

## Related pages

- [bch-peer-management](bch-peer-management.md)
- [bitcoin-cash-network](bitcoin-cash-network.md)
- [mastering-bitcoin-cash-chapter-5-network-resilience](mastering-bitcoin-cash-chapter-5-network-resilience.md)
