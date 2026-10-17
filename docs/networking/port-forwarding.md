# Port forwarding

It is very important that you forward ports to both your Ethereum execution and consensus clients, this ensures you are able to peer with other nodes efficiently.

Your execution and consensus client will still run without port forwarding, but you may notice it will take a very long time to find peers, and you may struggle to connect with a meaningful number of them too. So it is in your best interest (and heavily recommended) to have them forwarded.

Below are a list of the default ports that the software(s) are set to listen on.&#x20;

| Execution client                                                                                              | Port(s)                      |
| ------------------------------------------------------------------------------------------------------------- | ---------------------------- |
| [Besu](https://besu.hyperledger.org/en/stable/public-networks/how-to/connect/configure-ports/#p2p-networking) | 30303 TCP/UDP                |
| [Erigon](https://github.com/ledgerwatch/erigon#default-ports-and-protocols--firewalls)                        | 30303 TCP/UDP, 30304 TCP/UDP |
| [Geth](https://geth.ethereum.org/docs/fundamentals/security#networking-security)                              | 30303 TCP/UDP                |
| [Nethermind](https://docs.nethermind.io/nethermind/ethereum-client/configuration/network)                     | 30303 TCP/UDP                |



| Consensus client                                                                                            | Port(s)              |
| ----------------------------------------------------------------------------------------------------------- | -------------------- |
| [Lighthouse](https://lighthouse-book.sigmaprime.io/advanced\_networking.html#nat-traversal-port-forwarding) | 9000 TCP/UDP         |
| [Lodestar](https://chainsafe.github.io/lodestar/reference/cli/#beacon)                                      | 9000 TCP/UDP         |
| [Nimbus](https://nimbus.guide/networking.html)                                                              | 9000 TCP/UDP         |
| [Prysm](https://docs.prylabs.network/docs/prysm-usage/p2p-host-ip#incoming-p2p-connection-prerequisites)    | 12000 UDP, 13000 TCP |
| [Teku](https://docs.teku.consensys.net/Reference/CLI/CLI-Syntax/#p2p-port)                                  | 9000 TCP/UDP         |
| [Grandine](https://docs.grandine.io/beacon_node_api.html)                                                   | 9000 TCP/UDP         |

If your node is running and the port(s) have been forwarded, you can use an online tool [such as this one](https://www.yougetsignal.com/tools/open-ports/) to check whether the ports are forwarded correctly.

For more information on how to actually forward the ports, it is best to search for instructions via google, make sure to include your router make and model as the specific steps taken to forward ports will vary depending on your router.

### Static IP's

It is also recommended to configure your node with a static IP. This can be hardcoded on the machine itself or set as a reservation on your DHCP server (which is usually your router).

If your node gets a dynamic IP address assigned to it, there is always the chance that your machine may get assigned a different IP address and your port forwarding will no longer work as they will be pointing to the old IP.



Extra reading: [Exploring Eth2 – Why Open Ports Matter](https://www.symphonious.net/2021/08/14/exploring-eth2-why-open-ports-matter/)
