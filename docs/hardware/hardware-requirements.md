# Hardware requirements

A **full node** is one that runs both an [Execution Client](../../validator-clients/execution-clients) and a [Consensus Client](../../validator-clients/consensus-clients).

Here is a simple breakdown of what is required to run a full Ethereum node:

* A **stable Internet connection**. The longer you stay online, the better your rewards. A spotty Internet connection will hurt your returns.
* At least **10Mbps of bandwidth both up and down**. A full node usually takes around 8Mbps to 10Mbps up & down of network traffic, depending on your configuration. You'll also need to take into account other traffic happening on this network (downloads, video calls, streaming, gaming, etc).
* **No data cap** is imposed by your ISP. Running a full node will take a lot of data - as much as over 2 TB per month of on-chain data alone. This can be mitigated somewhat with a few settings tweaks to the ETH clients, but as a rule of thumb, don't run a full node if your Internet plan comes with a monthly data cap.
* **Stable electricity**. For the same reason as needing a stable Internet connection, you also want to have reliable power. This can be mitigated with a large UPS (backup battery) to deal with short blackouts.
* A **computer** with sufficient specs. This is pretty flexible because it _really_ depends on what Execution and Consensus client you use, and what settings you configure them with. The computer can be a local machine, or it can be a Virtual Private Server (VPS) hosted in the cloud. Read below for some more information on those two options, and how to decide which is best for you.

The following are considered _**minimum**_ requirements to run a full node:

* Linux or macOS Operating System
* Quad-core CPU (or dual-core hyperthreaded); both `x64` and `arm64` are supported
* 32 GB of RAM (preferably DDR4)
* 4 TB of free **SSD Disk Space**
  * A spinning platter hard drive _is not fast enough_ to handle the constant random reads and writes that blockchain activity requires. You **MUST** use a solid-state drive. [A list of tested SSD's can be found here.](https://gist.github.com/yorickdowne/f3a3e79a573bf35767cd002cc977b038)

**Recommendations:**

* The ideal setup, and best practice is to have a dedicated computer for staking. Try to limit additional processes running on your staking box. Especially if it is something that is connecting to the outside world. Every extra process and every file being downloaded is another opportunity for an exploit.
* Use Linux, it's easy! For the foreseeable future, Linux will receive better support from both the client teams and the community at large. If you choose Linux you will have access to more guides and more technical support from the community at large. Linux is lightweight, stable, secure, and it doesn't force you to restart for updates every other day.
* Use a [minority client](../../validator-clients/validator-clients-explained)! It is both good for the health of Ethereum and good for the health of your money.
* A battery backup (UPS) is **strongly** recommended! Plug your modem and router into it also. Many ISPs have generators to support emergency services communications, meaning the internet continues to work during a power outage as long as your equipment is powered. Your ISP may be the same. Aside from blackouts, not having your computer shut down on every momentary power flicker is a nice quality-of-life improvement when staking from home.
* Everything here applies to both solo staking and being a minipool node operator with [Rocket Pool ↗](https://rocketpool.net/).

## Hardware examples

Take a look under hardware examples for detailed explanations of real solo home staking setups.

## Hardware options

* [**Raspberry Pi**](hardware-requirements#raspberry-pi)
* [**Old laptop/desktop**](hardware-requirements#old-laptopdesktop)
* [**New laptop**](hardware-requirements#new-laptop)
* [**New pre-built desktop**](hardware-requirements#new-pre-built-desktop)
* [**Custom built desktop**](hardware-requirements#custom-built-desktop)
* [**Intel NUC**](hardware-requirements#intel-nuc)
* [**Server**](hardware-requirements#server)
* [**DAppNode**](hardware-requirements#dappnode)
* [**Avado**](hardware-requirements#avado)
* [**M1 Mac Mini**](hardware-requirements#m1-mac-mini)
* [**Virtual Private Server**](hardware-requirements#virtual-private-server)

### **Raspberry Pi**

**Price:** Lower cost.

**Performance:** Running an execution and consensus node on a Raspberry Pi is possible. Specifically, Nimbus which was designed to run on devices like a Raspberry Pi. Being able to run Ethereum nodes on low-powered hardware is great for decentralization and an honorable goal. However, running a validator is different. I maintain that the Pi’s lack of processing power and memory is a risk in some situations such as a period with no finalization. The reward of saving a few hundred dollars vs more powerful hardware does not even come close to outweighing the risk of extended downtime due to a lack of processing power or memory.

**Power Usage:** Approximately 8 watts.

### **Old laptop/desktop**

**Price:** Lower cost.

**CPU:** For staking on Mainnet, a CPU that scores at least 6000 or better on Passmark is strongly recommended. For initial sync times, single-thread performance is better than having many cores.

**Memory:** Unless you go with an extremely bare-bones OS, 16GB is the minimum amount of RAM recommended for Mainnet.

**Storage:** An SSD is required. You do not need to worry about SATA vs NVMe, either will be fast enough. Buying one with a high terabytes written spec will help with longevity. A 2TB or bigger drive is recommended.

**Caveats:** Stability and uptime are essential to maximize your profits. If you are using an older desktop consider replacing the PSU and the fans. Buying a titanium or platinum-rated PSU will help save on the monthly power bill as well.

If you are planning on staking with an older laptop, consider that they have reduced capacity to deal with heat due to their form factor, and in rare cases, running while plugged in 24/7 can cause issues with the battery. If you do choose to stake with a laptop, try using one that far exceeds the CPU requirements as running a laptop at nearly full load 24/7 is not advisable. You will probably be fine, but generally speaking, laptops are not designed with that in mind.

### **New laptop**

If you are buying brand new, there is not much value in paying the price premium for a portable form factor, screen, keyboard, and trackpad. Once you get your staking machine set up, you do not need any of these features. You can just remote into the staking machine from your normal computer. The low profile form factor will actually be a downside when taking thermal performance into account. Laptops typically do not include an ethernet port now, which means you will be relying on WiFi. WiFi is very reliable now, but you can't beat the simplicity and reliability of a cable.

### **New pre-built desktop**

This is likely the simplest option and it will be easy to upgrade and service in the future\*\*.\*\*

**Price:** Medium price.

**Power Usage:** Probably around 30 watts.

### **Custom built desktop**

This is essentially the same as using a prebuilt desktop. However, building your own gives you the option of choosing a case you like the look of, and buying higher-quality parts. For those of you who have never built a computer, it is easier than Lego because they only go together one way. Also, you won’t get any weird proprietary parts that will be difficult to replace should they ever fail. Unfortunately with prebuilt computers, concessions are sometimes made with components like the PSU to assuage the accountants and boost margins. Style points for adding a RAID card!

### **Intel NUC**

**Price:** Medium price.

**Power usage:** 20-25ish watts.

NUCs are super cute, and their small form factor gives them a very high significant-other approval factor. Unfortunately that does come with a bit of a price premium and slightly less performance than the larger desktop option. However, these are minor drawbacks. This is probably the best option for most people.

### **Server**

**Price:** Higher price.

**Power Usage:** It's bad. A modern server runs around 100 watts. If you get an older one, expect to be up around 150 watts.

Enterprise servers are jam packed with features, and are specifically designed to do exactly what a validator is trying to do. Run 24/7/365. They have redundant power supplies in case one breaks, they mostly have 2 CPUs, so in the unlikely event of one going bad, you can pop it out and restart with just one. They have built in RAID cards so you can have redundant storage. They have hot swappable drive trays, so if one of your drives goes bad, you don't even need to shut down. All of the components are high quality and built to last. You also get monitoring and maintenance tools that are not included in consumer gear like iDRAC and iLo. I would definitely caution that while servers are great for staking, you probably want to be the type of person who is willing to go into the weeds a bit and geek out. There is some research required to know what you are looking for before you go out and buy a server and there is a possibility you run into a weird technical issue that you will have to troubleshoot.

### [**DAppNode**](https://dappnode.io/)

**Price:** Medium price

**Performance:** The DAppNodeXtreme is a good option if you are looking for a custom built OS with an easy UX. A DAppNode box is just a NUC pre-configured with their software. If you are confident enough to install an OS by yourself, you can save a bit of money by purchasing a normal NUC and installing DAppNode yourself. You can also install the DAppNode OS on any computer. If you don’t want to mess around with installing operating systems and want an easy UX, buying a DAppNode box is a convenient and simple way to get started.

**Power Usage:** 20-25ish watts.

### [**Avado**](https://ava.do/shop)

Avado is an easy home-staking solution for people with limited technical knowledge or limited time. The Avado boxes are pre-configured computers with a user-friendly UI that allows you to use and manage the device from anywhere in the world.

Using an AVADO is convenient, secure and true to the spirit of decentralization.

### [**M1 Mac Mini**](https://www.apple.com/shop/buy-mac/mac-mini)

**Price:** Medium price.

**Performance:** Definitely upgrade to 16GB of memory. The CPU will be more than fast enough with a 15,108 passmark score. Make sure you have a plan to get up to 2TB or more of storage, the internal memory and storage is integrated into the motherboard and requires soldering and advanced technical knowledge to upgrade.

**Power Usage:** Slightly less than the NUC, but not enough to make any real difference.

It's not possible to run Linux on the new ARM architecture this uses. It is more expensive that the NUC and also falls short on upgradeability, and ease of service, but for the Mac OS fans out there this is a great option that will work very well.

### **Virtual Private Server**

**Price:** Anywhere from $20 - $50 per month.

**Performance:** You can buy as much as you can afford.

If you live somewhere that is prone to natural disaster or has an unstable power grid or internet connection but still want to solo stake, this is a good option. You can also consider using a DVT protocol.

If you do have stable power and internet, running your own hardware will be a cheaper/more profitable solution long term. You need to evaluate the pros/cons of this for your own situation. Remember that if one of the VPS providers goes down, it will mean all of the people using that VPS service to host will also go down, and the inactivity penalties will be much larger than if you have uncorrelated downtime yourself.

