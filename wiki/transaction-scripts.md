# Transaction Scripts

**Summary**: The locking and unlocking scripts used to secure and spend [bitcoin-cash](bitcoin-cash.md) outputs.

**Sources**: mastering-bitcoin-cash_transactions_5.md, mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-([BCH](bitcoin-cash.md))_3.md

**Last updated**: 2026-04-17

---

[bitcoin-cash](bitcoin-cash.md) uses scripts to manage the ownership and transfer of funds. The transaction script is a decentralized transaction verification system and is one of the four fundamental innovations that enable [bitcoin-cash](bitcoin-cash.md) (source: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-(BCH)_3.md). 

It provides the cryptographic means to ensure that only the legitimate owner of a digital asset can authorize its transfer, addressing the challenge of authenticity (source: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-(BCH)_3.md).

### Locking Scripts
Every transaction output contains a **locking script**. This script specifies the conditions that must be met for the output to be spent in the future (source: mastering-bitcoin-cash_transactions_5.md).

### Unlocking Scripts
To spend a [utxo](utxo.md), a transaction input must provide an **unlocking script**. This script must satisfy the conditions defined by the corresponding locking script to authorize the transfer of funds (source: mastering-bitcoin-cash_transactions_5.md).

### Advanced Scripting and P2SH
Beyond simple public-key ownership, the scripting system allows for more complex spending conditions. **Pay-to-Script-Hash (P2SH)** addresses allow the beneficiary to be a script rather than a [public key](addresses.md), enabling advanced functionalities such as **multi-signature (multi-sig)** requirements where multiple keys must authorize a spend (source: mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-10.md).

## Related pages

- [mastering-bitcoin-cash-transactions-5](mastering-bitcoin-cash-transactions-5.md)
- [utxo](utxo.md)
- [bitcoin-cash-transactions](bitcoin-cash-transactions.md)
- [bitcoin-cash](bitcoin-cash.md)
- [blockchain](blockchain.md)
- [mastering-bitcoin-cash-chapter-1](mastering-bitcoin-cash-chapter-1.md)
- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-10](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-10.md)
