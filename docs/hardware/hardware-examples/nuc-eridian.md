# NUC - Eridian

This is a simple NUC that I set up for my home staking validator. It was very easy to build - around 10 minutes to unpack everything, slot in the RAM and SSD, and turn it on.

I decided on the larger form factor for the NUC (there's a normal and a slim version) to avoid any problems with restricted airflow and overheating. I'm also not constrained on space so I didn't mind having a slightly larger form factor on my shelf.

2TB SSD is the right amount for me as I won't need to upgrade it within the next 1-2 years and possibly by that time there may be improvements made in the protocol and/or clients that allow for smaller states, needing less storage.

You don't need 64GB of RAM but I wanted to have extra in case I needed it in the future, but 16GB would have been fine.

**Total cost: £1165** (October 2022)

The machine only needed three parts:

* [Intel NUC 11 Pro NUC11TNHi7 Tiger Canyon Home & Business Mini PC Mini Desktop 11th Gen Intel® Core™ i7-1165G7 Processor Upto 4.7 GHz Turbo,4 Cores,8 Threads,12 MB L3 Cache(Without RAM\&SSD)↗](https://www.amazon.co.uk/gp/product/B09VGY1WMY)
* [Samsung 970 EVO Plus 2 TB PCIe NVMe M.2 (2280) Internal Solid State Drive (SSD) (MZ-V7S2T0), Black↗](https://www.amazon.co.uk/gp/product/B07MLJD32L)
* [Corsair Vengeance SODIMM 64GB (2x32GB) DDR4 2666MHz CL18 Memory for Laptop/Notebooks (Intel 6th Generation Intel Core i5 and i7 Processor Support) Black↗](https://www.amazon.co.uk/gp/product/B07YBW84K9)

<figure><img src="..//assets/img/gitbook/image (44).png" alt=""><figcaption></figcaption></figure>

To open the NUC, simply unscrew the four retaining screws, and detach the ribbon cable.&#x20;

<figure><img src="..//assets/img/gitbook/image (53).png" alt=""><figcaption></figcaption></figure>

The ribbon cable has a small plastic retainer that can be unclipped by hand.

<figure><img src="..//assets/img/gitbook/image (42).png" alt=""><figcaption></figcaption></figure>

With the ribbon cable removed, the NUC will look like this:

<figure><img src="..//assets/img/gitbook/image (40).png" alt=""><figcaption></figcaption></figure>

The first component to insert is the SSD. There is a retaining screw that needs to be removed before the SSD is inserted (1).

The SSD is placed in the slot that says "NVMe ONLY" (2). It can only fit one way because of the little notch, so there's nothing to worry about.

Replace the SSD retaining screw (1).

<figure><img src="..//assets/img/gitbook/image (92).png" alt=""><figcaption></figcaption></figure>

The SSD in place should look like this:

<figure><img src="..//assets/img/gitbook/image (27).png" alt=""><figcaption></figcaption></figure>

Insert the RAM into the slots. Again, they can only fit one way because of the little notch.

<figure><img src="..//assets/img/gitbook/image (51).png" alt=""><figcaption></figcaption></figure>

The finished setup should look like this:

<figure><img src="..//assets/img/gitbook/image (69).png" alt=""><figcaption></figcaption></figure>

Replace the NUC base plate and secure the four retaining screws... and that's it!

All you need to do now is plug in the power cable and press the power button to turn it on 🥳

To install the validator software, check out the [Linux installation guide](/tutorials/installing-linux).
