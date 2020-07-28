# Docker
Docker Configs for Add-blocking and DNS over HTTPS at home

## Goal is to run Pihole and Cloudflared as 2 docker containers


Pihole is a DNS based Add-Blocking service https://pi-hole.net/ 
CloudFlare offers DNS over HTTP services https://1.1.1.1/

The goal is to have Pihole to leverage the Cloudflared service as a DoH ( DNS over HTTP) service 
This keeps the containers nice and clean and allows for easy updating of any of the 2 containers.

1. Create Docker custom network. This allows you to use fixed / Static IP adresses.
2. run the docker-compose yaml
3. Setup your DHCP scope to use the PiHole instance as DNS server ( or forwarder )
4. verify using https://1.1.1.1/help

![Screenshot](https://github.com/verboompj/Docker/blob/master/Pictures/1.1.1.1.PNG)


Ubuntu might return an error stating that Port 53 is already in use. Fix this by disabling the `systemd-resolved.service`
Make sure you downloaded the docker images first using docker pull `pihole/pihole` and docker pull `crazymax/cloudflared` and then disable the service :-) 

`sudo systemctl stop systemd-resolved.service`
`sudo systemctl disable systemd-resolved.service`

