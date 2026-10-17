# Common errors and mistakes

<details>

<summary>My Geth is throwing errors and not syncing</summary>

A common cause of Geth's errors is an improper shutdown, for instance, due to power outage, or not enough time for a graceful process exit as geth writes data to disk. As a permanent fix for the latter case, you'll want to increase your systemd service's `TimeoutStopSec` value to at least `300`.

To fix, you can [resync Geth](https://app.gitbook.com/o/5TLAFycQGS1YA3kIVVOf/s/KnJhWg57YoZq2MPfatKE/\~/changes/57/tutorials/resync-geth).

</details>

<details>

<summary>Running network-wide Pihole? My node is experiencing DNS issues. </summary>

By Pihole's default settings, DNS rate limiting blocks any clients with >1000 queries per 60 seconds.

To fix, either increase the queries limit value or exclude your node from Pihole's DNS.

</details>

<details>

<summary>My Ledger Nano Hardware Wallet can't deposit 32ETH for a new validator</summary>

If you encounter difficulty making the deposit transaction, enable blind signing and contract data.

</details>
