# Network Discovery

**Summary**: The process by which [bitcoin-cash](bitcoin-cash.md) nodes locate and connect to each other to form a P2P network.

**Sources**: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_3.md

**Last updated**: 2026-04-17

---

Network discovery is the mechanism that allows a new node to boot up and integrate into the global P2P network without a central authority.

### Initial Connection
Nodes typically connect on TCP port 8333. To begin, a node needs at least one known peer. This peer is found via:
- **DNS Seeds**: Specialized DNS servers that return a list of IP addresses of active nodes (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_3.md).
- **Hardcoded IPs**: Manual entry of known peer IP addresses (source: mastering-bitcoin-cash-chapter-5-the-bitcoin-cash-network_3.md).

### Handshake Protocol
Once a TCP connection is established, the nodes perform a handshake to synchronize their capabilities:
1. The initiating node sends a `version` message containing its protocol version, services, timestamp, and current block height (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_3.md).
2. The remote peer responds with a `verack` message to confirm the connection (source: mastering-bitcoin-cash-chapter-5-the-bitcoin-cash-network_3.md).

### Peer Expansion
After the initial handshake, nodes expand their knowledge of the network using:
- **addr messages**: Nodes advertise their own IP addresses to neighbors (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_3.md).
- **getaddr messages**: Nodes request other known peers from their neighbors (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_3.md).

## Related pages

- [bitcoin-cash-network](bitcoin-cash-network.md)
- [mastering-bitcoin-cash-chapter-5-3](mastering-bitcoin-cash-chapter-5-3.md)
