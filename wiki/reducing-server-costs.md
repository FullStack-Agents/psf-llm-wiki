# Reducing Server Costs

TBD

TBD

TBD

---


**Summary**: Analysis of how the Permissionless Software Foundation (PSF) reduced recurring cloud costs by 92% (from ~$50 to ~$4/month) by transitioning from a Web 2 to a Web 3 architecture using IPFS.

**Sources**: reducing-server-costs.md

**Last updated**: 2026-04-17

---

The "Reduce Server Costs" strategy is a practical application of the **Web 3 Cash Stack**, moving resource-intensive [blockchain](blockchain.md) infrastructure from centralized cloud providers to home-hosted hardware.

## The Problem: The "Cloud Tax"
Traditional Web 2.0 deployments of [blockchain](blockchain.md) infrastructure (Full Node, Indexer, API Server) result in:
- **High Recurring Costs**: Approximately $50/month per instance.
- **High Barriers to Entry**: Cost is a deterrent for developers in developing countries.
- **Centralization Risks**: Vulnerability to corporate or government censorship on cloud platforms (AWS, Hetzner, etc.).

## The Solution: Web 3 Cash Stack Architecture
The PSF introduced an **IPFS networking layer** between the API and the front-end application. This allows the "heavy" parts of the stack to run on a home desktop while a "light" presence remains in the cloud.

### Workflow Comparison
- **Web 2**: Front-end $\rightarrow$ Cloud API $\rightarrow$ Cloud Indexer $\rightarrow$ Cloud Node.
- **Web 3**: Front-end $\rightarrow$ Cloud Consumer (`ipfs-bch-wallet-consumer`) $\rightarrow$ IPFS $\rightarrow$ Home Service (`ipfs-bch-wallet-service`) $\rightarrow$ Home Indexer $\rightarrow$ Home Node.

## Cost Impact
| Metric | Web 2 Model | Web 3 Model |
| :--- | :--- | :--- |
| **Monthly Cloud Cost** | ~$50 | **~$4** |
| **Hardware Cost** | $0 (OpEx) | ~$400 (One-time CapEx) |
| **Break-even Point** | N/A | ~8 months |
| **Total Cost Reduction** | — | **92%** |

## Strategic Benefits Beyond Cost
- **Censorship Resistance**: Infrastructure is no longer subject to cloud provider Terms of Service or political pressure.
- **Decentralized Resilience**: The network is a mesh of community-run `ipfs-bch-wallet-service` instances. If one goes offline, applications can switch to another provider on the IPFS subnetwork.
- **Accessibility**: Lowers the financial threshold for hobbyists and entrepreneurs to launch [blockchain](blockchain.md) services.

## Related pages
- [cash-stack-layers](cash-stack-layers.md)
- [ipfs-bch-wallet-service](ipfs-bch-wallet-service.md)
- [ipfs-bch-wallet-consumer](ipfs-bch-wallet-consumer.md)
- [circuit-relays](circuit-relays.md)
- [permissionless-software-foundation](permissionless-software-foundation.md)