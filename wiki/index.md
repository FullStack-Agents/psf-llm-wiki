# LLM Wiki Index

## Core Concepts
- [bitcoin-cash](bitcoin-cash.md): General overview of Bitcoin Cash.
- [blockchain-data-structure](blockchain-data-structure.md): The organization of the blockchain as a linked list.
- [blockchain-ledger](blockchain-ledger.md): The global double-entry bookkeeping system of BCH.
- [double-entry-bookkeeping](double-entry-bookkeeping.md): Principles of the double-entry system.
- [decentralization](decentralization.md): Principles of a decentralized network.
- [monetary-policy](monetary-policy.md): Rules governing the issuance of BCH.
- [proof-of-work](proof-of-work.md): The consensus mechanism to secure the network.
- [byzantine-generals-problem](byzantine-generals-problem.md): The coordination problem solved by PoW.
- [auditability](auditability.md): The ability to verify the blockchain's state.
- [double-spending](double-spending.md): The problem of spending the same coins twice.
- [utxo](utxo.md): Unspent Transaction Output; the fundamental unit of currency.

## Transactions
- [bitcoin-cash-transactions](bitcoin-cash-transactions.md): Overview of value transfer in BCH.
- [transaction-process](transaction-process.md): The lifecycle of a transaction.
- [transaction-anatomy](transaction-anatomy.md): Structure of transactions.
- [transaction-broadcasting](transaction-broadcasting.md): How transactions are sent across the network.
- [transaction-validation](transaction-validation.md): Node-level verification and propagation.
- [transaction-locktime](transaction-locktime.md): Mechanics of delaying transaction validity.
- [transaction-fees](transaction-fees.md): Compensation for miners and spam prevention.
- [transaction-chaining](transaction-chaining.md): Parent-child relationships between transactions.
- [orphan-transactions](orphan-transactions.md): Handling of child transactions arriving before parents.
- [coinbase-transaction](coinbase-transaction.md): The first transaction in a block.

## Scripting
- [transaction-scripts](transaction-scripts.md): Locking and unlocking scripts for spending funds.
- [transaction-script-language](transaction-script-language.md): The stack-based language for BCH scripts.
- [standard-transaction-types](standard-transaction-types.md): The five standard BCH transaction types.
- [p2sh](p2sh.md): Pay-to-Script-Hash mechanics and benefits.

## Infrastructure & Tools
- [asic](asic.md): Specialized hardware for SHA-256 mining.
- [blockchain-fork](blockchain-fork.md): Temporary splits in the blockchain.
- [genesis-block](genesis-block.md): The first block in the chain.
- [google-leveldb](google-leveldb.md): Key-value storage used by Bitcoin ABC.
- [merkle-root](merkle-root.md): Cryptographic summary of block transactions.
- [merkle-tree](merkle-tree.md): Binary hash tree for efficient data verification.
- [simplified-payment-verification](simplified-payment-verification.md): Lightweight transaction verification.
- [mempool](mempool.md): Storage for unconfirmed transactions.
- [sha-256](sha-256.md): The cryptographic hash function used by BCH.
- [mining](mining.md): Verification and block addition process.
- [clients](clients.md): Software implementations of the BCH protocol.
- [digital-wallets](digital-wallets.md): Software for managing keys and funds.
- [private-keys](private-keys.md): Cryptographic keys used for signing.
- [addresses](addresses.md): BCH address formats and derivation.
- [blockchain-explorers](blockchain-explorers.md): Tools for searching the blockchain.
- [technical-architecture](technical-architecture.md): High-level design of the BCH system.
- [bch-network-resilience](bch-network-resilience.md): Mechanisms ensuring network stability and adaptability.
- [bch-peer-management](bch-peer-management.md): Peer discovery, bootstrapping, and connectivity.
- [bchjs-network-commands](bchjs-network-commands.md): Network monitoring commands in bchjs.
- [bch-node-configuration](bch-node-configuration.md): Node configuration and peer overrides.
- [bitcoin-cash-network](bitcoin-cash-network.md): The communication infrastructure of Bitcoin Cash.
- [network-discovery](network-discovery.md): How nodes find and connect to each other.
- [blockchain-synchronization](blockchain-synchronization.md): How nodes catch up with the blockchain.
- [bloom-filters](bloom-filters.md): Privacy-preserving search for SPV nodes.
- [transaction-pools](transaction-pools.md): Management of unconfirmed transactions (mempools).
- [network-communication-protocol](network-communication-protocol.md): The message-based P2P protocol.

## Learning Materials
- [mastering-bitcoin-cash-chapter-1](mastering-bitcoin-cash-chapter-1.md): Introduction and core concepts.
- [mastering-bitcoin-cash-chapter-2](mastering-bitcoin-cash-chapter-2.md): How Bitcoin Cash works.
- [mastering-bitcoin-cash-chapter-2-how-bitcoin-cash-works-11](mastering-bitcoin-cash-chapter-2-how-bitcoin-cash-works-11.md): Supplementary material on how BCH works.
- [mastering-bitcoin-cash-chapter-6-1](mastering-bitcoin-cash-chapter-6-1.md): Blockchain data structure, genesis block, and immutability.
- [mastering-bitcoin-cash-chapter-6-2](mastering-bitcoin-cash-chapter-6-2.md): Block structure, headers, and identification.
- [mastering-bitcoin-cash-chapter-6-3](mastering-bitcoin-cash-chapter-6-3.md): Genesis block properties and block linking.
- [mastering-bitcoin-cash-chapter-6-4](mastering-bitcoin-cash-chapter-6-4.md): Merkle tree fundamentals and transaction verification.
- [mastering-bitcoin-cash-chapter-6-5](mastering-bitcoin-cash-chapter-6-5.md): Merkle path efficiency and validation.
- [mastering-bitcoin-cash-chapter-6-6](mastering-bitcoin-cash-chapter-6-6.md): Simplified Payment Verification (SPV) and lightweight clients.
- [mastering-bitcoin-cash-chapter-5-1](mastering-bitcoin-cash-chapter-5-1.md): Introduction to the Bitcoin Cash P2P network.
- [mastering-bitcoin-cash-chapter-5-network-resilience](mastering-bitcoin-cash-chapter-5-network-resilience.md): Deep dive into network resilience.
- [mastering-bitcoin-cash-chapter-5-2](mastering-bitcoin-cash-chapter-5-2.md): Node types and roles.
- [mastering-bitcoin-cash-chapter-5-3](mastering-bitcoin-cash-chapter-5-3.md): Network discovery process.
- [mastering-bitcoin-cash-chapter-5-4](mastering-bitcoin-cash-chapter-5-4.md): Blockchain synchronization.
- [mastering-bitcoin-cash-chapter-5-5](mastering-bitcoin-cash-chapter-5-5.md): Simplified Payment Verification (SPV).
- [mastering-bitcoin-cash-chapter-5-6](mastering-bitcoin-cash-chapter-5-6.md): Bloom filters for SPV privacy.
- [mastering-bitcoin-cash-chapter-5-7](mastering-bitcoin-cash-chapter-5-7.md): Bloom filter operation with SPV.
- [mastering-bitcoin-cash-chapter-5-8](mastering-bitcoin-cash-chapter-5-8.md): Transaction pools and orphans.
- [mastering-bitcoin-cash-chapter-5-9](mastering-bitcoin-cash-chapter-5-9.md): The UTXO database.
- [mastering-bitcoin-cash-chapter-5-10](mastering-bitcoin-cash-chapter-5-10.md): Network communication flow.
- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-2](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-2.md): Keys and addresses.
- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-3](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-3.md): Wallet mechanics.
- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-4](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-4.md): Advanced key management.
- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-5](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-5.md): Addressing.
- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-6](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-6.md): Script basics.
- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-7](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-7.md): Complex scripts.
- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-8](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-8.md): Multi-sig.
- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-9](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-9.md): P2SH.
- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-10](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-10.md): P2SH details.
- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-11](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-11.md): Script execution.
- [mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-12](mastering-bitcoin-cash-chapter-3-keys-addresses-and-wallets-12.md): Practical examples.
- [mastering-bitcoin-cash-transactions-1](mastering-bitcoin-cash-transactions-1.md): Transaction fundamentals and lifecycle.
- [mastering-bitcoin-cash-transactions-2](mastering-bitcoin-cash-transactions-2.md): Transaction creation, broadcasting, and validation.
- [mastering-bitcoin-cash-transactions-3](mastering-bitcoin-cash-transactions-3.md): Transaction structure and locktime.
- [mastering-bitcoin-cash-transactions-4](mastering-bitcoin-cash-transactions-4.md): UTXO fundamentals and the account-less model.
- [mastering-bitcoin-cash-transactions-5](mastering-bitcoin-cash-transactions-5.md): Transaction inputs and outputs structure.
- [mastering-bitcoin-cash-transactions-6](mastering-bitcoin-cash-transactions-6.md): Transaction fee mechanics and implications.
- [mastering-bitcoin-cash-transactions-7](mastering-bitcoin-cash-transactions-7.md): Transaction chaining and orphan transactions.
- [mastering-bitcoin-cash-transactions-8](mastering-bitcoin-cash-transactions-8.md): Transaction script language and limitations.
- [mastering-bitcoin-cash-transactions-9](mastering-bitcoin-cash-transactions-9.md): Standard transaction types (P2PKH, P2PK, etc).
- [mastering-bitcoin-cash-transactions-10](mastering-bitcoin-cash-transactions-10.md): Detailed look at Pay-to-Script-Hash (P2SH).
- [mastering-bitcoin-cash-transactions-11](mastering-bitcoin-cash-transactions-11.md): Practical script execution and P2PKH validation.

## Miscellaneous
- [use-cases](use-cases.md): Practical applications of Bitcoin Cash.
- [acquiring-bch](acquiring-bch.md): How to obtain BCH.
- [forging-and-consensus](forging-and-consensus.md): How the network agrees on the state.
