# bcmr-examples

**Summary**: Practical examples of Bitcoin Cash Metadata Registry (BCMR) implementations, demonstrating how to handle fungible tokens, NFT collections, dApp metadata, and asset migrations.

**Sources**: bcmr-examples.md

**Last updated**: 2026-04-18

---

The BCMR specification is illustrated through several common use cases, showing how metadata can be used to provide rich user interfaces and maintain historical records of on-chain assets (source: bcmr-examples.md).

## Key Use Case Examples

### Fungible Tokens and Rebranding
The `fungible-token.json` example demonstrates how an issuer manages a single fungible asset. It highlights the use of **Identity History** to track:
- **Redenomination**: Transitioning from one ticker symbol (`EXAMPLE`) and decimal precision (8) to another (`XAMPL`, 6 decimals).
- **Gradual Migration**: Using start and end timestamps to define a rebranding period, allowing wallets to show historical context to the user (source: bcmr-examples.md).

### NFT Art Collections
The `art-collection.json` example shows how to manage a collection of **sequential NFTs**.
- **Mapping**: Each NFT's commitment (a VM number) maps to a specific index in the registry.
- **Content Delivery**: Metadata for each NFT (e.g., `Example #0`) includes an icon published via **IPFS**, ensuring data integrity and availability (source: bcmr-examples.md).

### Decentralized Application (dApp) Metadata
The `decentralized-application.json` example illustrates the use of **parsable NFTs** to support complex dApp logic, such as crowdfunding.
- **Structured Data**: NFTs can contain specific fields (e.g., `Pledge Value`).
- **Aggregation**: The registry informs the wallet that these values are additive, allowing the UI to display a "Total BCH Pledged" sum across multiple NFTs (source: bcmr-examples.md).

### Payouts and Dividends
The `payouts-or-dividends.json` example demonstrates managing assets that evolve over time through payouts or re-issuances (e.g., equity or debt instruments).
- **Category Migration**: Shows how a token category `XAMPL-23Q1` is replaced by `XAMPL-23Q2` after a payout period.
- **Guidance**: The `migrate` URI provides users with instructions on how to exchange old tokens for new ones.
- **Future Planning**: The registry can include future-dated snapshots, enabling wallets to notify users of upcoming migrations before they occur (source: bcmr-examples.md).

## Related pages

- [bcmr-spec](bcmr-spec.md)
- [cashtokens](cashtokens.md)
- [cashtokens-spec](cashtokens-spec.md)
