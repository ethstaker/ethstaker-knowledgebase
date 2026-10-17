# Execution clients

!!! info "Info"
    For more info about Execution clients and Validator clients start here:
    [Validator clients explained](../../validator-clients/validator-clients-explained) 👀


The Ethereum community maintains multiple open-source execution clients (previously known as 'Eth1 clients', or just 'Ethereum clients'), developed by different teams using different programming languages. This makes the network stronger and more diverse. The ideal goal is to achieve diversity without any client dominating to reduce any single points of failure.

<table><thead><tr><th width="161">Client</th><th width="185">Documentation</th><th width="168">GitHub</th><th width="193">Discord</th></tr></thead><tbody><tr><td><strong>Geth</strong></td><td><a href="https://geth.ethereum.org/docs/">Link ↗</a></td><td><a href="https://github.com/ethereum/go-ethereum">Link ↗</a></td><td><a href="https://discord.com/invite/nthXNEv">Link ↗</a></td></tr><tr><td><strong>Besu</strong></td><td><a href="https://besu.hyperledger.org/">Link ↗</a></td><td><a href="https://github.com/hyperledger/besu">Link ↗</a></td><td><a href="https://discord.com/invite/hyperledger">Link ↗</a></td></tr><tr><td><strong>Nethermind</strong></td><td><a href="https://docs.nethermind.io/get-started/installing-nethermind">Link ↗</a></td><td><a href="https://github.com/NethermindEth/nethermind">Link ↗</a></td><td><a href="https://discord.com/invite/PaCMRFdvWT">Link ↗</a></td></tr><tr><td><strong>Erigon</strong></td><td><a href="https://github.com/ledgerwatch/erigon#erigon">Link ↗</a></td><td><a href="https://github.com/ledgerwatch/erigon">Link ↗</a></td><td><a href="https://github.com/ledgerwatch/erigon#erigon-discord-server">Link ↗ </a><br>(Request access)</td></tr></tbody></table>

### Geth

Go Ethereum (Geth for short) is one of the original implementations of the Ethereum protocol. Currently, it is the most widespread client with the biggest user base and variety of tooling for users and developers. It is written in Go, fully open source and licensed under the GNU LGPL v3.

### Besu

Hyperledger Besu is an enterprise-grade Ethereum client for public and permissioned networks. It runs all of the Ethereum Mainnet features, from tracing to GraphQL, has extensive monitoring and is supported by ConsenSys, both in open community channels and through commercial SLAs for enterprises. It is written in Java and is Apache 2.0 licensed.

Besu's extensive documentation will guide you through all details on its features and setups.

### Nethermind

Nethermind is an Ethereum implementation created with the C# .NET tech stack, licensed with LGPL-3.0, running on all major platforms including ARM. It offers great performance with:

* An optimized virtual machine.
* State access.
* Networking and rich features like Prometheus/Grafana dashboards, seq enterprise logging support, JSON RPC tracing, and analytics plugins.

### Erigon

Erigon, formerly known as Turbo‐Geth, started as a fork of Go Ethereum oriented toward speed and disk‐space efficiency. Erigon is a completely re-architected implementation of Ethereum, currently written in Go but with implementations in other languages under development. Erigon's goal is to provide a faster, more modular, and more optimized implementation of Ethereum. It can perform a full archive node sync using around 2TB of disk space, in under 3 days.

