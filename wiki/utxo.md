# UTXO (Unspent Transaction Outputs)

**Summary**: The mechanism by which Bitcoin Cash tracks ownership and available funds through unspent outputs of previous transactions.

**Sources**: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_3.md

**Last updated**: 2026-04-16

---

In Bitcoin Cash, funds are not stored in "accounts" with balances, but rather as **Unspent Transaction Outputs (UTXOs)**. A UTXO is an output from a previous transaction that has not yet been spent (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_3.md).

### How UTXOs Work
When a user wants to send BCH, their wallet must identify appropriate UTXOs associated with their cryptographic keys to serve as the **inputs** for the new transaction.

- **Tracking UTXOs**: Wallet applications typically maintain a local database of UTXOs.
- **Querying the Network**: If a local database is unavailable, wallets can query the network via APIs (such as ElectrumX) to retrieve a list of available unspent outputs for a specific address (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_3.md).

### Role in Transaction Construction
The selection of UTXOs is the first step in the [[transaction-process]]. Once selected, these outputs are combined with new outputs (credits) that encode the spending conditions for the recipient.

## Related pages

- [[transaction-anatomy]]
- [[transaction-process]]
- [[digital-wallets]]
- [[blockchain]]
- [[mastering-bitcoin-cash-chapter-2]]
