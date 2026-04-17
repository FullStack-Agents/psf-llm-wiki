# mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-7

**Summary**: This document discusses the different encoding formats for private and public keys, including WIF, hexadecimal, and the difference between compressed and uncompressed public keys.

**Sources**: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_7.md

**Last updated**: 2026-04-17

---

Cryptographic keys can be represented in various formats to improve readability and reduce errors during transcription.

### Private Key Formats
The same private key can be represented in several ways:
- **Hexadecimal**: A plain 64-hex-digit string.
- **Wallet Import Format (WIF)**: A format starting with "5".
- **WIF-Compressed**: A format starting with "K" or "L".

### Public Key Formats
Public keys have two primary representations:
- **Uncompressed**: 520 bits, identified by the prefix `04`.
- **Compressed**: 264 bits, identified by the prefix `02` (if $y$ is even) or `03` (if $y$ is odd). This format stores only the x-coordinate, reducing storage requirements by nearly 50%.

**Crucial Note**: Even though they are derived from the same private key, compressed and uncompressed public keys result in different Bitcoin Cash addresses.

## Related pages

- [[private-keys]]
- [[addresses]]
- [[digital-wallets]]
