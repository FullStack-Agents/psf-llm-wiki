# Bitcoin Cash Addresses

**Summary**: The alphanumeric strings used as identifiers for receiving Bitcoin Cash. A Bitcoin Cash address functions as a digital fingerprint of a public key and serves as the beneficiary name on a transaction (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_2.md). 

The address is created by applying a cryptographic hash function to the public key (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_3.md). More specifically, the derivation involves SHA256 followed by RIPEMD160 and Base58Check encoding (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_6.md).

**Sources**: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-(BCH)_7.md, mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_2.md, mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_3.md, mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_6.md, mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_10.md

**Last updated**: 2026-04-17

---

A Bitcoin Cash address is a long string of letters and numbers used to receive funds. These addresses typically start with 'q' or 'p' and may optionally include a `bitcoincash:` prefix (source: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-(BCH)_7.md).

### Key Features
- **Format**: Addresses are often displayed as strings or as QR codes for easy scanning via smartphones.
- **Flexibility**: While typically corresponding to public keys, addresses can also represent scripts, allowing for flexible transaction destinations (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_2.md).
- **Privacy**: Unlike email addresses, users can create new BCH addresses as frequently as desired. These new addresses can all direct funds into the same wallet, enhancing the user's privacy (source: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-(BCH)_7.md).
- **Advanced Types (P2SH)**: Some addresses (historically starting with "3") are Pay-to-Script-Hash addresses, where the beneficiary is a script rather than a public key, enabling multi-signature (multi-sig) requirements (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_10.md).

## Related pages

- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-10](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-10.md)
- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-11](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-11.md)
- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-12](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-12.md)
- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-2](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-2.md)
- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-3](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-3.md)
- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-4](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-4.md)
- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-5](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-5.md)
- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-6](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-6.md)
- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-7](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-7.md)
- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-8](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-8.md)
- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-9](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-9.md)
- [digital-wallets](digital-wallets.md)
- [private-keys](private-keys.md)
- [bitcoin-cash](bitcoin-cash.md)
- [mastering-bitcoin-cash-chapter-1](mastering-bitcoin-cash-chapter-1.md)
