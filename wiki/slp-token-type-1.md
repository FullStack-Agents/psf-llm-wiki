# slp-token-type-1

**Summary**: Detailed specification of the SLP Permissionless Token Type (Type 1), covering its transaction formats' (GENESIS, MINT, SEND, COMMIT), consensus rules, and validation security models.

**Sources**: slp-token-type-1.md

**Last updated**: 2026-04-18

---

The **SLP Token Type 1** is the permissionless implementation of the Simple Ledger Protocol. It allows for the creation and transfer of tokens without requiring permission from a central authority, utilizing the `OP_RETURN` field of Bitcoin Cash transactions (source: slp-token-type-1.md).

## Transaction Types

SLP Type 1 defines four specific transaction types:

### 1. GENESIS
The first transaction that defines the token's properties, metadata, and initial supply.
- **Key Fields**: Ticker, Name, Document URL, Document Hash, Decimals, and Initial Mint Quantity (source: slp-token-type-1.md).
- **Token ID**: The transaction hash of the GENESIS transaction serves as the `token_id` (source: slp-token-type-1.md).
- **Mint Baton**: Can specify a `mint_baton_vout` to allow future supply increases (source: slp-token-type-1.md).

### 2. MINT
Used to increase the token supply.
- **Requirement**: Requires a "baton" input derived from the GENESIS or a previous MINT transaction (source: slp-token-type-1.md).
- **Baton Management**: The MINT transaction can either pass the baton to a new output or end the minting capability by omitting the baton output (source: slp-token-type-1.md).

### 3. SEND
The primary mechanism for transferring tokens between users.
- **Mechanism**: Associates token amounts with specific transaction outputs (vout=1 to vout=19) (source: slp-token-type-1.md).
- **Validation**: The sum of output tokens must not exceed the sum of valid token inputs of the same `token_id` and `token_type` (source: slp-token-type-1.md).

### 4. COMMIT
A "Proof of Trust" mechanism where issuers or validators publish checksums (hashes) of valid transactions.
- **Purpose**: Allows users to verify that the issuer is honoring consensus rules without tracing the entire DAG (source: slp-token-type-1.md).
- **Structure**: Includes `for_bitcoin_block_hash`, `block_height`, and `token_txn_set_hash` (source: slp-token-type-1.md).

## Consensus and Validation

### Consensus Rules
- **OP_RETURN Position**: The SLP message must be in the first output (`vout=0`) and begin with opcode `0x6a` (source: slp-token-type-1.md).
- **Formatting**: Strict adherence to byte sizes and encoding (big-endian unsigned integers) is required; any violation renders the transaction invalid (source: slp-token-type-1.md).

### Security Model
Validation of tokens follows a **Directed Acyclic Graph (DAG)**. Users can choose their validation depth:
- **Full Validation**: Tracing all inputs back to the GENESIS transaction.
- **Limited Validation**: Tracing back a certain number of steps.
- **Proxy Validation**: Querying an infrastructure service (e.g., BitDB) for validity.
- **Checkpoint Validation**: Using COMMIT transactions as trusted starting points (source: slp-token-type-1.md).

## Infrastructure and Tools

### Tokengraph
A proposed virtual state machine and graph database that maintains the global state of all SLP tokens by processing BitDB events using SLP transition algorithms (source: slp-token-type-1.md).

### SLP Addr
A specialized address format using the prefix `simpleledger:` instead of `bitcoincash:`. This prevents users from accidentally spending token-containing UTXOs in non-token-aware wallets (source: slp-token-type-1.md).

## Regulated Security Tokens
While Type 1 is permissionless, the protocol supports the concept of regulated tokens (Type 2) which could employ whitelists and issuer-controlled access, potentially utilizing the minting baton to update whitelist rules (source: slp-token-type-1.md).

## Related pages

- [simple-ledger-protocol](simple-ledger-protocol.md)
- [slp-genesis](slp-genesis.md)
- [slp-mint](slp-mint.md)
- [slp-send](slp-send.md)
- [slp-token-protocol](slp-token-protocol.md)
- [cashaddr](cashaddr.md)
