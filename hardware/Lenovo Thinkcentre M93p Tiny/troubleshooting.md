# System crash when using rclone on debian 13 VM on proxmox

## issue

Running rclone command causes system to freeze and crash:

    `sudo rclone --progress --transfers 3 --checkers 3 sync /path/to/source remote:`

## cause

Crash happens due to hardware unit hang:

    ```kernel: e1000e 0000:00:19.0 eno1: Detected Hardware Unit Hang: TDH <32> TDT <61> next_to_use <61> next_to_clean <31> buffer_info[next_to_clean]: time_stamp <100154835> next_to_watch <32> jiffies <10017bd00> next_to_watch.status <0> MAC Status <80083> PHY Status <796d> PHY 1000BASE-T Status <7800> PHY Extended Status <3000> PCI Status <10>```

## solution

- In proxmox host shell run:

  `ethtool -K eno1 gso off gro off tso off tx off rx off`

or

- run community script: [Intel e1000e NIC Offloading Fix](https://community-scripts.github.io/ProxmoxVE/scripts?id=nic-offloading-fix&category=Proxmox+%26+Virtualization)

## testing

- Completed a transfer total size of 1.3GB from local NAS to remote using below command, no crash:

  `sudo rclone --progress --transfers 3 --checkers 3 sync /path/to/source remote:`

### sources

- [Intel NIC e1000e hardware unit hang](https://forum.proxmox.com/threads/intel-nic-e1000e-hardware-unit-hang.106001/)
- [e100e - eno1 detected hardware unit hang](https://www.reddit.com/r/Proxmox/comments/1jyu03g/e100e_eno1_detected_hardware_unit_hang/)
