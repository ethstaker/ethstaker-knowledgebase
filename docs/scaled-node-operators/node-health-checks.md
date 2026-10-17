# Node health checks

<figure><img src="/assets/img/gitbook/image (106).png" alt="" width="563"><figcaption></figcaption></figure>

To serve as a validator, both CL and EL need to be up to date with the network. There are a couple of techniques of how to check that.

All this health check data should lead to a [monitoring tool](https://github.com/gateway-fm/validator-kb/blob/main/reference/nodes/monitoring) of your choice.

### Internal health checks

Most of the nodes have exposed health checks APIs, that return `HTTP 5xx` if the node is not syncing properly, and `HTTP 200 OK` if everything is okay. That is the most simple and most basic version of the health check.

### Timestamp Checks

One more strategy is based on the timestamp of the latest block.

For EL that is a response to [`eth_getBlockByNumber("latest", false)`](https://docs.gateway.fm/v/api-docs/ethereum/eth\_getblockbynumber).

It has a field called `timestamp`. By knowing the timestamp of the block and the block production rate (1 block per 12 seconds), it is possible to see how "old" is the current block of the node.

Since sometimes the block proposals could be missed, it doesn't make sense to keep this threshold too tight, but if it is > 5 minutes old, it makes sense to mark the node as "unhealthy" and notify your [monitoring system](https://github.com/gateway-fm/validator-kb/blob/main/reference/nodes/monitoring).

### Source Of Truth Checks (Forks)

Finally, the case when the blocks are being synced, but you are on the wrong fork. Detection of that could happen on the EL very easily, by using the block hash returned from [`eth_getBlockByNumber("latest", false)`](https://docs.gateway.fm/v/api-docs/ethereum/eth\_getblockbynumber).

You can compare these hashes across the nodes and also across the external sources of truth.

> <img src="/assets/img/gitbook/image (108).png" alt="" data-size="line">The information in the Scaled Node Operators section has been written and reviewed by [Igor Mandrigin](https://x.com/mandrigin) and [Gateway.fm](https://gateway.fm), a leading large scale Ethereum staking infrastructure provider.
