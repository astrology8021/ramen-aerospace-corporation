# Allow remote SSH login

Next you will need to edit the sshd config file.

`nano /etc/ssh/sshd_config`

use CTRL + W to open the "Where Is" prompt and type PermitRootLogin. Once you have found that line you'll want to change it to the following:

`Before: PermitRootLogin without-password`

`After: PermitRootLogin yes`

Now that the change has been made use CTRL + X to close Nano. You will be prompted to save your changes with Y and ENTER.

Restart the sshd service for the changes to take effect.

`service ssh restart`

https://klabsdev.com/enable-remote-ssh-on-proxmox-lxc/
