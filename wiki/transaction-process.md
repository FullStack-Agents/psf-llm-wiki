# Transaction Process

**Summary**: The mechanism by which Bitcoin Cash is transferred from sender to recipient, including signing, propagation, and confirmation.

**Sources**: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-(BCH)_9.md

**Last updated**: 2026-04-16

---

Sending Bitcoin Cash involves creating a transaction that assigns a specific amount of BCH from the sender's address to the recipient's address (source: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-(BCH)_9.md).

### The Transaction Lifecycle
1. **Authorization**: The transaction is signed using the sender's [[private-keys]], which authorizes the movement of funds from their wallet.
2. **Propagation**: The transaction is broadcast across the network using the peer-to-peer protocol. Well-connected nodes receive and recognize the transaction within seconds.
3. **Visibility**: Transactions can be monitored in real-time via blockchain explorers.
4. **State - Unconfirmed**: When a transaction is first broadcast, it is marked as "Unconfirmed." It is visible to the network but not yet part of the ledger.
5. **Confirmation**: A transaction is confirmed when a miner includes it in a new block. This happens approximately every 10 minutes.

The confirmation process is critical as it prevents [[double-spending]] and ensures the overall integrity of the [[blockchain]] (source: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-(BCH)_9.md).

## Related pages

- [[blockchain]]
- [[mining]]
- [[private-keys]]
- [[double-spending]]
- [[bitcoin-cash]]
- [[mastering-bitcoin-cash-chapter-1]]
