# Private Keys

**Summary**: Cryptographic keys used to authorize transactions and prove ownership of [Bitcoin Cash](bitcoin-cash.md). Keys come in pairs: a private key (secret) and a [public key](addresses.md) (shareable). The private key acts as the control mechanism for funds, similar to a PIN or signature on a check, and is used to generate the signatures required for all transactions (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_2.md).

**Sources**: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-([BCH](bitcoin-cash.md))_1.md, mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_2.md

**Last updated**: 2026-04-17

---

A private key is the essential cryptographic requirement to unlock and spend bitcoins (source: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-([BCH](bitcoin-cash.md))_1.md). Possession of the private key is the sole requirement for spending funds.

The private key acts as the control mechanism for funds, similar to a PIN or signature on a check, and is used to generate the signatures required for all transactions (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_2.md). 

Mathematically, a private key is a random 256-bit number generated from a secure source of entropy (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_4.md). The [public key](addresses.md) is derived from the private key through elliptic curve multiplication ($K = k \times G$). While key pairs are often stored together, only the private key is strictly necessary for storage because the [public key](addresses.md) can be computed from it (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_3.md).

# Private Keys

**Summary**: Cryptographic keys used to authorize transactions and prove ownership of [Bitcoin Cash](bitcoin-cash.md). Keys come in pairs: a private key (secret) and a [public key](addresses.md) (shareable). The private key acts as the control mechanism for funds, similar to a PIN or signature on a check, and is used to generate the signatures required for all transactions (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_2.md). 

Mathematically, a private key is a random 256-bit number generated from a secure source of entropy (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_4.md). The [public key](addresses.md) is derived from the private key through elliptic curve multiplication ($K = k \times G$). While key pairs are often stored together, only the private key is strictly necessary for storage because the [public key](addresses.md) can be computed from it (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_3.md).

Private keys can be represented in multiple formats for easier transcription, such as plain hexadecimal or Wallet Import Format (WIF) (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_7.md). To balance confidentiality and availability, they can be encrypted using the BIP0038 standard ( AES encryption) or stored offline via paper wallets (source: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_11.md).

## Related pages

- [digital-wallets](digital-wallets.md)
- [bitcoin-cash](bitcoin-cash.md)
- [transaction-scripts](transaction-scripts.md)
- [mastering-bitcoin-cash-chapter-1](mastering-bitcoin-cash-chapter-1.md)
