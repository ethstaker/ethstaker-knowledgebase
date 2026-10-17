# My validator is offline! What do I do?

## Don't Panic!

The penalty for missing attestations is exactly the same as the reward for a successful one. Any downtime penalty will be recovered in the same amount of uptime.

[Proposing a block is rare](../../rewards/proposal-frequency). Depending on the size of the [validator pool](../../staking-glossary#validator-pool), a single validator will on average only propose a block every few months. If you are unlucky enough to be offline at the time that your validator is asked to propose a block, that's also ok.

The Ethereum network is robust and designed to handle these situations. If you miss your block proposal, the [slot](../../staking-glossary#slot) that should have contained your block will be empty. Other than the lost [rewards](../../rewards/chain-rewards) from missing the block proposal, there are **no penalties or slashing** that occurs from a missed block proposal.

If you have a large number of validators or want to minimize your downtime, [consider running a second consensus and execution client pair and adding this endpoint to your already running validator client. ](https://docs.ethstaker.cc/ethstaker-knowledge-base/tutorials/methods-to-minimize-downtime#running-multiple-consensus-execution-client-pairs)This will ensure that if one of your client pairs goes down, your validator client will automatically fallback to the other one.

Doing this is a supported function by all validator client software as each client has slashing protections to ensure that you do not attest twice, so you will not get you slashed. &#x20;

**Do not** however, configure a second validator service. By doing so your risk of slashing goes up _massively_. You should only ever have your validator keys in one place at any one time. Missing out on a few days of rewards may seem bad at the time, but getting slashed and bleeding ETH while you wait out the 5 week exit period post-slashing is a lot worse!

Having a second consensus-execution clients is great, but having a second validator client **is not.**&#x20;
