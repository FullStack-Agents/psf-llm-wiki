# Base58Check Encoding

**Summary**: A Base58 encoding format used in Bitcoin Cash to unambiguously encode data types via version bytes and ensure data integrity through a checksum.

**Sources**: base58check.md

**Last updated**: 2026-05-21

---

**Base58Check** is an encoding used for keys and addresses in Bitcoin Cash. It is designed to make information easier to copy and share (e.g., via QR codes) while preventing errors. Although supported, it is recommended to use [CashAddr](addresses.md) for addresses to avoid confusion with Bitcoin (BTC) addresses (source: base58check.md).

## Base58 Alphabet
Base58 is designed to avoid common copy errors by excluding visually similar characters. The excluded characters are `0` (zero), `O` (capital o), `I` (capital i), and `l` (lower-case L) (source: base58check.md).

**Alphabet**: `123456789ABCDEFGHJKLMNPQRSTUVWXYZabcdefghijkmnopqrstuvwxyz`

### Base58 Symbol Chart

| Value | Character | Value | Character | Value | Character | Value | Character |
| ----- | --------- | ------| --------- | ------| --------- | ------| --------- |
| 0     | 1         | 15    | G         | 30    | X         | 45    | n         |
| 1     | 2         | 16    | H         | 31    | Y         | 46    | o         |
| 2     | 3         | 17    | J         | 32    | Z         | 47    | p         |
| 3     | 4         | 18    | K         | 33    | a         | 48    | q         |
| 4     | 5         | 19    | L         | 34    | b         | 49    | r         |
| 5     | 6         | 20    | M         | 35    | c         | 50    | s         |
| 6     | 7         | 21    | N         | 36    | d         | 51    | t         |
| 7     | 8         | 22    | P         | 37    | e         | 52    | u         |
| 8     | 9         | 23    | Q         | 38    | f         | 53    | v         |
| 9     | A         | 24    | R         | 39    | g         | 54    | w         |
| 10    | B         | 25    | S         | 40    | h         | 55    | x         |
| 11    | C         | 26    | T         | 41    | i         | 56    | y         |
| 12    | D         | 27    | U         | 42    | j         | 57    | z         |
| 13    | E         | 28    | V         | 43    | k         |
| 14    | F         | 29    | W         | 44    | m         |

(source: base58check.md)

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

#### WIF Encoding Example
Given private key `1e99423a4ed27608a15a2616a2b0e9e52ced330ac530edcc32c8ffc6a526aedd`:
1. Prepend version byte `0x80` → `801e99423a4ed27608a15a2616a2b0e9e52ced330ac530edcc32c8ffc6a526aedd`
2. Compute double SHA-256 checksum → first 4 bytes: `c47e83ff`
3. Concatenate: `801e99423a4ed27608a15a2616a2b0e9e52ced330ac530edcc32c8ffc6a526aedd` + `c47e83ff`
4. Base58 encode → `5J3mBbAH58CpQ3Y5RNJpUKPE62SQ5tfcvU2JpbnkeyhfsYB1Jcn`

For compressed (WIF-compressed), append `0x01` to the private key before version byte prepending:
- Payload: `1e99423a4ed27608a15a2616a2b0e9e52ced330ac530edcc32c8ffc6a526aedd01`
- Encoded: `KxFC1jmwwCoACiCAWZ3eXa96mBM6tb3TYzGmf6YwgdGWZgawvrtJ`

(source: base58check.md)

### Legacy Addresses
Addresses encoded with Base58Check are referred to as "legacy addresses." 
- **P2PKH**: Always starts with `1` on mainnet.
- **P2SH**: Always starts with `3` on mainnet.

#### Legacy Address Encoding Example
Given a public key hash `211b74ca4686f81efda5641767fc84ef16dafe0b` (P2PKH):
1. Prepend version byte `0x00` → `00211b74ca4686f81efda5641767fc84ef16dafe0b`
2. Compute double SHA-256 checksum → first 4 bytes: `388c8d1d`
3. Concatenate: `00211b74ca4686f81efda5641767fc84ef16dafe0b` + `388c8d1d`
4. Base58 encode (leading zero `0x00` becomes prefix `1`) → `1424C2F4bC9JidNjjTUZCbUxv6Sa1Mt62x`

(source: base58check.md)

*Caution: Using Base58Check for P2SH is discouraged to avoid accidental sends to SegWit addresses, which are not supported by Bitcoin Cash (source: base58check.md).*

## Related pages
- [addresses](addresses.md)
- [sha-256](sha-256.md)
- [private-keys](private-keys.md)
- [p2sh](p2sh.md)
