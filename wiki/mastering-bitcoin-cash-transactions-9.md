# mastering-bitcoin-cash-transactions-9

**Summary**: Overview of the five standard transaction types accepted by the Bitcoin Cash reference client, including P2PKH, P2PK, Multi-Signature, Data Outputs, and P2SH.

**Sources**: mastering-bitcoin-cash_transactions_9.md

**Last updated**: 2026-04-17

---

## Standard Transaction Types

The Bitcoin Cash reference client accepts five standard transaction types (source: mastering-bitcoin-cash_transactions_9.md):

### 1. Pay-to-Public-Key-Hash (P2PKH)
This is the most common transaction type. It encumbers the output with a public key hash, which corresponds to a Bitcoin Cash address.
- **Locking Script**: `OP_DUP OP_HASH160 <Public Key Hash> OP_EQUAL OP_CHECKSIG` (source: mastering-bitcoin-cash_transactions_9.md)

### 2. Pay-to-Public-Key (P2PK)
A simplified version where the actual public key is stored in the locking script instead of its hash.
- **Locking Script**: `<Public Key> OP_CHECKSIG` (source: mastering-bitcoin-cash_transactions_9.md)

### 3. Multi-Signature (Multi-sig)
Implements an M-of-N scheme, requiring at least $M$ signatures from $N$ potential signers. Standard multi-sig scripts are limited to 15 public keys.
- **Locking Script**: `M <Public Key 1> <Public Key 2> ... <Public Key N> N OP_CHECKMULTISIG` (source: mastering-bitcoin-cash_transactions_9.md)

### 4. Data Output (OP_RETURN)
Used to store up to 220 bytes of non-payment data. These outputs are provably unspendable and are not stored in the UTXO set.
- **Locking Script**: `OP_RETURN <data>` (source: mastering-bitcoin-cash_transactions_9.md)

### 5. Pay-to-Script-Hash (P2SH)
Allows complex scripts to be referenced by a hash, simplifying the process of using sophisticated spending conditions (source: mastering-bitcoin-cash_transactions_9.md).

## Related pages

- [[standard-transaction-types]]
- [[transaction-scripts]]
- [[utxo]]
- [[mastering-bitcoin-cash-transactions-8]]
