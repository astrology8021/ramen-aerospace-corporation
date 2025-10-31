# add user

be root

`su -`

add

`adduser dockerVM`

enter password

full name as name of user > press enter for rest for defaults > y

#### source

https://linuxize.com/post/how-add -add-and-delete-users-on-debian/

# add to sudoers

be root

`su -`

add to sudo group

`usermod -aG sudo dockerVM`

verify

`groups dockerVM`

relog

#### sources:

https://itslinuxfoss.com/add-user-sudoers-debian-12/

# scheduled shutdown

In the Debian VM, open the root crontab:

`sudo crontab -e`

Add:

`30 23 * * * /sbin/shutdown -h now`

This will shut down the VM every night at 11:30 PM.

Save and exit.

You can confirm the cron job with:

`sudo crontab -l`

shutdown now

`sudo shutdown -h now`

# NFS install

1. Install NFS client

On Debian/Ubuntu:

`sudo apt install nfs-common`

On CentOS/RHEL:

`sudo yum install nfs-utils`

2. Add entry in /etc/fstab

Edit:

`sudo nano /etc/fstab`

Add a line like:

`192.168.0.1:/share  /mnt/share  nfs  defaults,_netdev  0  0`

192.168.1.50:/export/media → NFS server & export path

/mnt/nfs_share → local mount point

defaults,\_netdev → _netdev waits for network before trying

Save and test:

`sudo mount -a`

may need to run

`systemctl daemon-reload`

# cifs / smb etc fstab

install

`sudo apt-get install cifs-utils`

edit etc fstab

`//server/share /pathto/mountpoint cifs credentials=/home/username/.smbcredentials,uid=shareuser,gid=sharegroup 0 0`

`//192.168.0.1/share   /mnt/share   cifs   credentials=/home/docker/.smbcredentials,iocharset=utf8,vers=2.1,file_mode=0777,dir_mode=0777,nofail  0  0`

for SMB 1.0

`//192.168.0.1/share   /mnt/share   cifs   credentials=/home/docker/.smbcredentials,iocharset=utf8,vers=1.0,file_mode=0777,dir_mode=0777,nofail  0  0`

create .smbcredentials

<html>
    <head>
username=shareuser
password=sharepassword
domain=domain_or_workgroupname
    </head>
</html>

secure it

`sudo chmod 600 /etc/smbcredentials`

#### Sources

https://askubuntu.com/questions/157128/proper-fstab-entry-to-mount-a-samba-share-on-boot

# change hostname

change name

`sudo hostnamectl set-hostname jellytunes`

edit /etc/hosts
`sudo nano /etc/hosts`

from:

<html>
    <head>
127.0.0.1 localhost
127.0.1.1 linux-server
</html>
    </head>

to

<html>
    <head>
127.0.0.1 localhost
127.0.1.1 newhostname
</html>
    </head>

relog

# gpg

🧩 1. Install GPG

Make sure it’s installed:

`sudo apt update`

`sudo apt install -y gnupg`

Verify:

`gpg --version`

You should see something like:
gpg (GnuPG) 2.2.27

🧠 2. Generate a New GPG Key

Run:

`gpg --full-generate-key`

Follow the prompts:

Prompt

Recommended Choice

Please select what kind of key you want:

1 (RSA and RSA)

What keysize do you want?

4096

Key is valid for?

0 (never expires)

Real name:

Your name (e.g.Emily)

Email address:

e.g.Emily@example.com

Comment:

Optional

Passphrase:

Optional (omit if you want unattended backups)

⚠️ If this VM runs unattended cron jobs, don’t set a passphrase — otherwise GPG will block waiting for input.

📜 3. Confirm the Key Was Created

List your keys:
gpg --list-keys

<html>
    <head>
You’ll see something like:
pub rsa4096 2025-10-24 [SC]
1234ABCD5678EF901234ABCD5678EF90ABCDEF12
uid [ultimate] Emily <Emily@example.com>
sub rsa4096 2025-10-24 [E]
</html>
    </head>

Take note of either:

Your email address → e.g. Emily@example.com
Or your key ID → e.g. 1234ABCD5678EF90

You’ll use one of these in your backup script:
GPG_RECIPIENT="Emily@example.com"

🔑 4. Test Encryption and Decryption
🔹 Encrypt a test file

`echo "test" > test.txt`

`gpg --output test.txt.gpg --encrypt --recipient Emily@example.com test.txt`

🔹 Check the result

`ls -lh test.txt\*`

You should see:

<html>
    <head>
-rw-r--r-- test.txt
-rw-r--r-- test.txt.gpg
</html>
    </head>

🔹 Decrypt it

`gpg --output decrypted.txt --decrypt test.txt.gpg`

`cat decrypted.txt`

Output should be:

`test`
