# mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-6

**Summary**: This document describes the various formats of [bitcoin-cash](bitcoin-cash.md) addresses, specifically the transition from legacy addresses to the Cash Address format, and the technical process of deriving an [address](addresses.md) from a [public key](addresses.md).

**Sources**: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_6.md

**Last updated**: 2026-04-17

---

[bitcoin-cash](bitcoin-cash.md) addresses serve as user-friendly abstractions of the underlying [public key](addresses.md) cryptography. 

### Address Formats
- **Cash Address**: The most recent format, typically beginning with the `bitcoincash:` prefix.
- **Legacy Addresses**: Begin with the number `1` and are derived using a specific hashing and encoding process.

### Technical Derivation
To derive a legacy [address](addresses.md) from a [public key](addresses.md), the following sequence is applied:
1. **Hashing**: a [public key](addresses.md) is passed through **SHA256**, and the result is then passed through **RIPEMD160**.
2. **Encoding**: The resulting 160-bit hash is encoded using **Base58Check**, which adds version information and a checksum to prevent errors.

The mathematical representation of this process is:
`[bitcoin-cash](bitcoin-cash.md) Address = Base58Check(version + RIPEMD160(SHA256([public key](addresses.md))))`

## Related pages

- [addresses](addresses.md)
- [private-keys](private-keys.md)
- [transaction-scripts](transaction-scripts.md)
