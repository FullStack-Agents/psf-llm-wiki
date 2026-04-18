# Bloom Filters

**Summary**: A probabilistic data structure used by SPV nodes to retrieve transactions while maintaining the privacy of the node's wallet addresses.

**Sources**: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_6.md, bloom-filter.md

**Last updated**: 2026-04-18

---

Bloom filters are critical for preserving the privacy of lightweight clients (SPV nodes) when they interact with the P2P network.

### The Privacy Problem
Without Bloom filters, an SPV node would have to tell its peers exactly which addresses it is interested in to receive relevant transactions. This would effectively broadcast the node's identity and financial interests to anyone monitoring the network (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_6.md).

### Mechanism
A Bloom filter allows a node to send a "compressed" representation of its interests.

#### Technical Implementation
A Bloom filter is essentially a large bit-string. Data is added by hashing it with a series of hash operations, using the outputs as indices to set bits in the array (source: bloom-filter.md).
- **Hash Function**: Bitcoin uses the 32-bit Murmur Hash version 3.
- **Seed Calculation**: The seed for each hash operation is calculated as `hash_number * 0xFBA4C795 + tweak`, where the tweak (nonce) is chosen randomly by the filter creator (source: bloom-filter.md).
- **Scaling**: The size of the filter ($S$) and number of hash operations are calculated based on a target false-positive probability ($P$) and the expected number of items to store ($N$).

#### Probabilistic Nature
- **False Positives**: A peer might send a transaction that the node doesn't actually care about because the bits happened to overlap. This can lead to a "positive feedback loop" where unwanted data is automatically inserted, increasing future false positives (source: bloom-filter.md).
- **No False Negatives**: If a transaction matches the node's interest, the filter will always identify it (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_6.md).

### P2P Workflow
The SPV node utilizes the `filterload` message to share its Bloom filter with peers. The peers then filter the transaction stream and only push matching transactions to the SPV node (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_6.md).

#### Filter Contents
At a minimum, an [simplified-payment-verification](simplified-payment-verification.md) client must insert:
- **Addresses**: To report transactions paying *into* the wallet.
- **Outpoints**: To report transactions paying *out of* the wallet (source: bloom-filter.md).

#### Dynamic Updates and Maintenance
- **Automatic Insertions**: Based on a flag byte, peers can be directed to automatically insert new outpoints into the filter when a matching address is found. This is critical for cases where a receive and spend occur in the same transaction (source: bloom-filter.md).
- **Refresh**: Because of false-positive accumulation, clients must periodically refresh the filter using `filterload` to clear unnecessary entries (source: bloom-filter.md).

## Outpoints
Outpoints are serialized identifiers for transaction outputs, used in Bloom filters to match future transactions that spend those outputs. They consist of:
- **Transaction Hash**: 32 bytes (Little Endian).
- **Output Index**: 4 bytes, unsigned integer (Little Endian) (source: bloom-filter.md).

## Related pages

- [simplified-payment-verification](simplified-payment-verification.md)
- [p2p-network-messages](p2p-network-messages.md)
- [bitcoin-cash-network](bitcoin-cash-network.md)
- [mastering-bitcoin-cash-chapter-5-5](mastering-bitcoin-cash-chapter-5-5.md)
- [mastering-bitcoin-cash-chapter-5-6](mastering-bitcoin-cash-chapter-5-6.md)

