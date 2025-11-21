# cleaning

## clean unused old images

`docker image prune -a`

## clean unused docker data

`docker system prune -a`

# access terminal for container

`docker exec -it <mycontainer> sh`

https://stackoverflow.com/questions/30172605/how-do-i-get-into-a-docker-containers-shell

## stop all containers

`docker stop $(docker ps -q)`

stop all compose containers
docker compose stop

debian13:
sudo sh -c 'docker stop $(docker ps -q)'

start all containers in compose
docker compose up -d

app armor

```
sudo systemctl enable apparmor --now
sudo mount -t securityfs none /sys/kernel/security
```

stop and remove containers, networks, optional volumes/images
`docker compose down`

pull new image versions from compose
docker compose pull

start individual container
docker compose up -d gluetun

start a single container from compose stack
docker compose up -d qbittorrent

start multiple, not all
docker compose up -d jellyfin sonarr

shell into a container then check if vpn active on container
docker exec -it jdownloader2 bash

check public ip
wget -qO- https://ipinfo.io

can try curl
curl https://ipinfo.io

create and mount smb
docker volume create \
 --driver local \
 --opt type=cifs \
 --opt device=//192.168.10.9/SNAT \
 --opt o=username=natalie,password=Heaving-Poncho5,uid=1015,gid=102 \
 smbSNAT
