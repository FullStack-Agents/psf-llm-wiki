# mastering-bitcoin-cash-chapter-6-3

**Summary**: Details regarding the genesis block's properties and the process of block linking in [bitcoin-cash](bitcoin-cash.md) nodes.

**Sources**: mastering-bitcoin-cash_chapter-6-the-[blockchain](blockchain.md)_3.md

**Last updated**: 2026-04-17

---

The genesis block was created in 2009 and is statically encoded into all [bitcoin-cash](bitcoin-cash.md) node software (source: mastering-bitcoin-cash_chapter-6-the-[blockchain](blockchain.md)_3.md).

## The Genesis Block
- **Hash**: `000000000019d6689c085ae165831e934ff763ae46a2a6c172b3f1b60a8ce26f`
- **Coinbase Message**: "The Times 03/Jan/2009 Chancellor on brink of second bailout for banks." This serves as a timestamp and a commentary on the financial crisis (source: mastering-bitcoin-cash_chapter-6-the-[blockchain](blockchain.md)_3.md).

## Block Linking Process
Nodes maintain the [blockchain](blockchain.md) by validating the "previous block hash" field in new blocks:
1. A node checks its current tip (local chain end).
2. If a received block's `previousblockhash` matches the tip's hash, the node accepts it as a valid extension.
3. The new block is then added at the next block height (source: mastering-bitcoin-cash_chapter-6-the-[blockchain](blockchain.md)_3.md).

## Related pages
- [genesis-block](genesis-block.md)
- [data-structure](data-structure.md)
- [mastering-bitcoin-cash-chapter-6-1](mastering-bitcoin-cash-chapter-6-1.md)
- [mastering-bitcoin-cash-chapter-6-2](mastering-bitcoin-cash-chapter-6-2.md)
