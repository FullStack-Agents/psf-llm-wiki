# [bitcoin-cash](bitcoin-cash.md) Clients

**Summary**: The different types of software implementations used to interact with the [bitcoin-cash](bitcoin-cash.md) network, varying by the level of control and trust.

**Sources**: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-([BCH](bitcoin-cash.md))_6.md

**Last updated**: 2026-04-16

---

To interact with the [bitcoin-cash](bitcoin-cash.md) network, users employ different types of clients. The reference implementation is maintained as an open-source project, originally derived from [Satoshi](utxo.md) Nakamoto's code (source: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-([BCH](bitcoin-cash.md))_6.md).

### Client Types
The choice of client typically involves a trade-off between ease of use and control/security.

1. **Full Client ([Full Node](bchn-full-node.md))**: Stores the complete history of all transactions. It manages wallets and initiates transactions directly on the network, acting as a standalone server. This provides maximum control and security but requires the user to manage their own backups (source: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-([BCH](bitcoin-cash.md))_6.md).
2. **Lightweight Client**: Stores the user's wallet but relies on third-party servers for transaction data and network access, similar to an email client (source: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-([BCH](bitcoin-cash.md))_6.md).
3. **Web Client**: Accessed via a browser, with the wallet stored on third-party servers. This is the easiest to set up but introduces counterparty risk (source: mastering-bitcoin-cash_chapter-1-What-is-Bitcoin-Cash-([BCH](bitcoin-cash.md))_6.md).

Mobile clients may implement any of these three architectures and can sometimes synchronize with desktop clients for a multi-platform experience.

## Related pages

- [bitcoin-cash](bitcoin-cash.md)
- [digital-wallets](digital-wallets.md)
- [decentralization](decentralization.md)
- [mastering-bitcoin-cash-chapter-1](mastering-bitcoin-cash-chapter-1.md)
