# slp-data

**Summary**: Overview of how data is attached to SLP tokens, distinguishing between mutable, immutable, and genesis data, and detailing the specifications and hosting mechanisms used.

**Sources**: slp-data.md

**Last updated**: 2026-04-18

---

The value of the Simple Ledger Protocol (SLP) is significantly enhanced by the ability to attach diverse types of data to tokens, allowing them to represent dynamic real-world assets or digital entities (source: slp-data.md).

## Data Types

SLP utilizes three distinct categories of data:

### 1. Genesis Data
Data written directly to the blockchain during the token creation process. This data is **immutable** and represents the token's foundation (source: slp-data.md).

### 2. Immutable Data
Data that is fixed at the time of token creation and can never be changed. This is used for permanent records (source: slp-data.md).

### 3. Mutable Data
Data that **can change over time**. This is the most versatile data type, enabling use cases such as:
- **Gaming**: Tracking a character's level or stats as they evolve.
- **Supply Chain**: Tracking a product's movement and status.
- **Content**: Linking to dynamic websites or social media content.
- **Software**: Containing code that interacts with other software (source: slp-data.md).

## Governance and Control

### The Mutable Data Address (MDA)
Mutable data is managed via a **Mutable Data Address (MDA)**, which is a standard [Bitcoin Cash](bitcoin-cash.md) address.
- **Pointer Mechanism**: The MDA acts as a pointer to the latest version of the data.
- **Auditability**: The blockchain records the transaction history of the MDA, creating an immutable and undeletable audit trail of every update (source: slp-data.md).
- **Control**: Only the holder of the MDA's private key can update the data. This ensures that creators can retain control over metadata (e.g., to enforce royalty contracts) even after the tokens themselves have been transferred (source: slp-data.md).

## Technical Specifications and Tooling

### Specifications
The standardization of token data is governed by several specifications:
- **PS002**: The core specification for attaching data to a token (source: slp-data.md).
- **PS007**: Defines a common schema for reading token data (source: slp-data.md).
- **PS011**: Defines a schema for the `userData` property to ensure cross-compatibility between different applications (source: slp-data.md).

### Libraries
- `slp-mutable-data`: The core JavaScript library for token data operations (source: slp-data.md).
- `[minimal-slp-wallet](minimal-slp-wallet.md)`: Provides high-level functions for reading token data (source: slp-data.md).

## Data Hosting and Scalability

To prevent blockchain bloat and ensure scalability, only the **Genesis Data** is stored on-chain.

**Mutable and Immutable data** are hosted off-chain, typically on [IPFS](https://ipfs.io). The [PSF File Pinning Protocol](https://psffpp.com/docs/intro/) was specifically developed to ensure this data is redundantly hosted across a decentralized network of computers at a low cost (source: slp-data.md).

## Related pages

- [fungible-with-data](fungible-with-data.md)
- [slp-intro](slp-intro.md)
- [simple-ledger-protocol](simple-ledger-protocol.md)
- [minimal-slp-wallet](minimal-slp-wallet.md)
- [bitcoin-cash](bitcoin-cash.md)
