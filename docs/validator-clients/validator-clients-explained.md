# Validator clients explained

Ethereum is a peer-to-peer network with thousands of nodes that must be able to communicate with one another using standardized protocols. The "networking layer" is the stack of protocols that allow those nodes to find each other and exchange information. This includes "gossiping" information (one-to-many communication) over the network as well as swapping requests and responses between specific nodes (one-to-one communication). Each node must adhere to specific networking rules to ensure they are sending and receiving the correct information.

There are two parts to the client software (execution clients and consensus clients), each with its own distinct networking stack. As well as communicating with other Ethereum nodes, the execution and consensus clients have to communicate with each other. This page gives an introductory explanation of the protocols that enable this communication.

[Execution clients](../../validator-clients/execution-clients) gossip transactions over the execution-layer peer-to-peer network. This requires encrypted communication between authenticated peers. When a validator is selected to propose a block, transactions from the node's local transaction pool will be passed to consensus clients via a local RPC connection, which will be packaged into Beacon blocks.

<div class="grid">
  <a href="../../validator-clients/execution-clients" class="card local">Execution clients</a>
</div>

[Consensus clients](../../validator-clients/consensus-clients) will then gossip Beacon blocks across their p2p network. This requires two separate p2p networks: one connecting execution clients for transaction gossip and one connecting consensus clients for block gossip.

<div class="grid">
  <a href="../../validator-clients/consensus-clients" class="card local">Consensus clients</a>
</div>

[_Source ↗_](https://ethereum.org/en/developers/docs/networking-layer)
