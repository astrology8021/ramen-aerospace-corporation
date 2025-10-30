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

`rclone --log-level NOTICE --log-file=/home/dockerVM/.config/rclone/log.txt --stats 2s --progress --transfers 16 --checkers 16 --check-first --retries 1 --max-backlog 999999 --buffer-size 256M sync --copy-links /home/dockerVM/megatesttransfer megatest2:test1`
