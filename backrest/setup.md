# first setup

1. set mount points, either remote NAS share or local directory
   - on linux, can use /mnt
2. deploy compose from [here](https://github.com/garethgeorge/backrest)
3. set instanceID, username and password, uncheck disable authentication, save and close
4. follow docs [here](https://garethgeorge.github.io/backrest/introduction/getting-started)
5. do backup test

# moving container from one host to another

## on target host

1. backup to a remote NAS

## on source host

2. install backrest, create repo
3. backup container folders

## on target host

4. create new repo with same settings and password as the source host repo you created
5. index the repo
6. find the container/s and restore them
7. stop containers on source host, deploy and test on target host
8. if successful and container functions as intended, make a manual backup
