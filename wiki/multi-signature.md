# Multi-signature

**Summary**: A security mechanism requiring a threshold of signatures (M-of-N) from a set of public keys to authorize a transaction, eliminating single points of failure and enabling complex spending conditions.

**Sources**: multisignature.md, mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets-8.md, mastering-bitcoin-cash_chapter-8-bitcoin-cash-security_9.md

**Last updated**: 2026-04-18

---

Multi-signature (multisig) requires multiple independent private keys to authorize a transaction, rather than a single signature. This allows users to divide responsibility for fund possession and increase security (source: multisignature.md).

### M-of-N Multisignature Scheme
In an **M-of-N** scheme, $N$ public keys are recorded in the script, and at least $M$ of those must provide valid signatures to unlock the funds (source: multisignature.md).

### Public Multisignature (`OP_CHECKMULTISIG`)
Public multisig is implemented using the `OP_CHECKMULTISIG` and `OP_CHECKMULTISIGVERIFY` opcodes in the Bitcoin Cash [scripting language](script.md) (source: multisignature.md).

#### Execution and the "Dummy" Element
A minimal locking script for multisig follows the format: `M <pubkey1> ... <pubkeyN> N CHECKMULTISIG`.

Historically, a "dummy" element was required in the unlocking script due to a bug where `OP_CHECKMULTISIG` consumed too many items from the stack. Following HF-20191115, this dummy element was repurposed as a trigger for signature algorithms (source: multisignature.md):

- **ECDSA Mode**: If the dummy element is `0`, all signatures must be ECDSA. The script matches signatures to public keys sequentially (source: multisignature.md).
- **Schnorr Mode**: If the dummy element is non-zero, it is interpreted as `checkbits`. This bitfield determines specifically which public keys should be checked against the provided signatures (source: multisignature.md).

#### Example: 2-of-3 Setup
In a 2-of-3 scheme with participants Alice, Bob, and Carol:
- **Locking Script**: `2 <pubkeyA> <pubkeyB> <pubkeyC> 3 CHECKMULTISIG`
- **Unlocking (ECDSA)**: `0 <sigA> <sigC>` (Dummy is 0)
- **Unlocking (Schnorr)**: `5 <sigA> <sigC>` (Dummy is 5, binary `0b101`, mapping signatures to Alice and Carol while skipping Bob) (source: multisignature.md).

### Private Multisignature (Schnorr Aggregation)
N-of-N multisig can be implemented without a dedicated multisig script by using the aggregation property of Schnorr signatures. By combining public keys into a single combined public key, parties can jointly create a signature that validates as a normal Schnorr signature for that combined key (source: multisignature.md).

### Applications and Benefits
- **Corporate Security**: Distributing keys among executives to prevent theft or loss of a single key (source: mastering-bitcoin-cash_chapter-8-bitcoin-cash-security_9.md).
- **Escrow**: Using a 2-of-3 setup with a buyer, seller, and arbitrator.
- **Redundancy**: Storing backup keys in different geographic locations for recovery (source: mastering-bitcoin-cash_chapter-8-bitcoin-cash-security_9.md).

## Related pages

- [private-keys](private-keys.md)
- [signatures](signatures.md)
- [script](script.md)
- [locking-script](locking-script.md)
- [digital-wallets](digital-wallets.md)
- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-8](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-8.md)
- [mastering-bitcoin-cash-chapter-8-security-9](mastering-bitcoin-cash-chapter-8-security-9.md)
