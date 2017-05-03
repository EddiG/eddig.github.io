# Solve the poor work of the default driver r8188eu in Ubuntu 16.04

## Install new driver 
```bash
git clone https://github.com/lwfinger/rtl8188eu
sudo dkms add ./rtl8188eu
sudo dkms build 8188eu/1.0
sudo dkms install 8188eu/1.0
```
## Disable old driver
```bash
echo 'blacklist r8188eu' >> /etc/modprobe.d/blacklist.conf
```
## Verify
After restarting machine, execute `lsmod | grep 8188` in terminal. In output must be `8188eu`, not `r8188eu`.
