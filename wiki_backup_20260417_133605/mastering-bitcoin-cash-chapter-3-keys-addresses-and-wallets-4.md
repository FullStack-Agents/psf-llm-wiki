# mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-4

**Summary**: This document describes the nature of private keys as random numbers, the importance of entropy, and the one-way mathematical relationship between private and public keys.

**Sources**: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_4.md

**Last updated**: 2026-04-17

---

A [private key](private-keys.md) in [[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) is a random number between 1 and $n-1$ (where $n \approx 1.158 \times 10^{77}$), generated using a secure source of entropy typically passed through the SHA256 hash algorithm to create a 256-bit number.

The [public key](addresses.md) ($K$) is derived from the [private key](private-keys.md) ($k$) using the formula $K = k \times G$, where $G$ is a generator point. This elliptic curve multiplication is a one-way operation; calculating $k$ from $K$ (the discrete logarithm problem) is computationally infeasible.

## Related pages

- [private-keys](private-keys.md)
- [digital-wallets](digital-wallets.md)
