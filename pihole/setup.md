# proxmox lxc / raspberry pi

1. use command from https://docs.pi-hole.net/main/basic-install/

   `curl -sSL https://install.pi-hole.net | bash`

2. options:

- choose upstream server
- enable logging = full
- save password given on screen for web UI
- make sure to set ip as static from router or do it later

3. change password in pihole terminal

   `pihole setpassword <password>`

sources:

- https://github.com/pi-hole/docker-pi-hole/
- https://youtu.be/FUF64UPBq00
- https://youtu.be/Y3nm519xHfw
- https://youtu.be/6sznCZ7ttbI
