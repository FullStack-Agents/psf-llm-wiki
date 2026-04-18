# slp-intro

**Summary**: Introduction to the Simple Ledger Protocol (SLP), covering token types (fungible and non-fungible), the protocol's design philosophy of loose coupling, and its distinct address format.

**Sources**: slp-intro.md

**Last updated**: 2026-04-18

---

The **Simple Ledger Protocol (SLP)** is a protocol for creating tokens on UTXO blockchains, specifically focusing on Bitcoin Cash (BCH) and eCash (XEC) (source: slp-intro.md).

## Token Types

Tokens in SLP are categorized by their fungibility:

### Fungible Tokens
Units that are interchangeable. They are often referred to as **Type 1** tokens.
- **GENESIS**: Creates a new fungible token (source: slp-intro.md).
- **MINT**: Adds to the supply (source: slp-intro.md).
- **SEND**: Transfers ownership (source: slp-intro.md).
- **Mint Baton**: Used to mint an unlimited supply; if burned, the supply becomes finite (source: slp-intro.md).

### Non-fungible Tokens (NFTs)
Unique assets that are not interchangeable, supported via the **NFT1 specification**. Unlike Ethereum's ERC-721, SLP NFTs are represented by a UTXO on the blockchain and are not controlled by a smart contract (source: slp-intro.md).

*Note: A Type 1 fungible token can function as an NFT if the quantity is 1, the minting baton is burned, and decimal precision is 0 (source: slp-intro.md).*

## Design Philosophy and Loose Coupling

SLP is designed to be **permissionless, simple, robust, non-invasive, and extensible**. Its key technical advantage is being **loosely coupled** to the full node software.

The full node treats SLP transactions as standard BCH transactions with `OP_RETURN` data. Token validation is performed by a separate indexer rather than the full node itself (source: slp-intro.md).

### Comparison with Other Protocols
| Protocol | Issue | SLP Advantage |
| :--- | :--- | :--- |
| **Counterparty (BTC)** | Risk of core developer hostility | Loosely coupled; avoids dependency on core dev goodwill (source: slp-intro.md). |
| **Ethereum (ERC20)** | High transaction fees | More economically viable for businesses (source: slp-intro.md). |
| **Wormhole (BCH)** | Tight coupling to node fork | Avoids "ecosystem death" when node software diverges (source: slp-intro.md). |
| **CashTokens (BCH)** | Tight coupling to full node | Reduces platform risk; can be adapted to other blockchains (source: slp-intro.md). |

## Infrastructure and Scalability

### Risk of Burning
While miner-validated tokens (like CashTokens) prevent accidental burns, SLP tokens can be burned if outputs are improperly spent. However, mature tools like `[minimal-slp-wallet](minimal-slp-wallet.md)` and the PSF web wallet mitigate this risk (source: slp-intro.md).

### Scalability
The `[slp-token-indexer](slp-token-indexer.md)` allows for vertical and horizontal scaling. Operators can use a **blacklist** to ignore problematic tokens and reduce computational burden (source: slp-intro.md).

## SLP Address Format

To prevent users from accidentally spending token-bearing UTXOs in non-token-aware wallets, SLP uses a distinct address prefix:
- **Prefix**: `simpleledger:` (instead of `bitcoincash:`)
- **Example**: `simpleledger:qqmtw4c35mpv5rcjnnsrskpxvzajyq3f9ygldn8fj0` (source: slp-intro.md).

## Related pages

- [simple-ledger-protocol](simple-ledger-protocol.md)
- [slp-token-protocol](slp-token-protocol.md)
- [minimal-slp-wallet](minimal-slp-wallet.md)
- [slp-token-indexer](slp-token-indexer.md)
- [bitcoin-cash](bitcoin-cash.md)
