# fungible-with-data

**Summary**: An advanced guide to creating SLP fungible tokens with rich metadata, utilizing Mutable Data Addresses (MDA) and IPFS for storing token icons and dynamic information.

**Sources**: fungible-with-data.md

**Last updated**: 2026-04-18

---

Creating SLP tokens with rich, dynamic data allows for complex use cases such as tracking game characters or supply chain products. This is achieved by separating the token's value from its descriptive metadata (source: fungible-with-data.md).

## Token Data Concepts

SLP distinguishes between different types of data associated with a token:

### 1. Genesis Data
A small amount of fundamental data written directly to the blockchain at the moment of token creation (source: fungible-with-data.md).

### 2. Mutable Data
Data that **can change over time**. Common uses include:
- **Token Icons**: Visual identifiers for the token.
- **Dynamic Stats**: Tracking a character's attributes or a product's location (source: fungible-with-data.md).

### 3. Immutable Data
Data that **cannot be changed** once set. It is typically used for permanent records, such as original creator information or design intent (source: fungible-with-data.md).

### 4. Mutable Data Address (MDA)
The MDA is a specialized address that **controls the mutable data** for a token. 
- **Control**: The holder of the MDA's private key can update the token's metadata regardless of who owns the tokens themselves.
- **Pointer Mechanism**: The MDA acts as a pointer; updating it directs the protocol to a new version of the token's mutable data (source: fungible-with-data.md).

## Technical Workflow with `psf-slp-wallet`

To create a token with rich data, the following architectural steps are taken:

### Metadata Hosting (IPFS)
Metadata (such as token icons and JSON descriptions) is hosted on a decentralized network like IPFS. Each file is identified by a **Content ID (CID)**. The `ipfs://` prefix is used in SLP transactions to denote these references (source: fungible-with-data.md).

### Setting Up the MDA
1. **Separate Wallet**: It is best practice to use a dedicated wallet for the MDA, distinct from the token-holding wallet (source: fungible-with-data.md).
2. **Initialization**: The MDA is initialized on-chain via the `token-mda-tx` command. The resulting transaction ID is used as a "breadcrumb" to link the token to its mutable data (source: fungible-with-data.md).
3. **Linking**: The `token-update` command is used to point the MDA to a specific IPFS CID containing the mutable data JSON file (source: fungible-with-data.md).

### Creating the Token
The token is created using `token-create-fungible`, with two critical additional flags:
- `-u`: Specifies the IPFS CID of the **immutable data** (source: fungible-with-data.md).
- `-h`: Specifies the transaction hash (TxID) of the **MDA initialization**, linking the token to its mutable data stream (source: fungible-with-data.md).

## Updating Metadata
The primary advantage of the MDA system is that metadata can be updated after the token has been distributed. 
1. A new metadata file is uploaded to IPFS.
2. The MDA controller uses the `token-update` command to change the pointer to the new CID.
3. **Constraint**: Mutable data can only be updated **once per blockchain block** (source: fungible-with-data.md).

This process creates an immutable, auditable history of all metadata changes on the blockchain (source: fungible-with-data.md).

## Related pages

- [simple-fungible-tokens](simple-fungible-tokens.md)
- [slp-intro](slp-intro.md)
- [simple-ledger-protocol](simple-ledger-protocol.md)
- [bitcoin-cash](bitcoin-cash.md)
- [minimal-slp-wallet](minimal-slp-wallet.md)
