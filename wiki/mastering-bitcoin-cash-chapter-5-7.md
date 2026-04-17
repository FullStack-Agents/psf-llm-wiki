# Mastering [[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) Chapter 5 Part 7

**Summary**: Detail on how SPV nodes use Bloom filters to interact with peers, including the specific P2P messages used and the trade-off between privacy and efficiency.

**Sources**: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_7.md

**Last updated**: 2026-04-17

---

Following the establishment of a Bloom filter, SPV nodes and their peers use a specific set of messages to exchange transaction data without compromising privacy (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_7.md).

## P2P Interaction Workflow

When an SPV node requests data via `getdata`, the peer responds using:
1. **merkleblock**: This message contains only the block headers for blocks that have matching transactions in the filter, along with the Merkle path for each match (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_7.md).
2. **tx**: The actual data of the matching transactions is sent in separate transaction messages (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_7.md).

## Filter Management
Bloom filters are managed dynamically during a node's session:
- **Adding Patterns**: Nodes can add new patterns to an existing filter using `filteradd` messages (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_7.md).
- **Clearing Filters**: Because patterns cannot be removed individually, a node must use `filterclear` to wipe the filter entirely and then send a new one to remove a pattern (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_7.md).

## Balancing Privacy and Efficiency
The accuracy of a Bloom filter is determined by its tuning parameters: the array size ($N$) and the number of hash functions ($M$).
- **High Specificity**: A more accurate filter reduces irrelevant data (false positives) but reveals more about the node's interests, decreasing privacy.
- **Low Specificity**: A less accurate filter increases the amount of irrelevant data sent by peers but provides better privacy by obscuring the exact addresses of interest (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_7.md).

## Related pages

- [bloom-filters](bloom-filters.md)
- [mastering-bitcoin-cash-chapter-5-6](mastering-bitcoin-cash-chapter-5-6.md)
- [mastering-bitcoin-cash-chapter-5-7](mastering-bitcoin-cash-chapter-5-7.md)
