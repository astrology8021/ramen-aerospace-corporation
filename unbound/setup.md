# Install

1. run

   `sudo apt install unbound`

2. create config

   `nano /etc/unbound/unbound.conf.d/pi-hole.conf`

3. restart the service

   `sudo service unbound restart`

4. dig check

   `dig pi-hole.net @127.0.0.1 -p 5335`

5. go to pihole > settings > DNS > custom DNS > enter below then save

   `127.0.0.1#5335`

# Installing via docker

1. use this example
2. when doing dig check, do:

   `dig pi-hole.net @127.0.0.1 -p 5053`

3. make sure the environment variable in pihole compose excludes

   `FTLCONF_dns_listeningMode=all`

# for debian 11 (bullseye)+ disable resolvconf.conf entry for unbound

check if enabled, run
systemctl is-active unbound-resolvconf.service
disable it
sudo systemctl disable --now unbound-resolvconf.service
 Disable the file resolvconf_resolvers.conf¶

Disable the file resolvconf_resolvers.conf from being generated when resolvconf is invoked elsewhere.
sudo sed -Ei 's/^unbound_conf=/#unbound_conf=/' /etc/resolvconf.conf
sudo rm /etc/unbound/unbound.conf.d/resolvconf_resolvers.conf
restart unbound
sudo service unbound restart

#### sources

- [docker compose example](https://github.com/klutchell/unbound-docker/blob/main/examples/pi-hole/docker-compose.yml)
- [pihole unbound documentation](https://docs.pi-hole.net/guides/dns/unbound/)
- [jim's unbound conf](https://github.com/JamesTurland/JimsGarage/blob/main/Unbound/unbound.conf)
