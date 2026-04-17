# x402-bch

**Summary**: A protocol for facilitating per-call payments for API access using [Bitcoin Cash](bitcoin-cash.md) ([BCH](bitcoin-cash.md)).

**Sources**: [psf-bch-api](psf-bch-api.md).md

**Last updated**: 2026-04-17

---

The `x402-bch` protocol allows API providers to monetize their services by charging a micro-payment for each individual request (source: [psf-bch-api](psf-bch-api.md).md).

When implemented in `[psf-bch-api](psf-bch-api.md)`:
- The server responds with an HTTP `402 Payment Required` status if a valid payment header is missing (source: [psf-bch-api](psf-bch-api.md).md).
- The response includes payment details necessary to fulfill the request (source: [psf-bch-api](psf-bch-api.md).md).
- Client libraries, such as `[bch-js](bch-js.md)`, can handle these payments automatically (source: [psf-bch-api](psf-bch-api.md).md).

The system relies on a "facilitator service" to manage the payment process (source: [psf-bch-api](psf-bch-api.md).md).

## Related pages

- [psf-bch-api]([psf-bch-api](psf-bch-api.md).md)
- [bch-js]([bch-js](bch-js.md).md)
