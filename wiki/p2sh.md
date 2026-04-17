# P2SH

**Summary**: Pay-to-Script-Hash; a method to simplify complex transactions by using a script hash instead of the full script.

**Sources**: mastering-bitcoin-cash_transactions_10.md

**Last updated**: 2026-04-17

---

P2SH (Pay-to-Script-Hash) shifts the complexity of a transaction from the sender to the recipient by using a hash of the redeem script in the locking condition (source: mastering-bitcoin-cash_transactions_10.md).

### Key Technical Details
- **Locking Script**: `OP_HASH160 <hash> OP_EQUAL` (source: mastering-bitcoin-cash_transactions_10.md).
- **Address Format**: Starts with "3" (Base58Check prefix "5") (source: mastering-bitcoin-cash_transactions_10.md).
- **Validation**: The network first verifies the hash of the redeem script before executing the script itself (source: mastering-bitcoin-cash_transactions_10.md).

### Advantages
- Shorter outputs and reduced [utxo](utxo.md) set storage (source: mastering-bitcoin-cash_transactions_10.md).
- Senders do not need to know the details of the complex script they are paying into (source: mastering-bitcoin-cash_transactions_10.md).
- Fees for the complex script are paid by the recipient upon spending (source: mastering-bitcoin-cash_transactions_10.md).

### Warning
Funds can be permanently lost if the P2SH hash corresponds to an invalid or unspendable redeem script, as the network does not validate the redeem script at the time of output creation (source: mastering-bitcoin-cash_transactions_10.md).

## Related pages

- [mastering-bitcoin-cash-transactions-10](mastering-bitcoin-cash-transactions-10.md)
- [standard-transaction-types](standard-transaction-types.md)
- [transaction-scripts](transaction-scripts.md)
