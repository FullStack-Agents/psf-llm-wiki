# cashtoken-alternatives

**Summary**: Prior art and alternative token systems considered during the design of CashTokens, including PMv3, Bitauth, colored coin systems, SLP, and Unforgeable Groups.

**Sources**: CHIP-2022-02-CashTokens (cashtokens.org/docs/spec/alternatives.md)

**Last updated**: 2026-05-25

---

CashTokens was not designed in a vacuum. The specification builds on lessons from numerous prior token systems and proposals for Bitcoin and Bitcoin Cash. Below is a review of the key influences and alternatives (source: CHIP-2022-02-CashTokens alternatives.md).

## PMv3

The CashTokens CHIP builds on ideas behind **PMv3** (2021), a version 3 transaction format proposal for Bitcoin Cash. The CashToken primitives were identified and extracted from covenant applications designed for PMv3 transactions. The PMv3 proposal was withdrawn in favor of CashTokens (source: CHIP-2022-02-CashTokens alternatives.md).

## Bitauth

**Bitauth** (2016) is an identity resolution and message authentication protocol that uses transactions to define and update the signing requirements of identities. CashTokens' use of Transaction IDs as Token Category IDs is derived from Bitauth's identity resolution strategy, and the transferability of minting and mutable capabilities is derived from Bitauth's migration transactions (source: CHIP-2022-02-CashTokens alternatives.md).

## Colored Coins

Strategies for representing new asset types on Bitcoin are generally called **colored coin** systems. CashTokens differs from prior colored coin proposals by identifying **byte-string commitments** (NFTs) as the core primitive for dApp development, rather than focusing primarily on fungible tokens (source: CHIP-2022-02-CashTokens alternatives.md).

### OP_CHECKCOLORVERIFY (2013)
Proposed to verify that transactions cannot counterfeit the "coloring" of satoshis. Similar to CashTokens in its VM-focused approach but token units would have used satoshis (carrying monetary time value cost), and it would not have enabled cross-contract interfaces (source: CHIP-2022-02-CashTokens alternatives.md).

### Freimarkets (2013)
A comprehensive set of proposed changes including fungible tokens, token interest/demurrage, atomic exchanges, order matching, auctions, options, and numerous new opcodes. However, the magnitude of changes presented deployment obstacles and exposed new attack vectors requiring further analysis (source: CHIP-2022-02-CashTokens alternatives.md).

### Confidential Assets (2017)
Proposed blinding UTXO amounts and adding asset tags with concealed identifiers. Requires new transaction format and additional cryptographic algorithms. CashTokens maintains unblinded public auditability (source: CHIP-2022-02-CashTokens alternatives.md).

### OP_GROUP (2017)
Proposed redefining `OP_NOP4` to verify satoshi coloring, controlled by the public key used to derive the color identifier. Same limitations as OP_CHECKCOLORVERIFY (source: CHIP-2022-02-CashTokens alternatives.md).

### Group Tokenization (2018, 2021)
Expanded on OP_GROUP with unlimited minting, authorities, capabilities, authority migration transactions, and a new subsystem for script templates/covenants. CashTokens differs in enabling cross-contract interfaces and composable dApps with simpler constructions (source: CHIP-2022-02-CashTokens alternatives.md).

### Simple Ledger Protocol — SLP (2018)
The most widespread application-layer token system on Bitcoin Cash. SLP uses `OP_RETURN` data carrier outputs to associate tokens with transaction outputs, and includes an NFT standard (SLP NFT1, 2019). SLP transactions are **not validated by the network** — clients require indexing servers and client-side validation. CashTokens differs in being **network-validated** and enabling cross-contract interfaces and composable dApps (source: CHIP-2022-02-CashTokens alternatives.md).

### Unforgeable Groups
A colored coin proposal derived from Group Tokenization. CashTokens adopted the **output prefix codepoint strategy** from Unforgeable Groups to ensure backwards-compatible token encoding without requiring a new transaction format. Unforgeable Groups has since been updated to recommend the CashTokens primitives (source: CHIP-2022-02-CashTokens alternatives.md).

## Key Differentiator

Previous colored coin proposals focused primarily on fungible tokens, implementing NFTs as a fungible token category with supply of 1. This approach typically **fails to enable contract-issued commitments** and offers limited token-related functionality to contracts. CashTokens uniquely identifies byte-string commitments (NFTs) as the core primitive for advanced dApp development, with numeric commitments (fungible tokens) as a valuable but separate specialization (source: CHIP-2022-02-CashTokens alternatives.md).

## Related pages

- [cashtokens](cashtokens.md)
- [cashtokens-spec](cashtokens-spec.md)
- [cashtoken-rationale](cashtoken-rationale.md)
- [simple-ledger-protocol](simple-ledger-protocol.md)
- [slp-intro](slp-intro.md)
