# mastering-bitcoin-cash-transactions-10

**Summary**: In-depth look at Pay-to-Script-Hash (P2SH), how it shifts script complexity to the recipient, and its operational benefits and risks.

**Sources**: mastering-bitcoin-cash_transactions_10.md

**Last updated**: 2026-04-17

---

## Overview of P2SH

Pay-to-Script-Hash (P2SH) was introduced in 2012 to simplify the use of complex scripts. It allows a complex script to be replaced by its hash in the locking script, shifting the complexity of providing the full script from the sender to the recipient (source: mastering-bitcoin-cash_transactions_10.md).

## How P2SH Works

### The Locking Script
In a P2SH output, the locking script contains only the hash of the actual spending script (the "redeem script"):
`OP_HASH160 <20-byte hash of redeem script> OP_EQUAL` (source: mastering-bitcoin-cash_transactions_10.md).

### The Spending Process
To spend P2SH funds, the recipient must provide the original redeem script and the necessary signatures. Validation occurs in two steps:
1. **Hash Verification**: The provided redeem script is hashed and compared to the hash in the locking script (source: mastering-bitcoin-cash_transactions_10.md).
2. **Script Execution**: If the hash matches, the unlocking script is executed against the redeem script (source: mastering-bitcoin-cash_transactions_10.md).

## P2SH Addresses
P2SH addresses use Base58Check encoding with a prefix of "5", meaning they typically start with the character "3". This allows complex scripts to have a standard address format (source: mastering-bitcoin-cash_transactions_10.md).

## Benefits and Risks

### Benefits
- **Efficiency**: Produces shorter transaction outputs (source: mastering-bitcoin-cash_transactions_10.md).
- **Simplicity for Senders**: Complexity is hidden from the sender (source: mastering-bitcoin-cash_transactions_10.md).
- **Resource Optimization**: Reduces data storage in the [[utxo]] set and defers storage of complex scripts until they are spent (source: mastering-bitcoin-cash_transactions_10.md).
- **Fee Distribution**: The burden of the transaction fee for complex scripts is shifted from the sender to the recipient (source: mastering-bitcoin-cash_transactions_10.md).

### Risks
The network accepts P2SH hashes without knowing if the underlying redeem script is valid. This creates a risk where funds can be locked into a script that is impossible to satisfy, rendering the Bitcoin Cash unspendable (source: mastering-bitcoin-cash_transactions_10.md).

## Related pages

- [[p2sh]]
- [[standard-transaction-types]]
- [[transaction-scripts]]
- [[utxo]]
- [[mastering-bitcoin-cash-transactions-9]]
