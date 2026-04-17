# mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-3

**Summary**: This document explains the mathematical foundations of Bitcoin Cash ownership, specifically focusing on elliptic curve cryptography and the derivation process from private keys to addresses.

**Sources**: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_3.md

**Last updated**: 2026-04-17

---

The security of Bitcoin Cash relies on public key cryptography, specifically mathematical functions that are "one-way" (easy to calculate but hard to reverse). 

BCH utilizes **elliptic curve multiplication** to enable the creation of digital signatures and keys. This allows a user to prove ownership of funds by presenting a signature that can be validated against their public key without ever revealing the private key.

The derivation sequence is as follows:
`Private Key (k)` $\to$ `Elliptic Curve Multiplication` $\to$ `Public Key (K)` $\to$ `Cryptographic Hash Function` $\to$ `Bitcoin Cash Address (A)`

## Related pages

- [[private-keys]]
- [[addresses]]
- [[transaction-script]]
