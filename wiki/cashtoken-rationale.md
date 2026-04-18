# cashtoken-rationale

**Summary**: Documentation of the design decisions and trade-offs made in the CashTokens specification, explaining the "why" behind the technical implementation.

**Sources**: cashtoken-rationale.md

**Last updated**: 2026-04-18

---

The CashTokens specification is based on several key architectural insights designed to balance flexibility for decentralized applications (dApps) with the stability and performance of the Bitcoin Cash network (source: cashtoken-rationale.md).

## Key Design Decisions

### Fungibility vs. Commitments
The central insight of the proposal is that **token fungibility and token commitments are conceptually incompatible**. 
- **Fungible tokens** must be indistinguishable and freely divisible/mergable.
- **Non-fungible tokens (NFTs)** are designed as tamper-proof messages (commitments) for other contracts to read.
By separating these into two distinct primitives, the protocol avoids the complexity of "fungible tokens with commitments," which would require complex policies for splitting and merging (source: cashtoken-rationale.md).

### Commitment Types and Exclusions
The spec utilizes byte-string and numeric commitments but excludes others (booleans, bitfields, hashes, public keys, signatures) to avoid unnecessary protocol and wallet complexity.
- **Byte-string commitments** are sufficient for booleans and most other data types.
- **Numeric commitments** allow the protocol to handle the splitting/merging of amounts, offloading this logic from the contract bytecode (source: cashtoken-rationale.md).

### The `mutable` and `minting` Capabilities
The introduction of `mutable` and `minting` capabilities for NFTs is critical for covenants:
- **`minting`**: Allows long-running issuance and the ability for covenants to create new commitments during operation.
- **`mutable`**: Allows a covenant to modify a single NFT's commitment (e.g., a tracking token) without the risk of accidentally minting new tokens, which is essential for secure cross-covenant interfaces (source: cashtoken-rationale.md).

### Token Category ID Design
Token categories are identified by the transaction ID of their genesis transaction. This allows:
- **Simplified Indexing**: Wallet software can easily locate genesis transactions to verify total supply or inspect genesis metadata.
- **Predictability**: Category IDs can be predicted prior to creation, facilitating the design of mutually-aware contract ecosystems (source: cashtoken-rationale.md).

### Single Token Prefix Per Output
The limitation to one token prefix (and one NFT) per output serves two purposes:
- **Simplified VM API**: It removes the need for complex sub-indexing in token inspection opcodes.
- **Scaling**: It prevents the introduction of complex many-to-many relationships in node and indexing software.
Portfolio management is instead achieved through **depository child covenants**, where a parent covenant manages multiple sub-covenants, each holding a token (source: cashtoken-rationale.md).

## Security and UX Considerations

### `SIGHASH_UTXOS` Recommendation
The spec recommends `SIGHASH_UTXOS` for multi-entity transactions to protect light wallets and offline signers from vulnerabilities like unexpected fee or token burning, as these users may not have a full view of the UTXOs being spent (source: cashtoken-rationale.md).

### Token-Aware CashAddresses
By creating specific "token-aware" address types (`2` and `3`), the protocol prevents users from accidentally sending tokens to addresses that cannot support them, avoiding potential loss of funds (source: cashtoken-rationale.md).

### Supply Limits
Fungible token supply is capped at the maximum VM number (`9223372036854775807`). This prevents denial-of-service vulnerabilities in DEX covenants that might fail to validate excessively large amounts and simplifies UI display by avoiding arbitrary-precision arithmetic (source: cashtoken-rationale.md).

## Related pages

- [cashtokens-spec](cashtokens-spec.md)
- [cashtokens](cashtokens.md)
- [token-examples](token-examples.md)
