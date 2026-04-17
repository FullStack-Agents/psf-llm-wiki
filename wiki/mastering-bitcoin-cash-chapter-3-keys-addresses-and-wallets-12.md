# mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-12

**Summary**: This document explains vanity addresses—addresses with human-readable patterns—and the computational effort required to generate them.

**Sources**: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_12.md

**Last updated**: 2026-04-17

---

Vanity addresses are valid [bitcoin-cash](bitcoin-cash.md) addresses that contain a specifically chosen, human-readable pattern of characters at the beginning.

### Generation Process
Creating a vanity [address](addresses.md) is a brute-force process: a software generates and tests billions of private keys until one produces an [address](addresses.md) containing the desired character pattern.
- **Computational Cost**: The difficulty increases exponentially with the length of the pattern. Each additional character increases the required work by a factor of 58 (the size of the Base58 alphabet).
- **Timeframe**: A 4-character pattern may take minutes, while a 7-character pattern could take months on a standard PC.

### Security Implications
- **Cryptographic Strength**: Vanity addresses are cryptographically identical to random addresses; they are not "weaker" or "stronger" in terms of encryption.
- **Forgery Resistance**: They can make it harder for attackers to substitute a legitimate [address](addresses.md) with a fraudulent one, as the attacker would also need to generate a convincing vanity pattern.
- **Risk**: Attackers can potentially create addresses that closely resemble a legitimate vanity [address](addresses.md) to deceive users.

## Related pages

- [addresses](addresses.md)
- [private-keys](private-keys.md)
