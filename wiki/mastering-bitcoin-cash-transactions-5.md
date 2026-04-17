# mastering-bitcoin-cash-transactions-5

**Summary**: Detailed breakdown of the structure of transaction inputs and outputs in Bitcoin Cash.

**Sources**: mastering-bitcoin-cash_transactions_5.md

**Last updated**: 2026-04-17

---

## Transaction Outputs

A transaction output defines how much value is being transferred and the conditions required to spend it. It consists of two primary parts: an amount in satoshis and a locking script (source: mastering-bitcoin-cash_transactions_5.md).

### Output Structure
| Size | Field | Description |
| :--- | :--- | :--- |
| 8 bytes | Amount | Bitcoin Cash value in satoshis (10^8 BCH) |
| 1–9 bytes (VarInt) | Locking-Script Size | Length of the following locking script in bytes |
| Variable | Locking-Script | A script defining the conditions needed to spend the output |

(source: mastering-bitcoin-cash_transactions_5.md)

## Transaction Inputs

Transaction inputs act as pointers to [[utxo]]s being spent. They reference specific UTXOs using a transaction hash and an output index (source: mastering-bitcoin-cash_transactions_5.md). To successfully spend a UTXO, the input must provide an unlocking script that satisfies the requirements of the UTXO's locking script (source: mastering-bitcoin-cash_transactions_5.md).

### Input Structure
| Size | Field | Description |
| :--- | :--- | :--- |
| 32 bytes | Transaction Hash | Pointer to the transaction containing the UTXO |
| 4 bytes | Output Index | The index of the UTXO to be spent (starts at 0) |
| 1-9 bytes (VarInt) | Unlocking-Script Size | Length of the following unlocking script in bytes |
| Variable | Unlocking-Script | A script that fulfills the conditions of the locking script |
| 4 bytes | Sequence Number | Set to 0xFFFFFFFF (Tx-replacement feature currently disabled) |

(source: mastering-bitcoin-cash_transactions_5.md)

## Related pages

- [[transaction-scripts]]
- [[utxo]]
- [[bitcoin-cash-transactions]]
- [[mastering-bitcoin-cash-transactions-4]]
