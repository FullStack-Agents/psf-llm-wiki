# cashscript-multi-contract

**Summary**: Production-grade patterns for building complex multi-contract systems with CashScript on Bitcoin Cash, including Main+Sidecar, Function Contracts, and Input Position Pinning patterns.

**Sources**: BCH_Knowledge_Base (concepts/multi-contract-architecture.md, concepts/cashscript-mental-model.md, examples/real-world/parityusd-analysis.md)

**Last updated**: 2026-05-25

---

Multi-contract systems on [bitcoin-cash](bitcoin-cash.md) require a fundamentally different architecture than EVM-based chains. Contracts cannot "call" each other — instead, multiple contracts must participate in the same transaction, with each validating its own constraints. **Multi-contract systems are transaction-structure problems, not code-flow problems** (source: BCH_Knowledge_Base concepts/multi-contract-architecture.md).

## The Fundamental Challenge

In the UTXO model:
- **No contract calls**: Contracts cannot invoke other contracts
- **One token category per output**: A UTXO can only hold tokens from one category
- **No global state**: State lives in NFT commitments carried by UTXOs
- **Coordination via transactions**: Multiple contracts participate in the same transaction

## Pattern 1: Main+Sidecar

**Problem**: A UTXO can only hold ONE token category. A contract managing both an NFT (state) and fungible tokens cannot hold both in a single UTXO.

**Solution**: Pair every "main" contract with a "sidecar" that holds additional tokens.

```
┌─────────────────┐      ┌─────────────────────┐
│   Main.cash     │      │  MainSidecar.cash   │
│   (NFT state)   │◄────►│  (fungible tokens)  │
└─────────────────┘      └─────────────────────┘
```

**The Attach Pattern** — Sidecar proves it belongs to the main contract:
```cashscript
contract TokenSidecar() {
    function attach() {
        int mainIndex = this.activeInputIndex - 1;
        // CRITICAL: Same transaction hash proves co-creation
        require(tx.inputs[this.activeInputIndex].outpointTransactionHash ==
                tx.inputs[mainIndex].outpointTransactionHash);
        // CRITICAL: Sequential indices proves ordering
        require(tx.inputs[this.activeInputIndex].outpointIndex ==
                tx.inputs[mainIndex].outpointIndex + 1);
        // Self-replicate
        require(tx.outputs[this.activeInputIndex].lockingBytecode ==
                tx.inputs[this.activeInputIndex].lockingBytecode);
        require(tx.outputs[this.activeInputIndex].value == 1000);
    }
}
```

(source: BCH_Knowledge_Base concepts/multi-contract-architecture.md)

## Pattern 2: Function Contracts (Modular Logic)

**Problem**: Complex contracts with many functions become hard to maintain and expensive (all code loaded even for single operations).

**Solution**: Split each logical "function" into a separate contract file, authenticated by NFT commitment bytes:

```
MainCoordinator.cash
   ├── functionA.cash     (NFT commitment prefix: 0x00)
   ├── functionB.cash     (NFT commitment prefix: 0x01)
   ├── functionC.cash     (NFT commitment prefix: 0x02)
   └── functionD.cash     (NFT commitment prefix: 0x03)
```

**Routing Pattern** — Main contract routes based on function identifier:
```cashscript
contract MainCoordinator(bytes32 systemTokenId) {
    function interact(int functionInputIndex) {
        bytes functionId = tx.inputs[functionInputIndex].nftCommitment.split(1)[0];
        require(tx.inputs[functionInputIndex].tokenCategory == systemTokenId + 0x01);

        if (functionId == 0x00) { /* Function A constraints */ }
        else if (functionId == 0x01) { /* Function B constraints */ }
    }
}
```

**Benefits**: Modularity, smaller transactions (only needed function included), independent auditability (source: BCH_Knowledge_Base concepts/multi-contract-architecture.md).

## Pattern 3: Strict Input Position Pinning

**Rule**: Every contract in a multi-contract transaction must know exactly which input index it occupies.

```cashscript
function myOperation() {
    require(this.activeInputIndex == 2);  // ALWAYS validate own position

    // Validate other contracts at expected positions
    require(tx.inputs[0].tokenCategory == oracleCategory + 0x01);
    require(tx.inputs[1].tokenCategory == mainCategory + 0x01);
    require(tx.inputs[3].tokenCategory == 0x); // Pure BCH
}
```

**Why**: Without position validation, attackers can reorder inputs to bypass authentication (source: BCH_Knowledge_Base concepts/multi-contract-architecture.md).

## Pattern 4: Token Category as Identity + Authority

Token categories encode BOTH identity and capability using deterministic offsets:

```cashscript
bytes32 systemTokenId = 0x1234...;

// Different contracts/NFTs use offsets:
// systemTokenId + 0x00 = immutable NFTs (receipts, proofs)
// systemTokenId + 0x01 = mutable NFTs (stateful contracts)
// systemTokenId + 0x02 = minting NFTs (highest authority)

// Authenticate price contract (mutable NFT)
require(tx.inputs[0].tokenCategory == systemTokenId + 0x01);
```

**Hierarchy of trust**: Minting → Mutable → Immutable (irreversible downgrades) (source: BCH_Knowledge_Base concepts/cashscript-mental-model.md).

## Pattern 5: The 5-Point Covenant Validation

For ANY self-replicating covenant in a multi-contract system, validate ALL of:

```cashscript
require(tx.outputs[idx].lockingBytecode == tx.inputs[idx].lockingBytecode); // Same code
require(tx.outputs[idx].tokenCategory == tx.inputs[idx].tokenCategory);     // Same token
require(tx.outputs[idx].value == expectedValue);                            // BCH amount
require(tx.outputs[idx].tokenAmount == expectedTokenAmount);                // Token amount
require(tx.outputs[idx].nftCommitment == newCommitment);                    // State
```

### Four Covenant Categories
| Type | What Changes | Example |
|------|--------------|---------|
| Exactly Self-Replicating | Nothing | Factory contracts, routers |
| State-Mutating | Only NFT commitment | Price oracles, counters |
| State-and-Balance-Mutating | NFT commitment + BCH value | Liquidity pools, treasuries |
| Conditionally-Replicating | Sometimes doesn't replicate | Loans (close on repayment) |

## Pattern 6: NFT Capability as State Machine

Token capabilities encode contract state:

```
MINTING (0x02)  →  MUTABLE (0x01)  →  IMMUTABLE (0x)
Active state        Stopped state       Final state
```

Use cases: Active campaign → cancelled campaign → receipt NFT (source: BCH_Knowledge_Base concepts/cashscript-mental-model.md).

## Transaction Layout Documentation

Before writing ANY code, document every transaction type:

```cashscript
//////////////////////////////////////////////////////////////////////////////////////////
// Operation: payInterest
//inputs:
//  0   PriceOracle               [NFT]       (from PriceOracle contract)
//  1   loan                      [NFT]       (from Loan contract)
//  2   loanSidecar               [NFT]       (from LoanSidecar contract)
//  3   payInterestFunction       [NFT]       (from PayInterest contract)
//  4   collectorBCH              [BCH]       (from collector)
//outputs:
//  0   PriceOracle               [NFT]       (to PriceOracle contract)
//  1   loan                      [NFT]       (to Loan contract)
//  2   loanSidecar               [NFT]       (to LoanSidecar contract)
//  3   payInterestFunction       [NFT]       (to PayInterest contract)
//  4   collectorPayment          [BCH]       (to collector)
//////////////////////////////////////////////////////////////////////////////////////////
```

## Deployment Checklist

1. **Deploy all contracts** — Get P2SH32 addresses
2. **Create token category** — Genesis transaction
3. **Hardcode addresses** — Embed in source where needed
4. **Recompile** — With embedded addresses
5. **Redeploy** — Final deployment with trust anchors
6. **Mint system NFTs** — Create master/function/sidecar NFTs
7. **Initialize positions** — Send NFTs to their contracts
8. **Test transactions** — Verify all positions work

**CRITICAL**: Contracts are **immutable after deployment**. All inter-contract addresses must be correct at compile time (source: BCH_Knowledge_Base concepts/multi-contract-architecture.md).

## Real-World Example: ParityUSD

The ParityUSD stablecoin system uses **26 CashScript contracts** organized into 4 domains:
- **Loan Module** (10 contracts): Main state holder + 8 function contracts + sidecar
- **LoanKey Module** (3 contracts): Factory, origin enforcer, origin proof
- **Redeemer Module** (3 contracts): Main redeemer + redemption + sidecar
- **Stability Pool Module** (8 contracts): Pool, collector, payout, 4 function contracts
- **Core** (2 contracts): Borrowing contract + price oracle

This demonstrates all patterns working together in production (source: BCH_Knowledge_Base examples/real-world/parityusd-analysis.md).

## Related pages

- [cashscript-language](cashscript-language.md)
- [cashscript-security](cashscript-security.md)
- [cashscript-sdk](cashscript-sdk.md)
- [cashtokens-spec](cashtokens-spec.md)
- [token-examples](token-examples.md)
