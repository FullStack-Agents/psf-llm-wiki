# Cash Stack Layers

**Summary**: The layered architecture of the Cash Stack, inspired by the OSI model, focusing on the path data travels between an app and the blockchain.

**Sources**: intro.md

**Last updated**: 2026-04-17

---

The Cash Stack architecture is inspired by the OSI model to facilitate technical discussion and issue isolation (source: intro.md). It consists of the following layers:

- **Application Layer**: End-user UI and application libraries with business logic.
- **Interface Library Layer**: Libraries such as `[bch-js](bch-js.md)` and `bch-consumer` (source: intro.md).
- **API Layer**: REST API or JSON RPC servers.
- **Indexer Layer**: Search engines for blockchain data, such as [Fulcrum](fulcrum-indexer.md) (tracking balances and UTXOs) and `psf-slp-indexer` (tracking [SLP](slp-token-protocol.md) tokens) (source: intro.md).
- **[Full Node](bchn-full-node.md) Layer**: Base blockchain software for verifying and broadcasting blocks.

## Related pages

- [intro](intro.md)
- [psf-bch-api]([psf-bch-api](psf-bch-api.md).md)
