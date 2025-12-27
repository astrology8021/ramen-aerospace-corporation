# master command

```
rsync --exclude-from='/pathto/ignorefile.txt' -rthP --delete --delete-excluded /Volumes/VOLUME NAME/folder name /Volumes/backup/FOLDER/
```

# copy over without deleting in destination

```
rsync --exclude-from='/pathto/ignorefile.txt' -rthP /source /destination
```

# Volume to volume without delete on destination

```
rsync --exclude-from='/pathto/ignorefile.txt' -rthP --delete-excluded /source/ /dest/
```

# linux fedora

- login first via terminal
  ```
  sudo mount -t cifs //192.168.1.1/share /home/user/mnt/samba -o "username=username,password=password"
  ```
