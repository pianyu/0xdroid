# Configure target board in u-boot #

```
Beagleboard# setenv ubifsargs ‘setenv bootargs console=${console} ${optargs} root=ubi0:rootfs ubi.mtd=4 rw rootfstype=ubifs’
Beagleboard# setenv nandboot ‘echo Booting from nand …; run ubifsargs; nand read ${loadaddr} 280000 400000; bootm ${loadaddr}’
init=/init rootwait omapfb.video_mode=640x480MR-16@60'
Beagleboard# setenv optargs ‘init=/init omapdss.def_disp=dvi omapfb.mode=dvi:1024x768MR-24@60’
Beagleboard# saveenv
```

# Flash Linux Kernel #

Put kernel into SD card first partition, VFAT format. Named as "uImage.bin" (you can check [HowToGetAngstromRunning](http://code.google.com/p/beagleboard/wiki/HowToGetAngstromRunning) as SD card as reference)
  * NOTE: for Beagleboard rev B7, the kernel image name should be "uImage" instead of "uImage.bin".
```
Beagleboard# mmcinit
    or mmc init (depends on your u-boot)
Beagleboard# run loaduimage
Beagleboard# nand erase 280000 400000
Beagleboard# nand write ${loadaddr} 280000 400000
```

# Flash Root File system #
  * untar the [tarball](http://0xlab.org/~tick/lazy_flash_SD_image.tar.bz2) into SD card second partition.
  * put your android\_beagle.ubi image into /media//home/root/
    * If you [build from scratch](Source.md), rename from 'out/target/product/beagleboard/system.img' to 'android\_beagle.ubi'.
  * boot from SD
  * flash\_eraseall /dev/mtd4
  * nandwrite /dev/mtd4 android-beagle.ubi