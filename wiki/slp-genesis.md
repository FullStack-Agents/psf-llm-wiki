# SLP Genesis Transaction

**Summary**: Detailed specification of the SLP Genesis transaction, which defines a token's properties, metadata, and initial supply on the Bitcoin Cash network.

**Sources**: genesis.md

**Last updated**: 2026-04-18

---

The **Genesis Transaction** is the first transaction of an SLP token. It defines the token's fundamental properties and is the root of the token's identity; the hash of this transaction serves as the `token_id` (source: genesis.md).

## Token Properties

The Genesis transaction establishes several key parameters:

- **Token Type**: Indicates the SLP sub-protocol. Currently, Type 1 is the **Permissionless Token Type**. Other types (2, 3, 4) are reserved for Security, Voting, and Ticketing tokens, respectively. Tokens of different types cannot be mixed (source: genesis.md).
- **Decimals**: Defines the divisibility of the token. A token is divisible into $10^{\text{decimals}}$ base units. For example, a `decimals` value of 6 means 1.0 token is represented as 1,000,000 base units (source: genesis.md).
- **Initial Mint Quantity**: The amount of base units created and assigned to the initial receiver at the token's creation (source: genesis.md).
- **Minting Baton**: If a `mint_baton_vout` is specified, it endows a specific transaction output with a "minting baton." This baton allows for future supply increases via **MINT** transactions. If no baton is present, the token has a provably one-time issuance (source: genesis.md).

## Transaction Structure

### The OP_RETURN Output (vout=0)
The first output must be an `OP_RETURN` output containing the SLP metadata in the following sequence:
1. **Lokad ID**: `'SLP\x00'` (4 bytes).
2. **Token Type**: (1 to 2 byte integer).
3. **Transaction Type**: `'GENESIS'` (7 bytes).
4. **Token Ticker**: (0 to $\infty$ bytes).
5. **Token Name**: (0 to $\infty$ bytes).
6. **Document URL**: (0 to $\infty$ bytes).
7. **Document Hash**: (0 or 32 bytes).
8. **Decimals**: (1 byte, 0x00-0x09).
9. **Mint Baton Vout**: (0 or 1 byte, 0x02-0xff).
10. **Initial Mint Quantity**: (8 byte integer).

### Other Outputs
- **vout=1**: Receives the `initial_token_mint_quantity` of tokens.
- **vout=M (mint_baton_vout)**: Receives the minting baton (if applicable).

## Technical Notes
- **BCH Amounts**: SLP does not restrict the BCH amount in outputs. Typically, the `OP_RETURN` output contains 0 BCH, while token/baton receivers typically receive a minimal "dust" amount (0.00000546 BCH) to satisfy network rules (source: genesis.md).

## Related pages

- [simple-ledger-protocol](simple-ledger-protocol.md)
- [slp-token-protocol](slp-token-protocol.md)
- [transaction](transaction.md)
- [locking-script](locking-script.md)
