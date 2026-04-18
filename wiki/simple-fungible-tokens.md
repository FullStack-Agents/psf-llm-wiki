# simple-fungible-tokens

**Summary**: A practical guide to creating and managing fungible SLP tokens using the `psf-slp-wallet` command-line interface (CLI).

**Sources**: simple-fungible-tokens.md

**Last updated**: 2026-04-18

---

The creation and management of SLP tokens can be performed using the `psf-slp-wallet` CLI, which is the most comprehensive software for creating all SLP token types (Type 1, 65, 128), minting tokens, and attaching data (source: simple-fungible-tokens.md).

## Tooling: PSF SLP Wallet CLI

The `psf-slp-wallet` is an open-source tool that allows users to manage multiple wallets and tokens directly from a terminal environment (Ubuntu, Windows, macOS). It requires Node.js and npm for installation (source: simple-fungible-tokens.md).

### Basic Wallet Operations
- **Wallet Creation**: New wallets are created via the `wallet-create` command (source: simple-fungible-tokens.md).
- **Address Management**: Users can list wallets and retrieve their [Bitcoin Cash](bitcoin-cash.md) addresses to fund the wallet (source: simple-fungible-tokens.md).
- **Funding**: Because SLP transactions are standard [BCH](bitcoin-cash.md) transactions with `OP_RETURN` data, the wallet must be funded with a small amount of BCH to cover transaction fees (source: simple-fungible-tokens.md).

## Fungible Token Lifecycle

### 1. Token Creation
Fungible tokens are created using the `token-create-fungible` command. Key parameters include:
- **Decimals**: Defines the fractional precision of the token (e.g., 2 decimal places allow for `1.00`, `0.50`, etc.) (source: simple-fungible-tokens.md).
- **Quantity**: The initial amount of tokens created in the [slp-genesis](slp-genesis.md) transaction (source: simple-fungible-tokens.md).

### 2. Token Transfer
Tokens are transferred using the `send-tokens` command. To perform a transfer, the sender requires:
- The **Token ID**.
- The quantity of tokens to send.
- A **Simple Ledger address** (beginning with `simpleledger:`) from a token-aware wallet (source: simple-fungible-tokens.md).

## Safety and Compatibility
It is critical to use **token-aware wallets** when receiving tokens. Sending SLP tokens to an address in a wallet that is not SLP-aware can lead to the accidental burning of tokens, as the wallet may spend the UTXO without realizing it contains a token balance (source: simple-fungible-tokens.md).

## Related pages

- [simple-ledger-protocol](simple-ledger-protocol.md)
- [slp-intro](slp-intro.md)
- [slp-genesis](slp-genesis.md)
- [slp-send](slp-send.md)
- [bitcoin-cash](bitcoin-cash.md)
- [minimal-slp-wallet](minimal-slp-wallet.md)
