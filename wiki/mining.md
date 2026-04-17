# Mining

**Summary**: The process of verifying transactions and creating new Bitcoin Cash coins using computing power, transitioning from CPUs to specialized ASIC hardware.

**Sources**: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-(BCH)_2.md, mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_5.md

**Last updated**: 2026-04-16

---

Mining in Bitcoin Cash involves network participants competing to solve complex mathematical problems while processing transactions (source: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-(BCH)_2.md). It serves two essential functions: creating new coins through block rewards and establishing trust by requiring computational work to secure the [[blockchain]] (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_5.md).

### The Mining Process
Mining is a competitive race to solve a cryptographic puzzle that validates a block of transactions. This puzzle is asymmetrically difficult—hard to solve but easy to verify (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_5.md). 

Miners repeatedly hash the block header and a random number using the **SHA256 algorithm** until they find a solution matching a predetermined pattern. The first miner to find this solution publishes the block and claims the block reward.

### Hardware Evolution
Mining has evolved from using general-purpose CPUs to requiring specialized hardware for profitability:
- **ASICs**: Application-Specific Integrated Circuits designed specifically for Bitcoin Cash mining.
- **Mining Pools**: Miners often combine their computational resources into pools to share rewards proportionally.

### Difficulty Adjustment
The protocol includes algorithms that automatically adjust mining difficulty to ensure that a new block is created approximately every 10 minutes, regardless of the total processing power of the network (source: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-(BCH)_2.md).

## Related pages

- [[bitcoin-cash]]
- [[monetary-policy]]
- [[proof-of-work]]
- [[blockchain]]
- [[mastering-bitcoin-cash-chapter-1]]
- [[mastering-bitcoin-cash-chapter-2]]
