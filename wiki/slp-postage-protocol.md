# slp-postage-protocol

**Summary**: Specification for the Simple Ledger Postage Protocol, which allows SLP token senders to pay for transaction fees (miner fees and output balances) using SLP tokens instead of native Bitcoin Cash (BCH).

**Sources**: slp-postage-protocol.md

**Last updated**: 2026-04-18

---

The **Simple Ledger Postage Protocol** addresses the "gas" problem in SLP transactions. Because SLP transactions are carried within BCH transactions, they require native BCH satoshis to cover the minimum mining fee and to maintain the required balance for outputs (typically 546 satoshis per output). This creates friction for users who possess SLP tokens but no native BCH (source: slp-postage-protocol.md).

## The "Post Office" Model

The protocol introduces an intermediary called a **Post Office**. The Post Office provides "postage" (native BCH inputs) to a sender's transaction in exchange for a payment made in the SLP token being sent.

### How it Works
1. **Postage Rate Request**: The sender's wallet queries the Post Office for the current rate. The server returns a JSON payload containing:
    - The payment address for postage.
    - The `weight` (number of satoshis represented by one "stamp").
    - A list of supported tokens and their respective rates (in base units) (source: slp-postage-protocol.md).
2. **Payment Generation**: The sender creates a transaction where:
    - All inputs and outputs are valid SLP.
    - An additional output is included to pay the Post Office in SLP tokens.
    - Inputs use the `SIGHASH_ALL | SIGHASH_ANYONECANPAY` signature hash type to allow the Post Office to add inputs without invalidating the sender's signature (source: slp-postage-protocol.md).
3. **Adding Postage**: The Post Office validates the transaction and appends its own native BCH inputs ("stamps"). These inputs are signed with `SIGHASH_ALL` to lock the transaction and prevent further modification (source: slp-postage-protocol.md).
4. **Broadcasting**: By default, the Post Office broadcasts the resulting valid BCH transaction to the network. Alternatively, it can return the raw hex to the sender.

## Technical Details

### Postage Units (Stamps)
Postage is calculated in "stamps." Each stamp represents a specific amount of satoshis (typically 365). The Post Office maintains a stock of UTXOs of standardized weights to efficiently cover transaction costs (source: slp-postage-protocol.md).

### Transaction Security and Malleability
- **SIGHASH_ANYONECANPAY**: Used by the sender to allow the Post Office to add inputs.
- **SIGHASH_ALL**: Used by the Post Office for the stamp inputs, effectively freezing the transaction and preventing the sender's inputs from being replaced or malleated (source: slp-postage-protocol.md).
- **Quarantine**: If the Post Office returns the raw hex instead of broadcasting, it "quarantines" the stamp UTXOs for a period defined by `transactionttl` to prevent double-spending (source: slp-postage-protocol.md).

## Integration and Privacy

### Merchant Integration
Merchants using the Simple Ledger Payment Protocol can act as Post Offices for their customers. They can include postage rate data in their Payment Requests via the `postage` property of the JSON Merchant Data object (source: slp-postage-protocol.md).

### Privacy Considerations
To protect user privacy and prevent censorship (e.g., a Post Office refusing transactions that benefit a competitor), the protocol recommends:
- **Address Non-reuse**: Senders and payment servers should avoid reusing addresses.
- **Data Minimization**: Avoiding the inclusion of sensitive JSON Merchant Data when communicating with a Post Office (source: slp-postage-protocol.md).

## Related pages

- [simple-ledger-protocol](simple-ledger-protocol.md)
- [slp-token-type-1](slp-token-type-1.md)
- [slp-nft-1](slp-nft-1.md)
- [transaction-fees](transaction-fees.md)
