# decentralized-file-hosting

**Summary**: Overview of decentralized file hosting using the PSF File Pinning Protocol (PSFFPP) and IPFS, bridging the Bitcoin Cash ledger with distributed storage.

**Sources**: decentralized-file-hosting.md

**Last updated**: 2026-04-17

---

Decentralized file hosting in the Cash Stack is achieved through an optional **IPFS Layer** that complements the [bitcoin-cash](bitcoin-cash.md) blockchain. While the blockchain is ideal for tamper-proof data and value transfer, it is inefficient for large content; conversely, IPFS is excellent for content storage but requires a permanent data layer for coordination.

## The PSF File Pinning Protocol (PSFFPP)

The [PSF File Pinning Protocol (PSFFPP)](https://psffpp.com) creates a permissionless marketplace for file retention. It allows for censorship-resistant storage where files are paid for by burning **PSF Tokens** (an SLP Type 1 token).

### Protocol Targets
- **Cost**: ~$0.01 USD per megabyte.
- **Duration**: One-year renewable hosting guarantee.
- **Capacity**: Up to 100 MB per file.

### The Pin Claim Workflow
1. **IPFS Upload**: Generate a unique Content Identifier (CID).
2. **Proof of Burn (PoB)**: Permanently destroy PSF tokens via an SLP transaction to meet the cost requirements.
3. **Broadcast Pin Claim**: Broadcast a BCH transaction with an `OP_RETURN` containing the Lokad ID (0x00510000), PoB Transaction ID, CID, and filename.
4. **Detection & Validation**: Services running `ipfs-file-pin-service` detect the claim, validate the burn, and download the file.
5. **Redundant Pinning**: Valid files are pinned across multiple independent nodes to ensure redundancy.

## Economic Model: Proof of Burn
The protocol uses a "Proof of Burn" model rather than centralized payments. This ensures:
- **Permissionless Access**: No accounts or API keys required.
- **Value Capture**: Reducing token supply increases value for holders.
- **Decentralized Governance**: Prices are set by the [PSF Minting Council](https://psfoundation.info/governance/minting-council) via multisig approval (PS009).

## Data-Rich Tokens
By combining [slp-token-protocol](slp-token-protocol.md) and IPFS, tokens become layered assets:
- **On-Chain**: Core immutable data (ticker, name).
- **Immutable Layer**: Fixed metadata/media linked via CID.
- **Mutable Layer**: Updatable information linked via a Mutable Data Address (MDA).

## Software Components
- **psffpp**: npm JavaScript library for integrating the protocol into applications.
- **ipfs-file-pin-service**: Server-side infrastructure that monitors the blockchain and pins files.
- **file-pin-cli**: CLI tool for interacting with a local `ipfs-file-pin-service` instance.

## Related pages
- [slp-token-protocol](slp-token-protocol.md)
- [slp-token-indexer](slp-token-indexer.md)
- [permissionless-software-foundation](permissionless-software-foundation.md)
- [bitcoin-cash](bitcoin-cash.md)
