# bcmr-spec

**Summary**: Technical specification for Bitcoin Cash Metadata Registries (BCMR), a standard for sharing authenticated metadata about tokens, identities, and contract systems between Bitcoin Cash wallets.

**Sources**: BCMR CHIP (cashtokens.org/docs/bcmr/chip.md)

**Last updated**: 2026-05-25

---

The Bitcoin Cash Metadata Registry (BCMR) standard provides a way to associate user-recognizable names, descriptions, icons, and ticker symbols with on-chain artifacts such as [cashtokens](cashtokens.md) and identities, ensuring that metadata can be verified and distributed in a decentralized, censorship-resistant manner (source: BCMR CHIP).

## Registry Resolution and Authentication

Clients can acquire and authenticate metadata registries using three primary strategies (source: BCMR CHIP):

### 1. DNS-Resolved Registries
Registries are associated with a Fully-Qualified Domain Name (FQDN) and accessed via a **Well-Known URI**: `https://<domain>/.well-known/bitcoin-cash-metadata-registry.json`. Trust is bootstrapped from the domain name.

Key details:
- Must allow CORS with `Access-Control-Allow-Origin: *`
- HTTP `301` redirects update the canonical FQDN; `302` redirects are handled silently
- If no `Cache-Control max-age`, registries expire after `7` days
- DNS-resolved registries can specify a `registryIdentity` authbase to **upgrade to on-chain resolution** — metadata-validating clients then fetch all future updates from the blockchain instead of DNS (source: BCMR CHIP).

### 2. Chain-Resolved Registries
Registries are associated with an **authbase** (a 32-byte TXID). This method offers stronger security (multisig vaults, time-delayed fallbacks) and real-time updates (source: BCMR CHIP):

- **Authchains (Zeroth-Descendant Transaction Chains, ZDTC)**: A chain of transactions where the output at index `0` of each transaction is spent by the next. Every valid BCH transaction has a single identity output at index 0.
- **Authbase & Authhead**: The first transaction is the **authbase** (no special features). The final transaction with an unspent identity output is the **authhead**.
- **On-Chain Resolution**: Clients recursively follow the chain from authbase to authhead, locate the [publication output](#publication-output-encoding), fetch the registry from the provided URI, and verify the SHA-256 hash matches.
- **Burned Identities**: If the authhead's identity output begins with `OP_RETURN`, the identity is "burned" — no longer maintained. Identity merging is also supported by spending two identity outputs in the same transaction.
- **Authchain Acceleration**: DNS-resolved registries can include the `authchain` extension to accelerate initial chain resolution (source: BCMR CHIP).

### 3. Embedded and Manually-Imported Registries
Client software may include a default embedded registry or allow users to manually import registries from files or URLs. All clients are recommended to include an initially-trusted embedded registry (source: BCMR CHIP).

## Publication Output Encoding

Chain-resolved registries publish a hash (and optionally URIs) in the authhead transaction. The locking bytecode follows this structure:

```
OP_RETURN <'BCMR'> <sha256_hash> [<uri> <uri> ...]
```

- Identified by locking bytecode prefix `0x6a0442434d52` (`OP_RETURN <'BCMR'>`)
- The SHA-256 hash is in `OP_SHA256` byte order (matching `OP_HASH256` output order, which is little-endian)
- URIs without a protocol prefix default to HTTPS; without a file path, assume the Well-Known URI
- Example: `https://example.com/.well-known/bitcoin-cash-metadata-registry.json` is encoded as `<'example.com'>` — i.e. `0x0b6578616d706c652e636f6d`
- Clients must support HTTPS and IPFS protocols at minimum
- Every transaction can have zero or **one** metadata registry publication output (the first matching output at the lowest index is definitive) (source: BCMR CHIP).

## Metadata Structure

BCMRs use an extensible JSON schema to map identities to their history (source: BCMR CHIP).

### Identities and Snapshots
- **Authbase**: Every identity is uniquely identified by its authbase, serving as its root of trust.
- **Identity Snapshots**: Metadata is organized into snapshots associated with specific timestamps. A snapshot can include a name, description, and token-specific data (symbol, decimals, category).
- **Gradual Migration**: Using the `migrated` property, snapshots can define a transition period between two sets of metadata (source: BCMR CHIP).

### Tags and URIs
- **Tags**: Allow classification of identities (e.g., `stablecoin`, `exchange`, `organization`).
- **URI Identifiers**: Standardized keys like `icon`, `web`, `blog`, and `support` point to authenticated resources. All URIs must be fully qualified (absolute) (source: BCMR CHIP).

## Token and NFT Integration

### Ticker Symbols
- **Fungible Tokens**: Recommended base symbols are 4-6 characters.
- **NFTs**: Recommended base symbols are 6-13 characters to distinguish them from fungible tokens.
- **Full Symbol**: The concatenation of the category symbol and a numeric or hex-encoded suffix based on the NFT type (source: BCMR CHIP).

### NFT Rendering
Registries define how to interpret NFT commitments via the `NftCategory` definition:
- **Sequential NFTs**: The commitment is a VM number mapping to an index in `parse.types`.
- **Parsable NFTs**: The commitment contains encoded data a client can parse using provided `parse.bytecode` to extract specific fields (e.g., "Seat Number" or "BCH Pledged") (source: BCMR CHIP).

## Extensions and Localization
- **Extensions**: Allow vendor-specific metadata.
- **Locales Extension**: Supports localized versions of metadata. Clients assemble a localized registry by inheriting from the most specific available locale, falling back to English (`en`) (source: BCMR CHIP).

## Related pages

- [cashtokens](cashtokens.md)
- [cashtokens-spec](cashtokens-spec.md)
- [bcmr-examples](bcmr-examples.md)
- [bitcoin-cash](bitcoin-cash.md)
- [cashaddr](cashaddr.md)
