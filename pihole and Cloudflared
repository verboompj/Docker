Version: '3'

services:
  pihole:
    container_name: pihole
    domainname: docker
    hostname: pihole
    image: pihole/pihole:latest
    ports:
      - '53:53/tcp'
      - '53:53/udp'
      - '80:80'
    networks:
      dockerlan:
        ipv4_address: 172.31.0.10
    restart: unless-stopped
    volumes:
      - ${USERDIR}/docker/pihole/pihole:/etc/pihole
      - ${USERDIR}/docker/pihole/dnsmasq.d:/etc/dnsmasq.d
    cap_add:
      - NET_ADMIN
    environment:
      - ServerIP=172.16.10.200
      - TZ=Europe/Berlin
      - WEBPASSWORD=[insert Password]
      - DNS1=172.31.0.20#5053

  cloudflared:
    container_name: cloudflared
    domainname: docker
    hostname: cloudf
    image: crazymax/cloudflared
    ports:
      - '5053:5053/tcp'
      - '5053:5053/udp'
      - '49312:49312'
    networks:
      dockerlan:
        ipv4_address: 172.31.0.20
    restart: unless-stopped


networks:
  dockerlan:
    external: true
