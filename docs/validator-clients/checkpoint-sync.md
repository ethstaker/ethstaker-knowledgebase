# Checkpoint sync

!!! info "Info"
    A community maintained list of checkpoint sync endpoints can be found here: [Ethereum Beacon Chain checkpoint sync endpoints ↗](https://eth-clients.github.io/checkpoint-sync-endpoints/)

    The endpoint maintained by EthStaker can be found [here](https://beaconstate.ethstaker.cc/)


Checkpoint sync, also known as weak subjectivity sync, creates a superior user experience for syncing Beacon Node. It's based on assumptions of [weak subjectivity↗](https://ethereum.org/en/developers/docs/consensus-mechanisms/pos/weak-subjectivity) which enables syncing Beacon Chain from a recent weak subjectivity checkpoint instead of genesis. Checkpoint sync makes the initial sync time significantly faster with similar trust assumptions as syncing from [genesis](../../staking-glossary#genesis-block).

In practice, this means your node connects to a remote service to download recent finalized states and continues verifying data from that point. The third-party providing the data needs to be trusted to provide the correct information about the finalized state and should be picked carefully.

### Validate against a known trusted source

You must verify the `slot` and `state_root` against a known trusted source. This can be a friend, someone from the community that you know or any other source that you trust. There is a maintained list of publicly hosted checkpoint sync endpoints [here↗](https://eth-clients.github.io/checkpoint-sync-endpoints/), but it is recommended to use your own trusted source first if possible.

You will need to know the IP & Port of your beacon node.

#### Obtaining slot and state root

Option A:

1. Check your consensus client logs
2. Find the slot number.
3. Find the state\_root value.

Option B:

1. Open `http://YOUR_NODE_IP:YOUR_NODE_PORT/eth/v1/beacon/headers/finalized` in your browser.
2. Find the slot number.
3. Find the state\_root value.

Option C:

1. Install curl and jq.
2.  In a new terminal window run:

    ```bash
    curl -s http://YOUR_NODE_IP:YOUR_NODE_PORT/eth/v1/beacon/headers/finalized | jq .'data.header.message'
    ```

If the `slot` and `state_root` from your validator matches the `slot` and `state_root` from (multiple) other sources, then it's a match, congratulations 🎉. If it's not a match you should start from scratch by wiping your beacon node and starting from the top.

[Technical notes on checkpoint sync ↗](https://notes.ethereum.org/@djrtwo/ws-sync-in-practice)

[Weak Subjectivity ↗](https://ethereum.org/en/developers/docs/consensus-mechanisms/pos/weak-subjectivity)
