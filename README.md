# Google-Compute-Engine-Docker-Compose-Setup

This is my setup I use for Tailscale and Pihole(Unbound is included as a option.). In docker using compose. On a FREE Google Cloud Compute Engine VM instance.

## Create VM instance to be within free limits (https://cloud.google.com/free/docs/free-cloud-features#compute):
1. Sign up/Sign in if you have a google account already at: ```https://cloud.google.com/free``` (It is possible to sign up and use compute engine without activating the $300 credit/trial.).
2. Go to: ```https://console.cloud.google.com/compute```, and click "ENABLE"(Will take time.).
3. Now go to: ```https://console.cloud.google.com/compute/instancesAdd```.
4. Name it what you want, but note it will also be the boot disks name which can not easily be changed later, but you can change the VM instance name easily later.
5. For "Region" you MUST select one mentioned here: ```https://cloud.google.com/free/docs/free-cloud-features#compute``` otherwise it will cost money.
6. For "Zone" I leave it on the default, but certain zones have different hardware avaliable, which could prevent you from easy upgrades in the future so look into each zone: ```https://cloud.google.com/compute/docs/regions-zones``` or ```Cant find.```.
7. Go to "Machine configuration", and set the "Series" to "E2", now under "Machine type" select "e2-micro (2 vCPU, 1 GB memory)" if you cant find it, look under "Shared-core".
8. Go to "Boot disk", click "CHANGE", now under "Boot disk type" select "Standard persistent disk".
9. Under "Size (GB)" you can set it up to "30" note it is hard to change later to a lower amount.
(I used the default "Debian", "Debian GNU/Linux 11 (bullseye)" "x86/64, amd64 built on 20230411, supports Shielded VM features
".)
10. After selecting/confirming it go to "Firewall" and check "Allow HTTP traffic" and "Allow HTTPS traffic".
11. Expand:
```
Advanced options
Networking, disks, security, management, sole-tenancy
```
and then expand:
```
Networking
Hostname and network interfaces
```
and scroll to "Network interfaces", expand the default one and under "Network Service Tier" change it from "Premium" to Standard.
\
12. Click "CREATE".

### Setup VM instance:
#### Note: The commands are based on "https://docs.docker.com/engine/install/debian/#install-using-the-repository", and "https://levelup.gitconnected.com/the-easiest-docker-docker-compose-setup-on-compute-engine-ec171c09a29a".
These commands were ran in the order presented after each successfully finished:

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
curl -fsSL -O https://raw.githubusercontent.com/mhmatthewhugley/Google-Compute-Engine-Docker-Compose-Setup/main/tailscaled_docker-compose.yml -O https://raw.githubusercontent.com/mhmatthewhugley/Google-Compute-Engine-Docker-Compose-Setup/main/pihole_unbound_docker-compose.yml && sudo docker compose -f tailscaled_docker-compose.yml -f pihole_unbound_docker-compose.yml up -d
```

##### Additional Notes & Changes:
You have to modify in tailscaled_docker-compose.yml the "TS_AUTHKEY".

You should modify in tailscaled_docker-compose.yml its "hostname".

You have to modify the pihole_unbound_docker-compose.yml if you want it to use Unbound instead of Quad9.

You should modify the TimeZone in pihole_unbound_docker-compose.yml.

You have to look at the pihole docker container logs for the web interface randomly set password.

I manually add to a adlist and then only apply this to certain groups with certain devices(Depending on setup you might need it to apply to all devices.):
```
https://raw.githubusercontent.com/mhmatthewhugley/Google-Compute-Engine-Docker-Compose-Setup/main/blacklist%20(https%3A__d3ward.github.io_toolz_adblock.html)
```
