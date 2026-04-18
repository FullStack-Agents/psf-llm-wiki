# slp-nft-1

**Summary**: Specification for the NFT1 protocol, an extension of SLP Token Type 1 that enables "grouped NFTs" by allowing multiple individual NFT child tokens to be associated with a single Group ID.

**Sources**: slp-nft-1.md

**Last updated**: 2026-04-18

---

The **NFT1 Protocol** is an extension of the [slp-token-type-1](slp-token-type-1.md) protocol specifically designed to support non-fungible tokens (NFTs) in a grouped manner. While a "simple NFT" can be created using Type 1 by minting a single indivisible token, NFT1 allows for a structured grouping of NFTs under a single Group ID, similar to the functionality of ERC-721 (source: slp-nft-1.md).

## NFT1 Architecture

NFT1 distinguishes between two types of tokens: **Group Minting Tokens** (Parents) and **NFT Child Tokens**.

### 1. NFT1 Group Minting Tokens (Parents)
These tokens serve as the "Group ID" and act as the resource required to create child NFTs.
- **Token Type**: The Token Type field must be set to `0x81` in all GENESIS, MINT, and SEND transactions (source: slp-nft-1.md).
- **Function**: The quantity of group tokens minted determines the maximum number of NFT children that can be created for that group (source: slp-nft-1.md).
- **Decimals**: It is recommended (though not strictly required) that decimals be set to 0 (source: slp-nft-1.md).

### 2. NFT1 Child Tokens
These are the individual NFTs that belong to a specific group.
- **Token Type**: The Token Type field must be set to `0x41` in all GENESIS and SEND transactions (source: slp-nft-1.md).
- **Creation Requirements**:
    - The GENESIS transaction must spend at least one valid NFT1 parent token (quantity > 0) at transaction input index 0 (source: slp-nft-1.md).
    - The GENESIS quantity must be exactly 1 (source: slp-nft-1.md).
    - Decimals must be set to 0 (source: slp-nft-1.md).
    - No minting baton is allowed (`baton vout` must be `0x4c00`) (source: slp-nft-1.md).

## Protocol Workflow

To create a group of NFTs:
1. **Create the Group**: Issue an SLP token designated as an NFT1 group minting token (Type `0x81`). This transaction's ID becomes the Group ID.
2. **Distribute Group Tokens**: Use a fan-out SEND transaction to break the group supply into multiple outputs (typically 1 token each) to enable the creation of multiple children.
3. **Mint Children**: Create individual NFT child tokens (Type `0x41`) by spending the group tokens in new GENESIS transactions (source: slp-nft-1.md).

## Wallet and Interface Implementation

### Transaction Handling
Wallets must strictly adhere to the Token Type fields when spending NFT1 tokens:
- Group tokens must be spent as type `0x81`.
- Child tokens must be spent as type `0x41`.
Using the wrong Token Type field in a SEND transaction will result in the token being burned (source: slp-nft-1.md).

### UI Recommendations
- **Grouping**: Wallets should display child tokens as a single line item per Group ID, which can then be expanded to show individual NFTs (source: slp-nft-1.md).
- **Distinction**: Group minting supply should be visually distinguished from the actual child tokens (source: slp-nft-1.md).
- **Metadata**: Child tokens may have unique names, tickers, and document URIs different from the parent group token (source: slp-nft-1.md).

## Related pages

- [slp-token-type-1](slp-token-type-1.md)
- [simple-ledger-protocol](simple-ledger-protocol.md)
- [slp-genesis](slp-genesis.md)
- [slp-send](slp-send.md)
