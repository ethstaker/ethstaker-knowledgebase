# Alerting at scale

<figure><img src="/assets/img/gitbook/image (105).png" alt="" width="563"><figcaption></figcaption></figure>

Alerts should be carefully selected. It’s easy to set thresholds on every possible monitored metric and add an alarm to it... 🚨🚨🚨

But that leads to fatigue, distractions, and eventually ignoring alerts, see [this article](https://www.atlassian.com/incident-management/on-call/alert-fatigue) for more details.

Alerts should **never be ignored**, even if you think you have an idea what caused them. If you receive an alert, follow up on it and determine if it was a false positive, overly cautious, or a valid alert. If it is not a valid alert, update the process to ensure that it does not happen again in the future.

Multiple layers of alerting can help to reduce single points of failure and provide confidence in the metrics when something does go wrong. In an Ethereum validator example, alerting that says a validator machine is not contactable would be useful, but not enough on its own. Couple this with monitoring of the Beacon Chain to get alerts when a validator is missing attestations and you'll be much more confident that something is wrong.

For good tips on alerting in general, see [“My Philosophy on Alerting”](https://docs.google.com/document/d/199PqyG3UsyXlwieHaqbGiWVa8eMWi8zzAn0YfcApr8Q/edit).

### 🚨 What makes a good alert?

1. **Relevance and Specificity**: A good alert is highly relevant to the system's overall health and performance. It should target specific conditions that are indicative of real issues, avoiding general or vague triggers. This specificity helps in the quick identification and resolution of problems.
2. **Actionable Information**: The alert should provide enough information for immediate action. It needs to be clear about what the problem is, where the problem is, and ideally, suggest potential solutions or next steps. This reduces the time spent in diagnosing the issue.
3. **Prioritization**: Alerts should be categorized based on severity and impact. Critical alerts that require immediate attention should be distinguishable from lower-priority ones. This prioritization helps in managing and responding to alerts effectively.
4. **Minimization of False Positives**: A good alert system minimizes false positives. Frequent false alarms can lead to alert fatigue, causing important alerts to be overlooked. Regular review and adjustment of alert thresholds are necessary to maintain their accuracy and effectiveness.
5. **Contextual Information**: Providing context, such as historical data or related events, can be invaluable in understanding the significance of an alert. This helps in assessing the severity and potential impact of the issue.
6. **Integration with Response Systems**: Effective alerts are integrated with incident response systems or protocols. This integration ensures that alerts trigger appropriate responses, whether it’s notifying the right team or initiating automated remediation processes.
7. **Continuous Improvement**: A good alert system is not static. It evolves based on feedback and changes in the system it monitors. Regular reviews and updates to the alerting criteria and thresholds are essential for maintaining its effectiveness.
8. **Escalation Pathways**: There should be clear escalation pathways for alerts that are not addressed within a certain timeframe. This ensures that critical issues do not remain unresolved due to oversight or unavailability of initial responders.

By adhering to these principles, an alerting system can be both effective and efficient, providing timely and useful information to maintain the health and performance of the system it monitors.

#### Useful links:

* [Google SRE Handbook](https://sre.google/sre-book/table-of-contents/)

### 🤔 Should all alerts be on-call alerts?

There is a practice in every cloud service, called “being on-call”. That means that at some moment in time, there is a person responsible for reacting to alerts, regardless of when they happen.

<div class="grid">
  <a href="../../scaled-node-operators/on-call-incidence-response" class="card local">On-Call/Incidence response</a>
</div>

An example of the on-call policy can be found in this [GitLab On-Call Handbook](https://about.gitlab.com/handbook/on-call/).

Not all alerts necessitate an on-call response. While on-call duties are a critical component in operations, especially in cloud services, they involve individuals being ready to respond to alerts at any hour, including nights and weekends. This responsibility can be demanding and exhausting, hence the importance of regularly rotating staff in these positions.

The necessity for an alert to trigger an on-call response depends on several factors:

1. **Severity of the Issue**: Critical issues that can cause significant downtime or data loss should trigger on-call alerts. These require immediate attention to prevent or mitigate major impacts.
2. **Urgency of Response Needed**: If the issue can wait until regular working hours without causing significant harm, it may not need to be an on-call alert.
3. **Frequency of the Alert**: If an alert is triggered frequently but doesn't always require immediate action, it may be better handled during normal hours to avoid unnecessary disruptions.
4. **Availability of Automated Responses**: Some alerts can be resolved through automated processes, reducing the need for immediate human intervention.

In summary, while on-call alerts are crucial for addressing critical issues promptly, not every alert warrants an immediate on-call response. The decision should be based on the severity, urgency, frequency, and the possibility of automation in handling these alerts.

### 🔔 What alerts do we need for running staking services?

Running Ethereum staking services efficiently requires a robust and well-thought-out alerting system. This system should ensure maximum uptime and quick response to any issues that might affect staking operations. Here are key alerts necessary for managing Ethereum staking services:

1. **Validator Node Downtime**: Alerts for any downtime or unresponsiveness in validator nodes are crucial. Since continuous validator duties are essential for staking, any downtime can lead to missed rewards and penalties.
2. **Missed Attestations**: Monitoring and alerting for missed attestations are important. Validators need to constantly attest to the state of the blockchain, and missed attestations can indicate issues with network connectivity, hardware, or software.
3. **Hardware Health Monitoring**: Alerts related to the physical health of the servers, such as CPU temperature, disk space, and memory usage, help in preempting hardware failures that could affect staking operations.
4. **Network Connectivity Issues**: Since Ethereum staking relies heavily on network performance, alerts should be set up for any network connectivity issues or significant changes in latency.
5. **Software Updates and Forks**: Alerts for pending updates or upcoming forks in the Ethereum network are essential to ensure that the staking operation remains compatible and secure.
6. **Security Breaches or Anomalies**: Implementing alerts for any security breaches or unusual activities is crucial for protecting the staking infrastructure from malicious attacks. This could include alerting for access to staking key infrastructure.
7. **Performance Metrics**: Alerts based on performance metrics like changes in validator success rate, or participation rate, can give early warnings about potential issues in the staking process.
8. **Regulatory Compliance**: If applicable, alerts concerning regulatory compliance are important to ensure that the staking operations adhere to evolving regulations in different jurisdictions.
9. **Smart Contract Events**: For services using smart contracts, alerts for specific contract events like withdrawals, deposits, or contract updates are necessary.
10. **Delays in Attestations (Node Suboptimal Performance)**: Alerts for delays in attestations are crucial. Attestation delays can be a symptom of suboptimal performance of validator nodes. These delays might be due to various factors such as software issues, overloaded systems, or network congestion. Setting up alerts for these delays helps in identifying and rectifying performance issues before they lead to missed attestations and potential penalties.
11. **Long Block Processing Times**: Monitoring block processing times is important, as prolonged processing times can indicate deeper issues within the staking infrastructure. Alerts for unusually long block processing times can signal problems such as inadequate hardware resources or network bottlenecks. Early detection and resolution of these issues are vital to maintaining the efficiency and reliability of the staking service.

By monitoring these aspects and setting appropriate alerts, Ethereum staking services can operate reliably, maintain security, and optimize their staking rewards while minimizing risks and penalties.

> <img src="/assets/img/gitbook/image (108).png" alt="" data-size="line">The information in the Scaled Node Operators section has been written and reviewed by [Igor Mandrigin](https://x.com/mandrigin) and [Gateway.fm](https://gateway.fm), a leading large scale Ethereum staking infrastructure provider.
