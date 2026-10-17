# Hardware best practices

## The importance of using a UPS

It is strongly recommended that you connect your node/validator to a UPS. Doing so will ensure that it does not abruptly switch off should there be a sudden loss of power.&#x20;

There are many potential issues that an abrupt shutdown can cause, such as:&#x20;

* Database corruption
  * This will require you to (depending on the severity of the corruption) delete the stored DB and resync it from scratch. Depending on the speed of your SSD, this could put you offline for a while.
* OS corruption
  * This will require an OS reinstallation. You will then need to reconfigure the machine, install an execution and consensus client, set up your validators, _then_ get both clients in sync.&#x20;
*   Hardware failure

    * If your hard drive fails, you will need to source and install a new one, _then_ complete the above steps (Install an OS and sync the clients).



If a power outage doesn't damage any physical components, you might still be unsafe. When power is restored you could experience a power surge that could overload and fry components, meaning more downtime while you investigate which components are damaged and then have them replaced.&#x20;

Depending on the UPS model and the OS you are using, you can configure your UPS to gracefully shutdown the connected computer(s) once the battery level falls below a certain point. Incredibly powerful in protecting your data and computer.

My UPS (1600VA/960W) cost me roughly $200 USD and provides around an hour of power to all the connected devices. I have both my node and router connected, so in the event that there is a power outage, the node will still be online working away. I've had a few short power outages since becoming a validator so it has definitely come in handy!

## Configuring auto start

If things switch off while you are sleeping or not at home, the below steps are very useful in having things start back up automatically.&#x20;

#### Computer set to switch on automatically after loss of power

In your BIOS there will most likely be a power setting, in there you should be able to find an option to have your computer switch back on once power is restored.

If you cannot find the setting, you may need to check your motherboards user guide.&#x20;

NOTE - To enter your BIOS, you will need to press a specific button after switching on the machine (and before the OS loads). The most common keys are "DEL", "F1", "F2", "F10".

This does vary between motherboards, and if you are unsure what yours is, check your POST information once the PC starts as it may show it on the screen. Or you can check your motherboards user guide. _Or_ you can do what I do, which is to spread your hands out on the keyboard and press the before mentioned keys all at once and hope one of them works.&#x20;

#### If running a VM, setting servers to start

If you are using a hypervisor to host your nodes/validators, then you should set the VM's to automatically switch on once the computer has booted. It also saves you from manually starting them up should you manually restart the host computer.

#### Using services and configuring auto start

It is common practice to configure your execution node, consensus node and consensus validators as services and set them to automatically start once the OS has booted. This can be done with systemd.

Somer Esat has written great guides and has a few examples that can be referenced, [one of which can be found here. ](https://someresat.medium.com/guide-to-staking-on-ethereum-ubuntu-lighthouse-773f5d982e03)There are three examples in that guide are "geth.service", "lighthousebeacon.service" and "lighthousevalidator.service"



Doing the above three steps will help to minimise downtime.

## Very loud fan on a NUC

If you are using a NUC, you may notice that the fan is quite loud and can be uncomfortable on the ears. This is due to a setting called turbo boost which is enabled by default.

To switch this option off, [please go into your BIOS and find the option to toggle this to disabled.](https://www.intel.com.au/content/www/au/en/support/articles/000032427/processors/intel-core-processors.html)

Now, this isn't a best practice, so please don't take it as such. Instead, this should be viewed as a quality-of-life option if your NUC fan is very loud and is disturbing the peace.
