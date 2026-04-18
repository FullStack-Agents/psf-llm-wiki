# Difficulty Adjustment Algorithm

**Summary**: The mechanism used by Bitcoin Cash to adjust the mining target and difficulty to maintain a consistent average block time of 10 minutes regardless of changes in network hashing power.

**Sources**: difficulty-adjustment-algorithm.md

**Last updated**: 2026-04-18

---

The **Difficulty Adjustment Algorithm (DAA)** corrects for fluctuations in the total hashing power of the Bitcoin Cash network. As hardware improves or nodes join or leave the network, the DAA adjusts the [target](proof-of-work.md) and [difficulty](proof-of-work.md) to ensure blocks are mined at a steady rate (source: difficulty-adjustment-algorithm.md).

To validate the blockchain, nodes must use the specific DAA that was active at the time a block was mined.

### Current and Historical Algorithms

The DAA has evolved over time. The algorithms, from newest to oldest, are:

#### ASERT (Absolutely Scheduled Exponentially Rising Targets)
Implemented as part of HF-20201115, ASERT uses an exponential moving average to target a 10-minute block time (source: difficulty-adjustment-algorithm.md).
- **Key Components**: The fork block (first block mined with ASERT), the anchor block (parent of the fork block), and the current head block.
- **Implementation**: To avoid floating-point discrepancies across platforms, ASERT is calculated using fixed-point integer arithmetic with a cubic polynomial approximation of the exponential (source: difficulty-adjustment-algorithm.md).

#### CW-144
Implemented in HF-20171113, CW-144 ties the difficulty of new blocks to the [chainwork](proof-of-work.md) performed over the most recent 144 blocks (source: difficulty-adjustment-algorithm.md).
- **Mechanism**: It evaluates the difference in chainwork between a "new" block (median of the 3 most recent) and an "old" block (median of blocks 144, 145, and 146 prior), adjusting for the time elapsed between them to project the work for the next block (source: difficulty-adjustment-algorithm.md).

#### Emergency DAA
Introduced during the BCH-UAHF to protect against abrupt drops in hashing power (source: difficulty-adjustment-algorithm.md).
- **Mechanism**: If the median time past (MTP) of the chain tip is 12 hours or more after the MTP 6 blocks prior, the target is increased by 25% (reducing difficulty by 20%) to keep the chain viable (source: difficulty-adjustment-algorithm.md).

#### Legacy DAA
The original Bitcoin algorithm used prior to BCH-UAHF (source: difficulty-adjustment-algorithm.md).
- **Mechanism**: Difficulty is adjusted every 2016 blocks. The new target is calculated by dividing the actual time taken to mine the previous 2015 blocks by the expected time (1,209,600 seconds), with a correction factor bounded between 0.25 and 4 (source: difficulty-adjustment-algorithm.md).

## Related pages

- [proof-of-work](proof-of-work.md)
- [mining](mining.md)
- [blockchain](blockchain.md)
