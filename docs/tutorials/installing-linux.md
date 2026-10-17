# Installing Linux

To install Linux on a physical machine here are the steps to follow:

1. Download a Linux distribution image onto your everyday computer.
2. Flash a USB with the distribution image.
3. Boot your staking machine from the USB.
4. Select the right options for your installation.

### Download a Linux distribution image

There are lots of Linux distributions available. If you are an experienced Linux user then you will already know which distribution you want to use based on your skills and ability. However, if you are a new Linux user or just want to keep things simple, then the recommended Linux distribution is Ubuntu Linux.

There are two types of distribution that you can choose:

* Desktop: [https://ubuntu.com/download/desktop↗](https://ubuntu.com/download/desktop)
* Server: [https://ubuntu.com/download/server↗](https://ubuntu.com/download/server)

Desktop comes with a graphical interface that is similar to Windows or macOS desktops. For staking machines, the desktop version isn't ideal as it comes with additional overhead that isn't required, but it can be easier for new users who feel more comfortable with a graphical interface.

Server is a command line only interface. This can feel intimidating at first, but when following [solo staking guides](../../tutorials/solo-staking-guides) you will simply be copying and pasting commands, so it's not too difficult. You can remotely connect to your staking machine securely using protocols like SSH, but the easiest way to get started is to directly connect a keyboard and monitor. [SSH can always be used later](../../tutorials/connect-via-ssh).

### Flash a USB with the distribution image

There are lots of tools available to flash USB drives with disk images. One that is open source and works across multiple platforms is [https://www.balena.io/etcher↗](https://www.balena.io/etcher/). Simply select the Linux distribution image you downloaded previously, select the USB, then Flash!

<figure><img src="/assets/img/gitbook/image (80).png" alt="Balena Etcher Configuration Screen"><figcaption></figcaption></figure>

### Boot your staking machine from the USB

This step should be as easy as inserting the USB that you flashed with the disk image in the previous step and then turning on your staking machine. In some cases, you may need to force the machine to boot from the USB rather than any currently installed OS. This can be done by editing the BIOS boot order and allowing booting from USB. Google is the best place to find information about booting from a USB if you do encounter any problems at this stage.

### Select the right options for your installation

Once you have booted from a USB you will be presented with an installation menu. Use the arrow keys (up and down) to move the selection and use the return key (enter) to select the option.

<figure><img src="/assets/img/gitbook/image (56).png" alt="Linux installation page"><figcaption></figcaption></figure>

After selecting `Try or Install Ubuntu Server` you will see a screen like this. You don't need to do anything at this point, the system is just starting up.

<figure><img src="/assets/img/gitbook/image (26).png" alt="Linux installation loading screen"><figcaption></figcaption></figure>

Once the system has started you will be presented with the installation wizard. The first step is to select the language.

<figure><img src="/assets/img/gitbook/image (100).png" alt="Linux installation language selection"><figcaption></figcaption></figure>

Select the keyboard layout.

<figure><img src="/assets/img/gitbook/image (85).png" alt="Linux installation keyboard selection"><figcaption></figcaption></figure>

Select the installation type you want to use. For this, select `Ubuntu Server`.

<figure><img src="/assets/img/gitbook/image (93).png" alt="Linux installation type selection"><figcaption></figcaption></figure>

Select a network. If your staking machine uses an ethernet cable for a direct network connection (recommended) then this option should already be populated. If using WiFi, select those details.

<figure><img src="/assets/img/gitbook/image (54).png" alt="Linux installation network selection"><figcaption></figcaption></figure>

Select a proxy if required. If you are using a standard home network and don't know what this option means, don't worry, just leave it blank.

<figure><img src="/assets/img/gitbook/image (73).png" alt="Linux installation proxy selection"><figcaption></figcaption></figure>

Select where you want to download the updates for the operating system from. This location can be selected based on your geographic location so that the downloads are faster. But it's easier to just select the default option that's pre-populated.

<figure><img src="/assets/img/gitbook/image (36).png" alt="Linux installation archive mirror selection"><figcaption></figcaption></figure>

Select the storage configuration. As your staking machine is most likely a dedicated machine selecting `Use an entire disk` is the best option. Don't worry about encryption as you want your machine to be able to automatically restart, and encrypted disks make that process much more complex.

<figure><img src="/assets/img/gitbook/image (72).png" alt="Linux installation storage selection"><figcaption></figcaption></figure>

You'll be shown a summary screen of the storage configuration. Linux by default may not use the entire available disk space. In the screenshot above the local storage size is shown as 1.171 Terabytes, but the confirmation screen below only shows 100GB being used.

<figure><img src="/assets/img/gitbook/image (29).png" alt="Linux installation storage confirmation"><figcaption></figcaption></figure>

To use all the available disk space, use the arrow keys to highlight the `ubuntu-lv` row and hit the return/enter key to select `Edit`. Enter the `Max` value shown next to `Size` in the input field, then save the update.

<figure><img src="/assets/img/gitbook/image (66).png" alt="Edit available disk space"><figcaption></figcaption></figure>

<figure><img src="/assets/img/gitbook/image (43).png" alt="Save available disk space"><figcaption></figcaption></figure>

After confirming the storage settings you will be presented with an additional confirmation screen to make sure that you're ready to completely format and wipe any existing data on the storage disk. That's what we want, so select `Continue`.

<figure><img src="/assets/img/gitbook/image (23).png" alt="Linux installation storage confirmation screen"><figcaption></figcaption></figure>

Setting up the user profile is important as it's how you will access the machine, both directly and remotely. Select a name for your user and the name for your server that will appear on your local network. Your username is used to login to the machine and the password protects your user account.

<figure><img src="/assets/img/gitbook/image (31).png" alt="Linux installation user creation screen"><figcaption></figcaption></figure>

At this point it's a good idea to set up the SSH server so you don't have to install it manually later. If you never intend to SSH into your staking machine and only connect to it directly with a keyboard and monitor then you don't need this option. For information on SSH connections see the tutorial [Connect with SSH](../../tutorials/connect-via-ssh).

<figure><img src="/assets/img/gitbook/image (22).png" alt="Linux installation ssh setup"><figcaption></figcaption></figure>

This screen might be displayed asking you to select or deselect popular snaps. Don't worry about this page, it might even be empty for you. Simply move on to the next screen.

<figure><img src="/assets/img/gitbook/image (12) (1).png" alt="Linux installation server snaps"><figcaption></figcaption></figure>

At this point, the installation will begin using all the configuration settings you've provided. This can take a few minutes (10 or more) depending on your hardware and configuration. You don't need to do anything, just wait until it completes. At the end of the installation process, you will need to reboot your machine. Select `Reboot Now` and it will ask you to remove the installation device (the USB you used during the installation).

<figure><img src="/assets/img/gitbook/image (49).png" alt="Linux installation complete screen"><figcaption></figcaption></figure>

Once the system reboots you'll see startup information similar to the output below. Wait until that completes and you'll be shown a login screen.

<figure><img src="/assets/img/gitbook/image (19).png" alt="Linux startup screen "><figcaption></figcaption></figure>

This is the login screen for your validator machine. The name of this machine is `eridian-validator`.

<figure><img src="/assets/img/gitbook/image (6).png" alt="Linux login screen "><figcaption></figcaption></figure>

Enter the username you created during the installation. You will then be prompted for your password. As you type your password nothing will be shown on the command line (so it will look like it's not working!) but don't worry, this is for security and the typing is working.&#x20;

<figure><img src="/assets/img/gitbook/image (8) (1) (1) (1).png" alt="Linux password input screen "><figcaption></figcaption></figure>

And... you're in!

<figure><img src="/assets/img/gitbook/image (30).png" alt="Linux successful login screen "><figcaption></figcaption></figure>

Congratulations! You've successfully installed Ubuntu Linux server on your staking machine 🥳

At this point, you are now "on the command line" and can start to work through many of the [solo staking guides](../../tutorials/solo-staking-guides).
