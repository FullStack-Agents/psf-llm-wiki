# Base58Check Encoding

**Summary**: A Base58 encoding format used in Bitcoin Cash to unambiguously encode data types via version bytes and ensure data integrity through a checksum.

**Sources**: base58check.md

**Last updated**: 2026-04-18

---

**Base58Check** is an encoding used for keys and addresses in Bitcoin Cash. It is designed to make information easier to copy and share (e.g., via QR codes) while preventing errors. Although supported, it is recommended to use [CashAddr](addresses.md) for addresses to avoid confusion with Bitcoin (BTC) addresses (source: base58check.md).

## Base58
Base58 is designed to avoid common copy errors by excluding visually similar characters. The excluded characters are `0` (zero), `O` (capital o), `I` (capital i), and `l` (lower-case L) (source: base58check.md).

**Alphabet**: `123456789ABCDEFGHJKLMNPQRSTUVWXYZabcdefghijkmnopqrstuvwxyz`

## Construction Process
Base58Check combines a **payload** and a **version byte** using the following steps:

1. **Concatenation**: `version || payload`
2. **Checksum Generation**: The checksum is the first four bytes of the double SHA-256 hash of the concatenation:
   `checksum = SHA256( SHA256( version || payload ) )[:4]`
3. **Final Concatenation**: `version || payload || checksum`
4. **Base58 Encoding**: The final result is encoded using the Base58 alphabet. Leading zero bytes are represented by the character `1` (source: base58check.md).

## Version Bytes
The version byte indicates the type of encoded data.

### Mainnet Version Bytes
| Type | Hex | Decimal | Base58 Prefix |
|---|---|---|---|
| P2PKH Address | `0x00` | 0 | `1` |
| P2SH Address | `0x05` | 5 | `3` |
| Private Key (WIF) | `0x80` | 128 | `5` |
| Private Key (WIF-compressed) | `0x80` | 128 | `K` or `L` |
| Extended Private Key | `0x0488ade4` | 76066276 | `xpub` |
| Extended Public Key | `0x0488b21e` | 76067358 | `xprv` |

### Testnet Version Bytes
| Type | Hex | Decimal | Base58 Prefix |
|---|---|---|---|
| Testnet P2PKH Address | `0x6f` | 111 | `m` or `n` |
| Testnet P2SH Address | `0xc4` | 196 | `2` |
| Testnet Private Key (WIF) | `0xef` | 239 | `9` |
| Testnet Private Key (WIF-compressed) | `0xef` | 239 | `c` |
| Testnet Extended Private Key | `0x043587cf` | 70617039 | `tpub` |
| Testnet Extended Public Key | `0x04358394` | 70615956 | `tprv` |

## Common Use Cases

### Wallet Import Format (WIF)
Private keys are typically encoded using Base58Check in the Wallet Import Format.
- **Uncompressed**: Always starts with `5` on mainnet.
- **Compressed**: To derive a compressed public key, a `0x01` prefix is added to the private key bytes before encoding. These always start with `K` or `L` on mainnet (source: base58check.md).

### Legacy Addresses
Addresses encoded with Base58Check are referred to as "legacy addresses." 
- **P2PKH**: Always starts with `1` on mainnet.
- **P2SH**: Always starts with `3` on mainnet.
*Caution: Using Base58Check for P2SH is discouraged to avoid accidental sends to SegWit addresses, which are not supported by Bitcoin Cash (source: base58check.md).*

## Related pages
- [addresses](addresses.md)
- [sha-256](sha-256.md)
- [private-keys](private-keys.md)
- [p2sh](p2sh.md)
