# cashscript-faq

**Summary**: Essential developer knowledge and troubleshooting Q&A for CashScript on Bitcoin Cash, curated from BCH developer Telegram channels.

**Sources**: BCH_Knowledge_Base (Knowledge-Base-V2/FAQ_DISTILLED.md)

**Last updated**: 2026-05-25

---

## Troubleshooting Common Errors

### "Locktime requirement not satisfied"
If using `tx.time` checks in your contract, you need to set the locktime with `txBuilder.setLocktime()` to match your contract's requirements. Try `setLocktime(0)` first to isolate the issue (source: BCH_Knowledge_Base FAQ_DISTILLED.md).

### "bad-txns-nonfinal, non-final transaction"
You set a blockheight as locktime which has not been reached yet. The transaction cannot be mined until the locktime is met. Check your `setLocktime()` value (source: BCH_Knowledge_Base FAQ_DISTILLED.md).

### "Script evaluated without error but finished with false/empty top stack element"
This is related to your contract logic, not the compiler. Ensure matching versions of `cashc` and `cashscript` SDK (v0.11+ recommended). Use `.debug()` to step through your contract logic in Bitauth IDE (source: BCH_Knowledge_Base FAQ_DISTILLED.md).

### Locktime fails even though time has passed
The blockchain uses "median time past" — a trailing measure because it's decentralized. When using `tx.time` with seconds-based locktime, the blockchain time can lag behind real-world time (source: BCH_Knowledge_Base FAQ_DISTILLED.md).

### "missing inputs"
Your transaction is missing one or more inputs. Check that you're correctly using `transactionBuilder.addInput(someUtxo, someUnlocker)`. Log your UTXO data before adding it (source: BCH_Knowledge_Base FAQ_DISTILLED.md).

## SDK Gotchas

### TransactionBuilder.addOutput() Format
Use an object parameter: `txb.addOutput({ to: address, amount: bigintValue })`. Don't pass separate arguments (source: BCH_Knowledge_Base FAQ_DISTILLED.md).

### Compiler/SDK Version Matching
`cashc` and `cashscript` must be on the same major version for debugging tooling to work properly (source: BCH_Knowledge_Base FAQ_DISTILLED.md).

### `txb.build()` is NOT async
`txb.build()` is synchronous — no need to await it. Use `txb.send()` for async broadcasting (source: BCH_Knowledge_Base FAQ_DISTILLED.md).

### TypeScript Recommended
CashScript is a TypeScript library with full type checking. Many errors that are difficult to debug in JavaScript are caught immediately by TypeScript (source: BCH_Knowledge_Base FAQ_DISTILLED.md).

## Language Clarifications

### Locktime: Block Number vs Timestamp
Values less than 500,000,000 are block numbers. Values 500,000,000 or higher are Unix timestamps. Set via `txBuilder.setLocktime()`, check in contract via `tx.time` (source: BCH_Knowledge_Base FAQ_DISTILLED.md).

### split() vs slice()
- `.split(N)` returns a tuple `(bytes, bytes)` — best for head/tail extraction.
- `.slice(start, end)` returns `bytes` directly — best for middle extraction.
- If you only need the first N bytes, use `.split(N)[0]`. If you only need bytes from the middle, use `.slice(start, end)` (source: BCH_Knowledge_Base FAQ_DISTILLED.md).

### Tuple Destructuring
Tuple destructuring must happen when declaring variables. You cannot assign a tuple to already declared variables. Structure code to declare at the point of splitting (source: BCH_Knowledge_Base FAQ_DISTILLED.md).

### No Global Constants (Yet)
Constants can only be defined within functions and get put on the stack. Global inlining at compile time is planned (source: BCH_Knowledge_Base FAQ_DISTILLED.md).

### Variable-Length Data in Bytestring
Use length-prefixed encoding: `toPaddedBytes(data.length, 1) + bytes(data)` — manually implementing what a push opcode does (source: BCH_Knowledge_Base FAQ_DISTILLED.md).

## CashTokens Specifics

### Leaving Out Token = Burning
If you have tokens in an input and don't include them in an output, they are permanently destroyed. Always account for all tokens (source: BCH_Knowledge_Base FAQ_DISTILLED.md).

### Checking NFT Capability
The capability is the 33rd byte of `tokenCategory`:
- `0x` (empty/absent) = no NFT or immutable NFT
- `0x01` = mutable NFT
- `0x02` = minting NFT
- Check `tx.inputs[i].tokenCategory.length > 32` to verify it's an NFT (source: BCH_Knowledge_Base FAQ_DISTILLED.md).

### Token Category Endianness
CashScript uses little endianness, explorers display big endianness. You may need to reverse byte order when comparing (source: BCH_Knowledge_Base FAQ_DISTILLED.md).

### ERC20 to CashTokens Mapping
Basic fungible functionality (create, transfer, query) uses native CashTokens — no contracts needed. For advanced features, create a CashScript wrapper (source: BCH_Knowledge_Base FAQ_DISTILLED.md).

## State Management

### Simulated State is Antipattern
Modifying constructor arguments to simulate state is now considered an antipattern. Store contract state externally in an NFT commitment. This keeps the contract address stable (source: BCH_Knowledge_Base FAQ_DISTILLED.md).

### No Global State
BCH does not have global state like Ethereum. Create a CashToken NFT and store data in its commitment (40 bytes now, 128 bytes May 2026). Your contract introspects this local transferrable state (source: BCH_Knowledge_Base FAQ_DISTILLED.md).

## Architecture

### Why No Global State?
It's an advantage — global state is bad for scalability. BCH uses the UTXO model where state is carried with tokens. You can achieve similar functionality with slightly different patterns (source: BCH_Knowledge_Base FAQ_DISTILLED.md).

### Why Use Contracts vs Server?
Smart contracts hold funds trustlessly — even the creator cannot access them. With a server, you control a key and can change code anytime. "Code as law" (source: BCH_Knowledge_Base FAQ_DISTILLED.md).

### Bitauth IDE Integration
Use `const uri = await transactionBuilder.getBitauthUri()` to open Bitauth IDE with CashScript source, compiled opcodes, and execution results (source: BCH_Knowledge_Base FAQ_DISTILLED.md).

## Upgrade Timeline

- **May 2025 (ACTIVE)**: VM Limits removal, 10,000-byte stack elements, BigInt support
- **May 2026 (UPCOMING)**: Native loops (`OP_BEGIN`/`OP_UNTIL`), 128-byte NFT commitments, P2S standard

## Related pages

- [cashscript-language](cashscript-language.md)
- [cashscript-security](cashscript-security.md)
- [cashscript-multi-contract](cashscript-multi-contract.md)
- [cashscript-sdk](cashscript-sdk.md)
- [cashtokens-spec](cashtokens-spec.md)
