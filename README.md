# Google-Compute-Engine-Docker-Compose-Setup

https://cloud.google.com/free/docs/free-cloud-features#compute

(https://levelup.gitconnected.com/the-easiest-docker-docker-compose-setup-on-compute-engine-ec171c09a29a)
```
apt update && apt install --yes apt-transport-https ca-certificates curl gnupg2 software-properties-common && curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add - && add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" && apt update && apt install --yes docker-ce && curl -L "https://github.com/docker/compose/releases/download/1.26.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && chmod +x /usr/local/bin/docker-compose
```
```
curl -fsSL https://raw.githubusercontent.com/mhmatthewhugley/Google-Compute-Engine-Docker-Compose-Setup/main/tailscaled_docker-compose.yml https://raw.githubusercontent.com/mhmatthewhugley/Google-Compute-Engine-Docker-Compose-Setup/main/pihole_docker-compose.yml && docker-compose -f tailscaled_docker-compose.yml -f pihole_docker-compose.yml up
```
