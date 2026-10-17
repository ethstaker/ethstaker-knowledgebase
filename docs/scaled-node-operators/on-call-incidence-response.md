# On-Call/Incidence response

<figure><img src="/assets/img/gitbook/image (107).png" alt="" width="563"><figcaption></figcaption></figure>

As a scaled Ethereum staking provider, you're responsible for a significant part of the network's overall health and security. This guide provides you with targeted information on what to prioritize when incidents happen, ensuring that you can react effectively.

## On-Call

### What to Look for First? When Do You Raise an Alarm?

#### Key Metrics

Monitor performance and error metrics such as missed attestations, node latency, and validator performance to identify issues early. Implement alerts for any anomalies in these metrics.

#### Thresholds for Alarms

Set predefined thresholds for raising an alarm. For example, if more than 5% of validators are underperforming or if you observe an unusual surge in network requests, it should immediately trigger an alarm.

!!! info "Incident response example from GatewayFM"
    Once one of our machines went offline in one of our new bare metal providers, and we could only ask for help using the use website support ticket because we didn't have all the contacts yet. The communication was done via emails and there weren't not many updates from their side. After one hour our CEO called our account manager and we managed to create a Slack channel with their engineers. And things went quickly after that. In the end, they had to go to the data center physically and examine the machine. When the machine started again, our service was offline for 4 hours. In retrospect, it could have been longer if we didn't have the Slack channel.

    Lesson learned, always ask for a direct support/communication channel (phone, Slack, etc) when on-boarding a new data center provider.


### First Steps Required During Incidence Response

1. **Initial Assessment**: Determine the scope of the problem. Is it affecting one validator, multiple validators, or is it a network-wide issue?
2. **Isolate the Issue**: Segregate the affected validators to prevent the issue from spreading.
3. **Consult Logs**: Review system logs for any error messages or anomalies that could point to the root cause.
4. **Communication**: Notify your internal team. Transparency and quick communication are vital, especially if the issue impacts more than your operations.

### What Channels to Reach Out to if You Think It's a Network Attack?

1. **Message Channels and Forums**: While it's sensitive information, sharing what you suspect is an attack on public channels like Discord or Reddit can be valuable for corroborating with others.
2. **Social Media**: Use X or other platforms to alert the community; however, be very cautious and responsible with the language you use to prevent unnecessary panic.
3. **Network Peers**: If you're part of any coalitions or partnerships with other node operators, inform them so that they can also take precautionary measures.

### What Channels to Reach Out to if It’s a Possible Vulnerability?

1. **Security Team**: Alert your internal security team first for an initial assessment.
2. **Ethereum Foundation Security**: They have a responsible disclosure process for vulnerabilities.
3. **GitHub**: If the vulnerability is in an open-source tool, you may also open a confidential issue on the respective GitHub repository.
4. **Private Communication Channels**: For less immediate vulnerabilities, reach out to trusted peers in the industry via secure, private channels to verify the issue before going public.

## Incident Response

What to look for first?

1. Is the node up and running? Is the validator client up and running? CPU/RAM/Disk space okay?
2. Read the logs. Are there enough peers? Is the number of validators found by the validator client as you expected?
3. Is your node in sync/is it syncing? If so, is it on the right fork? Take [`eth/v1/beacon/headers/head` API](https://ethereum.github.io/beacon-APIs/#/Beacon/getBlockHeader) and check it against any public block explorer or in a community.
4. Is the network finalizing? [`eth/v1/beacon/headers/finalized` API](https://ethereum.github.io/beacon-APIs/#/Beacon/getBlockHeader) -- should be moving every 6.2 minutes.

***

Being a scaled node operator comes with the responsibility of ensuring the network's security and efficiency. Adequate preparation and knowing precisely what to focus on when issues arise will make your incidence response effective and timely. Always remember, in times of incidents, swift action and clear communication are key.

> <img src="/assets/img/gitbook/image (108).png" alt="" data-size="line">The information in the Scaled Node Operators section has been written and reviewed by [Igor Mandrigin](https://x.com/mandrigin) and [Gateway.fm](https://gateway.fm), a leading large scale Ethereum staking infrastructure provider.
