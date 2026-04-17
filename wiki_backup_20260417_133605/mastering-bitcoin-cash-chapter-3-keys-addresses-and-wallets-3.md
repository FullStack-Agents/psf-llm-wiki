# mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-3

**Summary**: This document explains the mathematical foundations of [[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) ownership, specifically focusing on elliptic curve cryptography and the derivation process from private keys to addresses.

**Sources**: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_3.md

**Last updated**: 2026-04-17

---

The security of [[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) relies on [public key](addresses.md) cryptography, specifically mathematical functions that are "one-way" (easy to calculate but hard to reverse). 

[BCH](bitcoin-cash.md) utilizes **elliptic curve multiplication** to enable the creation of digital signatures and keys. This allows a user to prove ownership of funds by presenting a signature that can be validated against their [public key](addresses.md) without ever revealing the [private key](private-keys.md).

The derivation sequence is as follows:
`Private Key (k)` $\to$ `Elliptic Curve Multiplication` $\to$ `Public Key (K)` $\to$ `Cryptographic Hash Function` $\to$ `[[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) Address (A)`

## Related pages

- [private-keys](private-keys.md)
- [addresses](addresses.md)
- [transaction-scripts](transaction-scripts.md)
