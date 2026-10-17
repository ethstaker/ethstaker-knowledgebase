# Automatic security updates

!!! info "Info"
  If you have multiple machines, make sure to stagger the `Unattended-Upgrade::Automatic-Reboot-Time` so they don't all restart at exactly the same time!


Automatic security updates are helpful when you are not able to access your machine but want critical security updates to be applied automatically.

```bash
sudo apt-get update -y
sudo apt-get install -y unattended-upgrades update-notifier-common

sudo vim /etc/apt/apt.conf.d/20auto-upgrades
```

```bash title="/etc/apt/apt.conf.d/20auto-upgrades"
APT::Periodic::Update-Package-Lists "1";
APT::Periodic::Unattended-Upgrade "1";
APT::Periodic::AutocleanInterval "7";
Unattended-Upgrade::Remove-Unused-Dependencies "true";
Unattended-Upgrade::Remove-New-Unused-Dependencies "true";

# This is the most important choice: auto-reboot.
# This should be fine since all services should auto-start on reboot.
Unattended-Upgrade::Automatic-Reboot "true";
Unattended-Upgrade::Automatic-Reboot-Time "02:00";
```

```bash
sudo systemctl enable unattended-upgrades
sudo systemctl restart unattended-upgrades
```

Update system packages again.

```bash
sudo apt-get update -y
sudo apt-get upgrade -y
sudo apt-get dist-upgrade -y
```

Restart the machine.

```bash
sudo shutdown -r now
```

Congratulations! You've successfully enabled `unattended-upgrades` on your staking machine 🥳
