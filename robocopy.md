robocopy

local
`robocopy "G:\" "D:\foldername" /s /z /j /r:0 /w:0 /COPY:DAT /DCOPY:DAT /mt:6 /MIR`

to NAS

- net use password first:
  net use \\<network-location>\<some-share> <password> /USER:<username>
- use full UNC in either source or destination path

net use z: \\ipaddress\share password /user:username

`robocopy "F:\filename" "\\ipaddress\share\subfolder\filename" /s /z /j /r:0 /w:0 /COPY:DAT /DCOPY:DAT /mt:6 /MIR`

## from NAS to local

robocopy "\\ipaddress\share\subfolder\file or folder name" "A:\foldername\subfolder" /s /z /j /r:0 /w:0 /COPY:DAT /DCOPY:DAT /mt:6 /MIR

robocopy "\\10.66.66.238\SOFI\ION_CHARGED\Main\Files\Twitch" "A:\Programs\Twitch" /s /z /j /r:0 /w:0 /COPY:DAT /DCOPY:DAT /mt:6 /MIR

Other commands

Cmd + shift + . = show hidden folder files

Mount = show all volumes attached

### Sources

https://linuxize.com/post/how-to-exclude-files-and-directories-with-rsync/

https://devhints.io/rsync

Troubleshooting

rsync: delete file unlink operation not permitted

Ownership Issue: Running rsync as root on a client computer doesn’t grant root permissions on the server, resulting in files being owned by the authenticated user.
Solution 1: Ignore Ownership: Use rsync -rltgoDv to copy files without setting ownership on the server, storing them as the authenticated user.
Solution 2: Preserve Ownership: Run rsync over SSH as root to preserve ownership, but note that allowing root SSH access is generally discouraged.
