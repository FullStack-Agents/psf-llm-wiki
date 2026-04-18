# Simple Ledger Protocol (SLP)

**Summary**: A token system for the Bitcoin Cash network based on a "colored coins" design, allowing the creation, issuance, and transfer of digital tokens utilizing the BCH blockchain as a public ledger.

**Sources**: slp.md

**Last updated**: 2026-04-18

---

The **Simple Ledger Protocol (SLP)** is one of the most prevalent token systems on Bitcoin Cash (BCH). It enables users to create, issue, and transfer digital tokens that inherit the security model and network of the BCH blockchain (source: slp.md).

## Design and Mechanism

SLP utilizes a "colored coins" design, associating token amounts with BCH [transaction](transaction.md) outputs. It uses `OP_RETURN` [data outputs](locking-script.md) to include messages in four predefined formats to annotate transaction information:

- **GENESIS**: Defines the SLP token and issues the first batch of tokens ([slp-genesis](slp-genesis.md)) (source: slp.md).
- **MINT**: Issues further batches of tokens ([slp-mint](slp-mint.md)) (source: slp.md).
- **SEND**: Denotes the number of tokens sent to each output ([slp-send](slp-send.md)) (source: slp.md).
- **COMMIT**: Proposed for periodical commits of all transaction hashes on the token (source: slp.md).

## Consensus and Validation

### Consensus Rules
Every SLP transaction must have an output script starting with `OP_RETURN` (opcode 0x6a) in the first output (`vout=0`). 
- For **SEND** transactions, the sum of token outputs specified in `OP_RETURN` cannot exceed the sum of valid token inputs (source: slp.md).
- For **GENESIS/MINT** transactions, MINT requires a "baton input" from the Genesis or a previous Mint transaction (source: slp.md).

### Validation Process
Because invalid SLP transactions may still be valid BCH transactions, validation requires a **Directed Acyclic Graph (DAG)**. The DAG traces transaction inputs back to the original Mint or Genesis transaction (source: slp.md).

Optimizations for validation include:
- Pruning vertices of transactions that provide zero tokens.
- Caching DAG proofs.
- Stopping the process once the sum of proved valid inputs exceeds the output sum (source: slp.md).

## Advantages and Risks

### Advantages
- **Non-invasive**: Does not change Bitcoin Cash protocols; typical BCH nodes accept SLP transactions as normal (source: slp.md).
- **Security**: Uses the BCH security model; any attempt to double-spend SLP tokens would require double-spending the associated BCH outputs, which the network rejects (source: slp.md).

### Disadvantages and Risks
- **Token Loss**: Since tokens are spent when the associated BCH output is spent, users may accidentally lose SLP tokens if their wallet is unaware of the tokens or if an invalid SLP transaction is submitted (source: slp.md).
- **BCH Requirements**: Due to the "colored coins" design, outputs must stay above the dust threshold, and users must possess additional BCH satoshis to cover transaction fees (source: slp.md). This can be mitigated via "Postage services" (source: slp.md).

## Related pages

- [slp-token-protocol](slp-token-protocol.md)
- [transaction](transaction.md)
- [locking-script](locking-script.md)
- [bitcoin-cash](bitcoin-cash.md)
