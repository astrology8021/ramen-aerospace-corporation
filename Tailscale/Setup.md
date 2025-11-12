## lxc container

template = debian 13

disk = 8GB

cpu = 4

RAM = 8192

# installing on linux with SSH access (tested on VM, with docker and containers)

install curl

`sudo apt install curl`

run command from https://tailscale.com/download/linux

`sudo curl -fsSL https://tailscale.com/install.sh | sh`

ssh in

`sudo tailscale up --ssh`

copy URL, paste in browser to login

# docker container

#### notes:

<ul>
<li>use the regular exit node setup below</li>
<li>set up ip forwarding in host not in container</li>
<li>tailscale container network mode to "host"</li>
</ul>

#### Sources

https://dausruddin.com/run-tailscale-in-docker-with-exit-node-enabled/

https://youtu.be/tqvvZhGrciQ

https://docs.docker.com/reference/compose-file/services/#network_mode

https://tailscale.com/kb/1282/docker#code-examples

# lxc configuration

after install go to proxmox root shell

`nano /etc/pve/lxc/111.conf`

enter from https://tailscale.com/kb/1130/lxc-unprivileged

`lxc.cgroup2.devices.allow: c 10:200 rwm`

`lxc.mount.entry: /dev/net/tun dev/net/tun none bind,create=file`

install curl

# Exit node

Advertise a device as an exit node

`sudo tailscale set --advertise-exit-node`

Enable IP forwarding

`echo 'net.ipv4.ip_forward = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf`

`echo 'net.ipv6.conf.all.forwarding = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf`

`sudo sysctl -p /etc/sysctl.d/99-tailscale.conf`

[Advertise subnet routes](https://tailscale.com/kb/1019/subnets?tab=linux#advertise-subnet-routes)

After you enable IP forwarding, run tailscale set with the --advertise-routes flag. It accepts a comma-separated list of subnet routes. Make sure to replace the subnets in the example above with the correct ones for your network. All platforms except Apple TV support both IPv4 and IPv6 subnets. Apple TV only supports IPv4 subnets.

`sudo tailscale set --advertise-routes=192.168.0.0/24`

# disable exit node

run command

`sudo tailscale up --advertise-exit-node=false --ssh`

go to admin console and disable

[How to disable advertise exit node?](https://www.reddit.com/r/Tailscale/comments/s3y8yk/how_to_disable_advertise_exit_node/)

# use pihole as dns

1. add pihole to tailscale (install on host/vm/ct running pihole)
2. in DNS settings in tailscale, add the tailscale IP
3. check override DNS

https://tailscale.com/kb/1114/pi-hole

# SSH

## enable

`tailscale set --ssh`

## disable

`tailscale set --ssh=false`
