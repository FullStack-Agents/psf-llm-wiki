# bchn-full-node

**Summary**: The base layer of the Cash Stack, providing the essential blockchain node software that validates transactions and blocks on the Bitcoin Cash (BCH) network.

**Sources**: bchn-full-node.md

**Last updated**: 2026-04-17

---

The **BCHN Full Node** (Bitcoin Cash Node) is the bottom-most layer of the Cash Stack (source: bchn-full-node.md). While various full node implementations exist, the Cash Stack prioritizes BCHN because it is the software most commonly used by miners (source: bchn-full-node.md).

## Role in the Cash Stack

The full node serves as the source of truth for the blockchain. Other layers of the Cash Stack, such as indexers and the [psf-bch-api](psf-bch-api.md), depend on the full node to perform actual transactions and provide direct access to the blockchain data (source: bchn-full-node.md).

## Deployment and Operation

BCH full nodes are designed to be accessible and can run on standard desktop computers or small devices like a Raspberry Pi (source: bchn-full-node.md). The Permissionless Software Foundation (PSF) provides a Docker container for simplified deployment (source: bchn-full-node.md).

### Key Operational Details:
- **Data Storage**: The blockchain database is stored in a dedicated directory (`blockchain-data/`), which is portable and can be moved between machines to avoid re-syncing (source: bchn-full-node.md).
- **Synchronization**: Initial synchronization involves downloading headers first, followed by blocks. This process can take between 1 to 14 days depending on hardware and network speed (source: bchn-full-node.md).
- **Annual Upgrades**: Bitcoin Cash undergoes a network hard fork every year. Nodes must be updated to the latest version before May 1st annually to avoid being disconnected from the network (source: bchn-full-node.md).

## Interaction Methods

The BCHN Full Node can be interacted with via two primary methods:
1. **Command Line**: Using `bitcoin-cli` inside the container for manual administrative tasks (source: bchn-full-node.md).
2. **JSON-RPC**: A programmatic interface (typically on port 8332) used by other Cash Stack components to communicate with the node (source: bchn-full-node.md).

## Related pages

- [cash-stack-layers](cash-stack-layers.md)
- [psf-bch-api](psf-bch-api.md)
- [permissionless-software-foundation](permissionless-software-foundation.md)
- [bitcoin-cash](bitcoin-cash.md)
