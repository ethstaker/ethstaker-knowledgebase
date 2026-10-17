# Connect with SSH

Connecting remotely to a staking machine, whether it's hosted by a cloud provider (AWS, etc.) or running in your home is most often achieved using SSH (Secure Shell).

SSH is a command line tool that allows direct access to a remote machine. This tutorial will cover:

1. [Installing SSH on your staking machine](#installing-ssh-on-your-staking-machine)
2. [Connecting to your staking machine using SSH](#connecting-to-your-staking-machine-using-ssh)
3. [Using Mosh to improve your remote connection experience](#using-mosh-to-improve-your-remote-connection-experience)
4. [Using Blink for iOS for mobile connections](#using-blink-for-ios-for-mobile-connections)
5. [Generating SSH keys](#generating-ssh-keys)
6. [Changing the default SSH Port](#changing-the-default-ssh-port)

This tutorial won't cover the networking setup required to get a static IP, hostname and/or [VPN](../../networking/setting-up-home-vpn-access) as those are covered in other tutorials.

While SSH on its own is a great tool, there are some limitations that can be frustrating when connecting over a poor internet connection. For example, if the internet drops even for a second (if you're in a moving car or train) or you change WiFi networks, the SSH connection will be closed.&#x20;

## Installing SSH on your staking machine

When you installed Linux on your staking machine the installation options should have asked if you would like to install SSH during the setup process.

<figure><img src="/assets/img/gitbook/image (25).png" alt="Linux Ubuntu Installation - Install SSH"><figcaption></figcaption></figure>

To check if SSH is installed on your staking machine run the command:

```bash
ssh -V
```

If SSH is installed you should see a response showing the installed version:

```
OpenSSH_8.9p1 Ubuntu-3ubuntu0.1, OpenSSL 3.0.2 15 Mar 2022
```

If you get an error or don't see the version output then it's likely that the SSH server is not installed. When you want to install any new packages to your Linux system it's best practice to make sure that your current packages are up to date for security purposes:

```bash
sudo apt-get update
```

Then install `openssh-server`:

```bash
sudo apt-get install -y openssh-server
```

If you are using UFW as your firewall and have restricted incoming and outgoing connections then you will need to add the SSH port to allow remote connections (replacing `<SSH_PORT>` with the configured SSH port - the default port is `22`):

```bash
sudo ufw allow in <SSH_PORT> comment 'Allow SSH in'
```

### Connecting to your staking machine using SSH

Once you have confirmed SSH is installed on your staking machine, you can connect from a different machine using the command:

```bash
ssh <USERNAME>@<IP_ADDRESS>
```

For example: `ssh eridian@186:204:70:208`

This command attempts to connect with your user's username at the specific IP address (or Host Name) of your staking machine.

You may get a prompt saying something like "You haven't connected to this machine before, do you want to trust it?" to which you should submit `Yes` as the response.

At this point, if everything is configured correctly, you should be prompted to input your password. This is the password you use to log in with your staking machine user.

If you are using a [different port for your SSH connection](#changing-the-default-ssh-port) then you can specify the port when connecting using:

```
ssh -p <PORT> <USERNAME>@<IP_ADDRESS>
```

## Using Mosh to improve your remote connection experience

**Benefits of using Mosh:**

* If you have an intermittent internet connection (e.g. a mobile connection or you're in a moving vehicle) a standard SSH connection will fail whenever the connection is lost. The connection must then be manually re-established, which can be annoying if it happens often and you are using additional security steps such as [2FA](../../validator-keys/ssh-security-2fa). Mosh allows connections to be dropped and automatically re-established when the internet signal reconnects.
* Mosh uses a predictive interface for typing commands into the console. Standard SSH only shows the typed command once it has returned from the remote server. If you have a slow connection, this can be perceived as a laggy/slow interface. Mosh displays the text as you type commands, giving a much nicer user experience.

**Limitations of using Mosh:**

* A limitation you will notice when using Mosh is that you can't scroll back up the terminal history. This is due to the way Mosh only renders the current screen, which has some performance advantages but can be frustrating if you miss something and can't scroll back to see it.&#x20;

The Mosh package should be installed on both sides of the connection. That means both your staking machine and the machine you want to connect from (e.g. your everyday computer) will need [Mosh↗](https://mosh.org/#getting) installed.

Install Mosh on your staking machine:

```bash
sudo apt-get install -y mosh
```

If you are using UFW, allowing Mosh ports through the firewall:

```
sudo ufw allow in 60000:60020/udp comment 'Allow Mosh in'
```

Mosh uses the same connection method as SSH, so once it is installed and the ports have been allowed it should be as simple as connecting with the command:

```
sudo mosh <USERNAME>@<IP_ADDRESS>
```

If you have changed the default SSH port you can specific the port used by Mosh using the command:

```
sudo mosh --ssh="ssh -p <MODIFIED_SSH_PORT>" <USERNAME>@<IP_ADDRESS>
```

## Using Blink Shell for iOS for mobile connections

The [Blink Shell↗](https://apps.apple.com/us/app/blink-shell-code-editor/id1594898306) mobile app for iOS allows you to connect to your staking machine using both SSH and Mosh.

On your device (iPhone or iPad) open the Blink Shell app and type:

```
config
```

![](</assets/img/gitbook/image (57).png>)

Keys & Certificates can be added if you are using an SSH key for your connections:

![](</assets/img/gitbook/image (97).png>)

Hosts can be configured so you have an alias command e.g. `ssh validator` that you can use with preconfigured settings

![](</assets/img/gitbook/image (77).png>)

iCloud sync can be turned off if you don't want your SSH keys and passwords to be stored in iCLoud.

Auto Lock is a useful feature to add additional security to your portable device.

And that's it! You can now connect to your home staking validator remotely from your iOS device 🗺️

![](</assets/img/gitbook/image (94).png>)

## Generating SSH keys

For additional security, SSH keys can be used alongside or instead of your username/password authentication when connecting to your staking machine.

Follow the instructions here to generate SSH keys: [https://linuxconfig.org/how-to-generate-and-manage-ssh-keys-on-linux](https://linuxconfig.org/how-to-generate-and-manage-ssh-keys-on-linux)&#x20;

## Changing the default SSH Port

The default port configured is `22` for SSH connections. If you want to change the default port for any reason (e.g. due to port forwarding on your router or the port being used by another service) follow these steps:

1.  Open the `/etc/ssh/sshd_config` file and locate the line:

    ```
    #Port 22
    ```
2.  Uncomment that line (by removing the leading `#` character) and change the value with an appropriate port number (for example, 22000):

    ```
    Port 22000
    ```
3. Save the change.
4.  Restart the SSH server:

    ```
    systemctl restart sshd
    ```
5.  To confirm the port has been updated correctly run:

    ```
    sudo netstat -tulpn | grep ssh
    ```
6.  The result should show the new port number:

    ```
    tcp        0      0 0.0.0.0:22000           0.0.0.0:*               LISTEN      1282/sshd: /usr/
    sbi 
    tcp6       0      0 :::22000                :::*                    LISTEN      1282/sshd: /usr/
    sbi 
    ```



