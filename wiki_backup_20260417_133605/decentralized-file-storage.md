# decentralized-file-storage

**Summary**: Concept page focusing on the technical and architectural aspects of decentralized storage, primarily using IPFS and the Cash Stack.

**Sources**: decentralized-file-storage.md, decentralized-file-hosting.md

**Last updated**: 2026-04-17

---

Decentralized file storage refers to the distribution of data across a network of independent nodes, removing the reliance on a single central authority (like AWS or Google). In the context of the Permissionless Software Foundation (PSF), this is implemented as a bridge between the [bitcoin-cash](bitcoin-cash.md) blockchain and the Inter-Planetary File System (IPFS).

## Core Concepts

### Content Addressability
Unlike traditional URLs that point to a location (where a file is), decentralized storage uses **Content Identifiers (CIDs)**. A CID is a cryptographic hash of the file's content. If the content changes, the CID changes. This ensures data integrity and prevents silent corruption.

### The Role of the Blockchain
The blockchain serves as the **Ledger of Truth**. While the actual large files reside on IPFS, the blockchain stores:
- **Pointers**: CIDs that link to the stored content.
- **Payment Proofs**: Evidence of "Proof of Burn" (PoB) that guarantees the storage duration.
- **Coordination**: A permissionless way for pinning services to discover what they need to host.

### Redundancy and Censorship Resistance
Because the [PSF File Pinning Protocol (PSFFPP)](decentralized-file-hosting.md) allows any independent node to run an `ipfs-file-pin-service`, data is replicated across multiple global operators. This removes any single point of failure or control.

## Comparison: Centralized vs. Decentralized Storage

| Feature | Centralized (S3/Google) | Decentralized (PSFFPP/IPFS) |
| :--- | :--- | :--- |
| **Control** | Corporate/Centralized | Permissionless/Distributed |
| **Addressing** | Location-based (URL) | Content-based (CID) |
| **Payments** | Subscription/Account | Proof of Burn (PSF Tokens) |
| **Persistence** | Based on account standing | Based on protocol-defined burn |

## Related pages
- [decentralized-file-hosting](decentralized-file-hosting.md)
- [bitcoin-cash](bitcoin-cash.md)
- [decentralization](decentralization.md)
