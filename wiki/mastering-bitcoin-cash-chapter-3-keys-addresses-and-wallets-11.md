# mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-11

**Summary**: This document discusses the secure storage and transport of private keys, focusing on the BIP0038 encryption standard and the use of paper wallets for cold storage.

**Sources**: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_11.md

**Last updated**: 2026-04-17

---

Private keys require a balance between absolute confidentiality and availability.

### Key Encryption (BIP0038)
BIP0038 is a standard for encrypting private keys with a passphrase. This allows users to securely back up or transport keys between wallets.
- **Process**: It takes a [private key](private-keys.md) in WIF format and a passphrase, using the Advanced Encryption Standard (AES).
- **Identification**: Encrypted keys produced by this standard start with the prefix `6P`.
- **Decryption**: The encrypted key can only be restored to a usable WIF format if the correct passphrase is provided.

### Paper Wallets
Paper wallets are a form of **cold storage** where the [private key](private-keys.md) and its corresponding [address](addresses.md) are printed on physical paper.
- **Security**: Because the keys are kept offline, they are immune to digital attacks.
- **Storage**: They are often stored in physical safes, sometimes using tamper-evident materials or holographic seals to ensure integrity.

## Related pages

- [private-keys](private-keys.md)
- [digital-wallets](digital-wallets.md)
- [addresses](addresses.md)
