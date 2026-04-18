# Transaction Signing

**Summary**: Transaction signing is the process of using asymmetric cryptography to secure Bitcoin Cash transactions, ensuring that only the authorized owners of funds (UTXOs) can spend them.

**Sources**: transaction-signing.md

**Last updated**: 2026-04-18

---

Transaction signatures prevent unauthorized spending by requiring the sender to generate a signature using their private key over a hash of the transaction data. This signature is then verified by any party with the corresponding public key, typically via `OP_CHECKSIG` or similar operations in a [locking script](locking-script.md).

## Signing Challenges and the Hash Type

Signing is complex because:
1. Transactions are identified by the hash of their full contents.
2. Signatures are themselves part of the transaction data.
3. Signatures are created from a hash of the transaction's data.

To avoid a circular dependency (where the signature changes the transaction hash, which would then invalidate the signature), the "signature preimage"—the data that is actually hashed and signed—does not include the full transaction data.

The [Hash Type](#hash-type) field (4 bytes) determines which parts of the transaction are included in the preimage:

- **SIGHASH_ALL (0x01)**: All outputs are included in the preimage.
- **SIGHASH_NONE (0x02)**: No outputs are included.
- **SIGHASH_SINGLE (0x03)**: Only the output with the same index as the input being signed is included.

### Special Hash Type Bits (Bitmasks)
- **SIGHASH_UTXOS (0x20)**: Includes a hash of the whole UTXOs being spent in the preimage. Introduced in HF-20230515 to commit to the entire input's prevouts.
- **SIGHASH_FORKID (0x40)**: Indicates the signature is for a Bitcoin Cash transaction. Required since BCH-UAHF to prevent replay attacks on the BTC chain.
- **SIGHASH_ANYONECANPAY (0x80)**: Only include information about the specific input being signed, allowing other inputs to be added without invalidating the signature.

## Bitcoin Cash Signature Process

BCH uses a modified version of the BIP143 digest algorithm to minimize redundant hashing and explicitly cover the input value.

### Signature Preimage
The preimage is a serialization of:
- Transaction version and locktime.
- Hashes of previous output identifiers, sequence numbers, and (if `SIGHASH_UTXOS` is set) the full content of previous outputs.
- The specific output being spent (ID, token contents, modified locking script, and value).
- The created transaction outputs (depending on the Hash Type).
- The signature hash type.

**Modified Locking Script**: For P2SH outputs, the redeem script is used instead of the locking script. In both cases, operations before the last `OP_CODESEPARATOR` are removed.

### Signature Formats

#### ECDSA Signatures
The traditional format using DER encoding. Structure:
`Magic Number (0x30) -> Length -> r (DER integer) -> s (DER integer) -> Hash Type (LSB)`.

#### Schnorr Signatures
Introduced in 2019, Schnorr signatures have a more fixed format:
`r (32 bytes) -> s (32 bytes) -> Hash Type (0-1 bytes)`.
(Hash type is omitted for `OP_CHECKDATASIG`).

## Contrast with Bitcoin Core (BTC)
Bitcoin Core signatures use a different preimage format:
1. They use the Modified Locking Script but replace the current input's script and empty all others.
2. They do **not** use `SIGHASH_FORKID`.
3. They primarily use the ECDSA format.

## Related pages

- [locking-script](locking-script.md)
- [transaction-scripts](transaction-scripts.md)
- [hash](hash.md)
- [utxo](utxo.md)
- [transaction-anatomy](transaction-anatomy.md)
