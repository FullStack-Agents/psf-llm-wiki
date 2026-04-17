# mastering-bitcoin-cash-transactions-5

**Summary**: Detailed breakdown of the structure of transaction inputs and outputs in [[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md).

**Sources**: mastering-bitcoin-cash_transactions_5.md

**Last updated**: 2026-04-17

---

## Transaction Outputs

A transaction output defines how much value is being transferred and the conditions required to spend it. It consists of two primary parts: an amount in satoshis and a locking script (source: mastering-bitcoin-cash_transactions_5.md).

### Output Structure
| Size | Field | Description |
| :--- | :--- | :--- |
| 8 bytes | Amount | [[bitcoin-cash](bitcoin-cash.md)](bitcoin-cash.md) value in satoshis (10^8 [BCH](bitcoin-cash.md)) |
| 1–9 bytes (VarInt) | Locking-Script Size | Length of the following locking script in bytes |
| Variable | Locking-Script | A script defining the conditions needed to spend the output |

(source: mastering-bitcoin-cash_transactions_5.md)

## Transaction Inputs

Transaction inputs act as pointers to [utxo](utxo.md)s being spent. They reference specific [utxo](utxo.md)s using a transaction hash and an output index (source: mastering-bitcoin-cash_transactions_5.md). To successfully spend a [[utxo](utxo.md)](utxo.md), the input must provide an unlocking script that satisfies the requirements of the [[utxo](utxo.md)](utxo.md)'s locking script (source: mastering-bitcoin-cash_transactions_5.md).

### Input Structure
| Size | Field | Description |
| :--- | :--- | :--- |
| 32 bytes | Transaction Hash | Pointer to the transaction containing the [[utxo](utxo.md)](utxo.md) |
| 4 bytes | Output Index | The index of the [[utxo](utxo.md)](utxo.md) to be spent (starts at 0) |
| 1-9 bytes (VarInt) | Unlocking-Script Size | Length of the following unlocking script in bytes |
| Variable | Unlocking-Script | A script that fulfills the conditions of the locking script |
| 4 bytes | Sequence Number | Set to 0xFFFFFFFF (Tx-replacement feature currently disabled) |

(source: mastering-bitcoin-cash_transactions_5.md)

## Related pages

- [transaction-scripts](transaction-scripts.md)
- [utxo](utxo.md)
- [bitcoin-cash-transactions](bitcoin-cash-transactions.md)
- [mastering-bitcoin-cash-transactions-4](mastering-bitcoin-cash-transactions-4.md)
