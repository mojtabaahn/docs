# LINUX Useful Commands

```bash
# Get operation system details:

cat /etc/os-release

# PRETTY_NAME="Ubuntu 22.04.1 LTS"
# NAME="Ubuntu"
# VERSION_ID="22.04"
# VERSION="22.04.1 LTS (Jammy Jellyfish)"
# VERSION_CODENAME=jammy
# ID=ubuntu
# ID_LIKE=debian
# HOME_URL="https://www.ubuntu.com/"
# SUPPORT_URL="https://help.ubuntu.com/"
# BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
# PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
# UBUNTU_CODENAME=jammy


```

```bash
# Docker installation for ubuntu:
# https://docs.docker.com/engine/install/ubuntu/
```

```bash
# DNS configuration
sudo nano /etc/netplan/00-installer-config.yaml

# add these after
# nameservers:
#  addresses: [185.51.200.2,178.22.122.100]
# Final result will be like:
network:
  ethernets:
    ens33:
      dhcp4: true
      nameservers:
        addresses: [185.51.200.2,178.22.122.100]
  version: 2
  
# THEN
sudo netplan apply
```

```bash
# Git Installation
sudo apt-get install -y git-all
```
