# How does my validator earn ETH?

Validators that participate in securing the [Beacon Chain](../../staking-glossary#beacon-chain) and execute "duties" get rewarded for this by new issuance of ETH. In addition, validators receive priority fees paid by users, and optionally [MEV](../../staking-glossary#MEV). Validators are rewarded for executing those duties by new ETH issuance to the "validator balance". The current APY can be seen on the [official launchpad ↗](https://launchpad.ethereum.org/).

| Type                                                    | Layer                                               | Frequency                                                                                  | Amount                                        |
| ------------------------------------------------------- | --------------------------------------------------- | ------------------------------------------------------------------------------------------ | --------------------------------------------- |
| [Attestation](../../staking-glossary#attestation)       | [Consensus](../../staking-glossary#consensus-layer) | Once per [Epoch](../../staking-glossary#epoch) (every 6.4 minutes on average)              | 0.000014 ETH\*                                |
| [Block Proposal](../../staking-glossary#block-proposer) | [Consensus](../../staking-glossary#consensus-layer) | [Every 2 months on average](../../rewards/proposal-frequency)                                         | 0.02403 ETH\*                                 |
| [Sync Committee](../../staking-glossary#sync-committee) | [Consensus](../../staking-glossary#consensus-layer) | Every 2 years on average\*\*                                                               | 0.11008 ETH\*                                 |
| [Slashing Reward](../../staking-glossary#slasher-node)  | [Consensus](../../staking-glossary#consensus-layer) | Very rarely included in Block Proposals                                                    | Up to 0.0625 ETH                              |
| [Priority Fees](../../staking-glossary#priority-fees)   | [Execution](../../staking-glossary#execution-layer) | Included in every Block Proposal containing transactions                                   | Typically 0.01 to 0.1 ETH; very rarely 1+ ETH |
| [MEV Rewards](../../staking-glossary#mev)               | [Execution](../../staking-glossary#execution-layer) | Also included in Block Proposals when using [MEV-boost](../../validator-clients/mev-boost) | Typically 0.01 to 0.1 ETH; very rarely 1+ ETH |

\*_Varies based on the total number of validators in the network. Estimate shown approximated for 435,000 active validators._

\*\*_These are subject to randomness; there can be "dry spells" multiple times longer than the average without being given one._

ETH on the [Consensus](../../staking-glossary#consensus-layer) layer is not liquid as it is being staked. Balances above 32 ETH will be automatically skimmed if a withdraw credential has been set, but to access the principal 32 ETH you will need to exit the validator.

Rewards provided on the [Execution](../../staking-glossary#execution-layer) layer are liquid and can be accessed instantly.

[Source ↗](https://docs.rocketpool.net/guides/node/responsibilities.html#how-ethereum-staking-works)

## Validator penalties

If the validator is offline and not executing its duties, it will be penalized at a rate slightly lower than the rewards for the same period of time.

Validators are penalized for small amounts of ETH if they are offline and fail to perform their assigned duties. This is called [**leaking**](../../staking-glossary#inactivity-leak). If a validator violates one of the core rules of the Beacon chain and appears to be attacking the network, it may get [**slashed**](../../staking-glossary#slashable-offenses). Slashing is a forceful exit of your validator without your permission, accompanied by a relatively large fine that removes some of your validator's ETH balance.

Realistically, the only condition that can cause a slashing is if you run your validator's keys on two nodes at the same time (such as a failover / redundancy setup, where your backup node accidentally turns on while your main node is still running). Don't let this happen, and **you won't get slashed**. Slashing _cannot occur_ from being offline for maintenance.

Below is a table that shows the penalties that can happen to a validator:

| Type                                                           | Layer                                               | Amount                                                                            |
| -------------------------------------------------------------- | --------------------------------------------------- | --------------------------------------------------------------------------------- |
| Missed [Attestation](../../staking-glossary#attestation)       | [Consensus](../../staking-glossary#consensus-layer) | -0.000011 ETH\* per attestation (-9/10 the value of a normal attestation reward)  |
| Missed [Block Proposal](../../staking-glossary#block-proposer) | [Consensus](../../staking-glossary#consensus-layer) | 0                                                                                 |
| Missed [Sync Committee](../../staking-glossary#sync-committee) | [Consensus](../../staking-glossary#consensus-layer) | -0.00047 ETH\* per epoch (-0.1 ETH total if offline for the whole sync committee) |
| [Slashing](../../staking-glossary#slashable-offenses)          | [Consensus](../../staking-glossary#consensus-layer) | At least 1/32 of your balance, up to your entire balance in extreme circumstances |

\*_Varies based on the total number of validators in the network. Estimate shown approximated for 435,000 active validators._

!!! info "Info"
    As a rule of thumb, if you're offline for X hours (and you aren't in a [sync committee](../../staking-glossary#sync-committee)), then you'll make all of your leaked ETH back after X hours once you're back online and attesting.

    [Source ↗](https://docs.rocketpool.net/guides/node/responsibilities.html#penalties)
