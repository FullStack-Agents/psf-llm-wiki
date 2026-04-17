# Bitcoin Cash Network

**Summary**: The communication infrastructure of Bitcoin Cash, comprising the P2P network and extended protocols.

**Sources**: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_1.md

**Last updated**: 2026-04-17

---

The [Bitcoin Cash Network](mastering-bitcoin-cash-chapter-5-1.md) is a decentralized P2P system. 

### Architecture
The network uses a flat topology where all participants are equal peers, removing the need for central servers (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_1.md).

## Node Types
The network consists of various node roles:
- **Full Nodes**: Maintain the complete blockchain for authoritative verification (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_2.md).
- **Lightweight (SPV) Nodes**: Use Simplified Payment Verification (SPV) and only store a subset of the blockchain (block headers). This is ideal for resource-constrained devices like smartphones, as it reduces the required storage by approximately 1,000x (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_2.md, mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_5.md).
- **Mining Nodes**: Specialized nodes that solve PoW to create blocks; can be full or lightweight pool participants (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_2.md).
- **Edge Routers**: Full nodes used by enterprises (exchanges, merchants) to facilitate service integration without mining or wallets (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_2.md).

### Extended Network
The "extended Bitcoin Cash network" includes:
- The primary P2P protocol.
- **Stratum**: A protocol supporting mining and lightweight mobile wallets.
- **Gateway Routing Servers**: Components that bridge the P2P network with extended protocols like Stratum (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_1.md).

## Related pages

- [decentralization](decentralization.md)
- [mastering-bitcoin-cash-chapter-5-1](mastering-bitcoin-cash-chapter-5-1.md)
