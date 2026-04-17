# ipfs-bch-wallet-service

TBD

TBD

TBD

---


**Summary**: A censorship-resistant microservice that provides wallet access to the [bitcoin-cash](bitcoin-cash.md) [blockchain](blockchain.md) by proxying the HTTP-based REST API of `psf-bch-api` over an IPFS-based JSON RPC.

**Sources**: ipfs-bch-wallet-service.md

**Last updated**: 2026-04-17

---

`ipfs-bch-wallet-service` is a critical bridge in the Cash Stack that enables [blockchain](blockchain.md) access without relying on centralized HTTP endpoints. It allows wallets to interact with the [bitcoin-cash](bitcoin-cash.md) network in a way that is resistant to censorship.

## Technical Functionality

The service acts as a proxy between the [blockchain](blockchain.md) backend and the IPFS network:

- **Backend Communication**: It uses [bch-js](bch-js.md) to communicate with a local instance of [psf-bch-api](psf-bch-api.md).
- **Protocol Translation**: It converts the standard HTTP/REST API calls from the backend into IPFS-based JSON RPC messages.
- **Delivery**: These messages are then routed over the IPFS network, making the service accessible to consumers who may be behind firewalls or in restrictive environments.

## Position in the Ecosystem

- **Source**: This service is a major fork of [ipfs-service-provider](ipfs-service-provider.md), inheriting its networking and authentication infrastructure.
- **Consumer**: The primary client for this service is [ipfs-bch-wallet-consumer](ipfs-bch-wallet-consumer.md), which provides a localized HTTP interface for front-end applications.

## Related Pages
- [ipfs-service-provider](ipfs-service-provider.md)
- [ipfs-bch-wallet-consumer](ipfs-bch-wallet-consumer.md)
- [psf-bch-api](psf-bch-api.md)
- [bch-js](bch-js.md)
- [bitcoin-cash](bitcoin-cash.md)