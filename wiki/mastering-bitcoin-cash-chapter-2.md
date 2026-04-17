# Mastering [Bitcoin Cash](bitcoin-cash.md) Chapter 2

**Summary**: A technical overview of how [Bitcoin Cash](bitcoin-cash.md) works, focusing on the interplay between users, wallets, transactions, miners, and the blockchain to establish trust in a decentralized system.

**Sources**: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_1.md, mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_2.md, mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_3.md, mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_4.md, mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_5.md, mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_6.md, mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_7.md, mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_8.md, mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_9.md, mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_10.md

**Last updated**: 2026-04-16

---

This chapter provides a deeper technical dive into the operational mechanics of [Bitcoin Cash](bitcoin-cash.md). It describes the system as one where trust is not centralized but emerges from the interactions between three primary entities: users, transactions, and miners (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_1.md).

## Core Interaction Model
The network operates through a continuous cycle:
1. **Users** utilize [digital-wallets](digital-wallets.md) and cryptographic keys to initiate transactions.
2. **Transactions** propagate across the peer-to-peer network to be verified by nodes.
3. **Miners** collect these transactions and use competitive computation to produce blocks.
4. **The Blockchain** acts as the final, authoritative ledger that records these blocks permanently.

This distributed consensus mechanism ensures that [Bitcoin Cash](bitcoin-cash.md) can operate securely without a central trusted authority.

## Transaction Mechanics
The chapter further details the structural "anatomy" of these transactions, explaining the role of inputs and outputs, the creation of a chain of ownership via digital signatures, and the derivation of miner fees from the difference between inputs and outputs (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_2.md).

It also explains the **construction process**, highlighting the role of [utxo](utxo.md) (Unspent Transaction Outputs) as the source of funds and how wallets query the network to identify available outputs to serve as transaction inputs (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_3.md).

Additionally, it covers the **propagation and validation** phase, explaining the "flooding" approach for rapid network distribution and the criteria nodes use to verify a transaction's validity and the pragmatic use of "zero confirmation" transactions for small payments (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_4.md).

## The Mining Process and Block Confirmation
The chapter explores the competitive nature of [mining](mining.md), describing the use of the SHA256 algorithm to solve cryptographic puzzles and the transition from CPU-based mining to the use of specialized ASIC hardware and mining pools (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_5.md).

It further details the **block creation process**, where miners select transactions from the [mempool](mempool.md) and include a "coinbase transaction" to claim a block reward (currently 12.5 [BCH](bitcoin-cash.md)). It explains how blocks build upon each other to provide confirmations, with six confirmations typically denoting irreversibility (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_6.md).

## The Distributed Ledger and Verification
The chapter concludes by explaining how transactions become part of the distributed ledger, creating an ongoing chain of ownership. It contrasts how full-index clients track the entire history of funds versus how lightweight clients use Simplified Payment Verification (SPV) to confirm transactions without a full copy of the blockchain (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_7.md).

## Wallet Management and Key Handling
The chapter also addresses the role of [digital-wallets](digital-wallets.md) in managing cryptographic keys and automating the transaction construction process. Notably, it mentions that transactions can be constructed offline and transmitted later, similar to a physical check (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_8.md).

## Forging and Consensus
The chapter explains the concept of "forging" a block and how the network achieves consensus. It details the requirement of solving a PoW puzzle and the use of the "longest chain" rule to resolve conflicts and maintain a single, authoritative blockchain (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_9.md).

## Visibility and Verification
The chapter introduces [blockchain-explorers](blockchain-explorers.md) as the primary tools for users to interact with the ledger, providing a transparent way to verify transactions, balances, and block details without needing to run a full node (source: mastering-bitcoin-cash_chapter-2-how-bicoin-cash-works_10.md).

## Related pages

- [bitcoin-cash](bitcoin-cash.md)
- [digital-wallets](digital-wallets.md)
- [transaction-process](transaction-process.md)
- [transaction-anatomy](transaction-anatomy.md)
- [utxo](utxo.md)
- [mining](mining.md)
- [blockchain](blockchain.md)
- [decentralization](decentralization.md)
- [forging-and-consensus](forging-and-consensus.md)
- [blockchain-explorers](blockchain-explorers.md)
