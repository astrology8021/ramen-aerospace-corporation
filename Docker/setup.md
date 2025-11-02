# proxmox VM specs

system = no changes
disks = 64GB
cpu:

6 cores
type = host
memory = 8GB
network = no changes

run through prompts to install

search for third party drivers = enable
set disk as lvm group = disable
install openssh server = enable

# Install on Proxmox VM

1. reboot from proxmox menu
2. ssh into the docker container doc
3. update via command

`sudo apt update`

4. then update

`sudo apt upgrade` 5. install then add docker to sudo group
`curl -sSL https://get.docker.com | sh`

`sudo usermod -aG docker $USER`

6. logout

`sudo reboot`

7. add docker to group
   `newgrp docker`
   configure hardware transcoding, add self to render group
   sudo usermod -aG render courtney
   install intel dependencies
   sudo apt install intel-gpu-tools
   verify
   sudo intel_gpu_top

step 9 - 12 source
https://youtu.be/Vwtx_dfYrtA

Moving from an another machine to a new machine (example is an RPI to a ubuntu VM)
on old host

make script: backup-docker-full.sh then make it executable
sudo chmod +x backup-docker-full.sh
make mountable folder
sudo mkdir -p /mnt/sena/hpp

mount folders in etc/fstab
10.66.66.238:/MODULAR/COURTNEY /mnt/courtney/modular nfs defaults,\_netdev 0 0
mount the folder
sudo mount -a
update systemd
systemctl daemon-reload
rsync backup from host to VM
sudo rsync -rthP /home/courtney/docker-backup-20250927 /mnt/sena/hpp/RPI5/amelia/docker-backup-20250927
on new host

make mountable folder
sudo mkdir -p /mnt/sena/hpp

mount folders in etc/fstab
10.66.66.238:/SOFI /mnt/sena/hpp nfs defaults,\_netdev 0 0
mount the folder
sudo mount -a
update systemd
systemctl daemon-reload
rsync backup from NAS to VM
sudo rsync -rthP /mnt/sena/hpp/RPI5/amelia/docker-backup-20250927 /home/courtney/docker-backup-20250927
create, make executable, then run restore script restore-docker-full.sh
sudo chmod +x restore-docker-full.sh
if error, may need to unnest, create + make execute + run unnest-configs.sh
sudo chmod +x unnest-configs.sh
create any mount points, fstab, env and docker compose files
sudo mkdir -p /mnt/courtney
sudo mkdir -p /mnt/courtney/modular
sudo mkdir -p /mnt/courtney/dl

sudo mkdir -p /mnt/snat && sudo mkdir -p /mnt/timeless && sudo mkdir -p /mnt/disco

umounnt, uncomment out the nas then mount
run docker compose
may need to enable apparmor
sudo systemctl enable apparmor --now
sudo mount -t securityfs none /sys/kernel/security

create folder, mount to it a share NFS or SMB/CIFS

1. Install NFS client

On Debian/Ubuntu:
sudo apt install nfs-common

On CentOS/RHEL:
sudo yum install nfs-utils

2. Add entry in /etc/fstab

Edit:
sudo nano /etc/fstab

Add a line like:
192.168.1.50:/export/media /mnt/nfs_share nfs defaults,\_netdev 0 0

192.168.1.50:/export/media → NFS server & export path
/mnt/nfs_share → local mount point
defaults,\_netdev → _netdev waits for network before trying

Save and test:
sudo mount -a

may need to run
systemctl daemon-reload
