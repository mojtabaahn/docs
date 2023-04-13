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

```bash
# Reverse proxy for multiple domains on one server
https://serverfault.com/questions/171678/nginx-config-front-end-reverse-proxy-to-another-port
```

```bash
# .deb installation
dpkg -i <filename>
```

‍‍‍ذشسا
```bash
# Generate ssh
ssh-keygen -t rsa
```

```bash
# Install make
sudo apt-get install make
```

```
# Using Parspack docker registery
echo "{\"registry-mirrors\": [\"https://registry.docker.ir\"]}" > /etc/docker/daemon.json
systemctl daemon-reload
systemctl restart docker
```

```
# Using google or someone's docker registry
echo "{\"registry-mirrors\": [\"https://mirror.gcr.io\"]}" > /etc/docker/daemon.json
systemctl daemon-reload
systemctl restart docker
```

```
# list of installed packages
apt list --installed
```

```
# List of open ports
sudo lsof -i -P -n | grep LISTEN
```

```
# Route table
sudo apt-get install net-tools -y
sudo route -n

Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         192.168.1.1     0.0.0.0         UG    600    0        0 wlp2s0
169.254.0.0     0.0.0.0         255.255.0.0     U     1000   0        0 wlp2s0
172.17.0.0      0.0.0.0         255.255.0.0     U     0      0        0 docker0
172.19.0.0      0.0.0.0         255.255.0.0     U     0      0        0 br-80956f029ba2
172.20.0.0      0.0.0.0         255.255.0.0     U     0      0        0 br-563591f4e131
172.21.0.0      0.0.0.0         255.255.0.0     U     0      0        0 br-4aa6f72fb3b0

# Removing route
sudo route del -net 172.21.0.0 gw 0.0.0.0 netmask 255.255.0.0 dev br-4aa6f72fb3b0 
```

```
# Replace in file
sed -i 's/search/replace/' filename
```

```
# MYSQL restore
mysql -uuser -ppassword < backupfile.sql
```


```
# Copying ssh public keys to hosts:
ssh-copy-id username@remote_host

# Then in host machine rune:
sudo systemctl restart ssh
```

```
# Gitlab runner installation: https://docs.gitlab.com/runner/install/linux-repository.html
sudo gitlab-runner register
sudo gitlab-runner list
sudo gitlab-runner run <runner-name>
```

```
# change gitlab runner user
nano /etc/systemd/system/gitlab-runner.service 
# then 
systemctl daemon-reload
# then 
service gitlab-runner restart
```


# Webserver Configuration
#### Installing SSL On Ubuntu And Nginx Reverse Proxy:

Follow This: https://certbot.eff.org/instructions?ws=other&os=ubuntufocal
Then make a nginx .conf file like this
```
server {
    listen 80;
    listen [::]:80;

    server_name www.domain.eu domain.eu;
    server_tokens off;

    location / {
        proxy_pass http://localhost:4000;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_redirect off;
    }
}

server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;

    server_name www.domain.eu domain.eu;

    ssl_certificate /var/www/ssl/fullchain.pem;
    ssl_certificate_key /var/www/ssl/privkey.pem;

    location / {
        proxy_pass http://localhost:4000;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_redirect off;
    }
}
```
And a dockerfile like below:
```
version: "3"

services:
  webserver:
    network_mode: host
    image: nginx:latest
    restart: always
    volumes:
      - "./nginx/:/etc/nginx/conf.d/:ro"
```
then run:
```
mkdir ssl
sudo cp -rL /etc/letsencrypt/live/domain.eu ./ssl
sudo chown -R user:user ssl
```

# Wordpress
Debug Bar Plugin: https://wordpress.org/plugins/debug-bar/
Debug Bar Console Plugin (Run PHP LIVE): https://wordpress.org/plugins/debug-bar-console/https://wordpress.org/plugins/debug-bar-console/
SMTP Plugin: https://wordpress.org/plugins/wp-mail-smtp/
