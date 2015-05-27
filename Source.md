Our project is hosted at http://gitorious.org/0xdroid. Follow below steps, it shows how to set up the building environment, how to download 0xdroid source code and how to build-from-scratch.

## Precondition: Sun JDK ##

You would need Sun JDK version 1.5 to build Donut.  However, Sun JDK version 1.5 is known to be EOL (End-Of-Line), and Ubuntu Linux 9.10 no longer ships with sun-java5-jdk.

If you are using Ubuntu Linux 9.10, just add these two line in file /etc/apt/sources.list:
```
deb http://us.archive.ubuntu.com/ubuntu/ karmic-updates multiverse
deb-src http://us.archive.ubuntu.com/ubuntu/ karmic-updates multiverse
```
and install Sun JDK 1.5:
```
$ sudo apt-get update
$ sudo apt-get install sun-java5-jdk
```
To set the system to use Java 5, you need to update your java alternatives by running
```
$ sudo update-alternatives --config java
```
Choose java-1.5.0-sun and it should be done.

## Precondition: git and repo ##

Before you download the source, you will need [git](http://git-scm.com/) and [repo](http://source.android.com/download/using-repo) tools.

On an Ubuntu 9.04 host, you can do the following:

Getting git:
```
$ sudo apt-get install git-core
```
Getting repo: (make sure ~/bin is included in $PATH)
```
$ curl https://dl-ssl.google.com/dl/googlesource/git-repo/repo > ~/bin/repo
$ chmod a+x ~/bin/repo
```
For reference details about Repo, see [Using Repo and Git](http://source.android.com/source/).

## Get 0xdroid source ##

Download the 0xdroid source code:
```
$ mkdir beagle-donut
$ cd beagle-donut
$ repo init -u git://gitorious.org/0xdroid/manifest.git -b BRANCH_NAME
$ repo sync
```

Where BRANCH\_NAME is:
  * beagle-eclair - for Eclair version of 0xdroid
  * beagle-donut - for Donut version 0f 0xdroid
  * beagle-cupcake - for Cupcake version of 0xdroid

Alternatively, use faster git mirror if encountering the problem during 'repo sync':
```
$ repo init -u git://gitorious.org/0xdroid/manifest.git -b BRANCH_NAME -m mirror.xml
$ repo sync 
```

## Build 0xdroid from source ##

Setup beagleboard specific configurations and enabled components:
```
$ echo "TARGET_PRODUCT := beagleboard" > buildspec.mk
$ echo "INSTALL_PREBUILT_DEMO_APKS := true" >> buildspec.mk
```

NOTE: If you want to build DevKit8000 instead of Beagleboard, replace the context "TARGET\_PRODUCT := beagleboard" to "TARGET\_PRODUCT := devkit8000".

Build as expected:
```
$ make
```

Once successfully built, the generated root file system is here:
  * out/target/product/beagleboard/root/
  * out/target/product/beagleboard/system/

And the corresponding [UBIFS](http://www.linux-mtd.infradead.org/doc/ubifs.html) system image for NAND flash:
  * out/target/product/beagleboard/system.img

For advanced usage, fetch and build Linux kernel from scratch.  You need uboot-mkimage installed in host machine:
```
# apt-get install uboot-mkimage
```

The instructions for building kernel image:
```
$ cd ..
$ git clone git://gitorious.org/0xlab-kernel/kernel.git
$ cd kernel
$ git checkout -b kernel_omap3 origin/omap3-2.6.32
```
Select proper default kernel configuration to match the machine.
Beagleboard:
```
$ make ARCH=arm omap3_beagle_defconfig
```
or DevKit8000:
```
$ make ARCH=arm devkit8000_defconfig # build for devkit8000
```
Finally, build kernel image along with kernel modules:
```
$ make ARCH=arm CROSS_COMPILE=../beagle-eclair/prebuilt/linux-x86/toolchain/arm-eabi-4.4.0/bin/arm-eabi- uImage
$ make ARCH=arm CROSS_COMPILE=../beagle-eclair/prebuilt/linux-x86/toolchain/arm-eabi-4.4.0/bin/arm-eabi- modules
```

## Flash images to target ##

After this long building process, we should get our own Android kernel and system images. Then we can use [happy Installer](http://www.youtube.com/watch?v=6E8aS6wxZV0) and then do a SD card booting. Here are the steps as below:

  * Format the first partition over than 100MB with VFAT on a SD card.
  * Download the installer [uImage.bin](http://downloads.0xlab.org/installer/)
  * Rename out/target/product/beagleboard/system.img to android-beagle.ubi
  * Rename arch/arm/boot/uImage to 0xkernel-beagle.bin
  * Copy above three files into the first partition of SD/MMC card
  * Plug the SD card in Beagle board SD slot and restart the Beagleboard
  * Wait for UI installer over. The installer would perform NAND flashing and u-boot environment setup.
  * Unplug SD card from the Beagleboard and reboot
  * Enjoy!