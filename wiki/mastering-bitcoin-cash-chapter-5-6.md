# Mastering [Bitcoin Cash](bitcoin-cash.md) Chapter 5 Part 6

**Summary**: Explanation of Bloom Filters in the context of SPV nodes, detailing how they provide privacy when requesting transactions from peers.

**Sources**: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_6.md

**Last updated**: 2026-04-17

---

SPV nodes face a privacy challenge: requesting specific transactions from peers can reveal the addresses in the node's wallet to third parties (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_6.md). To mitigate this, [Bitcoin Cash](bitcoin-cash.md) uses **Bloom Filters**.

## What is a Bloom Filter?

A Bloom filter is a probabilistic data structure used to test whether an element is a member of a set. It allows an SPV node to request transactions matching certain patterns without revealing the exact addresses of interest (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_6.md).

### How it Works
A Bloom filter consists of a bit array of size $N$ and multiple hash functions.

**Adding a Pattern:**
1. The pattern (e.g., a wallet [address](addresses.md)) is processed by each hash function.
2. Each hash function produces an index between 1 and $N$.
3. The corresponding bits in the array are set to 1 (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_6.md).

**Testing a Pattern:**
- If **all** bits indexed by the hash functions are 1 $\rightarrow$ The pattern is **probably** in the filter ("Maybe, Yes").
- If **any** bit is 0 $\rightarrow$ The pattern is **definitely not** in the filter ("Definitely Not").

Because bits can overlap as more patterns are added, the filter is probabilistic and can produce false positives, but never false negatives (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_6.md).

## Implementation in SPV

1. The SPV node creates a Bloom filter and adds patterns matching its wallet addresses.
2. The node sends the filter to peers using a `filterload` message (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_6.md).
3. Peers test every transaction against the filter and only transmit those that result in a "Maybe, Yes" (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_6.md).

## Related pages

- [mastering-bitcoin-cash-chapter-5-5](mastering-bitcoin-cash-chapter-5-5.md)
- [bitcoin-cash-network](bitcoin-cash-network.md)
- [mastering-bitcoin-cash-chapter-5-6](mastering-bitcoin-cash-chapter-5-6.md)
