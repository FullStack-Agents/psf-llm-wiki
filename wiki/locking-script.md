# Locking Script

**Summary**: A locking script defines the conditions under which funds in a Bitcoin Cash output can be spent. It is executed after an unlocking script to verify the validity of a spend attempt.

**Sources**: locking-script.md

**Last updated**: 2026-04-18

---

A locking script is a [Script](transaction-script-language.md) that dictates how funds can be spent in the future by defining a set of operations that must result in a successful execution. The corresponding [unlocking script](transaction-scripts.md) is provided in a future transaction's input.

The unlocking script is executed first, followed by the locking script. This order prevents unlocking scripts from simply erasing the stack and replacing it with a success value.

## Standard Locking Scripts

Standard locking scripts are those recognized and relayed by nodes on the Bitcoin Cash network. While non-standard scripts can be mined, they are less likely to propagate widely.

### Pay to Public Key (P2PK)
The P2PK script requires the unlocking script to provide a signature valid for the public key specified in the locking script.

- **Operations**: `OP_DATA_X` (public key), `OP_CHECKSIG`.
- **Status**: Largely obsolete because it leaks the recipient's public key before the funds are spent, increasing data size and reducing privacy and security (e.g., against potential ECDSA breaks).

### Pay to Public Key Hash (P2PKH)
P2PKH uses a hash of the public key (an [address](addresses.md)) instead of the public key itself. This provides better privacy and security.

- **Operations**: `OP_DUP`, `OP_HASH160`, `OP_DATA_X` (20-byte address), `OP_EQUALVERIFY`, `OP_CHECKSIG`.
- **Process**: The unlocking script provides a signature and the public key. The script verifies the public key hashes to the correct address and the signature is valid.

### Pay to Script Hash (P2SH)
P2SH allows the spender to specify complex spending conditions in a "redeem script," which is hashed into a 20-byte address.

- **Operations**: `OP_HASH160`, `OP_DATA_X` (20-byte hash), `OP_EQUAL`.
- **Advantages**:
    - **Simple Addresses**: Recipients can provide a simple address regardless of the script complexity.
    - **Recipient-Centric**: The recipient chooses the spending criteria and pays the transaction fees upon redemption.
    - **Efficiency**: Reduces the size of the UTXO set by replacing large scripts with 20-byte hashes.
    - **Privacy**: The actual spending conditions are not revealed until the funds are spent.
- **Execution**: Nodes verify the redeem script's hash, then execute the redeem script itself against the stack.

### Multisig (P2MS)
Multisignature scripts allow multiple parties to coordinate spending. A specified number of signatures from a set of public keys is required.

- **Operations**: `OP_X` (required signatures), `OP_DATA_X` (public keys), `OP_X` (total keys), `OP_CHECKMULTISIG`.
- **Note**: A historical bug requires an extra value (typically `OP_0`) to be pushed before signatures.
- **Alternative**: These are "bare" multisig scripts; others are wrapped in P2SH (see [multi-signature](multi-signature.md)).

### Data Output
Used for adding arbitrary data to the blockchain rather than spending funds.

- **Operations**: `OP_RETURN` (causes immediate failure).
- **Properties**: Typically associated with zero satoshis and are provably unspendable.

## Related pages

- [transaction-script-language](transaction-script-language.md)
- [transaction-scripts](transaction-scripts.md)
- [addresses](addresses.md)
- [multi-signature](multi-signature.md)
- [p2sh](p2sh.md)
