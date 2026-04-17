# Bloom Filters

**Summary**: A probabilistic data structure used by SPV nodes to retrieve transactions while maintaining the privacy of the node's wallet addresses.

**Sources**: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_6.md

**Last updated**: 2026-04-17

---

Bloom filters are critical for preserving the privacy of lightweight clients (SPV nodes) when they interact with the P2P network.

### The Privacy Problem
Without Bloom filters, an SPV node would have to tell its peers exactly which addresses it is interested in to receive relevant transactions. This would effectively broadcast the node's identity and financial interests to anyone monitoring the network (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_6.md).

### Mechanism
A Bloom filter allows a node to send a "compressed" representation of its interests. 
- **Structure**: A bit array and a set of hash functions (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_6.md).
- **Operation**: a pattern is hashed multiple times, and the resulting indices in the bit array are set to 1.
- **Probabilistic Nature**: 
    - **False Positives**: A peer might send a transaction that the node doesn't actually care about because the bits happened to overlap.
    - **No False Negatives**: If a transaction matches the node's interest, the filter will always identify it (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_6.md).

### P2P Workflow
The SPV node utilizes the `filterload` message to share its Bloom filter with peers. The peers then filter the transaction stream and only push matching transactions to the SPV node (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_6.md). 

When responding to `getdata` requests, peers send a `merkleblock` message (containing matching block headers and Merkle paths) followed by `tx` messages with the matching transactions (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_7.md).

## Related pages

- [mastering-bitcoin-cash-chapter-5-5](mastering-bitcoin-cash-chapter-5-5.md)
- [bitcoin-cash-network](bitcoin-cash-network.md)
- [mastering-bitcoin-cash-chapter-5-6](mastering-bitcoin-cash-chapter-5-6.md)
