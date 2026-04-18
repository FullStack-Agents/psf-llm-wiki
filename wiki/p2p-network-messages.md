# P2P Network Messages

**Summary**: Detailed specifications of the binary communication protocol used by Bitcoin Cash nodes to propagate block and transaction data.

**Sources**: messages.md

**Last updated**: 2026-04-18

---

The Bitcoin Cash Peer-to-Peer (P2P) Network protocol is a binary protocol transmitted over TCP/IP, used by Full Nodes and [simplified-payment-verification](simplified-payment-verification.md) (SPV) Nodes (source: messages.md). Nodes form a mesh network, which allows for fast propagation of validated transactions via a gossip protocol (source: messages.md).

## Protocol Design

The protocol is designed around self-contained messages. Nodes are expected to be tolerant of and ignore message types they do not understand. Each message acts as an event that a node can respond to, such as notifications of new data, requests for data, or the data itself (source: messages.md).

## Message Format

All P2P messages follow a specific binary structure:

| Field | Length | Format | Description |
|--|--|--|--|
| net magic | 4 bytes | byte array (BE) | Network identifier to separate blockchains and test networks. |
| command string | 12 bytes | string (BE) | Fixed-length ASCII string determining the message type. |
| payload byte count | 4 bytes | unsigned integer (LE) | Size of the payload (max 256 MiB). |
| payload checksum | 4 bytes | byte array (BE) | First 4 bytes of a double-sha256 hash of the payload. |
| payload | variable | message-specific | The actual data content. |

### Net Magic
For the Bitcoin Cash main net, the `net magic` field is `0xE3E1F3E8` (the ASCII string "cash" with the highest bit of each byte set). Messages with incorrect net magic are considered invalid (source: messages.md).

### Command String
A 12-byte ASCII string, right-padded with null bytes (`0x00`) if shorter than 12 bytes. This string determines the message type (source: messages.md).

## Message Types

### Announcements
- `inv`: Notifies peers about the existence of information (block or transaction).
- `filteradd`: Adds an item into an installed filter.
- `filterclear`: Removes an installed filter.
- `filterload`: Inserts a transaction and merkle block filter into the peer.
- `dsproof-beta`: Informs participants of a double spend attempt.

### Requests
- `getdata`: Requests specific information from a peer.
- `getblocks`: Requests block hash identifiers.
- `getheaders`: Requests block headers.
- `version`: Describes peer capabilities via the Services Bitfield.
- `ping`: Requests a `pong` confirmation.
- `getaddr`: Requests a list of active peers.
- `feefilter`: Requests that transactions without sufficient fees are not relayed.
- `sendheaders`: Requests that new blocks be sent as headers instead of hashes.
- `mempool`: Request mempool contents.

### Responses
- `tx`: Provides a transaction.
- `block`: Provides the contents of a block.
- `headers`: Provides a set of block headers.
- `addr`: Provides addresses of other peers.
- `verack`: Response to a `version` message.
- `pong`: Reply to a `ping` message.
- `notfound`: Indicates a requested resource could not be relayed.
- `merkleblock`: Provides a provable subset of a block's transactions.
- `reject`: Response when a message cannot be handled.

### Compact Blocks (BIP-152)
Designed to minimize data transfer by leveraging the fact that peers often already have most transactions in a new block (source: messages.md).
- `sendcmpct`: Indicates support for the Compact Block protocol.
- `cmpctblock`: Announces and provides abbreviated contents of a block.
- `getblocktxn`: Requests additional transactions from a block.
- `blocktxn`: Returns requested transactions from a block.

### Extensions (BCHUnlimited)
- **XVersion**: `xversion`, `xupdate`, `xverack` for extensible peer capabilities.
- **XThin**: `thinblock`, `xthinblock`, `get_xthin`, `get_xblocktx`, `xblocktx` for reduced data transfer.

## Node Specific Behavior: Bitcoin Unlimited
Bitcoin Unlimited does not validate the message checksum because TCP provides its own checksum mechanism (source: messages.md).

## Related pages
- [network-communication-protocol](network-communication-protocol.md)
- [mempool](mempool.md)
- [simplified-payment-verification](simplified-payment-verification.md)
- [block](block.md)
