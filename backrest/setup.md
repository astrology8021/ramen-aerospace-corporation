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

# add backblaze/b2

- need to set up as an Amazon S3 due to error handling with direct backrest connection

## in b2

1. create new key ID and app ID
   - give read/write
2. create new bucket, copy the endpoint

## in backrest

1. create repo, set the following then submit:
   - Repository URL: `s3:s3.us-east-1.backblazeb2.com/bucketname`
     - Can also have `s3:s3.us-east-1.backblazeb2.com/bucketname/folder`
   - Password - generate one, this is to encrypt/decrypt the backup
   - En vars:
     - AWS_ACCESS_KEY_ID=the keyID
     - AWS_SECRET_ACCESS_KEY=the applicationID
2. create plan, set the following then submit:
   - Backup Schedule: Everyday at 0:0
   - Retention Policy:
     - Monthly: 3
     - Weekly: 4
     - Daily: 7
     - Hourly: 0
3. Manually backup to test

docs

- https://restic.readthedocs.io/en/latest/030_preparing_a_new_repo.html#preparing-a-new-repository
- https://restic.readthedocs.io/en/latest/030_preparing_a_new_repo.html#amazon-s3
