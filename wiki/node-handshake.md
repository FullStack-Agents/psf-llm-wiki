# Node Handshake

**Summary**: The process by which two Bitcoin Cash nodes establish a connection and verify compatibility before exchanging blockchain data.

**Sources**: node-handshake.md

**Last updated**: 2026-04-18

---

When two nodes connect, they perform a connection handshake to ensure compatibility. This handshake informs each peer of the other's network protocol version, current block height, and supported network services (source: node-handshake.md).

## Handshake Process

The handshake relies on the exchange of specific P2P messages. Neither node should send any data other than a `version` message until it has received one from its peer (source: node-handshake.md).

### The Handshake Sequence
1. **Version Exchange**: Both nodes send a `version` message containing their protocol version and capabilities.
2. **Compatibility Check**: Nodes verify if the versions are compatible. If so, they typically adopt the lower of the two version numbers.
3. **Acknowledgment**: Once a `version` message is sent and received, the node may send a `verack` (version acknowledgment) message.
4. **Operational Readiness**: Normal node operation begins only after both nodes have sent and received `verack` messages (source: node-handshake.md).

*Note: A node may only send a `version` message once. While a node may send `verack` before its own `version` message, the exchange of both is required for full operation (source: node-handshake.md).*

## Self-Connection Prevention
Although nodes can technically connect to themselves, it is generally avoided. Nodes typically prevent this by checking the `nonce` provided in the `version` message against a list of nonces they have recently used (source: node-handshake.md).

## Related pages
- [p2p-network-messages](p2p-network-messages.md)
- [network-discovery](network-discovery.md)
- [bitcoin-cash-network](bitcoin-cash-network.md)
