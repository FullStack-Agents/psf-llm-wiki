# Transaction Process

**Summary**: The mechanism by which Bitcoin Cash is transferred from sender to recipient, including signing, propagation, and confirmation.

**Sources**: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-(BCH)_9.md, mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_4.md, mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_6.md, mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_7.md

**Last updated**: 2026-04-16

---

Sending Bitcoin Cash involves creating a transaction that assigns a specific amount of BCH from the sender's address to the recipient's address (source: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-(BCH)_9.md).

### The Transaction Lifecycle
1. **Authorization**: The transaction is signed using the sender's [[private-keys]], which authorizes the movement of funds from their wallet.
2. **Propagation**: The transaction is broadcast across the network using a peer-to-peer protocol. Nodes that receive a valid, unseen transaction immediately forward it to others, using a "flooding" approach to ensure the transaction reaches most nodes within seconds (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_4.md).
3. **Visibility**: Transactions can be monitored in real-time via blockchain explorers.
4. **State - Unconfirmed**: When a transaction is first broadcast, it is marked as "Unconfirmed." It is visible to the network but not yet part of the ledger.
5. **Confirmation**: A transaction is confirmed when a miner includes it in a new block. This happens approximately every 10 minutes.

### Confirmations and Irreversibility
Each block built on top of a block containing a transaction adds one "confirmation" to that transaction (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_6.md). 
- **Single Confirmation**: Occurs when a transaction is first included in a block.
- **Irreversibility**: By convention, transactions with **six or more confirmations** are considered irreversible, as reversing them would require an impractical amount of computational power (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_6.md).
- **Simplified Payment Verification (SPV)**: Lightweight clients use this method to confirm a transaction's existence and confirmation count in the blockchain without needing a full copy of the ledger (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_7.md).

### Validation and Trust
Recipients can independently verify that a transaction is well-formed, uses previously unspent inputs ([[utxo]]), and includes sufficient fees. For small-value transactions, merchants may accept "zero confirmation" transactions, as the risk is considered comparable to certain traditional payment methods (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_4.md).

The confirmation process is critical as it prevents [[double-spending]] and ensures the overall integrity of the [[blockchain]] (source: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-(BCH)_9.md).

## Related pages

- [[blockchain]]
- [[mining]]
- [[private-keys]]
- [[double-spending]]
- [[utxo]]
- [[bitcoin-cash]]
- [[mastering-bitcoin-cash-chapter-1]]
- [[mastering-bitcoin-cash-chapter-2]]
