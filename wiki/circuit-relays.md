# Circuit Relays

**Summary**: A mechanism in libp2p and IPFS that allows nodes behind firewalls or NATs to communicate by routing traffic through a public relay node.

**Sources**: helia-coord.md, circuit-relay.md

**Last updated**: 2026-04-17

---

Circuit Relays are critical for achieving **censorship resistance** and connectivity in distributed networks. They allow nodes that cannot accept direct incoming TCP connections (due to firewalls or NAT) to establish tunnels to other peers.

## Role in helia-coord

In the `helia-coord` library, relays are treated as a special subset of peers.

- **v2 Circuit Relay Protocol**: `helia-coord` utilizes the v2 protocol for tunneling.
- **Discovery**: The library downloads a maintained list of relay nodes from a GitHub Gist and the PSF bootstrap server.
- **Maintenance**: The `manageCircuitRelays()` timer periodically refreshes these connections to ensure the node remains connected to the rest of the network.

## Operating a Circuit Relay in the Cash Stack

In the Cash Stack, Circuit Relays are operated using the [ipfs-service-provider](ipfs-service-provider.md) software. These relays allow others to enjoy a high-uptime, censorship-resistant experience without every node needing to run a relay.

### Requirements for Operators
To successfully operate a Circuit Relay, the following network configuration is required:
- **Public IP**: The relay must have a public ipv4 or ipv6 address.
- **Configuration**: The `ENABLE_CIRCUIT_RELAY` environment variable must be set to `1`.
- **Web Access**: To provide network access to browser-based IPFS nodes, the relay must be available over secure websockets, requiring a registered domain name with an SSL certificate.

## Related pages
- [helia-coord](helia-coord.md)
- [ipfs-service-provider](ipfs-service-provider.md)
- [network-discovery](network-discovery.md)