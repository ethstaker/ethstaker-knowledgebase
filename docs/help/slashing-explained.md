# I'm worried about slashing 🔪

Slashing is a scary word. But what exactly is it, how can it happen and how worried should you be?

!!! info "Info"

    TLDR: Realistically, the only condition that can cause a [slashing event](../../staking-glossary#slashable-offenses) is if you run your validator's keys on two nodes at the same time (such as a failover / redundancy setup, where your backup node accidentally turns on while your main node is still running). Don't let this happen, and you won't get slashed.

    **Slashing cannot occur from being offline for maintenance**.

For a helpful visualization of various types of downtime penalties and less-common slashing conditions, see the [Staking Penalties and Slashing visual](https://ethstaker.org/staking-penalties).

### What is Slashing?

Slashing is a term used to describe the response of the Ethereum network to a validator acting against the rules of the network. Validators perform a number of duties (e.g. [attestations](../../staking-glossary#attestation) and [proposing blocks](../../staking-glossary#block-proposer)).

If someone wanted to attack the Ethereum network they could propose multiple blocks or attest to multiple conflicting blocks. To disincentivize attacks on the network, in a [Proof of Stake (PoS)](../../staking-glossary#proof-of-stake-pos) system, validators have something at stake, which is currently 32 ETH per validator. When a validator breaks the rules of the network, two things will happen:

1. The validator has some amount of ETH taken from that initial 32 ETH staked balance.
2. The validator is force exited and removed from the [validator pool](../../staking-glossary#validator-pool).

The amount of ETH taken as a penalty varies on the state of the network. If a small number of validators are slashed simultaneously, then a rough estimate of the slashing penalty is 1 or 2 ETH. In an incredibly rare Black Swan event, when a large portion of the network is simultaneously offline or breaking the rules (e.g. in a coordinated attack) then the slashing penalty can be up to and including 100% of the stake.

When your validator is force exited and the stake is withdrawn you are able to re-stake your remaining ETH (if you still have the 32 required), after going through both the [exit queue](../../staking-glossary#validator-queue) and [activation queue](../../staking-glossary#validator-queue) again.

### Slashing Tracker

<div class="grid">
  <a href="https://explorer.rated.network/slashings" class="card">Slashings | Ethereum Mainnet</a>
</div>
