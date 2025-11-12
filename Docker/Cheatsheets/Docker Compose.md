# network

## network_mode

    `network_mode: "host"`

    `network_mode: "none"`

    `network_mode: "service:[service name]"`

#### Sources

https://docs.docker.com/reference/compose-file/services/#network_mode

https://stackoverflow.com/questions/56582446/how-to-use-host-network-for-docker-compose

## give container each a random mac address and IP macvlan

basic compose setup:

```
networks:
  networkname:
    driver: macvlan
    driver_opts:
      parent: eth0 # ethernet interface on host
    name: networkname
    ipam:
      driver: default
      config:
        - subnet: 192.168.0.0/24
          gateway: 192.168.0.1
```

## Ports

["You don't need to publish ports when you use Macvlan network mode."](https://www.reddit.com/r/docker/comments/150npb1/comment/js4by7r/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)

#### sources

- https://github.com/sarunas-zilinskas/docker-compose-macvlan/blob/master/docker-compose.yml
- https://stackoverflow.com/questions/61831255/how-to-create-a-docker-macvlan-with-user-defined-ip-and-mac-address-using-compos
- https://docs.docker.com/engine/network/drivers/macvlan/
- https://forums.docker.com/t/ipvlan-or-macvlan-in-docker-compose-yml/133137/5
- https://www.reddit.com/r/homelab/comments/hm3paf/give_a_docker_container_its_own_ip_on_my_network/
