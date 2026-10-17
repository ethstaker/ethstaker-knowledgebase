# Configuring an RPC endpoint

This page will show you how to configure your execution client to serve HTTP RPC requests.

This will allow you to interact directly with the Ethereum network using your own node. No need to use a 3rd party service like Infura anymore!

### 1) Configure your execution client

You will need to add the following flags to your execution client.

=== "Geth"
    #### Required Flags

    ```bash
    --http
    --http.api eth,net,web3
    --http.corsdomain '*'
    ```

    _Please note, configuring your --http-corsdomain as per the above example will allow anyone to use your node as an RPC endpoint. Please ensure this is also paired with the appropriate firewall rule(s) to prevent this from happening._

    #### Optional Flags

    ```
    --http.addr 0.0.0.0
    --http.port 8545
    ```

    [Link to docs](https://geth.ethereum.org/docs/interacting-with-geth/rpc)

    This will indicate your Geth node is ready for RPC connections

    <figure><img src="/assets/img/gitbook/RPC-Geth.png" alt=""><figcaption></figcaption></figure>


=== "Nethermind"
    #### Required Flags

    ```bash
    --JsonRpc.Enabled true
    ```

    #### Optional Flags

    ```
    --JsonRpc.Port=8545
    --JsonRpc.Host="127.0.0.1"
    --JsonRpc.EnabledModules=[Eth,Web3,Net,Rpc]
    ```

    [Link to docs](https://docs.nethermind.io/nethermind/ethereum-client/configuration/jsonrpc)

    This will indicate your Nethermind node is ready for RPC connections

    <figure><img src="/assets/img/gitbook/RPC-Nethermind.png" alt=""><figcaption></figcaption></figure>


=== "Besu"
    #### Required Flags

    ```bash
    --rpc-http-api=ETH,NET,WEB3
    --rpc-http-cors-origins="*"
    --rpc-http-enabled=true
    ```

    _Please note, configuring your --rpc-http-cors-origins as per the above example will allow anyone to use your node as an RPC endpoint. Please ensure this is also paired with the appropriate firewall rule(s) to prevent this from happening._

    #### Optional Flags

    ```
    --rpc-http-host=0.0.0.0
    ```

    [Link to docs](https://besu.hyperledger.org/en/stable/public-networks/how-to/use-besu-api/)

    This will indicate your Besu node is ready for RPC connections

    <figure><img src="/assets/img/gitbook/RPC-Besu.png" alt=""><figcaption></figcaption></figure>


=== "Erigon"
    #### Required Flags

    ```bash
    --http.api=eth,erigon,web3,net,debug,trace,txpool
    --http.vhosts '*'
    ```

    _Please note, configuring your --http.vhosts as per the above example will allow anyone to use your node as an RPC endpoint. Please ensure this is also paired with the appropriate firewall rule(s) to prevent this from happening._

    #### Optional Flags

    ```
    --http            #HTTP-RPC server (enabled by default). Use --http=false to disable it (default: true)
    --http.addr value #HTTP-RPC server listening interface (default: "localhost")
    --http.port value #HTTP-RPC server listening port (default: 8545)
    ```

    [Link to docs](https://github.com/ledgerwatch/erigon#json-rpc-daemon)

    This will indicate your Erigon node is ready for RPC connections

    <figure><img src="/assets/img/gitbook/image (8) (2).png" alt=""><figcaption></figcaption></figure>



### 2) Configure your wallet

Now you will need a wallet that allows you to add custom RPC endpoints. You can find a list of wallets with this feature [via this link.](https://ethereum.org/en/wallets/find-wallet/)

The below example will show you how to use your RPC endpoint with Metamask as it is one of the most commonly used wallets.

#### 2.1) Open Metamask, click the menu icon at the top right, and select "Add Network"

<figure><img src="/assets/img/gitbook/image (7) (2).png" alt=""><figcaption></figcaption></figure>

#### 2.2) Scroll down the bottom and select "Add a network manually"

<figure><img src="/assets/img/gitbook/image (14).png" alt=""><figcaption></figcaption></figure>

#### 2.3) Fill in your node details

The specific details will vary depending on your local setup. As I am running Geth on the same machine as my Metamask installation, so I am using 127.0.0.1 as the IP address.

<figure><img src="/assets/img/gitbook/image (4).png" alt=""><figcaption></figcaption></figure>

If your RPC is unavailable or otherwise inaccessible, it may show an error when you enter the Chain ID and won't allow you to save the network.

#### 2.4) Look out for the confirmation message

<figure><img src="/assets/img/gitbook/image (12).png" alt=""><figcaption></figcaption></figure>

#### 2.5) Swap to your new network if Metamask hasn't done so already

<figure><img src="/assets/img/gitbook/image (3) (1).png" alt=""><figcaption></figcaption></figure>

Success! Now you can use Metamask as you normally would with the added benefit of accessing the Ethereum network through your own node 🥳
