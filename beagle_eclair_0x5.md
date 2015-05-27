# Release Note: beagle-eclair-0x5, devkit8k-eclair-0x5 #

0xlab team is glad to announce the fifth release of 0xdroid. 0xdroid
is community-developed Android distribution by 0xlab, runs on omap3
based boards include beagleboard and devkit8000.

Version: beagle-eclair-0x5-sgx, beagle-eclair-0x5-no-sgx,
devkit8k-eclair-0x5-sgx, devkit8k-eclair-0x5-no-sgx

  * Version: beagle-eclair-0x5
  * Date: July 30, 2010
  * Release Image:
    * [beagle-eclair-0x5\_no\_sgx.zip](http://downloads.0xlab.org/release/beagle-eclair-0x5-no-sgx/beagle-eclair-0x5_no_sgx.zip)
    * [beagle-eclair-0x5\_sgx.zip](http://downloads.0xlab.org/release/beagle-eclair-0x5-sgx/beagle-eclair-0x5_sgx.zip)
    * [devkit8k-eclair-0x5\_no\_sgx.zip](http://downloads.0xlab.org/release/devkit8k-eclair-0x5-no-sgx/devkit8k-eclair-0x5_no_sgx.zip)
    * [devkit8k-eclair-0x5\_sgx.zip](http://downloads.0xlab.org/release/devkit8k-eclair-0x5-sgx/devkit8k-eclair-0x5_sgx.zip)
  * MD5 sum:
    * [beagle-eclair-0x5\_no\_sgx](http://downloads.0xlab.org/release/beagle-eclair-0x5-no-sgx/md5sum.txt)
    * [beagle-eclair-0x5\_sgx](http://downloads.0xlab.org/release/beagle-eclair-0x5-sgx/md5sum.txt)
    * [devkit8k-eclair-0x5\_no\_sgx](http://downloads.0xlab.org/release/devkit8k-eclair-0x5-no-sgx/md5sum.txt)
    * [devkit8k-eclair-0x5\_sgx](http://downloads.0xlab.org/release/devkit8k-eclair-0x5-sgx/md5sum.txt)

# Release Details #

  * Eclair codebase
  * Feature: Major Linux kernel upgrade: from 2.6.29 to 2.6.32
  * Feature: Support TI's Android PowerVR SGX (hardware 2D/3D engine)
  * Feature: Support Android USB gadget: adb and mass-storage
> > Note: 0xdroid no longer support usbnet gadget driver. Use adb or USB Ethernet instead.
  * Feature: new Bluetooth Extensions -- HID
  * Feature: Make Launcher2 really usable
  * Feature: Make Gallery3D workable by fixing PixelFlinger regressions
  * Feature: Touchscreen Calibration shouldn't require reboot
  * Feature: [Robocat](http://code.google.com/p/0xrobocat/) i2c port support
  * Feature: Improved libgralloc for non HW accelerated targets

For more detail, please refer to our [roadmap and issues tracking](http://code.google.com/p/0xdroid/wiki/Roadmap)

## Where to download images ##
You can grab the image from [here](http://downloads.0xlab.org/release/) and
following the steps described on the wiki page to test the image.

This release comes with [PowerVR SGX](http://processors.wiki.ti.com/index.php/Render_to_Texture_with_OpenGL_ES#Introduction) from Texas Instruments. If you try both two images with SGX and without SGX, you would tell how amazing it displays photos in Gallery 3D application. Like usual, it also comes with a happy Installer and it would bring you an Android Eclair system in few seconds. If you are looking for more details about the integration, you could refer to this [wiki](How_to_Integrate_with_SGX.md) page.

## How to build from scratch ##
```
  $ repo init -u git://gitorious.org/0xdroid/manifest.git -b beagle-eclair -m beagle-eclair-0x5.xml
  $ echo "TARGET_PRODUCT := beagleboard" > buildspec.mk
  $ echo "TARGET_PRODUCT := devkit8000" > buildspec.mk ( if build for devkit8000 )
  $ echo "INSTALL_PREBUILT_DEMO_APKS := true" >> buildspec.mk ( optional for adding prebuilt demo apks )
  $ repo sync
  $ make (or make -j4 if there are 4 cores)
```

## Give us feedback ##
  * Join the [0xlab Development mailing-list](http://groups.google.com/group/0xlab-devel)
  * Join the [0xlab General discussion mailing-list](http://groups.google.com/group/0xlab-discuss)
  * [Issue tracking](http://code.google.com/p/0xdroid/issues)