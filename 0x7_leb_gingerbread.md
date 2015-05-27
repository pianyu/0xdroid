# Release Note: 0x7-LEB-Gingerbread for Beagleboard-xM and Pandaboard #
0xLab is glad to announce the availability of new 0xdroid release - version 0x7. This release is built upon the efforts of Linaro Evaluation Build (LEB) for Android.

[Linaro](http://www.linaro.org/) is a NFP (Not For Profit) organization that aims to make embedded open source development easier and faster.  Linaro distributes LEB which is tested, optimized and benchmarked.

In this release, 0xLab made an attempt to merge our effort to LEB, which provides both improvements by 0xLab and Linaro.

# Release Details #
  * Date: June 8, 2011
  * Codebase: Android Gingerbread
  * Target Board: Pandaboard (ARM Cortex-A9), Beagleboard-xM (ARM Cortex-A8)
  * Rebase kernel to Linaro 2.6.38
  * frameworks/base: Enable Software cursor
  * frameworks/base: Compute cursor dirty region aggressively
  * libagl: Optimize matrix multiply using ARM VFP
  * packages/apps: Replace Launcher2 with faster and powerful ADW.Launcher
  * frameworks/base: Improve efficiency of SoftKeyboard
  * webkit: Add optimizations done by QuIC: Adaptive request reordering, Memory Cache optimization, Efficient image caching
  * skia: Switch from VFP back to fixed scalar based calculation for performance considerations
  * skia: optimize blit routines
  * skia: Merge NEON optimizations from QuIC and ST-Ericsson
  * build: Use Linaro Toolchain for better code optimizations
  * libpng: Add ARM NEON optimization
  * zlib: Merge NEON improvements. Useful to APK manipulation and PNG
  * libpixelflinger: Re-enable ARM NEON optimizations
  * bionic: Merge Linaro optimized ARM Cortex String Routines
  * bionic: Add optimized memcpy() and memset() for ARM Cortex A9
  * bionic: Use ARMv6 instruction for handling byte order
  * libcore: Optimize byte-swapped accesses.  Known to bring better floating-point performance
  * Inherit the improvements from previous release

# Where to Download #
> In this release, we use Linaro Image Tool to install image to Sd Card. And this release supports two boards.
  * Beagleboard
    * [boot.tar.bz2](http://downloads.0xlab.org/release/0x7-leb-gingerbread-beaglexm/boot.tar.bz2)
    * [system.tar.bz2](http://downloads.0xlab.org/release/0x7-leb-gingerbread-beaglexm/system.tar.bz2)
    * [userdata.tar.bz2](http://downloads.0xlab.org/release/0x7-leb-gingerbread-beaglexm/userdata.tar.bz2)
  * Pandaboard
    * [boot.tar.bz2](http://downloads.0xlab.org/release/0x7-leb-gingerbread-pandaboard/boot.tar.bz2)
    * [system.tar.bz2](http://downloads.0xlab.org/release/0x7-leb-gingerbread-pandaboard/system.tar.bz2)
    * [userdata.tar.bz2](http://downloads.0xlab.org/release/0x7-leb-gingerbread-pandaboard/userdata.tar.bz2)

# Intall Prebuilt Image #
First, please insert your Sd Card and use dmesg to see its device file.
It might be /dev/sdb, /dev/sdc or /dev/mmcblk0. Depends on your machine.
```
 $ dmesg |tail
```
To install prebuilt image to Sd Card, we use [linaro-image-tool](http://launchpad.net/linaro-image-tools/) (see [#Moreover](#Moreover.md) to install needed modules. Or see [#Install\_Image\_Manually](#Install_Image_Manually.md) if you don't want to use the tool)
```
 $ mkdir /tmp/image
 $ cd /tmp/image
 $ wget http://launchpad.net/linaro-image-tools/trunk/0.4.5/+download/linaro-image-tools-0.4.5.tar.gz
 $ tar zxvf linaro-image-tools-0.4.5.tar.gz
 $ cd linaro-image-tools-0.4.5
```
  * For Beagleboard-xM
```
 $ wget http://downloads.0xlab.org/release/0x7-leb-gingerbread-beaglexm/boot.tar.bz2
 $ wget http://downloads.0xlab.org/release/0x7-leb-gingerbread-beaglexm/system.tar.bz2
 $ wget http://downloads.0xlab.org/release/0x7-leb-gingerbread-beaglexm/userdata.tar.bz2
 $ sudo ./linaro-android-media-create \
            --boot boot.tar.bz2 \
            --system system.tar.bz2 \
            --userdata userdata.tar.bz2 \
            --dev beagle --mmc /dev/mmcblk0
```
  * For Pandaboard
```
 $ wget http://downloads.0xlab.org/release/0x7-leb-gingerbread-pandaboard/boot.tar.bz2
 $ wget http://downloads.0xlab.org/release/0x7-leb-gingerbread-pandaboard/system.tar.bz2
 $ wget http://downloads.0xlab.org/release/0x7-leb-gingerbread-pandaboard/userdata.tar.bz2
 $ sudo ./linaro-android-media-create \
            --boot boot.tar.bz2 \
            --system system.tar.bz2 \
            --userdata userdata.tar.bz2 \
            --dev panda --mmc /dev/mmcblk0
```
> > Note: The parameter of --mmc refer to device file of the Sd Card. Once the installation complete,
> > insert the Sd Card to Beagleboard-xM/Pandaboard then power on, there you go.

# Build from scratch #
Assume All your works are under **$HOME/0xdroid/**. To build image from source code, just needs to finish these steps.
  1. Checkout source code
  1. Build source code
  1. Prepare Image tool
  1. Install Image to sdcard
  1. Insert sdcard and power on

  * For Beagleboard-xM
    1. Checkout source code
      * Getting repo: (make sure ~/bin is included in $PATH)
```
$ curl https://dl-ssl.google.com/dl/googlesource/git-repo/repo > ~/bin/repo
$ chmod a+x ~/bin/repo
```
      * If you have AOSP under /path/to/aosp, use --reference to reuse existing object to speed up fetching.
```
repo init -u git://gitorious.org/0xdroid/manifest.git \
--reference=/path/to/aosp/ -b leb-0xdroid -m LEB-beaglexm.xml
```
      * If you don't have AOSP
```
repo init -u git://gitorious.org/0xdroid/manifest.git -b leb-0xdroid -m LEB-beaglexm.xml
```
    1. Build source code
```
$ echo "TARGET_PRODUCT=beagleboard" > buildspec.mk
$ echo "TARGET_TOOLS=$HOME/0xdroid/prebuilt/linux-x86/toolchain/arm-eabi-4.5.4/bin/arm-eabi-">> buildspec.mk
$ echo "TARGET_TOOLS_PREFIX=$HOME/0xdroid/prebuilt/linux-x86/toolchain/arm-eabi-4.5.4/bin/arm-eabi-" >> buildspec.mk
$ echo "TARGET_SHELL=mksh" >> buildspec.mk
$ make boottarball systemtarball userdatatarball
```
    1. Prepare Image tool (see [#Moreover](#Moreover.md) to install needed modules. Or see [#Install\_Image\_Manually](#Install_Image_Manually.md) if you don't want to use the tool)
```
$ mkdir $HOME/0xdroid/lamc
$ cd $HOME/0xdroid/lamc
$ wget http://launchpad.net/linaro-image-tools/trunk/0.4.5/+download/linaro-image-tools-0.4.5.tar.gz
$ tar zxvf linaro-image-tools-0.4.5.tar.gz
```
    1. Install image to sdcard
```
$ cd $HOME/0xdroid/out/target/product/beagleboard
$ sudo $HOME/0xdroid/lamc/linaro-image-tools-0.4.5/linaro-android-media-create \
            --boot boot.tar.bz2 \
            --system system.tar.bz2 \
            --userdata userdata.tar.bz2 \
            --dev beagle --mmc /dev/mmcblk0
```
  * For Pandaboard
    1. Checkout source code
      * Getting repo: (make sure ~/bin is included in $PATH)
```
$ curl https://dl-ssl.google.com/dl/googlesource/git-repo/repo > ~/bin/repo
$ chmod a+x ~/bin/repo
```
      * If you have AOSP under /path/to/aosp, use --reference to reuse existing object to speed up fetching.
```
repo init -u git://gitorious.org/0xdroid/manifest.git \
--reference=/path/to/aosp/ -b leb-0xdroid -m LEB-panda.xml
```
      * If you don't have AOSP
```
repo init -u git://gitorious.org/0xdroid/manifest.git -b leb-0xdroid -m LEB-panda.xml
```
    1. Build source code
```
$ echo "TARGET_PRODUCT=pandaboard" > buildspec.mk
$ echo "TARGET_TOOLS=$HOME/0xdroid/prebuilt/linux-x86/toolchain/arm-eabi-4.5.4/bin/arm-eabi-">> buildspec.mk
$ echo "TARGET_TOOLS_PREFIX=$HOME/0xdroid/prebuilt/linux-x86/toolchain/arm-eabi-4.5.4/bin/arm-eabi-" >> buildspec.mk
$ echo "TARGET_SHELL=mksh" >> buildspec.mk
$ make boottarball systemtarball userdatatarball
```
    1. Prepare Image tool (see [#Moreover](#Moreover.md) to install needed modules. Or see [#Install\_Image\_Manually](#Install_Image_Manually.md) if you don't want to use the tool)
```
$ mkdir $HOME/0xdroid/lamc
$ cd $HOME/0xdroid/lamc
$ wget http://launchpad.net/linaro-image-tools/trunk/0.4.5/+download/linaro-image-tools-0.4.5.tar.gz
$ tar zxvf linaro-image-tools-0.4.5.tar.gz
```
    1. Install image to sdcard
```
$ cd $HOME/0xdroid/out/target/product/pandaboard
$ sudo $HOME/0xdroid/lamc/linaro-image-tools-0.4.5/linaro-android-media-create \
            --boot boot.tar.bz2 \
            --system system.tar.bz2 \
            --userdata userdata.tar.bz2 \
            --dev panda --mmc /dev/mmcblk0
```

# Install Image Manually #
Of course you can install image to Sd Card manually without Linaro Image Tool. Assume there are boot.tar.bz2, system.tar.bz2 and userdata.tar.bz2 under **/tmp/image**. And the device file of your Sd Card is **/dev/mmcblk0**

| **name** | **start,size,type**|
|:---------|:-------------------|
| boot     |63,270272,0x0C,`*`  |
| system   | 270337,524288,L    |
| cache    | 794624,524288,L    |
|extended partition|1318912,-,E         |
|data on extended parition|1318913,1048576,L   |
|sdcard on extended partition |2367489,-,L         |

  * Create partitions onto Sd Card according to previous table
```
echo -e "63,270272,0x0C,* \n270336,524288,L \n794624,524288,L \n1318912,-,E \n1318944,1048544,L \n2367520,-,L\
" | sudo sfdisk --force -D -uS -H 128 -S 32 /dev/mmcblk0

sudo mkfs.vfat -F 32 /dev/mmcblk0p1 -n boot
sudo mkfs.ext4 /dev/mmcblk0p2 -L system
sudo mkfs.ext4 /dev/mmcblk0p3 -L cache
sudo mkfs.ext4 /dev/mmcblk0p5 -L userdata
sudo mkfs.vfat -F 32 /dev/mmcblk0p6 -n sdcard
```
  * Mount and copy files to partitions
```
sudo mount /dev/mmcblk0p1 /tmp/image/boot
sudo mount /dev/mmcblk0p2 /tmp/image/system
sudo mount /dev/mmcblk0p5 /tmp/image/data

sudo tar xvf boot.tar.bz2 -C /tmp/image
sudo tar xvf system.tar.bz2 -C /tmp/image
sudo tar xvf userdata.tar.bz2 -C /tmp/image
sync
```
  * Generate boot script
```
echo "setenv bootcmd 'fatload mmc 0:1 0x80200000 uImage; fatload mmc 0:1 \
0x81600000 uInitrd; bootm 0x80200000 0x81600000'" > boot.txt
echo "setenv bootargs 'console=tty0 console=ttyO2,115200n8 rootwait ro earlyprintk \
fixrtc nocompcache vram=32M omapfb.vram=0:8M mem=456M@0x80000000 \
mem=512M@0xA0000000 init=/init androidboot.console=ttyO2 omapdss.def_disp=dvi \
omapfb.mode=dvi:1280x720MR-24@60 consoleblank=0'" >> boot.txt
echo "boot" >> boot.txt
sudo cp boot.txt /tmp/image/boot/
sudo mkimage -A arm -O linux -T script -C none -a 0 -e 0 -n 'boot script' -d /tmp/image/boot/boot.txt /tmp/image/boot/boot.scr
sync
sudo umount /tmp/image/boot/ /tmp/image/system/ /tmp/image/data/
```

# Moreover #
  * We use **u-boot** of rowboat for Beagleboard-xM since u-boot of Linaro is not bootable on Beagleboard-xM.
  * Beagleboard-xM has two video output: HDMI and DVI. Please use **DVI** to use release 0x7.
  * Install needed **python module** for Linaro Image Tool. Linaro Image Tool expects to run on Ubuntu and depends on some python modules.
```
 $ sudo aptitude install python-argparse python-parted
```