# Block Header

**Summary**: The block header is a fixed-width (80-byte) summary of a block used to identify the block, verify proof-of-work, and link the block to its predecessor.

**Sources**: block-header.md

**Last updated**: 2026-04-18

---

Block headers act as an efficient intermediary representation of a block. Because they are small (80 bytes), nodes can perform critical validity checks before committing to the resource-expensive process of downloading and validating all transactions within the block. This mechanism significantly increases the cost for attackers to perform denial-of-service (DoS) attacks.

## Functions of the Block Header
A block header allows a node to:
1. **Calculate the Block Hash**: The block's identity is the double SHA-256 hash of its header.
2. **Verify Proof-of-Work**: Confirm that the block hash is below the required target.
3. **Establish Blockchain Position**: Use the "previous block hash" to determine where the block fits in the sequence.

## Block Header Format

| Field | Length | Format | Description |
|---|---|---|---|
| Version | 4 bytes | unsigned integer (LE) | The block format version (currently `0x04000000`). |
| Previous Block Hash | 32 bytes | hash (LE) | The hash of the block immediately preceding this one. |
| Merkle Root | 32 bytes | hash (LE) | The root of the [Merkle Tree](merkle-tree.md) of the block's transactions. |
| Timestamp | 4 bytes | unix timestamp (LE) | Epoch timestamp of the block in seconds. |
| Target | 4 bytes | compressed target (LE) | The target the block hash must be below to be valid. |
| Nonce | 4 bytes | bytes (LE) | A random value changed by miners to find a valid block hash. |

## Compressed Target Format
To keep the header size small, the target uses a special floating-point representation. The target value is calculated as:
$\text{significand} \times 2^{8 \times (\text{exponent} - 3)}$

### Target Field Components
- **Exponent (1 byte)**: Used to calculate the offset for the significand.
- **Significand (3 bytes)**: The mantissa of the target value.

## Related pages

- [block](block.md)
- [proof-of-work](proof-of-work.md)
- [merkle-tree](merkle-tree.md)
- [hash](hash.md)
