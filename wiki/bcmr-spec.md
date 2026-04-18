# bcmr-spec

**Summary**: Technical specification for Bitcoin Cash Metadata Registries (BCMR), a standard for sharing authenticated metadata about tokens, identities, and contract systems between Bitcoin Cash wallets.

**Sources**: bcmr-spec.md

**Last updated**: 2026-04-18

---

The Bitcoin Cash Metadata Registry (BCMR) standard provides a way to associate user-recognizable names, descriptions, icons, and ticker symbols with on-chain artifacts such as [cashtokens](cashtokens.md) and identities, ensuring that metadata can be verified and distributed in a decentralized, censorship-resistant manner (source: bcmr-spec.md).

## Registry Resolution and Authentication

Clients can acquire and authenticate metadata registries using three primary strategies:

### 1. DNS-Resolved Registries
Registries are associated with a Fully-Qualified Domain Name (FQDN) and accessed via a **Well-Known URI**: `https://<domain>/.well-known/bitcoin-cash-metadata-registry.json`. Trust is bootstrapped from the domain name.

### 2. Chain-Resolved Registries
Registries are associated with an **authbase** (a 32-byte TXID). This method offers stronger security and real-time updates:
- **Authchains (Zeroth-Descendant Transaction Chains)**: A chain of transactions where the output at index `0` of each transaction is spent by the next.
- **Authhead Transaction**: The final transaction in the chain, whose identity output is currently unspent.
- **Publication Outputs**: The authhead transaction contains a data-carrier output (`OP_RETURN <'BCMR'> <hash> [<uris>]`) that points to the registry's hash and its download location (IPFS or HTTPS) (source: bcmr-spec.md).

### 3. Embedded and Manually-Imported Registries
Client software may include a default embedded registry or allow users to manually import registries from files or URLs.

## Metadata Structure

BCMRs use an extensible JSON schema to map identities to their history.

### Identities and Snapshots
- **Authbase**: Every identity is uniquely identified by its authbase, serving as its root of trust.
- **Identity Snapshots**: Metadata is organized into snapshots associated with specific timestamps. A snapshot can include a name, description, and token-specific data (symbol, decimals, category).
- **Gradual Migration**: Using the `migrated` property, snapshots can define a transition period between two sets of metadata (source: bcmr-spec.md).

### Tags and URIs
- **Tags**: Allow classification of identities (e.g., `stablecoin`, `exchange`, `organization`).
- **URI Identifiers**: Standardized keys like `icon`, `web`, `blog`, and `support` point to authenticated resources. All URIs must be fully qualified (absolute) (source: bcmr-spec.md).

## Token and NFT Integration

### Ticker Symbols
- **Fungible Tokens**: Recommended base symbols are 4-6 characters.
- **NFTs**: Recommended base symbols are 6-13 characters to distinguish them from fungible tokens.
- **NFT Ticker Symbols**: The full symbol is a concatenation of the category symbol and a numeric or hex-encoded suffix based on the NFT type (source: bcmr-spec.md).

### NFT Rendering
Registries define how to interpret NFT commitments via the `NftCategory` definition:
- **Sequential NFTs**: The commitment is a VM number mapping to an index in `parse.types`.
- **Parsable NFTs**: The commitment contains encoded data a client can parse using provided `parse.bytecode` to extract specific fields (e.g., "Seat Number" or "BCH Pledged") (source: bcmr-spec.md).

## Extensions and Localization
- **Extensions**: Allow vendor-specific metadata.
- **Locales Extension**: Supports localized versions of metadata. Clients assemble a localized registry by inheriting from the most specific available locale, falling back to English (`en`) (source: bcmr-spec.md).

## Related pages

- [cashtokens](cashtokens.md)
- [cashtokens-spec](cashtokens-spec.md)
- [bitcoin-cash](bitcoin-cash.md)
- [cashaddr](cashaddr.md)
