# SLP SEND Transaction

**Summary**: Detailed specification of the SLP SEND transaction, used to transfer tokens from one or more holding UTXOs to new recipients on the Bitcoin Cash network.

**Sources**: send.md

**Last updated**: 2026-04-18

---

The **SEND Transaction** is the mechanism used to transfer SLP tokens between users. When a SEND transaction is accepted by the blockchain, the UTXOs associated with the spent tokens (and their attached BCH) are considered totally spent (source: send.md).

## Transaction Mechanism

### Transaction Inputs
A SEND transaction can have any number of inputs. To be valid, these inputs must include sufficient tokens originating from valid token transactions that match the specific `token_id` and `token_type` being transferred (source: send.md).

### Transaction Outputs
Tokens are assigned to outputs based on the quantities specified in the `OP_RETURN` statement.

#### The OP_RETURN Output (vout=0)
The first output must be an `OP_RETURN` output containing the following data:
1. **Lokad ID**: `'SLP\x00'` (4 bytes).
2. **Token Type**: (1 to 2 byte integer).
3. **Transaction Type**: `'SEND'` (4 bytes).
4. **Token ID**: (32 bytes) The hash of the Genesis transaction for the token being sent.
5. **Token Output Quantities**: A sequence of up to 19 quantities (each an 8-byte integer) specifying how many base units are assigned to outputs `vout=1` through `vout=19` (source: send.md).

#### Token and BCH Outputs
- **Token Outputs (vout 1 to 19)**: Each output receives the quantity of tokens specified in the corresponding position of the `OP_RETURN` output (source: send.md).
- **BCH-only Outputs**: Any number of additional BCH-only outputs are allowed. If a BCH-only output appears before a token output, its associated token quantity in the `OP_RETURN` data must be specified as 0 (source: send.md).

## Related pages

- [simple-ledger-protocol](simple-ledger-protocol.md)
- [slp-genesis](slp-genesis.md)
- [transaction](transaction.md)
- [locking-script](locking-script.md)
