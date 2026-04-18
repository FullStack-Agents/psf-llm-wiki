# [bitcoin-cash](bitcoin-cash.md) Addresses

**Summary**: The alphanumeric strings used as identifiers for receiving [bitcoin-cash](bitcoin-cash.md). A [bitcoin-cash](bitcoin-cash.md) address functions as a digital fingerprint of a public key and serves as the beneficiary name on a transaction (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_2.md). 

The address is created by applying a cryptographic hash function to the public key (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_3.md). More specifically, the derivation involves SHA256 followed by RIPEMD160 and Base58Check encoding (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_6.md).

**Sources**: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-([BCH](bitcoin-cash.md))_7.md, mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_2.md, mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_3.md, mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_6.md, mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_10.md, addresses.md

**Last updated**: 2026-04-18

---

A [bitcoin-cash](bitcoin-cash.md) address is a long string of letters and numbers used to receive funds. These addresses typically start with 'q' or 'p' and may optionally include a `bitcoincash:` prefix (source: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-(BCH)_7.md).

Because Bitcoin Cash transactions do not have a concept of accounts with balances, addresses provide a shorthand for identifying which unspent outputs are spendable in similar ways (source: addresses.md).

### Encoding Formats
To ensure addresses are received and interpreted correctly, they are typically encoded using formats that include checksums:
- **Base58Check (Legacy)**: An older encoding format.
- **CashAddr**: Created to avoid conflicts with pre-existing BTC addresses (source: addresses.md).

### Address Types
- **Pay to Public Key Hash (P2PKH)**: Encodes the hash of the public key (`RIPEMD-160(SHA-256(publicKey))`).
    - Base58Check starts with `1`.
    - CashAddr starts with `q` (source: addresses.md).
- **Pay to Script Hash (P2SH)**: Encodes the redeem script hash (`RIPEMD-160(redeemScript)`).
    - Base58Check starts with `3`.
    - CashAddr starts with `p` (source: addresses.md).
- **Multisig Addresses**: Often these are actually P2SH addresses for redeem scripts that perform multisignature validation. With the introduction of Schnorr signatures, n-of-n multisig can also be performed using aggregated keys, which may result in an address that looks like a standard P2PKH (source: addresses.md).

### Key Features
- **Format**: Addresses are often displayed as strings or as QR codes for easy scanning via smartphones.
- **Flexibility**: While typically corresponding to public keys, addresses can also represent scripts, allowing for flexible transaction destinations (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_2.md).
- **Privacy**: Unlike email addresses, users can create new [BCH](bitcoin-cash.md) addresses as frequently as desired. These new addresses can all direct funds into the same wallet, enhancing the user's privacy (source: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-(BCH)_7.md).

## Related pages

- [p2sh](p2sh.md)
- [multi-signature](multi-signature.md)
- [locking-script](locking-script.md)
- [digital-wallets](digital-wallets.md)
- [private-keys](private-keys.md)
- [bitcoin-cash](bitcoin-cash.md)
- [mastering-bitcoin-cash-chapter-1](mastering-bitcoin-cash-chapter-1.md)

