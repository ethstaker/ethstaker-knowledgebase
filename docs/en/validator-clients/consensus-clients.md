# Consensus clients

!!! info "Info"
    For more info about Execution clients and Validator clients start here:
    [Validator clients explained](../../validator-clients/validator-clients-explained) 👀


Consensus clients run the Beacon Chain and provide a [proof-of-stake (PoS)](../../staking-glossary#proof-of-stake-pos) consensus mechanism to [execution clients](../../validator-clients/execution-clients).

Consensus clients all follow the same [specification ↗](https://github.com/ethereum/consensus-specs). If a client doesn't follow this spec it won't be able to come to consensus with the rest of the network.

<table><thead><tr><th width="161">Client</th><th width="185">Documentation</th><th width="168">GitHub</th><th width="193">Discord</th></tr></thead><tbody><tr><td><strong>Lighthouse</strong></td><td><a href="https://lighthouse-book.sigmaprime.io/">Link ↗</a></td><td><a href="https://github.com/sigp/lighthouse">Link ↗</a></td><td><a href="https://discord.gg/gdq27tnKSM">Link ↗</a></td></tr><tr><td><strong>Lodestar</strong></td><td><a href="https://chainsafe.github.io/lodestar/">Link ↗</a></td><td><a href="https://github.com/ChainSafe/lodestar">Link ↗</a></td><td><a href="https://discord.com/invite/yjyvFRP">Link ↗</a></td></tr><tr><td><strong>Nimbus</strong></td><td><a href="https://status-im.github.io/nimbus-eth2/intro.html">Link ↗</a></td><td><a href="https://github.com/status-im/nimbus-eth2">Link ↗</a></td><td><a href="https://discord.gg/aTDcbTG2gQ">Link ↗</a></td></tr><tr><td><strong>Prysm</strong></td><td><a href="https://docs.prylabs.network/docs/getting-started">Link ↗</a></td><td><a href="https://github.com/prysmaticlabs/prysm">Link ↗</a></td><td><a href="https://discord.gg/GVM5TJwzkU">Link ↗</a></td></tr><tr><td><strong>Teku</strong></td><td><a href="https://docs.teku.consensys.net/en/stable/">Link ↗</a></td><td><a href="https://github.com/ConsenSys/teku">Link ↗</a></td><td><a href="https://discord.gg/trQ378WCp4">Link ↗</a><br>(#teku channel)</td></tr><tr><td><strong>Grandine</strong></td><td><a href="https://docs.grandine.io/">Link ↗</a></td><td><a href="https://github.com/grandinetech/grandine">Link ↗</a></td><td><a href="https://discord.gg/H9XCdUSyZd">Link ↗</a></td></tr></tbody></table>

### Lighthouse

Lighthouse is a consensus client implementation written in Rust under the Apache-2.0 license. It is maintained by Sigma Prime and has been stable and production-ready since Beacon Chain genesis. It is relied upon by various enterprises, staking pools and individuals. It aims to be secure, performant and interoperable in a wide range of environments, from desktop PCs to sophisticated automated deployments.

### Lodestar

Lodestar is a production-ready consensus client implementation written in Typescript under the LGPL-3.0 license. It is maintained by ChainSafe Systems and is the newest of the consensus clients for solo-stakers, developers and researchers. Lodestar consists of a beacon node and validator client powered by JavaScript implementations of Ethereum protocols. Lodestar aims to improve Ethereum usability with light clients, expand accessibility to a larger group of developers and further contribute to ecosystem diversity.

### Nimbus

Nimbus is a consensus client implementation written in Nim under the Apache-2.0 license. It is a production-ready client in use by solo-stakers and staking pools. Nimbus is designed for resource efficiency, making it easy to run on resource-restricted devices and enterprise infrastructure with equal ease, without compromising stability or reward performance. A lighter resource footprint means the client has a greater margin of safety when the network is under stress.

Implemented by Trinity. Works like fast sync but also downloads the data needed to execute latest blocks, which allows you to query the chain within the first few minutes from starting.

* Syncs state first and enables you to query RPC in a few minutes.

### Prysm

Prysm is a full-featured, open source consensus client written in Go under the GPL-3.0 license. It features an optional webapp UI and prioritizes user experience, documentation, and configurability for both stake-at-home and institutional users.

### Teku

Teku is one of the original Beacon Chain genesis clients. Alongside the usual goals (security, robustness, stability, usability, performance), Teku specifically aims to comply fully with all the various consensus client standards.

Teku offers very flexible deployment options. The beacon node and validator client can be run together as a single process, which is extremely convenient for solo stakers, or nodes can be run separately for sophisticated staking operations. In addition, Teku is fully interoperable with [Web3Signer↗](https://github.com/ConsenSys/web3signer/)[ ](https://github.com/ConsenSys/web3signer/)for signing key security and slashing protection.

Teku is written in Java and is Apache 2.0 licensed. It is developed by the Protocols team at ConsenSys that is also responsible for Besu and Web3Signer.

### Grandine

Grandine is a consensus client implementation, written in Rust under the GPL-3.0 license. It is maintained by the Grandine Core Team and is fast, high-performance and lightweight. It fits a wide range of stakers from solo stakers running on low-resource devices such as Raspberry Pi to large institutional stakers running tens of thousands of validators.