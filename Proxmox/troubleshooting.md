# losing GUI access after adding SSL certificate

1. ssh into the machine
2. go to folder
   `cd /etc/pve/local`
3. make a copy of `pveproxy-ssl.pem` and `pveproxy-ssl.key`
   `cp pveproxy-ssl.pem pveproxy-ssl.pem.bak`
   `cp pveproxy-ssl.key pveproxy-ssl.key.bak`

4. rename `pveproxy-ssl.pem` and `pveproxy-ssl.key`
   `mv pveproxy-ssl.pem pveproxy-ssl-1.pem`
   `mv pveproxy-ssl.key pveproxy-ssl-1.key`

5. reboot
   `reboot`
