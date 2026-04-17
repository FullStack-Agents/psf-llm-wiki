# cash-stack-ports

**Summary**: A comprehensive reference of the default network ports used by the various components of the [Cash Stack](cash-stack-layers.md) infrastructure.

**Sources**: ports.md

**Last updated**: 2026-04-17

---

The [Cash Stack](cash-stack-layers.md) consists of multiple interdependent services, each communicating over specific ports. This page serves as a technical reference for network configuration and troubleshooting (source: ports.md).

## Core Blockchain Infrastructure

| Component | Container Name | Port | Function |
| :--- | :--- | :--- | :--- |
| **[BCHN](bchn-full-node.md) [Full Node](bchn-full-node.md)** | `bchn-main` | 8332 | JSON RPC |
| | | 8333 | p2p node communication |
| **[Fulcrum](fulcrum-indexer.md) Indexer** | `fulcrum-mainnet` | 50001 | Electrum TCP |
| | | 50002 | Electrum SSL |
| | `fulcrum-rest-api` | 3001 | REST API |
| **psf-slp-indexer** | `slp-indexer` | 5010 | REST API |
| **bch-api** | `bch-api-main` | 3000 | REST API |

## File Storage and IPFS Layer

### File Pinning Service
| Component | Container Name | Port | Function |
| :--- | :--- | :--- | :--- |
| **ipfs-file-pin-service** | `file-service` | 4001 | IPFS TCP |
| | | 4003 | IPFS WS |
| | | 5031 | REST API (Target for [SLP](slp-token-protocol.md) indexer webhooks) |
| | `mongo-file-service` | 5556 | MongoDB Connection |
| **psffpp-client** | N/A | 4201 | IPFS TCP |
| | | 4203 | IPFS WS |
| | | 5020 | REST API |

### Wallet Services
| Component | Container Name | Port | Function |
| :--- | :--- | :--- | :--- |
| **ipfs-bch-wallet-service**| `ipfs-bch-wallet` | 5668 | IPFS TCP |
| | | 5669 | IPFS WS |
| | | 5032 | REST API |
| | `mongo-bch` | 5557 | MongoDB Connection |
| **ipfs-bch-wallet-consumer**| N/A | 4101 | IPFS TCP |
| | | 4103 | IPFS WS |
| | | 5015 | REST API |
| | `mongo-bch-consumer` | 5558 | MongoDB Connection |

## Related pages

- [bchn-full-node](bchn-full-node.md)
- [fulcrum-indexer](fulcrum-indexer.md)
- [slp-token-indexer](slp-token-indexer.md)
- [psf-bch-api]([psf-bch-api](psf-bch-api.md).md)
- [cash-stack-layers](cash-stack-layers.md)
