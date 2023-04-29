# Google-Compute-Engine-Docker-Compose-Setup

https://cloud.google.com/free/docs/free-cloud-features#compute
```
sudo su
```
```
apt-get update && apt install --yes ca-certificates curl gnupg | install -m 0755 -d /etc/apt/keyrings && curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add - && add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" && apt update && apt install --yes docker-ce && curl -L "https://github.com/docker/compose/releases/download/v2.17.3/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && chmod +x /usr/local/bin/docker-compose
```
```
curl -fsSL -O https://raw.githubusercontent.com/mhmatthewhugley/Google-Compute-Engine-Docker-Compose-Setup/main/tailscaled_docker-compose.yml -O https://raw.githubusercontent.com/mhmatthewhugley/Google-Compute-Engine-Docker-Compose-Setup/main/pihole_docker-compose.yml && docker-compose -f tailscaled_docker-compose.yml -f pihole_docker-compose.yml up
```
