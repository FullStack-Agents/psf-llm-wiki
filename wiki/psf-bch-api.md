# psf-bch-api

**Summary**: A REST API server written in Node.js that provides a common web2 interface for developers to build blockchain-based business applications by abstracting underlying blockchain infrastructure.

**Sources**: psf-bch-api.md

**Last updated**: 2026-04-17

---

`psf-bch-api` is the heart of the Cash Stack, acting as a single web2 REST API that allows developers to access blockchain infrastructure without interacting directly with low-level nodes (source: psf-bch-api.md). It is written in Node.js using the Express.js framework and follows the Clean Architecture design pattern (source: psf-bch-api.md).

## Architecture and Dependencies

The server sits atop several critical pieces of blockchain infrastructure (source: psf-bch-api.md):
- **BCHN Full Node**: The base layer that validates transactions and blocks.
- **Fulcrum Indexer**: An address indexer tracking balances, transaction histories, and UTXOs.
- **SLP Token Indexer**: Tracks all SLP tokens on the blockchain.

Front-end applications typically interact with `psf-bch-api` using libraries such as [bch-js](https://github.com/Permissionless-Software-Foundation/bch-js) or `bch-consumer` (source: psf-bch-api.md).

## Access Control and Monetization

The API supports three primary access-control configurations via environment variables:

1. **Open Access**: No rate limits or authentication; ideal for local development or trusted private networks (source: psf-bch-api.md).
2. **Bearer Token Authentication**: Uses a secret token in the `Authorization` header to restrict access to known users or services (source: psf-bch-api.md).
3. **x402-bch Per-Call Payments**: Implements the [x402-bch protocol](https://github.com/x402-bch/x402-bch), requiring a BCH micro-payment for every API call. This is intended for public, monetized APIs (source: psf-bch-api.md).

It is possible to combine Bearer Tokens and x402 payments, allowing trusted clients free access while monetizing public users (source: psf-bch-api.md).

## Deployment and Testing

`psf-bch-api` is typically deployed via Docker. Deployment requires that the BCHN Full Node, Fulcrum Indexer, and SLP Token Indexer are all fully synced and running (source: psf-bch-api.md).

Verification is performed using integration tests provided by `bch-js`, which exercise endpoints to ensure connectivity between the API server and the underlying infrastructure (source: psf-bch-api.md).

## Related pages

- [cash-stack-layers](cash-stack-layers.md)
- [permissionless-software-foundation](permissionless-software-foundation.md)
- [bch-js](bch-js.md)
- [x402-bch](x402-bch.md)
