# BCHJS Network Commands

**Summary**: Documentation of network-related commands available in bchjs.

**Sources**: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_11.md

**Last updated**: 2026-04-17

---

The `bchjs` library provides tools to monitor the state of the node's network connections.

### getPeerInfo
The `getPeerInfo()` method allows users to retrieve detailed information about all currently connected peers. This includes:
- Peer [address](addresses.md)
- Version
- Connection time
- Data transmission statistics (source: mastering-bitcoin-cash_chapter-5-the-bitcoin-cash-network_11.md)

**Example Usage**:
```javascript
bchjs.Network.getPeerInfo().then(
  (result) => {
    console.log(result);
  },
  (err) => {
    console.log(err);
  }
);
```

## Related pages

- [bch-peer-management](bch-peer-management.md)
- [mastering-bitcoin-cash-chapter-5-network-resilience](mastering-bitcoin-cash-chapter-5-network-resilience.md)
