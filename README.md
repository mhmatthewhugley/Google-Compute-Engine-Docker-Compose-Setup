# Google-Compute-Engine-Docker-Compose-Setup

https://cloud.google.com/free/docs/free-cloud-features#compute

This is my setup for Tailscale and Pihole. In docker using compose.

First follow the below video from 0:58 to 6:31. Note at 3:08 he selects Ubuntu, make sure you select "debian-11-bullseye-v20230411" instead because that is what I tested and wrote these instructions for.
\
[![The words "Google Cloud Free Setup" on the far left on top of a white background with a man on the far right of the image.](http://img.youtube.com/vi/v46bRHR1Pq0/0.jpg)](http://www.youtube.com/watch?v=v46bRHR1Pq0)
\
The link used: http://www.youtube.com/watch?v=v46bRHR1Pq0

Then run the commands below in the order presented:

```
sudo su
```
```
apt-get update && apt install --yes ca-certificates curl gnupg && install -m 0755 -d /etc/apt/keyrings && curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg && chmod a+r /etc/apt/keyrings/docker.gpg
```
```
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  tee /etc/apt/sources.list.d/docker.list > /dev/null
```
```
apt-get update && apt-get --yes install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
```
exit
```
```
curl -fsSL -O https://raw.githubusercontent.com/mhmatthewhugley/Google-Compute-Engine-Docker-Compose-Setup/main/tailscaled_docker-compose.yml -O https://raw.githubusercontent.com/mhmatthewhugley/Google-Compute-Engine-Docker-Compose-Setup/main/pihole_docker-compose.yml && sudo docker compose -f tailscaled_docker-compose.yml -f pihole_docker-compose.yml up
```

I manually add to a adlist and then only apply this to certain groups with certain devices:
```
https://raw.githubusercontent.com/mhmatthewhugley/Google-Compute-Engine-Docker-Compose-Setup/main/blacklist%20(https%3A__d3ward.github.io_toolz_adblock.html)
```
