# Private Keys

**Summary**: Cryptographic keys used to authorize transactions and prove ownership of [bitcoin-cash](bitcoin-cash.md). Keys come in pairs: a private key (secret) and a [public key](addresses.md) (shareable). The private key acts as the control mechanism for funds and is used to generate the signatures required for all transactions.

**Sources**: keys.md, mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-([BCH](bitcoin-cash.md))_1.md, mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_2.md

**Last updated**: 2026-04-18

---

A private key is the essential cryptographic requirement to unlock and spend bitcoins (source: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-([BCH](bitcoin-cash.md))_1.md). Possession of the private key is the sole requirement for spending funds.

The private key acts as the control mechanism for funds, similar to a PIN or signature on a check, and is used to generate the signatures required for all transactions (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_2.md).

### Mathematical Foundation
Bitcoin Cash uses elliptic-curve cryptography (ECC), specifically the **secp256k1** curve (source: keys.md). 

- **Private Key Generation**: A private key is a random 256-bit value chosen from the set $[1, n-1]$, where $n$ is the order of the generator point $G$ (source: keys.md). It is derived from a secure source of entropy (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_4.md).
- **Public Key Derivation**: The public key is created by performing scalar multiplication of the generator $G$ with the private key ($K = k \times G$). Public keys are points on the elliptic curve, represented as two 256-bit coordinates $(x, y)$ (source: keys.md, mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_3.md).

### Public Key Formats
Because the elliptic curve is symmetrical across the x-axis, public keys can be represented in two formats to save space (source: keys.md):
- **Uncompressed**: Includes a magic number (`0x04`), the x-value (32 bytes), and the y-value (32 bytes). Total length: 65 bytes.
- **Compressed**: Includes a magic number (`0x02` or `0x03` to indicate the parity of the y-value) and the x-value (32 bytes). Total length: 33 bytes.

### Storage and Security
Private keys must be stored securely and never revealed to untrusted parties, as anyone with the key controls the associated funds (source: keys.md). 

- **Representations**: They can be represented as plain hexadecimal or in Wallet Import Format (WIF) (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_7.md).
- **Protection**: To balance confidentiality and availability, keys can be encrypted using the BIP0038 standard (AES encryption) or stored offline via paper wallets (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_11.md).

## Related pages

- [digital-wallets](digital-wallets.md)
- [bitcoin-cash](bitcoin-cash.md)
- [transaction-scripts](transaction-scripts.md)
- [addresses](addresses.md)
- [mastering-bitcoin-cash-chapter-1](mastering-bitcoin-cash-chapter-1.md)
