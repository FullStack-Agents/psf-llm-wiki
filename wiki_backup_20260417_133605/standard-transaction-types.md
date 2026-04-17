# Standard Transaction Types

**Summary**: The categorized set of transaction types accepted by the reference [[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) client.

**Sources**: mastering-bitcoin-cash_transactions_9.md

**Last updated**: 2026-04-17

---

[[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) defines five standard transaction types to manage different spending conditions and use cases (source: mastering-bitcoin-cash_transactions_9.md).

### Summary Table

| Type | Mechanism | Common Use Case |
| :--- | :--- | :--- |
| **P2PKH** | Public Key Hash | Standard addresses/wallets |
| **P2PK** | Public Key | Simple transfers |
| **Multi-sig** | M-of-N signatures | Shared wallets, escrow |
| **OP_RETURN** | Data storage | Non-payment data, timestamps |
| **P2SH** | Script Hash | Complex spending conditions |

### Detailed Notes
- **P2PKH** is the most prevalent type (source: mastering-bitcoin-cash_transactions_9.md).
- **OP_RETURN** outputs are uniquely unspendable and do not enter the [utxo](utxo.md) set (source: mastering-bitcoin-cash_transactions_9.md).
- **Multi-sig** is limited to 15 public keys in standard scripts (source: mastering-bitcoin-cash_transactions_9.md).

## Related pages

- [mastering-bitcoin-cash-transactions-9](mastering-bitcoin-cash-transactions-9.md)
- [transaction-scripts](transaction-scripts.md)
- [utxo](utxo.md)
