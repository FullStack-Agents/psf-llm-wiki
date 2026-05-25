# cashtokens-spec

**Summary**: Technical specification for Token Primitives on Bitcoin Cash, detailing the implementation of fungible and non-fungible tokens, token encoding, validation algorithms, and new VM opcodes.

**Sources**: CHIP-2022-02-CashTokens (cashtokens.org/docs/spec/chip.md)

**Last updated**: 2026-05-25

---

The CashTokens specification (CHIP-2022-02) introduces a consensus-layer upgrade to Bitcoin Cash that enables the creation and transfer of assets distinct from the native currency. It defines two primary primitives: **fungible tokens** and **non-fungible tokens (NFTs)** (source: CHIP-2022-02-CashTokens).

## Deployment & Activation

The specification was activated in the **May 2023 Bitcoin Cash upgrade**:
- **chipnet** activation: November 15, 2022 (MTP: `1668513600`)
- **mainnet, testnet3, testnet4, scalenet** activation: May 15, 2023 (MTP: `1684152000`)
- **Status**: Final (v2.2.2)
- **Maintainer**: Jason Dreyzehner

Multiple node implementations support CashTokens: Bitcoin Cash Node (BCHN), Bitcoin Verde, Bitcoin Unlimited, Flowee, Knuth, and BCHD (source: CHIP-2022-02-CashTokens).

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
Every token belongs to a **token category** identified by a 32-byte **Token Category ID**. The ID is the transaction ID of the outpoint spent to create the category in the **genesis transaction**. Specifically, only **token genesis inputs** — inputs which spend output `0` of their parent transaction — are eligible (i.e. outpoint transaction hashes with an outpoint index of `0`). This allows implementations to locate the genesis transaction of any category by finding the transaction that spent the 0th output of the transaction referenced by the category ID (source: CHIP-2022-02-CashTokens).

### Token Encoding

Tokens are encoded in outputs using a **token prefix** inserted before the locking bytecode. For backwards compatibility, the `CompactSize` length preceding the locking bytecode is increased to cover both fields.

#### Token Prefix Format

`PREFIX_TOKEN` is defined at codepoint `0xef` (`239`):

```
PREFIX_TOKEN <category_id> <token_bitfield> [nft_commitment_length nft_commitment] [ft_amount]
```

1. `<category_id>` – 32-byte **Token Category ID** in `OP_HASH256` byte order (source: CHIP-2022-02-CashTokens).
2. `<token_bitfield>` - A bitfield encoding two 4-bit fields:
   - **`prefix_structure`** (`token_bitfield & 0xf0`):
     - `0x80` - RESERVED, must be unset
     - `0x40` - HAS_COMMITMENT_LENGTH
     - `0x20` - HAS_NFT
     - `0x10` - HAS_AMOUNT
   - **`nft_capability`** (`token_bitfield & 0x0f`):
     - `0x00` - No capability (immutable)
     - `0x01` - Mutable capability
     - `0x02` - Minting capability
3. Commitment length (if HAS_COMMITMENT_LENGTH): minimally-encoded `CompactSize`, min `1`, max `40` bytes by consensus
4. Fungible token amount (if HAS_AMOUNT): minimally-encoded `CompactSize`, min `1`, max `9223372036854775807` (source: CHIP-2022-02-CashTokens).

#### Validation Rules
- A token prefix encoding no tokens (both HAS_NFT and HAS_AMOUNT unset) is invalid.
- HAS_COMMITMENT_LENGTH without HAS_NFT is invalid.
- If HAS_NFT is unset, nft_capability must be `0x00`.
- The commitment length is consensus-limited to `40` bytes, but implementers should parse up to `65535` for future upgrades (source: CHIP-2022-02-CashTokens).

#### Pre-Activation Token-Forgery Outputs (PATFOs)
Outputs mined before activation where locking bytecode index `0` is `0xef` are PATFOs. They remain nonstandard before activation and are **provably unspendable** after activation. This prevents forgery of token categories that don't map to confirmed transaction hashes (source: CHIP-2022-02-CashTokens).

### Token Validation Algorithm

For any transaction to be valid, the **token validation algorithm** must succeed. It operates on the following definitions:

**Inputs (Available):**
- `Available_Sums_By_Category` – sum of fungible token amounts from all input UTXOs
- `Available_Mutable_Tokens_By_Category` – count of input mutable NFTs per category
- `Genesis_Categories` – outpoint transaction hashes of inputs with outpoint index `0`
- `Input_Minting_Categories` – de-duplicated category IDs of input minting tokens
- `Available_Minting_Categories` – combination of Genesis_Categories and Input_Minting_Categories

**Outputs:**
- `Output_Sums_By_Category` – sum of fungible token amounts per category
- `Output_Mutable_Tokens_By_Category` – count of output mutable NFTs per category
- `Output_Minting_Categories` – de-duplicated category IDs of output minting tokens

**Validation checks:**

1. **Minting check**: Each output minting category must exist in Available_Minting_Categories (source: CHIP-2022-02-CashTokens).
2. **Fungible supply check**: Each output sum must either:
   - Have an equal or greater sum in Available_Sums_By_Category, **OR**
   - Exist in Genesis_Categories and not exceed `9223372036854775807` (source: CHIP-2022-02-CashTokens).
3. **Mutable check**: For each category in Output_Mutable_Tokens_By_Category, if the category exists in Available_Minting_Categories, skip. Otherwise, deduct from Available_Mutable_Tokens_By_Category. If it falls below `0`, fail (source: CHIP-2022-02-CashTokens).
4. **Immutable check**: For each output immutable NFT, if the category exists in Available_Minting_Categories, skip. Otherwise, try to match by (category, commitment) in Available_Immutable_Tokens. If no match, deduct from Available_Mutable_Tokens_By_Category. If none available, fail (source: CHIP-2022-02-CashTokens).

Note: Coinbase transactions can never include tokens (source: CHIP-2022-02-CashTokens).

## VM Integration

### Token Inspection Opcodes
Six new opcodes are introduced (codepoints `0xce` through `0xd3`). Each pops the top stack item as an input/output index (VM Number) and pushes a result. If the index is invalid or not minimally-encoded, an error is produced:

| Name | Codepoint | Description |
|------|-----------|-------------|
| `OP_UTXOTOKENCATEGORY` | `0xce` (206) | Pop input index. If UTXO has no tokens, push 0. If UTXO has no capability NFT, push category ID. If capability exists, push category + capability byte (`0x01` for mutable, `0x02` for minting) |
| `OP_UTXOTOKENCOMMITMENT` | `0xcf` (207) | Pop input index. Push UTXO's token commitment. If no NFT or zero-length commitment, push 0 |
| `OP_UTXOTOKENAMOUNT` | `0xd0` (208) | Pop input index. Push UTXO's fungible amount as VM Number. If none, push 0 |
| `OP_OUTPUTTOKENCATEGORY` | `0xd1` (209) | Pop output index. Same behavior as UTXOTOKENCATEGORY but for outputs |
| `OP_OUTPUTTOKENCOMMITMENT` | `0xd2` (210) | Pop output index. Same as UTXOTOKENCOMMITMENT but for outputs |
| `OP_OUTPUTTOKENAMOUNT` | `0xd3` (211) | Pop output index. Same as UTXOTOKENAMOUNT but for outputs |

Key design decisions:
- **Category + capability concatenation**: When capability is present, it's appended to the 32-byte category (1 byte). This makes the most secure validation (checking both) the default and cheaper than more lenient checks (source: CHIP-2022-02-CashTokens).
- **Zero-length commitments return 0**: This matches VM stack item behavior and saves bytes in many contracts. An output with no NFT and one with a zero-length immutable NFT both return 0 (source: CHIP-2022-02-CashTokens).
- **No impact on existing introspection opcodes**: `OP_UTXOBYTECODE`, `OP_ACTIVEBYTECODE`, and `OP_OUTPUTBYTECODE` continue to return only bytecode contents, excluding the token prefix (source: CHIP-2022-02-CashTokens).

### Signing Serialization and `SIGHASH_UTXOS`

- **Token prefix in signing serialization**: When evaluating a UTXO that includes tokens, the full encoded token prefix (including PREFIX_TOKEN) must be included immediately before the `coveredBytecode` (source: CHIP-2022-02-CashTokens).
- **`SIGHASH_UTXOS` (0x20/32)**: A new signing serialization type that inserts `hashUtxos` (double SHA256 of all spent UTXOs serialized as outputs) immediately after `hashPrevouts`. This protects against:
  - Unexpected fee burning
  - Unexpected token burning or theft
  - Unexpected actions in decentralized applications
- **Cannot combine** with `SIGHASH_ANYONECANPAY`; must be used with `SIGHASH_FORKID`. Wallets should enable `SIGHASH_UTXOS` when participating in multi-entity transactions (source: CHIP-2022-02-CashTokens).

### Fungible Token Supply Definitions

Several standardized supply measurements are defined for ecosystem compatibility. All values are capped at `9223372036854775807` (the maximum VM number):

#### Genesis Supply
An **immutable, easily-computed, maximum possible supply** known since the genesis transaction. Computed by summing the `amount` of fungible tokens matching the category ID in the genesis transaction's outputs (source: CHIP-2022-02-CashTokens).

#### Total Supply
The sum of tokens either in circulation or that may enter circulation. Computed by retrieving all UTXOs with the matching category ID, removing `OP_RETURN`-spent outputs, and summing remaining `amount`s. Emphasized in UIs for categories not meeting circulating-supply criteria (source: CHIP-2022-02-CashTokens).

#### Reserved Supply (Unissued Supply)
Tokens held in reserve by the issuing entity. Computed by summing `amount`s held in outputs with `minting` or `mutable` capability, excluding `OP_RETURN`-spent outputs (source: CHIP-2022-02-CashTokens).

#### Circulating Supply
Tokens not held in reserve. Computed as Total Supply - Reserved Supply. Emphasized in UIs for categories issued by trusted entities or covenants with verifiably-limited issuance (source: CHIP-2022-02-CashTokens).

### Token-Aware CashAddresses

Two new [CashAddress](cashaddr.md) types signal token acceptance:

| Type Bits | Meaning |
|-----------|---------|
| `2` (`0b0010`) | Token-Aware P2PKH |
| `3` (`0b0011`) | Token-Aware P2SH |

Token-aware wallets **must refuse** to send tokens to addresses without explicit token support (P2PKH type 0, P2SH type 1, and legacy Base58 addresses) (source: CHIP-2022-02-CashTokens).

### Token-Aware BIP69 Sorting

The BIP69 output sorting algorithm is extended: tokens sort after non-token outputs, then by amount, HAS_NFT flag, capability, commitment, and category (lexicographically, little-endian byte order) (source: CHIP-2022-02-CashTokens).

### Implementations

CashTokens is implemented in:
- **C++**: [Bitcoin Cash Node (BCHN)](https://bitcoincashnode.org/)
- **JavaScript/TypeScript**: [Libauth](https://github.com/bitauth/libauth)

See the [cashtokens.org test vectors](https://github.com/bitjson/cashtokens/tree/master/test-vectors) for comprehensive cross-implementation validation data (source: CHIP-2022-02-CashTokens).

## Wallet and Address Support
Two new `CashAddress` type bits are introduced to signal token support:
- `2` (`0b0010`): Token-Aware P2PKH.
- `3` (`0b0011`): Token-Aware P2SH.
Token-aware wallets must refuse to send tokens to addresses lacking these explicit support bits to prevent accidental token loss (source: cashtokens-spec.md).

## Related pages

- [cashtokens](cashtokens.md)
- [cashtokens-intro](cashtokens-intro.md)
- [cashtoken-rationale](cashtoken-rationale.md)
- [cashtoken-alternatives](cashtoken-alternatives.md)
- [cashtoken-stakeholders](cashtoken-stakeholders.md)
- [token-examples](token-examples.md)
- [bcmr-spec](bcmr-spec.md)
- [bitcoin-cash](bitcoin-cash.md)
- [script](script.md)
- [cashaddr](cashaddr.md)
