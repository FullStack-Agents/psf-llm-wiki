# cashscript-sdk

**Summary**: JavaScript/TypeScript SDK reference for the CashScript smart contract platform on Bitcoin Cash, covering contract instantiation, transaction building, token integration, and debugging.

**Sources**: BCH_Knowledge_Base (sdk/contracts/contract-instantiation.md, sdk/transactions/transaction-building.md, sdk/deployment/multi-contract-deployment.md, reference/quick-reference.md)

**Last updated**: 2026-05-25

---

The CashScript SDK provides JavaScript/TypeScript libraries for deploying and interacting with CashScript contracts on [bitcoin-cash](bitcoin-cash.md). It integrates with [cashtokens](cashtokens.md) natively and supports multi-contract transactions (source: BCH_Knowledge_Base sdk/contracts/contract-instantiation.md).

## Installation

```bash
npm install cashscript       # SDK
npm install -g cashc         # Compiler (optional)
```

## Basic Imports
```javascript
import { Contract, ElectrumNetworkProvider, SignatureTemplate, TransactionBuilder } from 'cashscript';
import { compileFile, compileString } from 'cashc';
```

## Contract Compilation

```javascript
// Compile from file
const artifact = compileFile('contract.cash');
// Compile from string
const artifact = compileString(contractCode);
// Import JSON artifact
import artifact from './contract.json' with { type: 'json' };
```

## Contract Instantiation

```javascript
const provider = new ElectrumNetworkProvider('mainnet');  // or 'chipnet'
const contract = new Contract(artifact, constructorArgs, { provider });

console.log('Address:', contract.address);
console.log('Balance:', await contract.getBalance());
```

**Contract type options:** `p2sh32` (default, most secure), `p2sh20` (legacy), `p2s` (direct script, more efficient, standard May 2026) (source: BCH_Knowledge_Base sdk/contracts/contract-instantiation.md).

## Transaction Building

### Simple Spend
```javascript
const sigTemplate = new SignatureTemplate(privateKey);
const contractUtxos = await contract.getUtxos();

const txDetails = await new TransactionBuilder({ provider })
    .addInput(contractUtxos[0], contract.unlock.spend(sigTemplate))
    .addOutput({ to: 'bitcoincash:qr...', amount: 100000n })
    .send();
```

### TransactionBuilder Options
```javascript
new TransactionBuilder({
    provider,                              // NetworkProvider (required)
    maximumFeeSatoshis: 2000n,             // Max fee safety check
    maximumFeeSatsPerByte: 2.0,            // Max fee per byte
    allowImplicitFungibleTokenBurn: false, // Default: false
})
```

### Multi-Input Transactions
```javascript
// Multiple different inputs
const txDetails = await new TransactionBuilder({ provider })
    .addInput(contractUtxo, contract.unlock.spend(contractSig))
    .addInput(userUtxo, userSig.unlockP2PKH())
    .addOutput({ to: bobAddress, amount: 100000n })
    .send();

// Share unlocker across inputs
const txDetails = await new TransactionBuilder({ provider })
    .addInputs(contractUtxos, unlocker)
    .addOutput({ to: recipientAddress, amount: 100000n })
    .send();
```

(source: BCH_Knowledge_Base sdk/transactions/transaction-building.md)

## Token Outputs

### Fungible Tokens
```javascript
const txDetails = await new TransactionBuilder({ provider })
    .addInput(contractUtxo, contract.unlock.transfer(sigTemplate))
    .addOutput({
        to: address,
        amount: 1000n,
        token: {
            category: tokenCategory,
            amount: 100n  // BigInt
        }
    })
    .send();
```

### NFTs
```javascript
const txDetails = await new TransactionBuilder({ provider })
    .addInput(contractUtxo, contract.unlock.mintNFT(sigTemplate))
    .addOutput({
        to: address,
        amount: 1000n,
        token: {
            category: tokenCategory,
            nft: {
                capability: 'mutable',  // 'none', 'mutable', 'minting'
                commitment: Buffer.from('data')
            }
        }
    })
    .send();
```

(source: BCH_Knowledge_Base sdk/transactions/transaction-building.md)

## Time Constraints
```javascript
const txDetails = await new TransactionBuilder({ provider })
    .addInput(contractUtxo, contract.unlock.spend(sigTemplate))
    .addOutput({ to: address, amount: amount })
    .setLocktime(1640995200)  // Unix timestamp
    .send();
```

## OP_RETURN Data
```javascript
const txDetails = await new TransactionBuilder({ provider })
    .addInput(contractUtxo, contract.unlock.spend(sigTemplate))
    .addOutput({ to: address, amount: amount })
    .addOpReturnOutput(['Hello, Bitcoin Cash!'])
    .send();
```

## Debugging

### Debug Mode
```javascript
const txBuilder = new TransactionBuilder({ provider })
    .addInput(utxo, contract.unlock.spend(sigTemplate))
    .addOutput({ to: address, amount: amount });

// Debug locally (returns intermediate values)
const debugResult = txBuilder.debug();

// Generate Bitauth URI for line-by-line opcode debugging
const uri = txBuilder.getBitauthUri();

// Build hex without broadcasting (synchronous)
const txHex = txBuilder.build();
```

### Fee Calculation
```javascript
const totalInput = txBuilder.inputs.reduce((s, i) => s + i.satoshis, 0n);
const totalOutput = txBuilder.outputs.reduce((s, o) => s + o.amount, 0n);
const feeSats = totalInput - totalOutput;
```

(source: BCH_Knowledge_Base sdk/transactions/transaction-building.md)

## Multi-Contract Deployment

When deploying a multi-contract system:
1. Deploy all contracts (get P2SH32 addresses)
2. Hardcode addresses in source where needed
3. Recompile with addresses
4. Create token category (genesis transaction)
5. Mint master NFTs for each contract
6. Send master NFTs to their contracts

**CRITICAL**: Contracts are **immutable after deployment**. All inter-contract addresses must be correct at compile time (source: BCH_Knowledge_Base sdk/deployment/multi-contract-deployment.md).

## Version Compatibility

| CashScript | Key Features |
|------------|-------------|
| `^0.13.0` | Loops, shift/`~` operators, `unsafe_` casts, `toPaddedBytes`, P2S support |
| `^0.12.0` | Removed old `contract.functions` builder |
| `^0.11.0` | BCH 2025 upgrade support, debug on optimized bytecode |
| `^0.9.0` | TransactionBuilder for multi-contract |
| `^0.8.0` | CashTokens support, P2SH32 |

Remember: `cashc` (compiler) and `cashscript` (SDK) should be on the **same major version**. The `contract.functions` simple builder was removed in v0.13.0 — use `TransactionBuilder` with `contract.unlock` instead (source: BCH_Knowledge_Base reference/quick-reference.md).

## Related pages

- [cashscript-language](cashscript-language.md)
- [cashscript-security](cashscript-security.md)
- [cashscript-multi-contract](cashscript-multi-contract.md)
- [cashtokens-spec](cashtokens-spec.md)
- [bchn-full-node](bchn-full-node.md)
