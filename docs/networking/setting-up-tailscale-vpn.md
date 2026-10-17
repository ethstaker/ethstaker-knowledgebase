# Setting up Tailscale VPN

!!! info "Info"

    This is optional. You only need to consider this section if you run a node at home and would like to connect to it from outside of your home network.


!!! warning "Warning"

    Tailscale requires the use of an SSO identity provider, ensure you are aware of and are comfortable with the additional risks associated with this before proceeding. For details, visit [their SSO Page ↗](https://tailscale.com/kb/1013/sso-providers/).


If you would like to log into your home network remotely, such as while on vacation or on a business trip, the most common route is to use a **Virtual Private Network** server. This will allow you to connect to your node via SSH **and** view your monitoring dashboards from anywhere in the world, all without exposing your SSH port to the internet.

Many node operators use [Tailscale ↗](https://tailscale.com/blog/how-tailscale-works/) as their VPN server of choice for this. Tailscale is an open-source P2P VPN tunnel and hosted endpoint discovery service. It takes care of authentication, publication, and the NAT traversal required to establish an end-to-end encrypted path between your machine and your node without sending any sensitive traffic to a centralized server. It is a very powerful tool.

We will briefly cover a basic configuration of it, but feel free to [review their documentation ↗](https://tailscale.com/kb/start/) for more details.

## Setting Tailscale Up

First, create a free [Tailscale account ↗](https://tailscale.com/). Tailscale requires the use of an SSO identity provider such as Google, GitHub, Okta, Microsoft, etc. For details, visit [their SSO Page ↗](https://tailscale.com/kb/1013/sso-providers/).

It is recommended that you enable 2FA (Two Factor Authentication) on whichever identity provider you choose for added security.

Next, follow [their onboarding guide ↗](https://tailscale.com/kb/1017/install/) to install Tailscale on your **client** - the machine you want to connect to your network with. For example, this could be a laptop or your phone. **Note that it is **_**not**_** your validator node!**

Once completed you should see your computer as 'connected' on the [**Tailscale dashboard ↗**](https://login.tailscale.com/admin/machines).

<figure><img src="/assets/img/gitbook/tailscale-client.png" alt=""><figcaption><p>Tailscale dashboard showing the client machine.</p></figcaption></figure>

Now, [install Tailscale on your **node** ↗](https://tailscale.com/kb/1039/install-ubuntu-2004/). First, add Tailscale’s package signing key and repository **on your node**:

```bash
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/focal.noarmor.gpg | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/focal.tailscale-keyring.list | sudo tee /etc/apt/sources.list.d/tailscale.list
```

Now, install Tailscale **on your node**:

```bash
sudo apt-get update
sudo apt-get install tailscale
```

Finally, authenticate and connect your machine to your Tailscale network **on your node**:

```bash
sudo tailscale up
```

You’re connected! You can find your Tailscale IPv4 address by running:

```bash
tailscale ip -4
```

You should now see your node machine added to the [**Tailscale dashboard ↗**](https://login.tailscale.com/admin/machines). You may also **change the name** of the node machine and **disable key expiry** through the dashboard.

<figure><img src="/assets/img/gitbook/tailscale-client-and-node.png" alt=""><figcaption><p>Tailscale dashboard showing the client and node machines.</p></figcaption></figure>

!!! info "Info"

    If you would like to access your node using its name rather than its IP address, you can do so by enabling [MagicDNS ↗](https://tailscale.com/kb/1081/magicdns/) in the Tailscale settings.


You should now be able to `exit` the SSH session to your node on your client, and SSH into your node again through Tailscale using `ssh <user>@<node-name> -p <ssh-port>`.

### Updating UFW

If you have UFW configured, you can now add a rule to [accept any incoming SSH connections over Tailscale ↗](https://tailscale.com/kb/1077/secure-server-ubuntu-18-04/).

!!! warning "Warning"

    The following steps will modify your firewall rules. **You must have at least 2 SSH sessions open to your node machine before proceeding** - one for modifying the configuration and testing it afterward, and one that will stay logged in as a backup in case your changes break SSH so you can revert them!


**Run these commands on the node machine.**

Allow access to all incoming ssh connections over Tailscale.

```bash
sudo ufw allow in on tailscale0
```

You may also remove access to the SSH port to completely lock down your node. Note that you **will not** be able to log in from the local network as Tailscale will become the only way to log in. Only run the following command if you are okay with this.

```bash
sudo ufw delete "22/tcp"
```

Once you’ve set up firewall rules to restrict all non-Tailscale connections, restart UFW and SSH:

```bash
sudo ufw reload
sudo service ssh restart
```

Now, confirm that everything is working as expected. `exit` from one of your current SSH sessions (**but remember to keep the second one open as a backup**). Next, connect to the **node machine** via SSH using the Tailscale IP address or hostname: `ssh <user>@<node-name> -p <ssh-port>`

If it works, you did everything right and can now safely log into your home network while abroad!

!!! info "Info"

    If you've previously port-forwarded your node's SSH port in your router, you can now remove it.


_This documentation was adapted from the_ [_Rocket Pool docs ↗_](https://docs.rocketpool.net/guides/node/tailscale.html)
