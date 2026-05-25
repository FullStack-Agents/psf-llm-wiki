# cashscript-language

**Summary**: Reference for the CashScript smart contract language on Bitcoin Cash, covering type system, operators, built-in functions, global variables, and common patterns.

**Sources**: BCH_Knowledge_Base (language/language-reference.md, CORE_REFERENCE.md, concepts/utxo-vs-account-model.md)

**Last updated**: 2026-05-25

---

CashScript is a high-level language that compiles to Bitcoin Cash Script bytecode. It provides type safety, transaction introspection, and native [cashtokens](cashtokens.md) support for building decentralized applications on [bitcoin-cash](bitcoin-cash.md).

## The UTXO Mental Model

**This is NOT Ethereum.** Bitcoin Cash uses an Unspent Transaction Output (UTXO) model. A CashScript contract doesn't "do" anything — it only **validates** whether a proposed transaction meets its rules.

| Aspect | UTXO (CashScript/BCH) | Account (EVM/Solidity) |
|--------|----------------------|------------------------|
| State | No global state, independent atomic UTXOs | Global state tree, persistent storage |
| Execution | Transaction-level validation, stateless scripts | Contract-level execution, stateful |
| Concurrency | Parallel spending of different UTXOs | Sequential (nonce-based) |
| Persistence | UTXO chains, NFT commitments | Storage slots, state variables |
| Introspection | Full tx visibility (`tx.inputs[]`, `tx.outputs[]`) | Limited (`msg.sender`, `msg.value`) |
| Tokens | Native CashTokens (FT/NFT) | ERC-20/721 contract standards |
| Inter-Contract | Via multi-input transactions | `call`, `delegatecall` |
| Reentrancy | N/A (atomic transactions) | Vulnerable (requires guards) |
| Fees | Based on tx size (bytes) | Computational steps (gas) |

**The Core Question**: For every contract, ask: "What transformation of UTXOs does this contract permit?" Not "what does this contract do" but "what does this contract ALLOW to happen to itself?" (source: BCH_Knowledge_Base concepts/utxo-vs-account-model.md).

## Type System

| Type | Size | Operations | Methods | Conversions |
|------|------|-----------|---------|-------------|
| `bool` | 1 bit | `! && \|\| == !=` | - | `int(bool)` |
| `int` | Variable | `+ - * / % < <= > >= == !=` `<< >>` (May 2026) | - | `bytes(int)` `bool(int)` `toPaddedBytes(int, N)` |
| `string` | Variable | `+ == !=` | `.length` `.reverse()` `.split(i)` `.slice(s,e)` | `bytes(string)` |
| `bytes` | Variable | `+ == != & \| ^` `<< >> ~` (May 2026) | `.length` `.reverse()` `.split(i)` `.slice(s,e)` | - |
| `bytesN` | N bytes (1-64) | Same as bytes | Same as bytes | `unsafe_bytesN(bytes)` |
| `pubkey` | 33 bytes | `== !=` | - | Auto to bytes |
| `sig` | 65 (Schnorr) or 71-73 (ECDSA) | `== !=` | - | Auto to bytes |

**Common bytesN**: `bytes1` (byte), `bytes4` (prefix), `bytes20` (hash160), `bytes32` (sha256), `bytes64` (signature) (source: BCH_Knowledge_Base language/language-reference.md).

### Script Number Encoding

BCH Script uses sign-magnitude encoding: little-endian, MSB of last byte indicates sign. Minimal encoding required.

**Maximum positive values by byte size:**
- `bytes1`: 127 (2^7 - 1)
- `bytes2`: 32,767 (2^15 - 1)
- `bytes4`: 2,147,483,647 (2^31 - 1)
- `bytes8`: 9,223,372,036,854,775,807 (2^63 - 1)

Post-May 2025: BigInt support enables arbitrary precision up to 10,000 bytes (source: BCH_Knowledge_Base CORE_REFERENCE.md).

### `unsafe_` Casts

The `unsafe_` prefix means the compiler performs **no runtime checks or conversions**. Always comment why the cast is safe:

```cashscript
// SAFE: commitment is always 40 bytes (enforced by output constraints)
bytes40 commitment = unsafe_bytes40(tx.inputs[0].nftCommitment);
bytes20 ownerPkh = commitment.split(20)[0];  // bytes20 — compiler knows
bytes2 lockBlocks = commitment.split(38)[1]; // bytes2  — compiler knows
```

**When `unsafe_` is NOT needed:** After casting to bounded `bytesN`, all splits return bounded types. `split(literal)[0]` and `slice(literal, literal)` return bounded `bytesN`.
**When `unsafe_` IS needed:** Casting unbounded `bytes` to bounded type, `split(literal)[1]` on unbounded `bytes`, or `split(variable)` (source: BCH_Knowledge_Base CORE_REFERENCE.md).

## Operators

| Category | Operators | Valid Types | Notes |
|----------|-----------|-------------|-------|
| Arithmetic | `+ - * / %` | `int` | Integer only, div/0 fails |
| Comparison | `< <= > >= == !=` | `int` `bool` `bytes` `string` | - |
| Logical | `! && \|\|` | `bool` | **NO short-circuit** (all operands evaluated) |
| Bitwise | `& \| ^` | `bytes` (same size) | May 2026 adds `~ << >>` |
| Concatenation | `+` | `string` `bytes` | - |

**No compound assignment** — use `x = x + 1` not `x++` or `x += 1` (source: BCH_Knowledge_Base CORE_REFERENCE.md).

## Global Variables

### Transaction Properties
```cashscript
tx.time       // int: nLocktime (<500M=block height, ≥500M=Unix timestamp)
tx.version    // int: Transaction version
tx.locktime   // int: Locktime value
tx.inputs     // Input[]: Transaction inputs
tx.outputs    // Output[]: Transaction outputs
```

### Input/Output Properties
```cashscript
// Inputs and outputs share these:
.value              // int: BCH amount in satoshis
.lockingBytecode    // bytes: Script bytecode
.tokenCategory      // bytes: 32-byte ID + optional capability byte
.nftCommitment      // bytes: NFT data (current max 40 bytes, 128 in May 2026)
.tokenAmount        // int: Fungible token amount

// Inputs ONLY:
.outpointTransactionHash  // bytes32: UTXO source tx hash
.outpointIndex            // int: UTXO source output index
.unlockingBytecode        // bytes: scriptSig
.sequenceNumber           // int: nSequence value
```

### Contract Context
```cashscript
this.activeInputIndex  // int: Current input being evaluated
this.activeBytecode    // bytes: Current input's locking bytecode
this.age               // int: Relative UTXO age in blocks (SDK limitation)
```

### Locking Bytecode Constructors
```cashscript
new LockingBytecodeP2PKH(bytes20 pkHash)       // Pay to public key hash
new LockingBytecodeP2SH20(bytes20 scriptHash)  // Pay to script hash (20-byte, legacy)
new LockingBytecodeP2SH32(bytes32 scriptHash)  // Pay to script hash (32-byte, default)
new LockingBytecodeNullData([chunk1, chunk2])  // OP_RETURN data
```

(source: BCH_Knowledge_Base CORE_REFERENCE.md)

## Built-in Functions

| Function | Returns | Description |
|----------|---------|-------------|
| `abs(int)` | `int` | Absolute value |
| `min(int, int)` | `int` | Minimum of two |
| `max(int, int)` | `int` | Maximum of two |
| `within(int x, int lower, int upper)` | `bool` | `x >= lower && x < upper` (upper exclusive) |
| `sha256(any)` | `bytes32` | SHA-256 hash |
| `sha1(any)` | `bytes20` | SHA-1 hash |
| `ripemd160(any)` | `bytes20` | RIPEMD-160 hash |
| `hash160(any)` | `bytes20` | SHA-256 then RIPEMD-160 |
| `hash256(any)` | `bytes32` | Double SHA-256 |
| `checkSig(sig, pubkey)` | `bool` | Transaction signature. NULLFAIL: invalid=fail, empty=`false` |
| `checkMultiSig([sig,...], [pubkey,...])` | `bool` | Multi-sig. Inline arrays only. NOT in TypeScript SDK |
| `checkDataSig(datasig, bytes, pubkey)` | `bool` | Data signature. NULLFAIL applies |
| `bytes(any)` | `bytes` | Type conversion |
| `toPaddedBytes(int, int)` | `bytes` | Pads int to fixed-length bytes (v0.13+) |
| `unsafe_bytesN(bytes)` | `bytesN` | Semantic cast (v0.13+). No runtime check. |
| `unsafe_bool(int)` | `bool` | Semantic bool cast (v0.13+). No conversion. |

(source: BCH_Knowledge_Base language/language-reference.md)

## Token Category & Capabilities

`tokenCategory` is 33 bytes when capability is present: 32-byte categoryId + 1-byte flag.

| Capability | Byte | Description |
|------------|------|-------------|
| Immutable | `0x` (absent) | Cannot modify NFT commitment when spent |
| Mutable | `0x01` | Can modify commitment, downgrade to immutable |
| Minting | `0x02` | Can create unlimited NFTs, downgrade to mutable/immutable |

```cashscript
// Validate minting NFT
require(tx.inputs[0].tokenCategory == systemTokenId + 0x02);
// Validate mutable NFT
require(tx.inputs[1].tokenCategory == systemTokenId + 0x01);
// Extract category and capability
bytes category, bytes capability = tx.inputs[0].tokenCategory.split(32);
require(capability == 0x02);
```

## Byte Extraction: split() vs slice()

| Method | Returns | Use Case |
|--------|---------|----------|
| `.split(i)` | `(bytes, bytes)` tuple | Head/tail separation |
| `.slice(s, e)` | `bytes` | Extract from middle |

```cashscript
// split for START or END
bytes20 ownerPkh = commitment.split(20)[0];           // bytes20 — bounded
bytes2 suffix = unsafe_bytes2(commitment.split(38)[1]); // bytes2 — needs cast

// slice for MIDDLE (literal bounds → bounded)
bytes8 reserveBytes = commitment.slice(64, 72);  // bytes8 directly
int reserve = int(reserveBytes);

// RECOMMENDED: Cast commitment ONCE at read time
bytes40 c = unsafe_bytes40(tx.inputs[0].nftCommitment);
bytes20 owner = c.split(20)[0];  // bytes20
bytes4 suffix = c.split(36)[1];  // bytes4 (compiler knows: 40-36=4)
```

## Common Patterns

### Self-Replicating Covenant (5-Point Validation)
```cashscript
require(tx.outputs[0].lockingBytecode == tx.inputs[0].lockingBytecode);
require(tx.outputs[0].tokenCategory == tx.inputs[0].tokenCategory);
require(tx.outputs[0].value == expectedValue);
require(tx.outputs[0].tokenAmount == expectedAmount);
require(tx.outputs[0].nftCommitment == newCommitment);
```

### Output Count Limiting
```cashscript
// EVERY function MUST limit outputs — FIRST validation
require(tx.outputs.length <= 5);
```

### Time-Locked Release
```cashscript
function unlock() {
    require(tx.time >= lockTime);      // ALWAYS use >=, not >
    require(this.age >= requiredAge);  // Relative: blocks only
}
```

### Token-Gated Access
```cashscript
require(tx.inputs[1].tokenCategory == requiredCategory);
require(tx.inputs[1].tokenAmount >= minimumAmount);
```

### NFT Commitment Packing (40 bytes)
```cashscript
// Layout: userPkh(20) + reserved(18) + lockBlocks(2) = 40 bytes
require(tx.outputs[0].nftCommitment == userPkh + toPaddedBytes(0, 18) + toPaddedBytes(lockBlocks, 2));

// READ:
bytes40 commitment = unsafe_bytes40(tx.inputs[0].nftCommitment);
bytes20 storedPkh = commitment.split(20)[0];
bytes2 stakeBlocks = commitment.split(38)[1];
```

## VM Limits

**May 2025 (Active):**
- Stack element limit: 10,000 bytes (was 520)
- 201-opcode limit removed; replaced by operation cost system
- Operation cost budget: `(41 + unlocking_bytecode_length) × 800`
- BigInt support enabled

**May 2026 (Upcoming):**
- NFT commitment: 128 bytes (was 40)
- 10,000 bytes unlocking bytecode limit
- P2S becomes standard
- New opcodes: `<< >>` on int and bytes, `~` on bytes
- Native loops (`OP_BEGIN`/`OP_UNTIL`)

## Related pages

- [cashtokens-spec](cashtokens-spec.md)
- [cashtokens](cashtokens.md)
- [script](script.md)
- [transaction-script-language](transaction-script-language.md)
- [cashscript-security](cashscript-security.md)
- [cashscript-multi-contract](cashscript-multi-contract.md)
- [cashscript-sdk](cashscript-sdk.md)
- [bitcoin-cash](bitcoin-cash.md)
