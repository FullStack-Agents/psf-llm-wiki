# CashAddr Encoding

**Summary**: A Base32 encoding format used in Bitcoin Cash to provide a human-readable, error-resistant way to represent addresses and distinguish them from Bitcoin (BTC) addresses.

**Sources**: cashaddr.md

**Last updated**: 2026-04-18

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
3. **Data Size**: The last 3 bits indicate the size of the data payload (e.g., `0b000` for 20 bytes), allowing the node to verify the address length (source: cashaddr.md).

**Common Legacy Version Bytes**:
- **P2PKH**: Version byte `0` (starts with `q` in the payload).
- **P2SH**: Version byte `5` (starts with `p` in the payload).

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
