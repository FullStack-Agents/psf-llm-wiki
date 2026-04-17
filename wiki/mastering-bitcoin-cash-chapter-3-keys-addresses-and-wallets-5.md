# mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-5

**Summary**: This document provides a technical deep dive into the secp256k1 elliptic curve used by Bitcoin Cash, including its equation and the properties of point addition and multiplication.

**Sources**: mastering-bitcoin-cash_chapter-3-keys-addresses-and-wallets_5.md

**Last updated**: 2026-04-17

---

Bitcoin Cash utilizes the **secp256k1** elliptic curve, defined by the equation $y^2 = (x^3 + 7) \pmod p$, where $p$ is a specific large prime number.

### Mathematical Properties
- **Finite Field**: The curve is defined over a finite field of prime order, meaning it consists of a discrete set of points rather than a continuous line.
- **Point Addition**: The sum of two points $P_1$ and $P_2$ is found by drawing a line through them and reflecting the intersection point across the x-axis.
- **Point Multiplication**: Defined as repeated addition ($kP$ is $P$ added to itself $k$ times). This efficiency in one direction and difficulty in reverse is what secures the network.

## Related pages

- [[private-keys]]
- [[transaction-scripts]]
