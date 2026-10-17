# Firewalls and subnetting

A firewall is a security mechanism that monitors both incoming and outgoing network connections and can either accept or reject traffic based on a set of configurable rules. It is heavily recommended to have one configured to improve the security of your node/validator setup.

There are two kinds of firewalls:

### Software firewalls

Software firewalls are run on the individual machine and protect it from other devices within the local network that it sits on.&#x20;

It is recommended to have all traffic dropped by default and to set up individual rules allowing it where required, that way traffic can only enter the machine where it is _explicitly_ allowed.

For example, if you run your execution node and consensus node on different machines, you can set up a firewall rule on your execution node to _only_ allow traffic on port 8551 from the IP address of your consensus node.

If you are running Ubuntu Server, a firewall will already be installed by default under [the ufw package](https://manpages.ubuntu.com/manpages/trusty/man8/ufw.8.html), you will just have to configure it and enable it.

If you are running Geth and Prysm and have the software running on different machines, you could set the below config.

**Execution (Assuming Geth with IP 192.168.1.50)**

<pre><code><strong>sudo ufw default deny incoming
</strong>sudo ufw default allow outgoing
sudo ufw allow from 192.168.1.51 to any port 8551 proto tcp
sudo ufw allow 30303
<strong>sudo ufw enable
</strong></code></pre>

**Consensus (Assuming Prysm with IP 192.168.1.51)**

```
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 12000/udp
sudo ufw allow 13000/tcp
sudo ufw enable
```

Very secure! No traffic in or out unless it is strictly Ethereum related. A full list of external ports by execution and consensus client [can be found here.](../../networking/port-forwarding)

From here additional ports can be unblocked such as SSH, the consensus HTTP API (If you are also running your validator on another machine) or the execution RPC API (If you wish to interact with the Ethereum network using your own node).

### Hardware firewalls

Hardware firewalls are run on dedicated devices (Usually your router) and can manage traffic both within networks and between networks.

One way to really fortify your setup is to configure a dedicated subnet on your router solely for your nodes/validators and have the firewall drop traffic from any other subnet from reaching this subnet (Also known as blocking all RFC 1918 traffic)

Should your regular everyday computer (Or any other device on your network) become compromised, the infiltrator won't even know about your nodes as they are sitting on another subnet that is completely blocked off.&#x20;
