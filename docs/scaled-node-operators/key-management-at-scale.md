# Key management at scale

<figure><img src="/assets/img/gitbook/image (110).png" alt="" width="563"><figcaption></figcaption></figure>

Effective key management is crucial for Ethereum validators, especially at scale. Poor key management has historically been a primary reason for [validators being slashed](https://blog.lido.fi/post-mortem-launchnodes-slashing-incident/). Understanding and implementing robust key management practices is essential to maintain both the integrity and security of validator operations.

**Best Practices**

* **Systematic Tracking of Keys**:\
  Maintaining an organized record of all keys is vital. Utilize key management software to track the status and usage of each key. Regular audits and checks are necessary to ensure accuracy.
* **Backup Strategies**:\
  Implement a robust backup protocol for keys. Backups should be stored securely, ideally in physically different locations to mitigate risks like natural disasters or local hardware failures.
* **Risks of Hot Standbys**:\
  While hot standbys offer quick recovery, they can be vulnerable to attacks if not properly secured. Ensure these systems are as secure as the primary systems and limit their exposure to potential threats.
* **Use of Web3Signer**:\
  Incorporate Web3Signer for secure and scalable key management. It separates key management from validator duties, reducing the risk of key exposure and facilitating ease of management across multiple validators.
* **Integration with Secure Vaults**:\
  Store keys in secure vaults, such as hardware security modules (HSMs), which offer robust protection against physical and digital threats. Ensure these vaults are accessible only to authorized personnel and have multi-factor authentication (MFA) mechanisms.
* **Audit and Compliance**:\
  Regularly audit key management practices and maintain logs for compliance purposes. This not only ensures adherence to best practices but also aids in identifying potential areas of improvement.
* **Training and Awareness**:\
  Educate your team on the importance of key security and the potential risks of mismanagement. Regular training sessions can help maintain a high level of awareness and vigilance.

### 🔍 Systematic Tracking of Keys

**What You Need to Know**

Tracking and managing a large number of keys in Ethereum validator operations is critical. This ensures that each key is accounted for and its status is known, thus reducing the risk of unauthorized access or loss.

!!! info "Best Practices"
    * **Implement Key Management Software**: Use specialized software designed for key management. This software should provide a clear overview of all keys, their statuses, and usage history.
    * **Regular Audits**: Conduct periodic audits to verify the status and security of each key. This can be a mix of automated systems and manual checks.


**Example**: Consider using a tool like HashiCorp's Vault, which allows you to securely manage keys and perform automated audits. Implementing automated alerts for any irregularities in key usage can provide early warning signs of potential security breaches.

**Suggestions**

* Keep a detailed log for each key, noting when it was used and by whom.
* Regularly review and update your key management policies to adapt to new threats and technological advancements.

### 💾 Backup Strategies

**What You Need to Know**

Backups are essential for key management, providing a safety net in case of key loss or corruption.

!!! info "Best Practices"
    * **Secure and Redundant Storage**: Store backups in multiple, physically secure locations. Use encryption to protect backup data.
    * **Regular Testing**: Periodically test backup keys to ensure they work as expected.


**Example**: Create encrypted backups of keys and store them in different geographical locations. For instance, one copy could be in a bank safe deposit box, while another is in a secure cloud storage service.

**Suggestions**

* Develop a clear, written procedure for backup and restoration processes.
* Never assume that a backup will work until it has been tested!

### 🚨 Risks of Hot Standbys

**What You Need to Know**

Hot standbys can be a double-edged sword: they offer quick recovery but can be vulnerable if not properly managed.

!!! info "Best Practices"
    * **Secure Environment**: Ensure that hot standby systems are as secure as the primary system. They should be in a controlled environment with limited access.
    * **Regular Updates and Patches**: Keep the software on hot standbys up-to-date to protect against vulnerabilities.


**Example**: If using a hot standby server for key management, it should be in a locked, climate-controlled server room with access restricted to authorized personnel only, and with all the same security measures as the primary server.

**Suggestions**

* Regularly test the security of hot standby systems to ensure they are not vulnerable to attacks.
* Limit network exposure of hot standbys and monitor them for unusual activities.

### 🔑 Use of Web3Signer

**What You Need to Know**

Web3Signer provides a secure and flexible way to manage keys for Ethereum validators, separating key management from operational duties.

!!! info "Best Practices"
    * **Integration with Existing Systems**: Integrate Web3Signer with your existing infrastructure to streamline key management processes.
    * **Secure Configuration**: Ensure that Web3Signer is configured securely, with access controls and audit logging.


**Example**: Use Web3Signer to manage validator keys while keeping the keys in secure hardware wallets. This way, the keys are not exposed to the internet and are protected against online attacks.

**Suggestions**

* Regularly update Web3Signer to the latest version to benefit from security updates and new features.
* Train staff on using Web3Signer effectively and securely.

### 🏦 Integration with Secure Vaults

**What You Need to Know**

Using secure vaults like HSMs (Hardware Security Modules) is essential for storing sensitive keys securely.

!!! info "Best Practices"
    * **Restricted Access**: Limit physical and digital access to the vaults to authorized personnel only.
    * **Multi-Factor Authentication**: Implement MFA for accessing the vaults.


**Example**: Employ HSMs to store the master keys and use them to generate and manage subordinate keys. HSMs can be configured to allow access only after multiple authentication factors are verified.

**Suggestions**

* Regularly audit the physical and network security of the vaults.
* Consider using vaults that offer tamper-evident features and logging capabilities.

### 📝 Audit and Compliance

**What You Need to Know**

Regular audits ensure that key management practices are up to standard and comply with relevant regulations.

!!! info "Best Practices"
    * **Regular Internal and External Audits**: Conduct both internal reviews and external audits to ensure compliance with best practices.
    * **Maintain Detailed Logs**: Keep comprehensive logs of key management activities.


**Example**: Engage a third-party security firm to conduct an annual audit of your key management practices. They can provide an unbiased view and suggest improvements.

**Suggestions**

* Use automated tools to maintain logs and facilitate audits.
* Stay updated with industry standards and regulations related to key management.

### 🎓 Training and Awareness

**What You Need to Know**

Human error can often be a weak link in key management. Regular training and awareness programs can mitigate this risk.

!!! info "Best Practices"
    * **Regular Training Sessions**: Conduct periodic training for staff on key management best practices and security protocols.
    * **Awareness Campaigns**: Keep staff informed about the latest security threats and the role of key management in mitigating these threats.


**Example**: Organize quarterly training workshops for staff, covering topics like key security, threat scenarios, and the importance of following protocols.

**Suggestions**

* Use real-world case studies and examples in training to highlight the importance of proper key management.
* Encourage a culture of security awareness within the organization.

### 📖 Other Resources

<div class="grid">
  <a href="https://www.kiln.fi/post/how-to-monitor-ethereum-validation-keys-at-scale" class="card">How to monitor Ethereum validation keys at scale</a>
</div>
<div class="grid">
  <a href="https://www.kiln.fi/post/ethereum-anti-slashing-strategies" class="card">Ethereum anti-slashing strategies</a>
</div>

> <img src="/assets/img/gitbook/image (108).png" alt="" data-size="line">The information in the Scaled Node Operators section has been written and reviewed by [Igor Mandrigin](https://x.com/mandrigin) and [Gateway.fm](https://gateway.fm), a leading large scale Ethereum staking infrastructure provider.
