# bch-js

**Summary**: A JavaScript library used by front-end applications to interact with the `psf-bch-api` REST server.

**Sources**: psf-bch-api.md

**Last updated**: 2026-04-17

---

`bch-js` is a library that allows front-end applications to communicate with the `psf-bch-api` server (source: psf-bch-api.md). 

It is also used for end-to-end testing of the `psf-bch-api` installation. By running `bch-js` integration tests, developers can verify that the API server is correctly wired to the BCHN Full Node, Fulcrum Indexer, and SLP Token Indexer (source: psf-bch-api.md).

`bch-js` supports multiple authentication modes, including no-auth, Bearer token authentication, and x402-bch payments (source: psf-bch-api.md).

## Related pages

- [psf-bch-api](psf-bch-api.md)
- [x402-bch](x402-bch.md)
