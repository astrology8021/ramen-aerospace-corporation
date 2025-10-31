# initial install

linux script

`sudo -v ; curl https://rclone.org/install.sh | sudo bash`

https://rclone.org/install/#linux

add remote mount

### find conf location - mac

`rclone config file`

https://rclone.org/commands/rclone_config_file/

### open conf - mac

`open -a TextEdit ~/.rclone.conf`

https://forum.rclone.org/t/rclone-conf-location-on-os-x/1871

### backup command

`rclone --log-level NOTICE --log-file=/home/user/.config/rclone/log.txt --stats 2s --progress --transfers 16 --checkers 16 --check-first --retries 1 --max-backlog 999999 --buffer-size 256M sync --copy-links /home/user/dir remote:`

current working on RPI 3B+

`rclone --progress --transfers 3 --checkers 3 sync /path/to/source/ remote-destination:`

current testing

`rclone --progress --transfers 3 --checkers 3 --delete-excluded sync /path/to/source/ remote-destination:`

`rclone --progress --transfers 3 --checkers 3 --delete-excluded sync /mnt/share remotenamecrypt:`

- to get sudo to work, copy the conf file to root

`sudo cp .config/rclone/rclone.conf /root/.config/rclone/rclone.conf`

- this works without needing to add a local remote if the destination is mounted
  `sudo rclone --progress --transfers 3 --checkers 3 --delete-excluded sync crypt:/ /mnt/share/decrypt-test/`

# adding remote for encryption

- prereq: add the remote
- add the encrypted remote by referencing the remote
- add the path
- add a password
- add a salt
- decrypting is using the same crypt remote to a location, either:
  - mounted via /etc/fstab
  - locally on the machine
  - a remote mount added as a local

https://youtu.be/0sWfXdOWK0Y
https://youtu.be/0vPRGLlh3V0
https://youtu.be/L87b6MMqSjw

## B2

- add the bucket name when adding the remote, can have the bucket already added from the B2 web UI or can generate one when adding a remote eg. b2:BUCKETNAME
