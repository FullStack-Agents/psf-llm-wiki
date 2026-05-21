# bcmr-spec

**Summary**: Technical specification for Bitcoin Cash Metadata Registries (BCMR), a standard for sharing authenticated metadata about tokens, identities, and contract systems between Bitcoin Cash wallets.

**Sources**: bcmr-spec.md

**Last updated**: 2026-05-21

---

The Bitcoin Cash Metadata Registry (BCMR) standard provides a way to associate user-recognizable names, descriptions, icons, and ticker symbols with on-chain artifacts such as [cashtokens](cashtokens.md) and identities, ensuring that metadata can be verified and distributed in a decentralized, censorship-resistant manner (source: bcmr-spec.md).

## Registry Resolution and Authentication

Clients can acquire and authenticate metadata registries using three primary strategies:

### 1. DNS-Resolved Registries
Registries are associated with a Fully-Qualified Domain Name (FQDN) and accessed via a **Well-Known URI**: `https://<domain>/.well-known/bitcoin-cash-metadata-registry.json`. Trust is bootstrapped from the domain name.

### 2. Chain-Resolved Registries
Registries are associated with an **authbase** (a 32-byte TXID). This method offers stronger security and real-time updates:
- **Authchains (Zeroth-Descendant Transaction Chains)**: A chain of transactions where the output at index `0` of each transaction is spent by the next. The first transaction is the **authbase**, the final unspent is the **authhead**.
- **Authhead Transaction**: The final transaction in the chain, whose identity output is currently unspent.
- **Publication Outputs**: The authhead transaction contains a data-carrier output (`OP_RETURN <'BCMR'> <hash> [<uris>]`) that points to the registry's hash and its download location (IPFS or HTTPS).
- **Burned Identities**: If the authhead's identity output is an `OP_RETURN`, the identity is "burned" — the owner signals it is no longer maintained (source: bcmr-spec.md).

### 3. Embedded and Manually-Imported Registries
Client software may include a default embedded registry or allow users to manually import registries from files or URLs.

## Metadata Structure

BCMRs use an extensible JSON schema to map identities to their history.

### Identities and Snapshots
- **Authbase**: Every identity is uniquely identified by its authbase, serving as its root of trust.
- **Identity Snapshots**: Metadata is organized into snapshots associated with specific timestamps. A snapshot can include a name, description, and token-specific data (symbol, decimals, category).
- **Gradual Migration**: Using the `migrated` property, snapshots can define a transition period between two sets of metadata (source: bcmr-spec.md).

### Publication Output Specification

Chain-resolved registries use data-carrier outputs with locking bytecode prefix `OP_RETURN <'BCMR'>` (`0x6a0442434d52`). The structure is:

`OP_RETURN <'BCMR'> <sha256-hash> [<uri> <uri> ...]`

- **Hash**: SHA-256 of the registry content (OP_SHA256 byte order — little-endian like block headers)
- **URIs**: Zero or more download locations. Clients must support HTTPS and IPFS protocols.
- Each transaction may have at most one publication output (first match is definitive).

**HTTPS**: Bare domain (e.g. `example.com`) resolves to the Well-Known URI. A trailing slash (e.g. `test.example.com/`) means root path.

**IPFS**: Must use `ipfs://` prefix. Clients without a full IPFS node may use HTTP gateways (e.g. `cf-ipfs.com`). Registry hash verification is done client-side, so gateways are untrusted (source: bcmr-spec.md).

### DNS Caching and Redirects

Clients must support HTTP `301` (permanent) and `302` (temporary) redirects. On `301`, notify the user and update the canonical FQDN. On `302`, follow without notification. If no `Cache-Control max-age` is set, registries expire after 7 days (source: bcmr-spec.md).

### Upgrade from DNS to On-Chain Resolution

DNS-resolved registries may include a `registryIdentity` authbase. Metadata-validating clients must then switch to chain resolution. DNS-only clients should warn that the registry prefers on-chain resolution (source: bcmr-spec.md).

## Tags

Tags classify identities by characteristics: `individual`, `organization`, `token`, `wallet`, `exchange`, `stablecoin`, `utility-token`, `security-token`, `collectable`, `deflationary`, `governance`, `decentralized-exchange`, etc. Tags can also represent external certifications (audited, endorsed) (source: bcmr-spec.md).

## URI Identifiers

Standardized URI keys for identity metadata (source: bcmr-spec.md):

| Identifier | Description |
| ---------- | ----------- |
| `icon` | Square static icon (SVG recommended, or AVIF/WebP/PNG) |
| `icon-intro` | Square animated intro icon (plays once, non-looping) |
| `image` | Static image of the asset |
| `web` | Website offering info about the identity |
| `blog` | Blog or news source |
| `chat` | Community chatroom |
| `forum` | Community forum |
| `support` | User-facing support |
| `migrate` | Guidance for migrating from a previous token category |
| `registry` | Primary-source registry URI |

All URIs must be fully qualified (absolute). Custom identifiers follow pattern `/^[-a-z0-9]+$/` (e.g. `discord`, `github`, `telegram`, `twitter`).

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
