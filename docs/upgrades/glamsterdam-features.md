# New Staking Features in Glamsterdam

[Glamsterdam](https://eips.ethereum.org/EIPS/eip-7773), combining changes on the consensus layer ([Gloas](https://github.com/ethereum/consensus-specs/tree/master/specs/gloas)) with changes on the execution layer (Amsterdam), is a hard fork planned to upgrade the Ethereum protocol. This document covers the new staking-related features and changes included in this upgrade.

A good overview of all Glamsterdam changes is on [Forkcast](https://forkcast.org/upgrade/glamsterdam/).

## Fork Schedule

Glamsterdam has not yet been announced for public testnets and mainnets as of mid-July 2026. It is widely expected to ship in 2026, possibly by November 2026. You can follow the discussion at [Forkcast](https://forkcast.org/calls)

## Two headliners

The two major changes in Glamsterdam are [ePBS](https://forkcast.org/eips/7732/) and [BAL](https://forkcast.org/eips/7928/).

ePBS, "Enshrined Proposer Builder Separation", does two main things. It changes the slot timing and decouples broadcast and verification of the execution payload from the consensus block. And it removes the need for PBS sidecars such as mev-boost or commit-boost-pbs as well as trusted relays, instead enabling direct connections to builders and also broadcasting builder bids via P2P, peer to peer, protocol. Relays are still expected to be in use, but will function just like a direct builder connection.

BAL, Block Level Access list, allows clients to know what accounts and smart contracts were changed in the block and how. For stakers that means faster re-execution of the payload, as transactions that are independent of each other can now be processed in parallel, using all CPU cores. Pre-Glamsterdam, most clients use a single-core implementation of the EVM, Ethereum Virtual Machine. Some clients already used heuristics for parallel processing: BAL makes this far more efficient and predictable.

BAL also enables a new syncing protocol for execution layer clients, [snap/2](https://eips.ethereum.org/EIPS/eip-8189). Pre-Glamsterdam, the final stage of snap sync is "state healing". Depending on the speed of the disk, this can take hours; on slow disks, state may move faster than healing can process, and it'll never complete. The new snap protocol can instead apply the state diffs in the BAL for final state catch-up, which is far faster. 

Between them, these two changes allow the clients more time and resources to handle re-execution of the execution payload. As a result, together with gas repricings, the gas limit is expected to be raised to 300M with Glamsterdam, from 60M pre-Glamsterdam. It is a 5-fold increase, to match the roughly 5-fold increase in available processing time.

## ePBS configuration changes

For concrete changes, check your validator client's `--help` as well as any staking guide or staking tooling you use. If you do not use mev-boost or commit-boost-pbs now, no configuration changes are needed.

High-level, the relay parameters move from your sidecar to your validator client.
- Pre-Glamsterdam, configure relays on the validator client, as well as parameters such as min-bid
- Wait for Glamsterdam hard fork
- Post-Glamsterdam, remove your mev-boost or commit-boost-pbs side car, and remove the consensus layer client parameter that connected the CL to the side car

## ePBS block timing changes

Pre-Glamsterdam, all block broadcasting as well as re-execution and validation needs to be completed by four seconds into a twelve-second slot, "t=4s".

![pre-Glamsterdam slot timing](/assets/img/glamsterdam/pre_Glamsterdam_Timing.png)

Relays play timing games pre-Glamsterdam and release a block roughly at the 1s mark. It then takes another 500ms to 1s to propagate to a node, leaving roughly 2s for re-execution and validation of the block, before attesting at t=4s.

If building a block locally, it and its blobs can be broadcast at t=0s, leaving at least 3s for re-execution. About 10% of Ethereum blocks are being built locally pre-Glamsterdam.

[Empirical data](https://ethresear.ch/t/an-analysis-of-attestation-timings-in-a-6-s-slot/23016) about propagation time by geographic region has been published.

Post-Glamsterdam, the timing changes to allow 9-10s for re-execution and validation of the payload.


![ePBS slot timing](/assets/img/glamsterdam/ePBS_Timing.png)

An attesting validator receives a beacon block before t=3s and attests to that block, its execution payload hash, and the *previous* slot's execution payload validity.

It then receives the current slot's payload by t=6s, and has until the next slot's t=3s to re-execute it, using all CPU cores. This gives it at least 9s time to handle re-execution, and potentially 10s or more, depending on how soon it sees the payload. This is roughly a 5x increase in time to handle re-execution, on top of the speedup afforded by parallel execution.

Individual validators attest once an epoch. An epoch is 32 slots, and lasts 6.4 minutes.

At 9s, 512 randomly selected validators out of the entire validator set form the PTC, the Payload Timeliness Committee, and vote on whether they have seen the payload by 6s and all blobs for it by 9s.

A proposing validator, chosen randomly to propose a block, can get payload bids at t=0s from any configured relays or builders, and from P2P. It will then typically compare those and its locally built payload, choose the one that pays the most, and publish a beacon block that contains the hash of the execution payload, but not the payload itself. The choice of whether to use a remotely built payload or a locally built payload is moderated by parameters the operator sets: Min-bid, minimum payment of a remote payload; max execution payment, maximum payment of a builder bid;
proposer boost, percentage that a remote payload has to pay above a local payload.

If choosing a local payload, the payload and all blobs can be broadcast immediately by the node.

If choosing a remote payload, the builder needs to release the payload after it sees it was chosen, and in time for the payload to arrive by t=6s. Likewise, all chosen blobs for the payload need to
arrive by t=9s.

The chance to be chosen randomly for a proposal is the validator's EB (Effective Balance) divided by the total EB of all active validators on the network. For example, a type 1 validator with 32 ETH would
have a 1 in 1 million chance, if 32 million ETH are staked total.

## Support

If you have questions or need additional support, connect with the EthStaker community on:

* Discord: [dsc.gg/ethstaker](https://dsc.gg/ethstaker)
* Reddit: [reddit.com/r/ethstaker](https://www.reddit.com/r/ethstaker/)
