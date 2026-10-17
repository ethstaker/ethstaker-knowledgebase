# Methods to minimize downtime

!!! info "Info"
    This is a reminder that you should never have your validator keys configured across multiple machines at the same time, because if the same validator key is active twice across the network _it will get_ [_slashed_](../../staking-glossary#slashable-offenses). They should _only_ ever be configured to run in one place at one time!


With that out of the way, let's get into it. There are a few things that you can do to minimize your potential downtime.&#x20;

There will always be situations where you will have downtime, it is inevitable when running a validator so please don't chase a perfect attestation record. There are however some things you can do to _minimize_ downtime.

The below ideas may or may not be feasible depending on how many validators you are running. Please weigh up the pros and cons yourself and decide if it is appropriate for you to do in your circumstances.

### Connecting your node and router to a UPS

This will ensure abrupt shutdowns don't occur potentially saving your hardware from breaking, or your DB/OS from corrupting saving you a resync/reinstall. More information can be found about this on the [hardware best practices page.](../../hardware/hardware-best-practices)

### **Running multiple Consensus-Execution client pairs.**

Either on the same machine but on a different SSD or an entirely separate machine and running different consensus/execution client software. A separate machine is more important _if_ you are running a sizeable number of validators, otherwise, it may be overkill.

It is perfectly safe to run multiple nodes for redundancy, just not multiple validators. [Lighthouse for example supports this natively.](https://lighthouse-book.sigmaprime.io/redundancy.html)

The benefit of doing this is you won't have any downtime should one of the client pairs go offline, or corrupt, or if the SSD where it is sitting breaks and it requires manual maintenance to bring back online. You'll be able to fix the broken node in your own time while the validator will happily use the other configured beacon node and continue performing its duties.

You can even take it a step further and have your validator client on a separate SSD (For example, with your OS) and have it point to your beacon nodes, both of which would _also_ be on separate SSDs, with less points of failure all around.

### **Having spare hardware ready to go.**

It can be useful to have a spare SSD ready to be swapped out in case of hardware failure. You will be able to immediately start the process to recover your nodes/validators and when that is done you can then buy a replacement drive at your own leisure.

If you travel around a lot, you could even have it plugged into your machine on standby ready to go meaning your node could be recovered remotely, unless of course, the drive that fails is your OS drive.

There will be times when you are offline and are missing attestations, do not stress or panic when this happens and focus on getting yourself back online. If for example, you are offline for 4 hours, it will take 4 hours of being online to be back where you started in terms of validator balance.

For more information about downtime see our helper posts:&#x20;

* [I'm worried about downtime 😔](../../help/downtime-explained)
* [I'm worried about slashing 🔪](../../help/slashing-explained)
