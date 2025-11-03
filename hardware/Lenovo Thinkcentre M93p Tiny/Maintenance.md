# Updating BIOS

My Proxmox install was dying alot and found out this was running an outdated BIOS, after researching this is what I ended up with to successfully update the BIOS to version FBKTE0A.

## Required

- [FreeDOS "FullUSB"](https://www.freedos.org/download/)
- [Rufus](https://rufus.ie/en/)
- [Flash UEFI BIOS update – EFI Shell utility fbjte0usa.zip](https://pcsupport.lenovo.com/us/en/products/desktops-and-all-in-ones/thinkcentre-m-series-desktops/thinkcentre-m93p/downloads/ds035753-flash-bios-update-thinkcentre-e93-m73p-m83-m93-m93p-thinkstation-e32-p300?category=BIOS%2FUEFI)
- Windows PC (untested on Linux, can't copy files over on Mac)
- A USB Thumb Drive

0. Make a backup of your machine if it has an OS installed (Clonezilla or similar)
1. Boot the M93p and press **F12** repeatedly until the boot menu comes up, select **enter setup**
2. Make a note of the version and date of your BIOS
3. In the BIOS settings for the M93p Tiny, make sure CSM compatability is **enabled** in `Startup > CSM`
4. Flash FullUSB FreeDOS to a USB using Rufus
5. Open the newly flashed FreeDOS usb in the file explorer
6. Unzip fbjte0usa.zip (or whatever version it's named) and copy all contents inside the extracted folder to the root directory of the USB (don't put them in a subfolder)
7. Make a note/screenshot of the file names, have them ready nearby
8. Insert USB in the M93p Tiny, press **F12** to bring up the boot menu, select your USB
9. FreeDOS will prompt you to install, **do not select this**, choose the option to go to DOS
10. The basic syntax for flashing using the flash.exe will be:

    `flash.exe biosromname.rom \quiet`

**CHECK NAMES OF THE UNZIPPED FILES** This may be different for other versions/machines, etc., from the "fbjte0usa.zip" bios I used, the contained files were:

    `flash2.exe IMAGEFB.ROM \quiet`

11. Shutdown the machine, remove the USB and boot back into BIOS to check your version and version date to verify a successful install

### sources

- [M93p and M910q BIOS updates](https://www.reddit.com/r/homelab/comments/hjed0s/m93p_and_m910q_bios_updates/):

> I recently had to update the bios on a m93 sff which uses the same bios as the m93p, and the iso's didnt work. I had to create a freedos usb using rufus, and copy the contents of the bios zip file to the usb. I was then able to boot off the usb and update the bios

- [How to Update Bios Lenovo ThinkCentre M83](https://youtu.be/ZE0ugmZqeFk)
- BIOS walkthrough: [Lenovo Thinkcentre M93p UEFI BIOS Update - Set UEFI Boot with Secure Boot](https://youtu.be/zmnDsm3GolM?t=488)
