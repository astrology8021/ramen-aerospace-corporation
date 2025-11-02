# running command crashes system

known cause:
`rclone --log-level NOTICE --log-file=/home/debian13/.config/rclone/log.txt --stats 2s --progress --transfers 16 --checkers 16 --check-first --retries 1 --max-backlog 999999 --buffer-size 256M sync --copy-links /home/dockerVM/megatesttransfer megatest2:test1`

possible reasons:

- not enough memory assigned to VM/host
  https://forum.rclone.org/t/rclone-crash-on-osx-leaving-mount-folder-inaccessible/11421/4

resolutions:

- increase RAM to 4GB
