# Docker
Docker Configs for Add-blocking and DNS over HTTPS at home

## Goal is to run Pihole and Cloudflared as 2 docker containers


Pihole is a DNS based Add-Blocking service https://pi-hole.net/ 

CloudFlare offers DNS over HTTP services https://1.1.1.1/

#

The goal is to have Pihole to leverage the Cloudflared service as a DoH ( DNS over HTTP) service. 

I want to have 2 seperate containers, each with its own role.

This keeps the containers nice and clean and allows for easy updating of any of the 2 containers.


### steps
1. Create Docker custom network. This allows you to use fixed / Static IP adresses.
2. run the docker-compose yaml
3. Setup your DHCP scope to use the PiHole instance as DNS server ( or forwarder )
4. verify using https://1.1.1.1/help

![Screenshot](https://github.com/verboompj/Docker/blob/master/Pictures/1.1.1.1.PNG)

### troubleshooting
Ubuntu might return an error stating that Port 53 is already in use, and therefore cannot start pihole and use port 53 ( DNS). 

Fix this by disabling the `systemd-resolved.service` on the docker host

Make sure you downloaded the docker images first using docker pull `pihole/pihole` and docker pull `crazymax/cloudflared` and only then disable the service :-) 


`sudo systemctl stop systemd-resolved.service`

`sudo systemctl disable systemd-resolved.service`

re-run your docker compose. 

You might need to kill and delete the previously failed containers first


