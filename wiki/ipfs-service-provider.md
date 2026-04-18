# ipfs-service-provider

TBD

TBD

TBD

---


**Summary**: A production-ready boilerplate application that wraps the `helia-coord` library in a web server, providing REST API, JSON RPC endpoints, and user management. It serves as the foundational starting point for building IPFS-based services in the Cash Stack.

**Sources**: ipfs-service-provider.md

**Last updated**: 2026-04-17

---

`ipfs-service-provider` bridges the gap between the low-level networking capabilities of [helia-coord](helia-coord.md) and the requirements of a production web service. While `helia-coord` handles peer discovery and encryption, `ipfs-service-provider` adds the necessary infrastructure for application delivery.

## Core Features

- **API Surface**: Provides both a Koa-based REST API and a JSON RPC interface.
- **JSON RPC over IPFS**: Enables API communication between service providers and consumers routed directly over the IPFS network.
- **User Management**: Implements account creation, authentication, and authorization using JWT tokens.
- **Infrastructure**: Includes built-in rate limiting, logging, and database integration (MongoDB).
- **Censorship Resistance**: By integrating `helia-coord`, it can operate behind residential firewalls via [Circuit Relays](circuit-relays.md).

## The Boilerplate Pattern

The project is designed to be **forked**. Instead of building from scratch, developers fork `ipfs-service-provider` to inherit the networking and authentication plumbing, then implement their domain-specific business logic in the `use-cases` and `controllers` layers.

### Major Forks in the Cash Stack
- **ipfs-bch-wallet-service**: Provides censorship-resistant wallet access to the BCH [blockchain](blockchain.md) over IPFS.
- **ipfs-bch-wallet-consumer**: A lightweight REST API that consumes services from the wallet-service over IPFS.
- **ipfs-file-pin-service**: Implements paid IPFS file pinning using the Pin Claim protocol (PS010).

## Operational Roles

Beyond being a boilerplate for new services, it can be deployed as a standalone **Circuit Relay**. By setting `ENABLE_CIRCUIT_RELAY`, the instance helps other nodes behind firewalls communicate, contributing to the overall resilience of the PSF IPFS network.

## Architecture

Following **Clean Architecture**, the project is structured into:
- **Adapters**: IPs (Helia/helia-coord) and LocalDB (Mongoose).
- **Controllers**: REST API routes, JSON-RPC handlers, and periodic timer controllers.
- **Entities**: Business logic validation.
- **Use Cases**: Application-specific business rules.

## Related pages
- [helia-coord](helia-coord.md)
- [circuit-relays](circuit-relays.md)
- [ipfs-bch-wallet-consumer](ipfs-bch-wallet-consumer.md)
- [permissionless-software-foundation](permissionless-software-foundation.md)
- [cash-stack-layers](cash-stack-layers.md)