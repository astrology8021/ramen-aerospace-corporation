# speed

> This_Act3491
>
> 2mo ago
> I've got a 1gb connection and I was running sabnzbd on docker on a windows 11 machine, behind a vpn and I was getting 8 mb/s. I made the following changes:
>
> Run sabnzbd on top of windows and with no VPN.
> On their documentation they state that:
> Is the speed listed as Internet Bandwidth near your expected bandwidth?
> If not, make sure the network connection to your device is working correctly.
> Test your device’s speed via fast.com.
> Is the Pystone score at least 100.000 or above? If the score is lower than this, the CPU in your device is either too slow or something else is preventing SABnzbd from using its power.
> Is the Folder Speed at least 150MB/s? Both Incomplete and Complete should be on a SSD/M.2/NVMe disk.
> Download the 10GB test download, is the speed higher than on regular downloads?
> After this, do you see Download speed limited by Disk Speed in the Status Window? If so, either your disk are too slow or something is preventing SABnzbd from writing fast to your disks.
> NOTE When you seek support on our forums/Discord/Reddit, please make sure that you have used the diagnostics above and report the results.
>
> Optimizations
>
> Make sure Maximum line speed in Config->General is set to the correct value for your connection.
> Try different connection numbers for your servers. Start with 8 and increase from there. A higher number will increase the overhead so more connections might actually reduce your speed.
> Turn Off Direct Unpack in Config->Switches to reduce disk load.
> Turn On Pause Downloading During Post-Processing in Config->Switches. This will reduce disk load, as downloading and post-processing are not performed simultaneously.
> Change SSL Ciphers to AES128 or CHACHA20 in Config->Servers. This can slightly reduce CPU load.
> Turn off Unwanted Extensions and Action when encrypted RAR is downloaded, as these use a substantial amount of disk and CPU power.
> After all this I now get 110 mb/s

source: https://www.reddit.com/r/SABnzbd/comments/1ni512e/anyone_know_how_to_increase_speeds/
