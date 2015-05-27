# Introduction #

We provide the [pre-built images](http://downloads.0xlab.org/) and also come with a [happy Installer](http://www.youtube.com/watch?v=6E8aS6wxZV0). We can use the images and then get the newest Android in Beagleboard or Devkit8000. It would take only few minutes to achieve it. Besides these pre-buit images, we can [build from scratch](Source.md) and gain the images too.

## Obtain Prebult Images ##

There are two kinds of pre-built images. One is [official released images](http://downloads.0xlab.org/release/)  (stable) and the other one is [daily build images](http://downloads.0xlab.org/dailybuild/) (experimental). You can download the pre-built images from [0xlab download website](http://downloads.0xlab.org/) and then follow the instructions to install into Beagleboard/Devkit8000 environment.

**NOTE**: for newer Beagleboard (rev C4), you need to rename "uImage.bin" to uImage (on the SD card) for the default bootloader to pick it up. [(naming problem)](http://groups.google.com/group/0xlab-discuss/browse_thread/thread/00bf82f395d65b3a#)

## Installation ##

Make sure that Beagleboard hardware is properly set up first.  Check wiki page [hardware\_beagleboard](hardware_beagleboard.md) in advance.  You can either use automated approach from Installer  (for dummies)or go through the details (for geeks).

### for dummies ###

|  | **[beagle-eclair-0x5](beagle_eclair_0x5.md)** | **[devkit8k-eclair-0x5](beagle_eclair_0x5.md)** |
|:-|:----------------------------------------------|:------------------------------------------------|
| with SGX | [beagle-eclair-0x5\_sgx.zip](http://downloads.0xlab.org/release/beagle-eclair-0x5-sgx/beagle-eclair-0x5_sgx.zip) | [devkit8k-eclair-0x5\_sgx.zip](http://downloads.0xlab.org/release/devkit8k-eclair-0x5-sgx/devkit8k-eclair-0x5_sgx.zip) |
| no SGX | [beagle-eclair-0x5\_no\_sgx.zip](http://downloads.0xlab.org/release/beagle-eclair-0x5-no-sgx/beagle-eclair-0x5_no_sgx.zip) | [devkit8k-eclair-0x5\_no\_sgx.zip](http://downloads.0xlab.org/release/devkit8k-eclair-0x5-no-sgx/devkit8k-eclair-0x5_no_sgx.zip) |

| | **[devkit8k-eclair-0x4](beagle_eclair_0x4.md)** | **[beagle-eclair-0x4](beagle_eclair_0x4.md)** | **[beagle-donut-0x3](beagle_donut_0x3.md)** | **beagle-cupcake-0x2** | **beagle-cupcake-0x1** |
|:|:------------------------------------------------|:----------------------------------------------|:--------------------------------------------|:-----------------------|:-----------------------|
| Installer | [devkit8k-eclair-0x4.zip](http://downloads.0xlab.org/release/devkit8k-eclair-0x4/devkit8k-eclair-0x4.zip) | [beagle-eclair-0x4.zip](http://downloads.0xlab.org/release/beagle-eclair-0x4/beagle-eclair-0x4.zip) | [uImage.bin](http://downloads.0xlab.org/installer/beagle-donut-0x3/uImage.bin) | [uImage.bin](http://downloads.0xlab.org/installer/beagle-cupcake-0x2/uImage.bin) | [uImage.bin](http://downloads.0xlab.org/installer/beagle-cupcake-0x1/uImage.bin) |
| Kernel | [devkit8k-eclair-0x4.zip](http://downloads.0xlab.org/release/devkit8k-eclair-0x4/devkit8k-eclair-0x4.zip) | [beagle-eclair-0x4.zip](http://downloads.0xlab.org/release/beagle-eclair-0x4/beagle-eclair-0x4.zip) | [0xkernel-beagle.bin](http://downloads.0xlab.org/release/beagle-donut-0x3/0xkernel-beagle.bin) |[0xkernel-beagle.bin](http://downloads.0xlab.org/release/beagle-cupcake-0x2/0xkernel-beagle.bin) | [0xkernel-beagle.bin](http://downloads.0xlab.org/release/beagle-cupcake-0x1/0xkernel-beagle.bin) |
| System | [devkit8k-eclair-0x4.zip](http://downloads.0xlab.org/release/devkit8k-eclair-0x4/devkit8k-eclair-0x4.zip) | [beagle-eclair-0x4.zip](http://downloads.0xlab.org/release/beagle-eclair-0x4/beagle-eclair-0x4.zip) | [android-beagle.ubi](http://downloads.0xlab.org/release/beagle-donut-0x3/android-beagle.ubi) | [0xkernel-beagle.bin](http://downloads.0xlab.org/release/beagle-cupcake-0x2/0xkernel-beagle.bin) | [0xkernel-beagle.bin](http://downloads.0xlab.org/release/beagle-cupcake-0x1/0xkernel-beagle.bin) |


## 0xdroid release 0x4~0x5 ##

### Beagle board ###
  * Format the first partition over than 100MB with VFAT on a SD card.
  * Download the release archive beagle-eclair-0x?.zip
  * unzip the archive into SD card first partition
  * Plug the SD card in beagleboard SD slot and restart the beagleboard
  * Wait for UI installer over
  * Unplug the beagleboard and restart it
  * Enjoy it

### Devkit8000 ###
The stock bootloader uses a old machine id that does not match upstream registry. So new users have to reflash a newer bootloader. We provide some [key events](EnhanceButton.md) for Android UI. Also, make sure what size of panel you are using ! You probably need to edit **[install.conf](InstallConf.md)** file.

  * Prepare the SD card as described above. Then unzip the release image onto the **VFAT** partition.
```
cd /media/sdb1
unzip ~/devkit8k-eclair-0x?.zip
```
  * Download the [new bootloader](http://downloads.0xlab.org/release/devkit8k-eclair-0x4/flash-uboot.bin) to the same partition.
  * Edit install.conf, uncomment the U\_BOOT\_IMAGE line.
  * Edit install.conf, choose the correct size of panel. (7 inch or 4.3 inch)
  * Plug the SD card in Devkit8000 SD slot and restart it.
  * Enter the u-boot prompt, use the following command the chainload the new bootloader.
```
mmcinit;mmc init
fatload mmc 0 80300000 flash-uboot.bin
go 80300000
```
  * Then use the new bootloader to load installer
```
boot
```
  * Wait until all the leds turned on, then the installation is finished.
  * Remove the SD card and reboot.

**NOTE**: These steps only have to do once. After the bootloader is updated, the subsequence re-install will be as simple as **beagleboard**.

## 0xdroid release 0x1~0x3 ##

### Beagle board ###

  * Format the first partition over than 100MB with VFAT on a SD card.
  * Download the installer [uImage.bin](http://downloads.0xlab.org/installer/)
  * Download 0xkernel-beagle.bin and android-beagle.ubi [release folder](http://downloads.0xlab.org/release/)
  * Copy above three files into the first partition of SD/MMC card
  * Plug the SD card in Beagle board SD slot and restart the Beagleboard
  * Wait for UI installer over. The installer would perform NAND flashing and u-boot environment setup.
  * Unplug SD card from the Beagleboard and reboot
  * Enjoy!

#### Format SD card instructions under GNU/Linux ####
  * insert the SD card, wait it been detected, say /dev/mmcblk0
    * It may be different with different SD device, you can check it via "dmesg")
```
dmesg | tail
```
> > You should see something like -
```
scsi 5:0:0:0: Direct-Access     Multi    Flash Reader     1.00 PQ: 0 ANSI: 0
sd 5:0:0:0: Attached scsi generic sg2 type 0
usb-storage: device scan complete
sd 5:0:0:0: [sdb] Attached SCSI removable disk
sd 5:0:0:0: [sdb] 3862528 512-byte logical blocks: (1.97 GB/1.84 GiB)
sd 5:0:0:0: [sdb] Assuming drive cache: write through
sd 5:0:0:0: [sdb] Assuming drive cache: write through
 sdb: sdb1 sdb2
```
> > If you are using the built-in SD/MMC slot, the device name would be /dev/mmcblk?
  * If any partition been mounted automatically, please umount.
  * According to the above device name about SD/MMC, create and format the partitions:
```
sudo fdisk /dev/mmcblk0
```

> or
```
sudo fdisk /dev/sdb
```
    * press "d" delete the origin partitions
    * press "n" creating new partition, select partition 1, and give over 100MB to it
    * press "t" and select partition 1. Change the partition label to "b" (W95 FAT32)
      * creating other partitions as you wish (optional)
    * press "p" to confirm the partitions.  The reference output:
```
Command (m for help): p

Disk /dev/sdd: 1977 MB, 1977614336 bytes
64 heads, 63 sectors/track, 957 cylinders
Units = cylinders of 4032 * 512 = 2064384 bytes
Disk identifier: 0x00000000

Device Boot      Start         End      Blocks   Id  System
/dev/sdd1            1          30       60448+   b  W95 FAT32
/dev/sdd2           31         957     1868832   83  Linux
```
    * press "wq" write back and quit fdisk
  * Format the partition for use:
```
sudo mkfs.vfat -n DISK_INSTALLER /dev/mmcblk0p1
```
> or
```
sudo mkfs.vfat -n DISK_INSTALLER /dev/sdb1
```


### for geeks ###
Check wiki page [boot\_nand](boot_nand.md) as reference.