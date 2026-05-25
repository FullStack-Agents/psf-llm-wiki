# cashscript-security

**Summary**: Security patterns and vulnerability prevention for CashScript smart contracts on Bitcoin Cash, covering covenant validation, output limiting, minting authority protection, and cross-contract trust.

**Sources**: BCH_Knowledge_Base (best-practices/security/smart-contract-security.md, Knowledge-Base-V2/SECURITY_ARCHITECTURE.md)

**Last updated**: 2026-05-25

---

Smart contract security is critical when handling value on the [bitcoin-cash](bitcoin-cash.md) blockchain. CashScript contracts operate in the UTXO model with native [cashtokens](cashtokens.md) support, requiring unique security considerations compared to EVM-based chains (source: BCH_Knowledge_Base best-practices/security/smart-contract-security.md).

## The 5-Point Covenant Validation (MANDATORY)

For ANY self-replicating covenant, you MUST validate ALL five properties. Missing ANY creates critical vulnerabilities:

```cashscript
// 1. Same contract code (prevents code injection)
require(tx.outputs[0].lockingBytecode == tx.inputs[0].lockingBytecode);

// 2. Same token category (prevents category substitution)
require(tx.outputs[0].tokenCategory == tx.inputs[0].tokenCategory);

// 3. Expected satoshi value (prevents value extraction)
require(tx.outputs[0].value == expectedValue);

// 4. Expected token amount (prevents token extraction)
require(tx.outputs[0].tokenAmount == expectedTokenAmount);

// 5. Expected/new state commitment (prevents state manipulation)
require(tx.outputs[0].nftCommitment == newCommitment);
```

### Common Mistakes
**Missing lockingBytecode check**: Attacker can substitute the entire contract.
**Missing tokenCategory check**: Attacker can substitute the token with a different category.
**Missing value check**: Attacker can drain BCH from the contract.

| Covenant Type | What MUST Be Validated |
|--------------|------------------------|
| Exactly self-replicating | All 5 properties unchanged |
| State-mutating | 4 properties + valid new state |
| Balance-mutating | 3 properties + valid new value + valid new state |
| Conditionally-replicating | Full validation when replicating |

(source: BCH_Knowledge_Base SECURITY_ARCHITECTURE.md)

## Output Count Security (CRITICAL)

### The Minting Attack
Without output count limits, attackers can add unauthorized outputs to mint tokens:
1. Attacker creates a valid transaction satisfying contract constraints
2. Attacker adds extra outputs minting new tokens or NFTs
3. Contract validates expected outputs but ignores the extras

**EVERY contract function MUST limit output count as FIRST validation:**
```cashscript
function anyOperation() {
    // CRITICAL: ALWAYS include this first
    require(tx.outputs.length <= 5);
    // ... rest of logic
}
```

### Standard Output Limits
| Operation Type | Recommended Limit | Reason |
|---------------|-------------------|--------|
| Simple transfer | 3-4 | Input + output + change |
| Swap/exchange | 5-6 | Multiple participants |
| Complex DeFi | 7-10 | Multiple contracts + change |
| Batch operations | 15-20 | Multiple recipients |

(source: BCH_Knowledge_Base SECURITY_ARCHITECTURE.md)

## Minting Authority Control

### The Minting NFT Problem
Minting NFTs (capability `0x02`) can create unlimited tokens. If a minting NFT escapes to an untrusted address, the entire token system is compromised.

### Secure Patterns

**1. Never release minting NFT:**
```cashscript
// CRITICAL: Keep minting NFT in contract
require(tx.outputs[0].lockingBytecode == tx.inputs[0].lockingBytecode);
require(tx.outputs[0].tokenCategory == tx.inputs[0].tokenCategory);
```

**2. Downgrade to mutable when possible:**
```cashscript
require(tx.outputs[0].tokenCategory == category + 0x01); // Mutable only
```

**3. Burn minting authority when done:**
```cashscript
require(tx.outputs[destroyIdx].lockingBytecode == 0x6a);  // OP_RETURN
```

**4. Validate all outputs in transactions with minting contracts:** Every output's tokenCategory must be checked (source: BCH_Knowledge_Base SECURITY_ARCHITECTURE.md).

## Cross-Contract Trust & Position Validation

### Input Position Attacks
Without position validation, attackers can reorder inputs to bypass authentication.

**ALWAYS validate your position AND other contracts' positions:**
```cashscript
function operation() {
    // ALWAYS validate your own position first
    require(this.activeInputIndex == 2);

    // ALWAYS validate other contracts at expected positions
    require(tx.inputs[0].tokenCategory == oracleCategory + 0x01);
    require(tx.inputs[1].tokenCategory == mainCategory + 0x01);
}
```

### Same-Origin Verification
For sidecar/main contract pairs, verify they were created together:
```cashscript
function verifySidecar() {
    int mainIdx = this.activeInputIndex - 1;
    require(tx.inputs[this.activeInputIndex].outpointTransactionHash ==
            tx.inputs[mainIdx].outpointTransactionHash);
    require(tx.inputs[this.activeInputIndex].outpointIndex ==
            tx.inputs[mainIdx].outpointIndex + 1);
}
```

### Document Transaction Layouts
Always document input/output positions in function headers:
```cashscript
//////////////////////////////////////////////////////////////////////////////////////////
//inputs:
//  0   PriceOracle               [NFT]       (from PriceOracle contract)
//  1   MainContract              [NFT]       (from Main contract)
//  2   userBCH                   [BCH]       (from user)
//outputs:
//  0   PriceOracle               [NFT]       (to PriceOracle contract)
//  1   MainContract              [NFT]       (to Main contract)
//  2   userPayment               [BCH]       (to user)
//////////////////////////////////////////////////////////////////////////////////////////
```

(source: BCH_Knowledge_Base SECURITY_ARCHITECTURE.md)

## Critical Gotchas

### No Short-Circuit Evaluation
`&&` and `\|\|` evaluate ALL operands. Use separate `require()` statements:
```cashscript
// ✅ SAFE — separate statements
require(tx.outputs.length > 3);
require(tx.outputs[3].tokenCategory == 0x);
```

### Time Comparison — ALWAYS use `>=`
```cashscript
// ❌ WRONG
require(tx.time > lockTime);
// ✅ CORRECT
require(tx.time >= lockTime);
```

### NULLFAIL Rule
Passing an invalid signature to `checkSig()` fails the script — it doesn't return `false`:
```cashscript
// ❌ FAILS — one sig will be invalid for the other key
require(checkSig(userSig, seller) || checkSig(userSig, referee));
// ✅ SAFE — use 2 different sigs, set unused to 0x for false
require(checkSig(sellerSig, seller) || checkSig(refereeSig, referee));
```

### Bitwise Operations on bytes Only
```cashscript
// ❌ COMPILE ERROR — & on int
require((flags & 0x01) == 0x01);
// ✅ CORRECT — use bytes
bytes1 flags = 0x05;
require((flags & 0x01) == 0x01);
```

### Zero-Length TokenCategory Check
```cashscript
// Prevent tokens on output — require EMPTY category
require(tx.outputs[N].tokenCategory == 0x);
```

## Security Checklist (Pre-Deployment)

- [ ] All 5 covenant properties validated for self-replicating contracts
- [ ] Output count limited in ALL functions (first validation)
- [ ] Input positions validated with `this.activeInputIndex`
- [ ] All input contracts authenticated via `tokenCategory`
- [ ] Minting authority contained — never sent to user addresses
- [ ] Change outputs restricted to BCH-only or known tokens
- [ ] State byte layouts documented and validated
- [ ] Locktime uses `>=` not `>`
- [ ] Division by zero prevented
- [ ] Minimum amounts enforced
- [ ] Tested on testnet first; code audited by security experts

## Related pages

- [cashscript-language](cashscript-language.md)
- [cashscript-multi-contract](cashscript-multi-contract.md)
- [cashscript-sdk](cashscript-sdk.md)
- [cashtokens-spec](cashtokens-spec.md)
- [script](script.md)
