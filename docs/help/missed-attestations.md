# Missed Attestations! What can I do?

## Don't panic!

Missing some [attestations](../../staking-glossary#attestation) is completely normal and extremely low-cost. The penalty for missing an attestation is exactly the same as the reward for a successful one. So, with around 240 attestations per day per validator, missing one or two is still a successful attestation rate of over 99%!

## Understanding missed attestations, low effectiveness and improving your setup

> There are two causes of missing an attestation or having a low effectiveness with your validator. Some causes are under your control as a staker and some causes are outside of your control.

Even with a perfect setup, you might miss some attestations or incorrectly vote during an attestation lowering your [effectiveness](../../staking-glossary#effectiveness) once in a while. Causes that are outside of your control are often related to network propagation or related to some of your [peers](../../staking-glossary#peers) being late in performing their own duties.

To go on a deep dive and learn everything about the attestation duty, timings, effectiveness and network propagation, check out these great articles.

- [Understanding Attestation Misses ↗](https://www.symphonious.net/2022/09/25/understanding-attestation-misses/) by Adrian Sutton
- [Exploring ETH2: Attestation Inclusion ↗](https://www.symphonious.net/2020/09/08/exploring-eth2-attestation-inclusion/) by Adrian Sutton
- [Defining Attestation Effectiveness ↗](https://www.attestant.io/posts/defining-attestation-effectiveness/) by Jim McDonald

As a staker, you cannot do much about the causes that are outside of your control. What you can do is work on elements of your setup that are under your control to maximize your rewards. Even if you have a setup that was performing well before the merge, it's possible that with the additional work being introduced, some overlooked part of your setup might be the cause of additional misses or lower effectiveness since the merge happened. That's why you should double check all these items.

1. Make sure your clients are _up-to-date_. Client updates often include optimizations and improvements that will help perform your duties on time.

2. Make sure your machine consistently has enough _resources_ (CPU, RAM, disk, etc). Using a dedicated machine can help. If your clients are starved of any of these resources, it will likely be a cause for more misses and lower effectiveness.

3. Make sure your _time_ is properly in sync. The beacon chain protocol is quite time sensitive. chrony is a good tool to improve your time sync. On Ubuntu or Debian derivatives, installing chrony is often as easy as `sudo apt install chrony`. On Windows, you can use [these instructions ↗](https://www.reddit.com/r/ethstaker/comments/nfca22/an_opiniated_solution_to_improve_time_sync_on/) to improve your time sync.

4. Make sure you have good _internet_ latency, bandwidth and quality. For home validators, it's unrealistic to ask for a dedicated ISP or internet connection for your validator, but make sure your other network uses don't interfere too much with your validator. In case of doubt, see if you can get a better plan from your provider or check if there is an alternative provider in your area that can improve your internet.

5. Make sure you consistently have enough _peers_. Monitoring your clients peers count is not a bad idea if you have the technical ability.

6. Make sure you have properly configured _open ports_ that permit incoming connections. Not only can this improve your setup networking health and your peers count, but it will also improve the Ethereum network health as a whole. To test if your ports are opened, you can use the StakeHouse open ports checker. Calling `curl https://eth2-client-port-checker.vercel.app/api/checker?ports=30303,9000` should return a result that includes 30303 and 9000 in the `open_ports` field if those ports are opened from the Internet. 30303 is the default P2P port for Geth and 9000 is the default P2P port for many consensus clients. Adjust these values if you use custom ports or if you use clients which have different default ports. Consult your client documentation to find more about this.

Once you have those in place, there is little more you can do to help. There might be some marginal benefits in connecting with more peers at the cost of higher resources usage, especially bandwidth. Under normal circumstances, the default peers count from your clients should be good. Monitoring internet quality with tools like those from [pingman ↗](https://pingman.com/) can help pinpoint the cause of some of these missed attestations if they are network related, but it will likely still be out of your control.

[Source ↗](https://www.reddit.com/r/ethstaker/comments/xto0dm/understanding_missed_attestations_understanding/)
