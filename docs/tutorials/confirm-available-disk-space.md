# Use all available disk space

Even if you have a large SSD installed, you may only have (Ubuntu Server) 200GB of total available space depending on whether or not you have a LVM configured for your disk.

This can cause the system to run out of disk space when syncing.

The error message is similar to:

`Fatal: Failed to register the Ethereum service: write /var/lib/goethereum/geth/chaindata/383234.ldb: no space left on device`

To address this issue, assuming you have an SSD that is larger than 200GB, expand the space allocation for the LVM by following these steps:

```bash
sudo lvdisplay # Check your logical volume size

sudo lvm # Attach the lvm console
lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv
lvextend -l +100%FREE -r /dev/ubuntu-vg/ubuntu-lv
exit

sudo resize2fs /dev/ubuntu-vg/ubuntu-lv
df -h # Check results
```

Congratulations! You're now using all available disk space on your staking machine 🥳
