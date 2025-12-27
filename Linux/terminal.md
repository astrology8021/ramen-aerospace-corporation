# crontab

scheduled actions

user running a job
crontab -e

root running a job
sudo crontab -e

to check jobs
crontab -l
sudo crontab -l
restart machine
0 4 \* \* \* /sbin/shutdown -r now

notes

path is different for vm vs proxmox

sources

How can I schedule a nightly reboot?
Linux - Auto-Reboot and Shutdown with Cron Jobs - Task Scheduler alternative
'crontab' in Linux with Examples
How to Schedule Daily Reboots in Linux Using Crontab
check uid/gid
id
resize, increase (usecase proxmox vm debian)

just use gparted live booted lmao

add to hardware on vm
set boot priority for the SCSI to first
boot into it, leave defaults for language, keyboard and next option
in gparted interface, move the swap at the end of the partiiton to the end

it's ok to have 1mb left of space unused
click and drag or extend the partition if it's in the middle
save with the green tick
shut down

other helpful links:

Extend LVM size
Resizing disks for Ubuntu - where am I going wrong?

install parted
sudo apt install parted

install fdisk
sudo apt install fdisk
AppArmor Enable
sudo systemctl enable apparmor --now
sudo mount -t securityfs none /sys/kernel/security

/etc/fstab

make a script executable
sudo chmod +x <name of file>

execute script
./rsync-backup-to-nas.sh

see all UIDs
cat /etc/passwd

see all GIDs
cat /etc/group
/etc/passwd file format

guest:x:65534:65534:guest:/tmp:/bin/sh

From the above image:

Username: It is used when user logs in. It should be between 1 and 32 characters in length.
Password: An x character indicates that encrypted and salted password is stored in /etc/shadow file. Please note that you need to use the passwd command to computes the hash of a password typed at the CLI or to store/update the hash of the password in /etc/shadow file.
User ID (UID): Each user must be assigned a user ID (UID). UID 0 (zero) is reserved for root and UIDs 1-99 are reserved for other predefined accounts. Further UID 100-999 are reserved by system for administrative and system accounts/groups.
Group ID (GID): The primary group ID (stored in /etc/group file)
User ID Info (GECOS): The comment field. It allow you to add extra information about the users such as user’s full name, phone number etc. This field use by finger command.
Home directory: The absolute path to the directory the user will be in when they log in. If this directory does not exists then users directory becomes /
Command/shell: The absolute path of a command or shell (/bin/bash). Typically, this is a shell. Please note that it does not have to be a shell. For example, sysadmin can use the nologin shell, which acts as a replacement shell for the user accounts. If shell set to /sbin/nologin and the user tries to log in to the Linux system directly, the /sbin/nologin shell closes the connection. If the user entry in the /etc/passwd file doesn’t have an entry in the shell field, the user gets a Bourne shell (/bin/sh).
