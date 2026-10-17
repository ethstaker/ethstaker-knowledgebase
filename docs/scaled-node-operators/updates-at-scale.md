# Updates at scale

<figure><img src="/assets/img/gitbook/image (1).png" alt="" width="535"><figcaption></figcaption></figure>

Rolling out software upgrades is a common operation task. It is often overlooked during the service scaling up. Ensuring that the new release is deployed in time is particularly important for running Ethereum or blockchain infrastructure in general because:

* New upgrades & forks are only supported by the new release, failing to do so in time will result in the node stopping syncing or producing invalid blocks. In the worst-case scenario, it will cause validators going offline.
* New releases might contain security patches. It will harden the network and your system, preventing financial or data loss.

While understanding the importance of timely software upgrades is crucial, it's also essential to recognize the challenges associated with implementing them effectively. In the next section, we'll discuss the difficulties of maintaining up-to-date software at scale and best practices for overcoming these obstacles.

## Challenges

### Technical challenges

Managing software upgrades becomes increasingly complex as the number of nodes and clients in a network grows. When operating at scale, challenges such as breaking changes in configurations and newly introduced bugs can significantly impact the upgrade process. Furthermore, updating in production environments is more difficult due to the need to minimize downtime.

### Non-technical challenges

Apart from technical issues, several non-technical challenges can hinder the upgrade process:

* **De-prioritization:** Software upgrades can often be considered as good-to-have rather than essential, leading to outdated software and potential security vulnerabilities.
* **Different versioning schemas:** Inconsistent versioning schemes across clients can complicate the upgrade process and increase the likelihood of errors.
* **Too many software releases to track:** Monitoring and managing numerous software releases that require regular updates can be a daunting task, especially in large-scale environments with multiple nodes and clients.

While these challenges can seem overwhelming, adopting effective strategies, processes, and best practices can streamline the software upgrade process. In the following sections, we'll discuss potential solutions to address the challenges faced by Ethereum validator operators during software upgrades.

## Solutions

### 1. Keep an inventory of what you have in the system

> If you haven't already, consider tracking your deployments and configurations in a Git repository or adopting GitOps practices for streamlined version control and consistency.

A software inventory is a comprehensive record of all software components within your system, including client implementations, versions, and configurations. Maintaining an up-to-date software inventory is crucial for successful software upgrades, as it helps you better plan for and execute upgrades while minimizing the risk of unexpected issues. The following approaches can help you achieve a well-organized software inventory:

* **Metrics:** Many clients expose version information through their Prometheus metrics, making it simple to create a Grafana panel that displays version information for all your workloads. By visualizing this data, you can easily monitor software versions and identify any discrepancies that may require attention.

<figure><img src="/assets/img/gitbook/image (1) (1) (1).png" alt=""><figcaption><p>A panel for Lighthouse version distribution</p></figcaption></figure>

* **Third-party tools:** Leverage third-party tools to help manage your software inventory. There are many open-source tools available for generating inventory reports. If you're using Kubernetes, you can use [Kubernetes Inventory Docker image](https://hub.docker.com/r/linkbn/kubernetes-inventory) or [Anchore's k8s-inventory](https://github.com/anchore/k8s-inventory) to help you track client versions in your deployments.
* **In-house solution:** Develop a custom in-house solution tailored to your specific needs, such as a simple shell script. Creating a solution that fits your organization's requirements allows for seamless integration with your existing systems and processes.

<figure><img src="/assets/img/gitbook/image (10).png" alt=""><figcaption><p>Gateway.FM in-house tool</p></figcaption></figure>

### 2. Stay informed about new software releases

To keep your software up to date, it's essential to stay informed about the latest releases and improvements. Most software projects publish new releases on GitHub, making it an ideal starting point to subscribe to new release events for all the clients you use. There are several tools and services available to help you accomplish this:

* **GitHub's built-in subscription feature:** Use the native subscription feature on GitHub to receive notifications about new releases from your followed repositories.
* **NewReleases.io:** [NewReleases.io](https://newreleases.io/) is a handy service that allows you to track new releases across various platforms, including GitHub.

<figure><img src="/assets/img/gitbook/image (3).png" alt=""><figcaption><p>Track releases on newreleases.io</p></figcaption></figure>

* **Other alternatives:** Explore [alternative services](https://alternativeto.net/software/newreleases/) for monitoring new software releases and choose the one that best suits your needs.

Alternatively, you can develop a custom bot tailored to your requirements for tracking new releases and staying informed about the latest updates.

### 3. Plan for software upgrades

Proper planning is crucial for the smooth execution of software upgrades. By incorporating software upgrade planning into your project management process, you can ensure timely implementation, address the risk of de-prioritization, and mitigate potential technical issues due to more time to research and prepare.

* Ensure that all important data is backed up in advanced. Have a detailed, repeatable process for this. A backup is only truly a backup if you are actually able to restore it, so make sure to test the full end to end process, not just to assume that if you too a backup that it will work.
* Make sure you talk about software upgrades in the planning session: For example, if your team uses Scrum and conducts planning every two weeks, allocate 20 minutes just to go through all the software new releases. This practice will help ensure that upgrades are prioritized and completed within the designated time frame.
* Check for deadlines and breaking changes: When you go through the releases, make sure you check for any deadlines associated with software upgrades, such as hard forks or security patches, and plan accordingly. Also, examine the release notes for breaking changes that may require additional work or adjustments to your existing configurations. Keep in mind that some changes, like database upgrades, might be irreversible and must be rolled out with care.

### 4. Automate the software upgrade process

Automation can significantly streamline the software upgrade process, minimizing the risk of human error and reducing the time required to complete the upgrade. Implementing automation in your upgrade process can increase efficiency and ensure that updates are consistently applied. Here are some example tasks that can benefit from automation:

* **Automated OS Security Patches and Updates:** Use automated systems for scheduling and deploying patches. This reduces human error and ensures timely update. Classify patches based on security risk and functionality impact. Prioritize critical security patches to mitigate vulnerability risks. Implement patches in stages, start with a small, controlled group to identify potential issues before wider deployment. Test patches in a separate environment to ensure compatibility and functionality without affecting live systems. Maintain detailed records of all patches for compliance. Document the patch, affected systems, and deployment dates.
* **Automated pull requests:** Utilize tools or scripts that automatically create pull requests when new software releases are detected, updating the deployment definition accordingly. This approach ensures that your system stays up-to-date with the latest software versions and reduces the manual effort required to initiate updates.
* **Automated rollout and rollback:** Use tools like Argo Rollouts to define acceptance criteria and roll out new versions automatically. This method is particularly useful if you require several hours to confirm the success of each deployment. Additionally, these tools often provide built-in rollback capabilities, ensuring that your system can quickly recover from any issues encountered during the upgrade process.
* **Incremental rolling upgrades:** When running Ethereum validators, unless there is a critical update required, it is usually the case that not all nodes need to all be updated at the same time. To avoid problems with new versions of software having bugs, incrementally upgrading nodes during automated upgrades can improve resiliency.

By incorporating automation into your software upgrade strategy, you can greatly improve the overall efficiency and reliability of your update process, ensuring that your Ethereum nodes remain secure and up-to-date.

### 5. What to do when something goes wrong

A key principle of DevOps is to treat servers like "cattle, not pets". This means that infrastructure should not be seen as unique snowflakes, but instead as replaceable. When an update doesn't work as expected, e.g. a database gets corrupted, rather than on the fly creating exotic new scripts and performing heroics in an attempt to fix it, processes should be in place that demand servers be shut down and recreated.

Important data, such as validator keys, should already be securely backed up. If you're ever in a situation where an update breaks a server and you lose critical data, it is not the fault of the update but some important steps missing from your processes!

***

Keeping software up-to-date requires commitment and is an essential part of operating a secure and stable blockchain infrastructure, such as Ethereum. By understanding the challenges associated with software upgrades and implementing effective solutions, such as maintaining an accurate software inventory, staying informed about new releases, planning for upgrades, and automating the upgrade process, you can ensure timely and successful software updates.

Updates at scale are a complex yet critical component of maintaining a large-scale Ethereum staking operation. By following these guidelines and continuously refining your processes, you can achieve a balance of security, performance, and reliability in your infrastructure.

### Other Resources

<div class="grid">
  <a href="https://www.kiln.fi/post/ethereum-upgrades-at-scale" class="card">Ethereum upgrades at scale</a>
</div>

> <img src="/assets/img/gitbook/image (108).png" alt="" data-size="line">The information in the Scaled Node Operators section has been written and reviewed by [Igor Mandrigin](https://x.com/mandrigin) and [Gateway.fm](https://gateway.fm), a leading large scale Ethereum staking infrastructure provider.
