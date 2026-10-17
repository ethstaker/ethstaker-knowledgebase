# Migration at scale

<figure><img src="/assets/img/gitbook/image (111).png" alt="" width="563"><figcaption></figcaption></figure>

For large-scale node operators managing 100s of validators, migrating validators to new servers is a crucial process that requires meticulous planning and execution. This section provides detailed guidelines and best practices for a seamless migration.

### **📝 Pre-Migration Checklist**

Before commencing the migration of Ethereum validators, a comprehensive pre-migration checklist is imperative. This checklist serves as the foundation for a successful transition, ensuring that all critical data is secured and that the new server environments are primed for a seamless takeover. This phase focuses on safeguarding validator keys, securing beacon node data, meticulously documenting server configurations, and ensuring software version consistency.

1. **Validator Keys Backup**:\
   Validator keys are the cornerstone of your Ethereum staking operation. Securing these keys is paramount to maintaining control over your validators. The backup process must be robust, secure, and foolproof.
   * Implement hardware security modules (HSMs) to store validator keys. These devices offer enhanced security features, making them ideal for protecting high-value cryptographic keys.
   * Establish a regular schedule for updating and verifying backups. This includes checking the integrity of the backups and ensuring they are uncorrupted and accessible.
   * Diversify the storage of backups by using multiple physical and geographical locations. This approach mitigates risks associated with natural disasters, power outages, or other localized incidents.
2. **Execution and Beacon Node Data Backup**:\
   Beacon nodes play a critical role in maintaining network consensus. Backing up beacon node data and the associated execution layer data ensures that you can quickly recover from hardware failures or other disruptions without compromising the network's integrity or your validators' performance.
   * Automate the backup process for the blockchain database and beacon node configuration files. Automation reduces human error and ensures consistent, timely backups.
   * Leverage incremental backup techniques to efficiently manage storage space while keeping the data up-to-date.
   * Regularly test recovery procedures to ensure that backups can be restored without issues, thereby minimizing downtime during unplanned disruptions.
3. **Server Configuration Details**:\
   Accurate documentation of server configurations ensures that the new servers can be set up identically to the old ones, minimizing the risk of configuration-related issues post-migration.
   * Use "infrastructure as code" (IaC) methodologies to codify server configurations. This approach allows for automated, error-free deployment of server environments.
   * Maintain a version-controlled repository for all IaC scripts, ensuring an audit trail of changes and an easy rollback mechanism.
   * Document every detail of the network setup, including configurations, firewall rules, and custom settings, to facilitate a precise replication on the new servers.
4. **Software Version Consistency**:\
   Consistent software versions across old and new servers are crucial to avoid compatibility issues during and after migration. This consistency is vital for both the operating system and the Ethereum staking client software.
   * Adopt containerization technologies like Docker, or use virtualization to create consistent software environments that are easily replicable across different servers.
   * Establish a procedure for regularly updating and maintaining a catalog of all software versions in use. This catalog should include not only the main staking client software but also any auxiliary tools and dependencies.
   * Document interdependencies between software components to ensure that updates or changes to one component do not adversely affect others, thereby maintaining a stable and predictable server environment.

!!! warning "Warning"
      If a backup isn't checked and verified, then it's not a backup, but a Schrodinger's backup box where the data is both restorable and not restorable at the same time. You'll only find out when it's too late, so you _**MUST**_ test your backups!


### &#x20;**🧳 Migration Process**

The migration process is a critical phase in the transition of Ethereum validators to new servers. This process involves meticulously preparing the new servers, transferring all essential data securely, and conducting thorough testing to ensure operational integrity and performance. Each step in this process is designed to minimize downtime and risk, ensuring a smooth and secure transition.

1. **Preparation of New Servers**:\
   The first step in the migration process is to prepare the new servers. This involves ensuring that the hardware is up to the task and that all systems are correctly configured and ready for deployment.
   * Perform a detailed hardware performance assessment to confirm that the new servers meet or exceed the specifications of the current servers. This assessment should include checks on processing power, memory, storage capacity, and network capabilities.
   * Develop and implement automated deployment scripts. These scripts should handle the installation and configuration of the necessary software, including the Ethereum staking clients and any related dependencies.
   * Thoroughly check network connectivity and security settings. Ensure that the new servers comply with the organization’s security protocols and that they can connect to the necessary network infrastructure without issues.
2. **Data Transfer**:\
   Safely transferring data from the old to the new servers is a delicate task. It requires a methodical approach to ensure data integrity and security.
   * Use a staged transfer process. Begin with non-critical data to test the transfer mechanism's integrity and reliability.
   * Employ secure and encrypted transfer protocols such as SFTP or SCP. This ensures that data is protected during transit and reduces the risk of interception or corruption.
   * In cases where the dataset is too large for practical network transfer, consider using physical transfer methods. This could involve shipping encrypted hard drives, ensuring data security while moving large volumes of data.
3. **Testing on New Servers**:\
   After transferring data, it is crucial to test the new servers extensively. These tests confirm the integrity and performance of the migrated systems.
   * Conduct a series of comprehensive tests, including load testing and failover simulations. Load testing checks the servers’ performance under high usage, while failover simulations test the resilience of the system in case of a server failure.
   * Verify the integrity of the transferred data by comparing it against the original hashes. This step is vital to ensure that no data corruption occurred during the transfer process.
   * Perform integration tests to check how the new servers interact with the rest of the network. It’s essential to ensure that this integration is seamless and does not negatively impact the ongoing operations of the network or other servers.

### **🚧 Ensuring Offline Status of Old Validators**

After the migration of Ethereum validators to new servers, it's crucial to ensure that the old servers are taken offline correctly. This stage is vital to prevent any conflicts that might arise from having validators running simultaneously on both old and new servers, which could lead to issues like accidental slashing.

1.  **Network Disconnection**:&#x20;

    The initial step in decommissioning the old servers is to isolate them from the network. This action prevents any communication between the old servers and the Ethereum network, thereby mitigating the risk of simultaneous validator operations.

    * Physically disconnect the network cables or disable the network interfaces of the old servers. This step should be done methodically to ensure that no server remains inadvertently connected to the network.
    * Implement a protocol to check and double-check that all old servers are disconnected. This might involve a physical inspection or a network scan to confirm the absence of signals from the old servers.
2.  **Destroy Old Servers:**&#x20;

    Completely eliminating the risk of the old servers inadvertently coming back online is a critical safety measure. This step involves permanently disabling or destroying the old servers.

    * In cloud environments, securely terminate the instances hosting the old validators. Ensure that all data is securely wiped and that the instances cannot be reactivated accidentally.
    * For physical servers, perform a secure formatting of the drives. This might include using specialized software to overwrite all data, ensuring that no residual data can be recovered or that the servers can be mistakenly restarted.
3. **Monitoring Tools**:\
   Continuous monitoring is essential to confirm that the old validators are fully offline and no longer part of the network. This reassurance is crucial for the overall security and integrity of the validator operation.
   * Employ network monitoring tools to keep an eye on the network traffic. These tools should be configured to detect any unauthorized or unexpected activity that might indicate the old servers are still operational.
   * Set up alerts to notify the team immediately if any activity from the old servers is detected. This prompt response mechanism ensures that any potential issues can be addressed swiftly, reducing the risk of network conflicts or security breaches.
   * Regularly review and analyze the network logs for a period post-migration to ensure that there are no traces of the old validators. This thorough analysis helps in confirming the success of the migration process and the decommissioning of the old servers.

!!! warning "Do not blindly trust monitoring tools! Implement "fail-safe" processes."
      Monitoring tools can fail. [Slashing incidents occur](https://blog.lido.fi/post-mortem-launchnodes-slashing-incident/) when things don't work as expected and tools that alert to those anomalies fail.&#x20;

      Processes should be designed to be "fail-safe" such that if something does go wrong, the outcome is a safe mode of failure. Scenarios often happen like this:

      > Admin 1: "The old servers are offline, I the monitoring tool says they are shutdown"
      >
      > Admin 2: "Ok great, I'll turn on the new servers then."
      >
      > X Post: "BREAKING! Slashing incident occurred!"
      >
      > Admin 1: "Oh, an automated system noticed the old servers were off and restarted them, I didn't expect that..."

      This is not a scenario anyone wants to experience, and implementing a fail-safe process can avoid these type of issues.

      > Admin 1: "I've turned off the old servers, physically disconnected them from the network, isolated the network they were on, formatted their drives and confirmed the servers are offline and not reachable."
      >
      > Admin 2: "Ok great, I'll turn on the new servers then."
      >
      > X Post: "BREAKING! First uneventful day in crypto recorded. Nothing bad happened."


### **🔄 Rolling Migration Strategy**

Implementing a rolling migration strategy is a prudent approach to transferring Ethereum validators to new servers. This strategy involves moving validators in controlled batches, allowing for more effective monitoring and reducing the overall risk of the migration process. By adopting this approach, you can ensure a smoother transition, with opportunities to adjust the strategy based on the performance and feedback from each batch.

1. **Batch Migration**: Migrating validators in batches, instead of all at once, provides a more manageable and less risky process. This approach allows for focused attention on each batch, ensuring a higher success rate with minimal disruption to the network.
   * Plan the migration in several phases, dividing the validators into logical groups. These groups can be based on their function, performance, or other relevant criteria.
   * Ensure each batch is small enough to manage effectively but large enough to provide meaningful insights into the migration process.
   * Develop a detailed schedule for each batch, including specific timelines and checkpoints, to maintain control over the migration process.
2.  **Test Batch**:

    Starting the migration with a test batch is a crucial step. This initial batch serves as a pilot, helping to identify any unforeseen issues or challenges that might arise during the migration.

    * Monitor the test batch closely, paying particular attention to performance metrics and potential issues.
    * Use the insights gained from this test batch to refine and optimize the process for subsequent batches.
3. **Monitoring and Verification**:\
   Continuous monitoring and verification after each batch migration are essential to ensure the validators are operating correctly on the new servers.
   * Implement robust monitoring tools to track the performance and behavior of the newly migrated validators.
   * Verify that each batch of validators is correctly interacting with the Ethereum network and performing as expected.
   * Conduct a post-migration review for each batch, documenting any issues and the steps taken to resolve them.
4. **Iterative Approach**:\
   An iterative approach to migration allows for continuous improvement of the process. Feedback and performance data from each batch should inform adjustments and refinements for subsequent batches.
   * After each batch, gather feedback from the team involved in the migration process. This feedback should cover technical, operational, and performance aspects.
   * Analyze performance data to identify any trends or recurring issues.
   * Adjust the migration plan and strategy based on this analysis, applying lessons learned to future batches to increase efficiency and reduce potential risks.

### **✅ Post-Migration**

The post-migration phase is crucial in solidifying the success of the Ethereum validators' transfer to new servers. This phase involves rigorous data validation, continuous performance monitoring, having redundancy plans in place, and thorough documentation and reporting. Each aspect is essential to ensure the integrity and optimal performance of the validators in their new environment.

1. **Data Validation**:\
   Post-migration, it's imperative to verify that all data transferred to the new servers is intact and accurate. This step ensures that the validators operate based on complete and uncorrupted data.
   * Perform detailed checks to compare the transferred data with the original datasets. This can include hash checks, record counts, and sample data verification.
   * Validate the operational status of each validator, ensuring they are actively and correctly participating in the network.
   * Employ automated scripts to scan through data and flag any inconsistencies or missing elements for further investigation.
2. **Performance Monitoring**:\
   Continuous monitoring of the validators' performance on the new servers is essential to promptly identify and address any issues.
   * Set up comprehensive monitoring systems to track various performance metrics such as block production, attestation effectiveness, and hardware resource utilization.
   * Establish alerts for any deviations from expected performance benchmarks.
   * Regularly review performance data to identify trends or patterns that may require intervention or optimization.
3. **Redundancy Plans**:\
   Despite thorough planning and execution, unforeseen issues can arise. Having a redundancy or rollback plan is crucial for quick recovery without significant impact.
   * Keep the old servers in a standby mode for a predetermined period after migration. This acts as a safety net in case a rollback is necessary.
   * Document and rehearse the rollback process to ensure a swift and efficient response if needed.
   * Regularly update and test backup systems even after migration to ensure they are ready for use in any emergency rollback scenario.
4. **Documentation and Reporting**:\
   Detailed documentation and reporting of the entire migration process are vital for future reference and for understanding the migration's impact.
   * Create comprehensive reports detailing each step of the migration process, including strategies used, challenges encountered, and solutions implemented.
   * Document any performance improvements or operational enhancements observed post-migration.
   * Share these insights with relevant teams and stakeholders to inform future migrations and to contribute to the organization’s knowledge base.

***

Migrating validators to new servers at scale is a complex process that requires careful planning and execution. Following these guidelines and best practices will help ensure a smooth transition with minimal downtime or risk to your validators. Always prioritize the security and integrity of your validator keys and data during the migration process.

> <img src="/assets/img/gitbook/image (108).png" alt="" data-size="line">The information in the Scaled Node Operators section has been written and reviewed by [Igor Mandrigin](https://x.com/mandrigin) and [Gateway.fm](https://gateway.fm), a leading large scale Ethereum staking infrastructure provider.
