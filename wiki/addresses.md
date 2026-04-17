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

- [[digital-wallets]]
- [[private-keys]]
- [[bitcoin-cash]]
- [[mastering-bitcoin-cash-chapter-1]]
