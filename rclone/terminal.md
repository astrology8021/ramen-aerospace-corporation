# sync

## sync source to destination

`sudo rclone --progress --transfers 3 --checkers 3 sync /path/to/source remotename`

`rclone --log-level NOTICE --log-file=/home/user/.config/rclone/log.txt --stats 2s --progress --transfers 16 --checkers 16 --check-first --retries 1 --max-backlog 999999 --buffer-size 256M sync --copy-links /home/user/dir remote:`

## delete excluded (need to specify list)

`rclone --progress --transfers 3 --checkers 3 --delete-excluded sync /mnt/share remotenamecrypt:`

## decrypt and send from remote to local

- this works without needing to add a local remote if the destination is mounted

  `sudo rclone --progress --transfers 3 --checkers 3 --delete-excluded sync crypt:/ /mnt/share/decrypt-test/`
