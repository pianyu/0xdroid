# Hardware Overview #

Device: [Gumstix Overo](http://www.gumstix.net/)

# 0xdroid Build Instructions #

  * Format the SD card with two partitions and make the first partition in VFAT. (about 50MB is very enough)
> > second partition as ext3
  * Build an angstrom image with OpenEmbedded
```
# mkdir gumstix_OE;cd gumstix_OE
# git clone git://gitorious.org/gumstix-oe/mainline.git
# git clone git://git.openembedded.net/bitbake
# cp -a org.openembedded.dev/contrib/gumstix/build .
```
    * modify build/profile build/conf/**to your environment
    * bitbake console-base-image (You may need to fix some OpenEmbedded issues)
  * Clone 0xdroid
```
# mkdir 0xdroid;cd 0xdroid
# repo init -u git://gitorious.org/0xdroid/manifest.git -b beagle-donut
# repo sync
# echo TARGET_PRODUCT := beagleboard > buildspec.mk
# make
```
  * Clone 0xlab-kernel:
```
# git clone git://gitorious.org/0xlab-kernel/kernel.git 0xlab-kernel
# cd 0xlab-kernel
# make omap3_beagle_defconfig
```
    * editing .config to add the following two configurations manually:
```
       CONFIG_MACH_OVERO=y
       CONFIG_SND_OMAP_SOC_OVERO=y
```
  * Build kernel image
```
 # env PATH=${PATH_TO_0xdroid}/prebuilt/linux-x86/toolchain/arm-android-eabi-4.4.1/bin/:$PATH \
           CROSS_COMPILE=arm-android-eabi- \
    make ARCH=arm -j2 uImage
```
  * put uImage first partition of mini SD card
```
# sudo tar xvjpf ${PATH_TO_OE}/tmp/deploy/glibc/images/overo/console-base-image-overo.tar.bz2  -C
${second partition of miniSD}
```
    * then put the 0xdroid out/target/product/beagleboard/system.img to ${econd partition of miniSD}/home/root
  * write kernel
> > plug in the mini SD card, and reboot, get in u-boot :
```
# mmc init
# fatload mmc 1 ${loadaddr} uImage
# nand erase 280000 400000
# nand write ${loadaddr} 280000 400000
# setenv nandargs 'setenv bootargs console=${console} vram=${vram} omapfb.mode=dvi:${dvimode} omapfb.debug=y omapdss.def_disp=${defaultdisplay} ${ubiargs} ${optargs}'
# setenv mmcargs 'setenv bootargs console=${console} vram=${vram} omapfb.mode=dvi:${dvimode} omapfb.debug=y omapdss.def_disp=${defaultdisplay} root=/dev/mmcblk0p2 rw rootfstype=ext3 rootwait ${optargs}'
# setenv ubiargs ubi.mtd=4 root=ubi0:rootfs rootfstype=ubifs
# setenv optargs init=/init
# saveenv
```
  * boot from SD card.  in u-boot :
```
# setenv optargs init=/bin/ash
```
    * boot
  * After booting from SD card
```
# cd /home/root
# flash_eralseall -j /dev/mtd4  # be careful It's "mtd4" (definedas rootfs partition)
# nandwrite /dev/mtd4 system.img
```
  * remove miniSD card then reboot.
Done.**

You can download other images with mtd utils into SD card, that should works as well.
When booting 0xdroid on overo the init will try to find machine specified settings on init.gumstix.rc
(It's not there in 0xdroid, but it is okay in this case.)