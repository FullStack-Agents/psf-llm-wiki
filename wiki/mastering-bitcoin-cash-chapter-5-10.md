# Mastering [bitcoin-cash](bitcoin-cash.md) Chapter 5 Part 10

**Summary**: Overview of the [bitcoin-cash](bitcoin-cash.md) P2P network communication flow, focusing on the message-based protocol and the exchange of blocks, headers, and transactions.

**Sources**: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_10.md

**Last updated**: 2026-04-17

---

[bitcoin-cash](bitcoin-cash.md) nodes use a simple, extensible message-based protocol to communicate. Every message consists of a header (specifying the `command` or message type) and a payload (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_10.md). This design allows nodes to ignore unrecognized messages, ensuring backward compatibility during protocol upgrades (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_10.md).

## Block and Header Synchronization

Nodes requesting [blockchain](blockchain.md) updates follow a specific request-response pattern:

### Full Nodes
1. **Request Inventories**: Nodes use `getblocks` to request a list of block inventories.
2. **Receive Hashes**: The peer responds with `inv` messages containing up to 500 block hashes (source: mastering-bitcoin-cash-chapter-5-the-bitcoin-cash-network_10.md).
3. **Request Data**: The node requests specific blocks using `getdata`.
4. **Receive Data**: The peer sends the full block data via a `block` message (source: mastering-bitcoin-cash-chapter-5-the-bitcoin-cash-network_10.md).

### SPV Nodes
1. **Request Headers**: SPV nodes use `getheaders` to request block headers.
2. **Receive Headers**: The peer responds with a `headers` message containing up to 2,000 headers (source: mastering-bitcoin-cash-chapter-5-the-bitcoin-cash-network_10.md).

## The Role of Inventory (inv) Messages

`inv` messages are used to announce the availability of data across the network:
- **Blocks**: If a node receives an `inv` for a block it doesn't have, it uses `getdata` to retrieve the block via a `block` message (source: mastering-bitcoin-cash-chapter-5-the-bitcoin-cash-network_10.md).
- **Transactions**: If an `inv` announces a transaction the node doesn't have, it uses `getdata` to retrieve the transaction via a `tx` message (source: mastering-bitcoin-cash-chapter-5-the-bitcoin-cash-network_10.md).

## Related pages

- [bitcoin-cash-network](bitcoin-cash-network.md)
- [synchronization](blockchain-synchronization.md)
- [mastering-bitcoin-cash-chapter-5-10](mastering-bitcoin-cash-chapter-5-10.md)
