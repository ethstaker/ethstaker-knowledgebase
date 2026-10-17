# Obol DVT

## Connect existing EC & BN clients

If you are already running an Execution Client (EC) e.g. Geth and a Beacon Node (BN) e.g. Lighthouse you can connect your Obol DVT node to them. This allows you to reuse existing hardware and continue to run your solo staking validator alongside Obol DVT validators.

<table data-card-size="large" data-column-title-hidden data-view="cards"><thead><tr><th align="center"></th><th data-hidden></th><th data-hidden></th></tr></thead><tbody><tr><td align="center"><p></p><p><img src="/assets/img/gitbook/image (15).png" alt="" data-size="original"></p></td><td></td><td></td></tr></tbody></table>

### Update HTTP flags on existing Beacon Node

On your existing Beacon Node, ensure these flags are added so the Charon client can communicate directly.

=== "Lighthouse Flags"
    ```
    --http
    --http-address=0.0.0.0
    --http-port=5052
    ```

    [https://lighthouse-book.sigmaprime.io/api-bn.html#starting-the-server](https://lighthouse-book.sigmaprime.io/api-bn.html#starting-the-server)

=== "Teku Flags"
    ```
    --rest-api-enabled=true
    --rest-api-interface=0.0.0.0
    --rest-api-host-allowlist=*
    ```

=== "Nimbus Flags"
    ```
    --rest=true
    --rest-port=5052
    --rest-address=0.0.0.0
    --rest-allow-origin=*
    ```


### Clone the ObolNetwork/charon-distributed-validator-node repo

```
# Clone this repo
git clone https://github.com/ObolNetwork/charon-distributed-validator-node.git

# Change directory
cd charon-distributed-validator-node
```

There are three steps needed to change the configuration:

1. [Copy and edit the .env](#copy-and-edit-the-.env)
2. [Copy and edit the example override file](#copy-and-edit-the-example-override-file)

#### Copy and edit the .env

Copy the sample `.env` file.

```
cp .env.sample .env
```

Uncomment (remove the `#`) the line `CHARON_BEACON_NODE_ENDPOINTS`. Add your existing Beacon Node IP address, for example `"http://192.168.1.8:5052"`. As the Charon Client is running inside a Docker container you can't use `localhost`, even though it might be running on the same physical machine, it requires the IP address of the host machine.


``` title=".env"
# Connect to one or more external beacon nodes. Use a comma separated list excluding spaces.
CHARON_BEACON_NODE_ENDPOINTS="http://<EXISTING_BEACON_NODE_IP_ADDRESS>:<PORT>"
```


#### Copy and edit the example override file

Any uncommented section will automatically override the same section in `docker-compose.yml` when run with `docker-compose up`. This allows you to edit the variables used by Docker without changing the `docker-compose.yml` which could be modified in future updates.

```
cp docker-compose.override.yml.sample docker-compose.override.yml
```

Edit the newly copied file `docker-compose.override.yml` and uncomment (remove the `#`) the following lines:

* `services:`
  * `geth:`
    * `profiles: [disable]`
  * `lighthouse:`
    * `profiles: [disable]`

```yaml title="docker-compose.override.yml"
...

services:
  geth:
    #Disable geth
    profiles: [disable]
    # Bind geth internal ports to host ports
    #ports:
      #- 8545:8545 # JSON-RPC
      #- 8551:8551 # AUTH-RPC
      #- 6060:6060 # Metrics
      
  lighthouse:
    #Disable lighthouse
    profiles: [disable]
    # Bind lighthouse internal ports to host ports
    #ports:
      #- 5052:5052 # HTTP
      #- 5054:5054 # Metrics
      
...
```

You are now ready to start the Obol tutorial for creating an ENR and getting your new DVT validator set up!

[https://docs.obol.org/run/start/quickstart_overview](https://docs.obol.org/run/start/quickstart_overview)
