# Signatures

**Summary**: Cryptographic proofs generated using a private key to authorize the spending of funds in a Bitcoin Cash transaction.

**Sources**: signatures.md

**Last updated**: 2026-04-18

---

Signatures are required for most Bitcoin Cash transactions to prove that the intended recipient (or owner) of the funds approves the transaction (source: signatures.md). A signature is generated using a [private key](private-keys.md) and can be verified using the corresponding public key.

Bitcoin Cash supports two primary signature algorithms: **ECDSA** and **Schnorr**.

### ECDSA Signatures
ECDSA (Elliptic Curve Digital Signature Algorithm), as defined in RFC 6979, uses three primary inputs: the private key, the message (a hash of the transaction preimage), and a random value $k$ (source: signatures.md).

- **Deterministic $k$**: It is recommended to use a deterministic $k$ value (per RFC 6979) to prevent private key leakage that can occur if the same $k$ is used for different messages (source: signatures.md).
- **LOW_S Rule**: Following HF-20171113, Bitcoin Cash enforces the "LOW_S" rule, requiring the lower of the two possible valid $s$ values to be used (source: signatures.md).

### Schnorr Signatures
Accepted since HF-20190515, Schnorr signatures provide an alternative to ECDSA and are generally more efficient (source: signatures.md).

- **Compatibility**: Existing public and private keys are valid for generating Schnorr signatures (source: signatures.md).
- **Implementation**: Bitcoin Cash uses the $(r, s)$ variant of Schnorr.
- **Recognition**: In scripts, 64-byte signatures passed to `OP_CHECKDATASIG`/`VERIFY` and 65-byte signatures passed to `OP_CHECKSIG`/`VERIFY` are interpreted as Schnorr signatures (source: signatures.md).

## Related pages

- [private-keys](private-keys.md)
- [transaction-signing](transaction-signing.md)
- [transaction-scripts](transaction-scripts.md)
- [bitcoin-cash-transactions](bitcoin-cash-transactions.md)
