# Security at scale

<figure><img src="/assets/img/gitbook/image (1) (2) (1).png" alt="" width="375"><figcaption></figcaption></figure>

Security is non-negotiable when you're running Ethereum validators at scale. This guide focuses on best practices specifically tailored for scaled Ethereum staking providers. The objective is to offer a comprehensive security framework that goes beyond typical measures used by solo stakers.

### 💻 Good Inventory Management Hygiene

#### What You Need to Know

Maintaining a precise inventory of all active servers is critical. Each unidentified machine is a potential security risk.

!!! info "Best Practices"
    * Keep an updated inventory list, including the server type, purpose, and responsible team.
    * Use automation tools to detect and report any unauthorized machines.


To mitigate these risks, employ automated tools that continuously monitor your network, identifying and flagging any new devices that appear without authorization. Such tools not only save time but also ensure that your security measures are not reliant on fallible manual processes. They can alert you to the presence of rogue or unauthorized hardware, enabling a swift response to potential security breaches. By keeping an up-to-date inventory, you can also ensure that all machines are running the necessary security software and updates, thereby reducing the surface area for potential attacks.

### 📲 MFA on Servers

#### What You Need to Know

Multi-Factor Authentication (MFA) adds an additional layer of security, reducing the risk of unauthorized access.

!!! info "Best Practices"
    * Implement MFA for all administrative access.
    * Use hardware-based authentication methods when possible.


MFA requires users to provide multiple credentials to authenticate themselves, which significantly decreases the likelihood of successful intrusions. Traditional username and password combinations can often be compromised, but with MFA, an attacker would need to obtain both the user's password and the second factor, which could be a temporary code from an app or a token from a hardware device. The use of hardware-based authentication methods, such as security keys, is particularly effective as they are resistant to phishing attacks and provide a high-security level. These devices can be required to be present during login attempts, ensuring that even if login credentials are compromised, access to the server is not possible without the physical key. Employing MFA on all administrative access points adds depth to your security strategy, acting as a critical line of defense for protecting your Ethereum staking operations from unauthorized access and potential security breaches.

### 🔑 Use SSH Private Keys Instead of Passwords

#### What You Need to Know

SSH keys are more secure than passwords and should be used for secure shell access.

!!! info "Best Practices"

    * Rotate keys regularly.
    * Store keys securely in a key vault.


Employing SSH private keys instead of passwords for secure shell access is a cornerstone of secure system administration. SSH keys offer a more robust security posture because they are cryptographic keys that are almost impossible to decipher by brute force methods, unlike passwords which can often be guessed or cracked with enough time. To enhance the security offered by SSH keys, it's important to rotate them regularly, much like passwords, to mitigate the risks associated with key exposure over time. Additionally, these keys should be stored securely, using a key vault—a dedicated storage system designed to manage digital keys and secrets. Key vaults typically offer heightened security measures such as limited access, audit logs, and sometimes, automatic rotation of keys. By centralizing key storage, you can manage access more effectively and respond quickly if keys need to be revoked, ensuring that your secure shell environment remains a strong link in your Ethereum staking infrastructure's security chain.

### 🚧 Bastion/Jump Host for Access to Critical Infra

#### What You Need to Know

A Bastion or Jump Host serves as an intermediary between your local machine and critical infrastructure.

!!! info "Best Practices"
    * This host should be highly secured, monitored, and only accessible via MFA.
    * "[Defence in Depth](https://www.cyberteamsecurity.com/defence-depth-security-model.html)" model


A Bastion or Jump Host is a hardened and closely monitored entry point to your network that acts as the single, auditable gateway through which all access to critical infrastructure must pass. The primary function of a Bastion Host is to provide a strong security layer that separates sensitive internal systems from external threats. By funneling all traffic through a Bastion Host, you significantly reduce the attack surface of your network by limiting the number of access points to the essential infrastructure. This also means that if an attack occurs and a Bastion Host becomes overwhelmed with requests and crashes, it does not impact the application server.

To ensure the Bastion Host provides effective security, it should have stringent access controls in place, including the use of Multi-Factor Authentication (MFA) to verify the identity of users before granting access to internal networks. It's also vital that the Bastion Host is monitored continuously for any suspicious activities or unauthorized access attempts. Logs should be maintained meticulously and reviewed regularly to detect potential security incidents promptly. The Bastion Host itself should be updated and patched without delay to protect against vulnerabilities. By centralizing access to critical infrastructure through a highly secured and monitored Bastion Host, organizations can create a controlled environment that adds a significant layer of security to their network management practices.

### 🔥 Firewall Configuration

#### What You Need to Know

Start with a 'deny all' default firewall rule and open only those ports necessary for operations.

!!! info "Best Practices"
    * No direct SSH/RDP should be accessible from the internet.
    * Access should be enabled through an MFA-enabled VPN.


Implementing a robust firewall configuration is a fundamental aspect of network security, particularly for infrastructure managing Ethereum validators. The initial stance of any firewall should be to deny all incoming and outgoing traffic by default. This 'default deny' posture ensures that only traffic that has been explicitly permitted is allowed to pass through the firewall, minimizing potential points of entry for attackers.

From this secure baseline, carefully control and limit the exceptions by opening only the ports necessary for your operations. Essential services should be the only ones with open ports.

For remote administrative access, such as SSH (Secure Shell) for Unix-based systems or RDP (Remote Desktop Protocol) for Windows, it's a best practice to ensure that these services are not exposed directly to the internet. Instead, access should be funneled through a secure, MFA-enabled Virtual Private Network (VPN). By doing so, you create a secure tunnel for remote connections, and the use of MFA adds an additional layer of security, ensuring that even if VPN credentials are compromised, attackers still require the second authentication factor, dramatically reducing the likelihood of unauthorized access. This approach aligns with the principle of least privilege, ensuring that only authenticated and authorized users can access the network infrastructure necessary to perform their duties.

### 📍 IP-based DDoS Mitigation

#### What You Need to Know

IP-based DDoS attacks can incapacitate your network.

!!! info "Best Practices"
    * Utilize DDoS protection services.
    * Regularly monitor network traffic for anomalies.


IP-based Distributed Denial of Service (DDoS) attacks are designed to overwhelm your network with traffic, which can disrupt operations and potentially lead to significant downtime. These attacks can be volumetric, flooding your bandwidth; protocol-based, targeting network layer protocols; or application-layer attacks, disrupting specific functions of services.

To protect against such threats, it is imperative to implement DDoS protection services that can detect and mitigate these types of attacks. These services often employ a variety of tactics, such as traffic analysis, rate limiting, and filtering, to distinguish between legitimate user traffic and malicious data packets aiming to disrupt service. They can absorb and scrub the traffic, allowing only legitimate requests to pass through to your network.

In addition to employing external DDoS mitigation services, it's crucial to regularly monitor your network traffic for anomalies. Establishing a baseline of normal traffic patterns allows you to quickly identify unusual spikes or patterns that could indicate a DDoS attack in progress. By promptly detecting these irregularities, you can act quickly to investigate and address the issue before it escalates into a full-blown attack that could incapacitate your critical infrastructure. Regular monitoring, coupled with a robust DDoS mitigation service, forms a strong defense against the disruptive and potentially destructive forces of DDoS attacks.

### 🛑 Engine API Being Filtered + Auth for Engine API

#### What You Need to Know

Your Engine API is an attack surface that needs to be minimized.

!!! info "Best Practices"
    * Filter access to the Engine API.
    * Implement authentication mechanisms like API tokens.


The Engine API, which serves as a critical interface for interacting with Ethereum clients, represents a significant aspect of your network's attack surface. It's essential to restrict and control access to this API to prevent unauthorized manipulation or information disclosure that could be exploited by attackers.

Filtering access to the Engine API is a fundamental security practice. This typically involves configuring firewalls or other network security tools to allow connections only from specific, trusted IP addresses or networks. By doing so, you limit the potential for unauthorized access and reduce the risk of malicious entities exploiting the API.

On top of stringent access controls, it's also crucial to implement robust authentication mechanisms. The use of API tokens is a common and effective method. These tokens should be unique to each user or service that interacts with the Engine API, ensuring that only authenticated requests are processed. The tokens act as an additional layer of security, as they can be revoked or rotated regularly to maintain tight control over access. Moreover, it's important to transmit these tokens securely, typically using HTTPS to encrypt the data in transit and prevent interception by attackers.

By carefully managing who can access the Engine API and requiring secure, authenticated requests, you can significantly reduce the vulnerabilities in your Ethereum staking operation and enhance your overall security posture.

### 🌐 VLAN Segmentation

#### What You Need to Know

Using VLANs can effectively segregate different types of traffic and reduce the attack surface.

!!! info "Best Practices"
    * Group related servers and services into VLANs.
    * Limit inter-VLAN routing to only necessary services.


Virtual Local Area Network (VLAN) segmentation is a powerful network design strategy that enhances security by segregating traffic into distinct, isolated segments based on function, application, or data sensitivity. By using VLANs, you can control traffic flow within your network, effectively minimizing the attack surface by ensuring that devices or services only have access to the network resources they require to function.

When grouping related servers and services into VLANs, the aim is to apply the principle of least privilege at the network level. For example, you might group all payment processing servers in one VLAN, while servers handling internal communications might reside in another. This separation ensures that if one segment of the network is compromised, the breach is contained and doesn't automatically spread to other parts of the network.

Furthermore, it's critical to limit inter-VLAN routing. While some communication between VLANs is necessary for certain operations, it should be strictly controlled. Access Control Lists (ACLs) or firewall rules should be implemented to allow only the necessary traffic to pass between VLANs, and all such traffic should be monitored and logged for security purposes. By restricting and scrutinizing the traffic allowed to cross VLAN boundaries, you can further protect sensitive data and services from potential attacks originating from less secure areas of the network.

### 🪨 OS Hardening

#### What You Need to Know

Hardening the Operating System can reduce the number of vulnerabilities.

!!! info "Best Practices"
    * Follow guidelines like [NIST SP 800-123](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-123.pdf) for detailed steps.
    * Use hardening playbooks that automate many of these processes.


Operating System (OS) hardening is a critical process that involves configuring the OS to protect against a wide array of vulnerabilities. The goal is to eliminate as many security risks as possible by removing non-essential applications, closing unused network ports, and disabling unnecessary services. By hardening the OS, you reduce the attack surface that could be exploited by malicious actors.

Adhering to established hardening guidelines, such as those provided by the National Institute of Standards and Technology (NIST) can offer a comprehensive set of instructions for securing your servers. These guidelines encompass a variety of best practices, from setting up user permissions to applying the latest security patches.

Moreover, leveraging hardening playbooks, particularly those that can be automated with configuration management tools like Ansible, Puppet, or Chef, can significantly streamline the hardening process. These playbooks are designed to automate the enforcement of security policies and the application of configurations that align with best practice guidelines, ensuring a consistent and repeatable hardening process across all your systems.

Such playbooks not only save time and reduce the possibility of human error but also provide documentation of your security stance and facilitate rapid adjustments in response to new threats. Regularly updating these playbooks to reflect the evolving security landscape is a crucial aspect of maintaining hardened systems. By implementing these best practices in OS hardening, you can create a solid foundation for the overall security of your Ethereum validators and other critical infrastructure.

### 🔍 EDR, SIEM, NDR and When to Use Them

#### What You Need to Know

Endpoint Detection and Response (EDR), Security Information and Event Management (SIEM), and Network Detection and Response (NDR) are powerful tools for monitoring and responding to security events.

!!! info "Best Practices"
    * EDR for endpoint-level visibility.
    * SIEM for comprehensive security event management and reporting.
    * NDR for network-level monitoring and response.


**EDR** is designed to provide real-time monitoring and response capabilities at the endpoint level, which includes workstations, servers, and mobile devices. It helps in detecting, investigating, and mitigating suspicious activities on these endpoints. EDR solutions are particularly valuable for identifying and responding to malware infections, ransomware attacks, and other threats that might bypass traditional antivirus solutions. They often use behavioral analysis and machine learning to identify anomalies that indicate a security incident.

**SIEM** systems are comprehensive solutions that aggregate and analyze data from various sources across your network, including logs from firewalls, routers, servers, and other network devices. They provide a holistic view of the security state of your organization's IT infrastructure. SIEM tools are adept at correlating events from different sources, identifying patterns indicative of a security incident, and generating alerts for further investigation. They also play a crucial role in compliance reporting by centralizing log data for audit purposes.

**NDR** focuses on the network level, monitoring network traffic to detect and respond to anomalies that could indicate a security threat. NDR tools analyze network traffic patterns to identify malicious activities such as DDoS attacks, network reconnaissance, and lateral movement within the network. By continuously monitoring network traffic, NDR systems can quickly identify and mitigate threats that could otherwise go unnoticed.

In practice:

* **EDR** should be used for granular visibility and response capabilities on individual endpoints, which are often the target of attacks.
* **SIEM** should be employed for overarching security event management, correlation, and reporting across the entire IT ecosystem.
* **NDR** is ideal for gaining visibility into network traffic and behaviors, allowing for early detection and response to network-based threats.

Integrating these systems allows for a more comprehensive security posture, as each tool complements the others, providing layers of defense against a wide range of cyber threats.

***

Security at scale is an ongoing commitment that involves continual assessment and evolution. By implementing these practices, scaled Ethereum staking providers can not only secure their own operations but also contribute to the overall security of the Ethereum network.

> <img src="/assets/img/gitbook/image (108).png" alt="" data-size="line">The information in the Scaled Node Operators section has been written and reviewed by [Igor Mandrigin](https://x.com/mandrigin) and [Gateway.fm](https://gateway.fm), a leading large scale Ethereum staking infrastructure provider.
