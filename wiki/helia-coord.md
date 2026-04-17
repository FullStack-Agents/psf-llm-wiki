# helia-coord

TBD

TBD

TBD

---


**Summary**: A JavaScript npm library that provides coordination between IPFS nodes, enabling discovery, subnetworks, and secure communication. It serves as the networking backbone for the Cash Stack's IPFS layer.

**Sources**: helia-coord.md

**Last updated**: 2026-04-17

---

`helia-coord` (short for Helia Coordination) is a wrapper around [Helia](https://github.com/ipfs/helia), the JavaScript implementation of IPFS. Its primary purpose is to replace conventional REST APIs with a distributed, coordinated IPFS-based API.

## Core Features

- **Subnets**: Uses pubsub channels to create on-the-fly subnetworks.
- **Peer Discovery**: Automatic discovery of other peers within a subnetwork.
- **End-to-End Encryption (E2EE)**: Secure communication using Elliptic Curve cryptography.
- **Censorship Resistance**: Utilizes [Circuit Relays](wiki/circuit-relays.md) to tunnel through firewalls.
- **Payments**: Integrates [Bitcoin Cash](wiki/bitcoin-cash.md) (via `minimal-slp-wallet`) for peer-to-peer payments for services.

## Architecture

The library follows **Clean Architecture** with four layers:
1. **Entities**: `thisNode`, `peers`, `relays`, and `pubsub` channels.
2. **Use Cases**: Logic for identity creation, peer management, and messaging.
3. **Controllers**: Interval timers that maintain the self-healing mesh network.
4. **Adapters**: Interfaces for IPFS, BCH, Encryption, and GitHub Gists.

## Technical Implementation

### Pubsub Channels
- **Coordination Channel**: Public/unencrypted for peer announcements (every 2 minutes).
- **Private Channels**: Individual channels for E2EE messaging based on peer IDs.
- **CoinJoin Channel**: Reserved for financial privacy coordination (under development).

### Interval Timers
The "self-healing" nature of the network is maintained by:
- `manageCircuitRelays()`: Refreshing relay connections.
- `manageAnnouncement()`: Broadcasting the node's presence.
- `managePeers()`: Restoring disconnected peer connections.

## Related Pages
- [minimal-slp-wallet](wiki/minimal-slp-wallet.md)
- [circuit-relays](wiki/circuit-relays.md)
- [bitcoin-cash](wiki/bitcoin-cash.md)
- [permissionless-software-foundation](wiki/permissionless-software-foundation.md)
- [cash-stack-layers](wiki/cash-stack-layers.md)