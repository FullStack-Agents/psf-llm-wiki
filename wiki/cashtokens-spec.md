# cashtokens-spec

**Summary**: Technical specification for Token Primitives on Bitcoin Cash, detailing the implementation of fungible and non-fungible tokens, token encoding, validation algorithms, and new VM opcodes.

**Sources**: cashtokens-spec.md

**Last updated**: 2026-04-18

---

The CashTokens specification introduces a consensus-layer upgrade to Bitcoin Cash that enables the creation and transfer of assets distinct from the native currency. It defines two primary primitives: **fungible tokens** and **non-fungible tokens (NFTs)** (source: cashtokens-spec.md).

## Core Primitives

### Fungible Tokens
- **Definition**: Undifferentiated units where groups can be freely divided and merged.
- **Supply**: All fungible tokens for a category are created at the category's genesis. The combined amount cannot exceed the maximum VM number (`9223372036854775807`).
- **Use Cases**: Representing shares, pegged assets, bonds, loans, and voting outcomes (source: cashtokens-spec.md).

### Non-Fungible Tokens (NFTs)
- **Definition**: Unique units containing a **commitment** (a byte string attested to by the issuer).
- **Capabilities**:
    - `none` (Immutable): Commitment cannot be modified when spent.
    - `mutable`: Allows the spending transaction to create one NFT of the same category with a new commitment.
    - `minting`: Allows the spending transaction to create any number of new NFTs of the same category.
- **Purpose**: Enabling contract-issued commitments, allowing contracts to "call" other contracts via impersonation-proof messages (source: cashtokens-spec.md).

## Technical Architecture

### Token Categories
Every token belongs to a **token category** identified by a 32-byte ID. The ID is the transaction ID of the outpoint spent to create the category (the genesis transaction). Specifically, only token genesis inputs (spending output 0 of their parent) are eligible (source: cashtokens-spec.md).

### Token Encoding
Tokens are encoded in outputs using a **token prefix** (`0xef`) inserted before the locking bytecode.
- **Format**: `PREFIX_TOKEN <category_id> <token_bitfield> [nft_commitment_length nft_commitment] [ft_amount]`
- **Bitfield**: Encodes the presence of an NFT, an amount of fungible tokens, and the NFT capability (source: cashtokens-spec.md).

### Token Validation Algorithm
Transactions must pass a validation check to ensure token integrity:
1. **Minting/Mutable Check**: New NFTs or mutable tokens can only be created if the spending transaction has appropriate capabilities or is the genesis transaction.
2. **Supply Check**: Fungible token output sums must not exceed input sums unless the category is being created (genesis) and remains within the maximum VM number.
3. **Immutable Check**: Immutable NFTs must be matched exactly by category and commitment unless a mutable token is spent to "downgrade" the requirement (source: cashtokens-spec.md).

## VM Integration

### Token Inspection Opcodes
Six new opcodes allow contracts to inspect tokens in inputs (UTXOs) and outputs:
- `OP_UTXOTOKENCATEGORY` / `OP_OUTPUTTOKENCATEGORY`: Retrieves the category ID (and capability).
- `OP_UTXOTOKENCOMMITMENT` / `OP_OUTPUTTOKENCOMMITMENT`: Retrieves the NFT commitment.
- `OP_UTXOTOKENAMOUNT` / `OP_OUTPUTTOKENAMOUNT`: Retrieves the fungible token amount (source: cashtokens-spec.md).

### Signing Serialization and `SIGHASH_UTXOS`
- **SIGHASH Enhancement**: The encoded token prefix is now included in the signing serialization immediately before the covered bytecode.
- **`SIGHASH_UTXOS` (0x20)**: A new signing type that includes a hash of all spent UTXOs, protecting against certain types of transaction manipulation, especially in multi-entity transactions (source: cashtokens-spec.md).

## Wallet and Address Support
Two new `CashAddress` type bits are introduced to signal token support:
- `2` (`0b0010`): Token-Aware P2PKH.
- `3` (`0b0011`): Token-Aware P2SH.
Token-aware wallets must refuse to send tokens to addresses lacking these explicit support bits to prevent accidental token loss (source: cashtokens-spec.md).

## Related pages

- [cashtokens](cashtokens.md)
- [cashtokens-intro](cashtokens-intro.md)
- [bitcoin-cash](bitcoin-cash.md)
- [script](script.md)
- [cashaddr](cashaddr.md)
