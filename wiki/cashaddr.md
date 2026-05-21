# CashAddr Encoding

**Summary**: A Base32 encoding format used in Bitcoin Cash to provide a human-readable, error-resistant way to represent addresses and distinguish them from Bitcoin (BTC) addresses.

**Sources**: cashaddr.md

**Last updated**: 2026-05-21

---

**CashAddr** is the preferred address format for Bitcoin Cash. It is designed to be easier to share and copy (e.g., via QR codes) and specifically prevents confusion with [Base58Check](base58check.md) legacy addresses used by Bitcoin (BTC) (source: cashaddr.md).

## Address Structure
A full Cash Address consists of four components:
1. **Prefix**: A human-readable string indicating the network or metaprotocol.
2. **Separator**: A colon (`:`).
3. **Payload**: A Base32 encoded string containing the version byte and the data (hash).
4. **Checksum**: A Base32 encoded error-detection code.

### Network Prefixes
The prefix identifies the valid network for the address:
- **Mainnet**: `bitcoincash`
- **Testnet**: `bchtest`
- **Regtest**: `bchreg`
- **Metaprotocols**: Prefixes like `simpleledger` are used for protocols like the Simple Ledger Protocol (SLP) to prevent tokens from being sent to non-SLP wallets (source: cashaddr.md).

## Base32 Alphabet
CashAddr uses a specific Base32 alphabet to avoid ambiguous characters, excluding `1`, `b`, `i`, and `o`.
**Alphabet**: `qpzry9x8gf2tvdw0s3jn54khce6mua7l`

## Version Bytes
The version byte in CashAddr is bit-mapped into three parts:
1. **Reserved**: The most significant bit must be `0`.
2. **Address Type**:
   - `0b000`: P2PKH
   - `0b001`: P2SH
3. **Data Size**: The last 3 bits indicate the size of the data payload, allowing the node to verify the address length.

| Size bits | Data size (bytes) |
| --------- | ----------------- |
| 0b000     | 20                |
| 0b001     | 24                |
| 0b010     | 28                |
| 0b011     | 32                |
| 0b100     | 40                |
| 0b101     | 48                |

(source: cashaddr.md)

**Common Legacy Version Bytes**:
- **P2PKH**: Version byte `0` (starts with `q` in the payload).
- **P2SH**: Version byte `5` (starts with `p` in the payload).

### Base32 Symbol Chart

| Value | Char | Value | Char |
| ----- | ---- | ------| ---- |
| 0     | q    | 16    | s    |
| 1     | p    | 17    | 3    |
| 2     | z    | 18    | j    |
| 3     | r    | 19    | n    |
| 4     | y    | 20    | 5    |
| 5     | 9    | 21    | 4    |
| 6     | x    | 22    | k    |
| 7     | 8    | 23    | h    |
| 8     | g    | 24    | c    |
| 9     | f    | 25    | e    |
| 10    | 2    | 26    | 6    |
| 11    | t    | 27    | m    |
| 12    | v    | 28    | u    |
| 13    | d    | 29    | a    |
| 14    | w    | 30    | 7    |
| 15    | 0    | 31    | l    |

(source: cashaddr.md)

Uppercase characters are valid (enabling efficient QR encoding), but any mixture of lowercase and uppercase must be rejected (source: cashaddr.md).

## Checksum
CashAddr uses a 40-bit BCH code defined over the finite field GF(2^5). This provides a high degree of security, capable of detecting up to 6 errors in the address or 8 errors in a row (source: cashaddr.md).

## Encoding Process
1. **Payload Creation**: Concatenate the version byte and the address data (e.g., public key hash).
2. **Chunking**: Divide the payload into 5-bit chunks, padding with zero bits if necessary.
3. **Checksum Computation**: Apply a `polymod` function to the prefix, separator, payload chunks, and a checksum template.
4. **Base32 Encoding**: Encode the payload and checksum chunks using the CashAddr Base32 alphabet (source: cashaddr.md).

## Related pages
- [addresses](addresses.md)
- [base58check](base58check.md)
- [p2sh](p2sh.md)
- [slp-token-protocol](slp-token-protocol.md)
