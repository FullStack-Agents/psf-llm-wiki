# Network Communication Protocol

**Summary**: The message-based communication system used by [bitcoin-cash](bitcoin-cash.md) nodes to propagate blocks, transactions, and headers.

**Sources**: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_10.md

**Last updated**: 2026-04-17

---

The [bitcoin-cash](bitcoin-cash.md) network operates on a request-response communication protocol that prioritizes efficiency and backward compatibility.

### Message Structure
Messages are structured with a header containing a `command` name (identifying the message type) and a payload. This extensibility allows nodes to ignore messages they do not recognize, facilitating seamless protocol upgrades (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_10.md).

### Data Propagation Workflow
Nodes use **Inventory (`inv`) messages** as signals. An `inv` message announces that a node possesses certain data (blocks or transactions) without sending the actual data immediately.

1. **Announcement**: Node A sends an `inv` message to Node B.
2. **Check**: Node B checks its local database to see if it already has the data.
3. **Request**: If the data is missing, Node B sends a `getdata` message.
4. **Delivery**: Node A responds with the actual data:
   - **Block data** $\rightarrow$ `block` message.
   - **Transaction data** $\rightarrow$ `tx` message (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_10.md).

### SPV Optimization
To reduce bandwidth, SPV nodes avoid requesting full blocks. Instead, they use `getheaders` to request only block headers, receiving up to 2,000 headers per `headers` message (source: mastering-bitcoin-cash-chapter-5-the-bitcoin-cash-network_10.md).

## Related pages

- [bitcoin-cash-network](bitcoin-cash-network.md)
- [[blockchain](blockchain.md)-synchronization]([blockchain](blockchain.md)-synchronization.md)
- [mastering-bitcoin-cash-chapter-5-10](mastering-bitcoin-cash-chapter-5-10.md)
