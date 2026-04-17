# Hash

**Summary**: Comprehensive overview of hashing algorithms used in the Bitcoin Cash protocol, including SHA-256, RIPEMD-160, and MurmurHash.

**Sources**: hash.md

**Last updated**: 2026-04-17

---

Bitcoin Cash utilizes several hashing algorithms for different purposes, ranging from network identifiers to anonymity and filter efficiency.

## SHA-256
[SHA-256](sha-256.md) is used extensively throughout the protocol (source: hash.md).

- **Block Hashing**: A double application of SHA-256 is performed on the block header to create the block hash. This double-hashing prevents length extension attacks (source: hash.md). This is also available via the `OP_HASH256` script operation.
- **Transaction Hashing**: Transactions are similarly identified by a double SHA-256 hash. Note that historical coinbase transactions could have duplicate hashes, but the inclusion of block height (since BIP-34) largely mitigates this (source: hash.md).
- **Numerical Interpretation**: In certain contexts (e.g., mining or block validation), hashes are interpreted as 256-bit little-endian numbers (source: hash.md).

## RIPEMD-160
Used in combination with SHA-256 to create shorter, quasi-anonymous representations of payees for transaction addresses (source: hash.md).

- **Address Generation**: The process follows the path: `(public key) -> SHA-256 -> RIPEMD-160 -> (address)`.
- **Script Operation**: This sequence is implemented as `OP_HASH160` for efficiency (source: hash.md).

## MurmurHash
The protocol uses MurmurHash version 3 (32-bit) specifically to support [bloom-filters](bloom-filters.md) (source: hash.md).

## Related pages

- [sha-256](sha-256.md)
- [bloom-filters](bloom-filters.md)
- [addresses](addresses.md)
- [transaction-scripts](transaction-scripts.md)
