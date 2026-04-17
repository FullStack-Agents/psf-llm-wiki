# Mastering [Bitcoin Cash](bitcoin-cash.md) Chapter 5 Part 3

**Summary**: Detailed explanation of the network discovery process, handshake protocol, and peer discovery mechanisms in [Bitcoin Cash](bitcoin-cash.md).

**Sources**: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_3.md

**Last updated**: 2026-04-17

---

When a new node joins the [Bitcoin Cash](bitcoin-cash.md) network, it must discover existing peers to participate. The geographic location of nodes is irrelevant to the network topology (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_3.md).

## The Handshake Process

Nodes establish connections via TCP (typically port 8333). A connection begins with a handshake using a `version` message containing:
- **PROTOCOL_VERSION**: The P2P protocol version.
- **nLocalServices**: Supported local services.
- **nTime**: Current time.
- **addrYou**: IP [address](addresses.md) of the remote node.
- **addrMe**: IP [address](addresses.md) of the local node.
- **subver**: Software version/type.
- **BestHeight**: The node's current block height (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_3.md).

The peer acknowledges the connection with a `verack` (version acknowledgment) message.

## Peer Discovery Mechanisms

Nodes locate peers using several methods:
1. **DNS Seeds**: DNS servers that provide lists of known [Bitcoin Cash](bitcoin-cash.md) node IP addresses (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_3.md).
2. **Direct IP Specification**: Manually specifying a known node's IP [address](addresses.md) (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_3.md).
3. **addr Messages**: After connecting, nodes send `addr` messages containing their IP to neighbors, who forward them.
4. **getaddr Messages**: Nodes can request the IP addresses of other peers from their connected neighbors to expand their peer list (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_3.md).

## Related pages

- [bitcoin-cash-network](bitcoin-cash-network.md)
- [mastering-bitcoin-cash-chapter-5-2](mastering-bitcoin-cash-chapter-5-2.md)
