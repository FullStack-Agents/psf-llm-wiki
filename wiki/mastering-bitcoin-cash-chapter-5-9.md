# Mastering [[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) Chapter 5 Part 9

**Summary**: Exploration of the [[utxo](utxo.md)](utxo.md) database ([[utxo](utxo.md)](utxo.md) pool), explaining its purpose, how it differs from the transaction pool, and its role in transaction validation.

**Sources**: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_9.md

**Last updated**: 2026-04-17

---

Some [[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) client implementations maintain a **[[utxo](utxo.md)](utxo.md) database** (or [[utxo](utxo.md)](utxo.md) pool) that keeps track of all unspent transaction outputs currently on the [blockchain](blockchain.md) (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_9.md).

## The [[utxo](utxo.md)](utxo.md) Pool vs. The Transaction Pool

Although both are described as "pools," they serve fundamentally different purposes:

| Feature | Transaction Pool (Mempool) | [[utxo](utxo.md)](utxo.md) Pool |
| :--- | :--- | :--- |
| **Contents** | Unconfirmed transactions (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_9.md) | Confirmed unspent outputs (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_9.md) |
| **Persistence** | Volatile (RAM), starts empty on boot (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_9.md) | Persistent (Database), contains all historical [utxo](utxo.md)s (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_9.md) |
| **Network State** | Local perspective (varies by node) (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_9.md) | Network consensus (consistent across nodes) (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_9.md) |
| **Lifecycle** | Temporary (until mined or discarded) | Long-term (until spent) |

## Role in Validation
The [[utxo](utxo.md)](utxo.md) database is critical for efficient transaction validation. Instead of scanning the entire [blockchain](blockchain.md) for every transaction, a node uses the [[utxo](utxo.md)](utxo.md) pool to quickly verify:
1. That the transaction inputs reference outputs that actually **exist** and are **unspent** (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_9.md).
2. That the outputs are available to be spent by the sender.

Without this database, nodes would be unable to validate new transactions in a reasonable amount of time (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_9.md).

## Related pages

- [utxo](utxo.md)
- [transaction-pools](transaction-pools.md)
- [mastering-bitcoin-cash-chapter-5-9](mastering-bitcoin-cash-chapter-5-9.md)
