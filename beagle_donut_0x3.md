# Release notes page for beagle-donut-0x3

# Release Note: beagle-donut-0x3 #
0xlab is very glad to give announcement here that we have a new release **beagle-donut-0x3** that is based on the donut branch. In **beagle-donut-0x3** release, there are more improvements including easier to get on Internet, performance tweak, and better usability with supporting more peripheral.

  * Version: beagle-donut-0x3
  * Date: Dec 18, 2009
  * Release Image:
    * Rootfs image: [android-beagle.ubi](http://downloads.0xlab.org/release/beagle-donut-0x3/android-beagle.ubi)
    * Kernel image: [0xkernel-beagle.bin](http://downloads.0xlab.org/release/beagle-donut-0x3/0xkernel-beagle.bin)
    * MD5 sum: [md5sum.txt](http://downloads.0xlab.org/release/beagle-donut-0x3/md5sum.txt)

## Release Details ##
  * Easy access to Internet through USB OTG network routed via host
    * Ethernet support + USB OTG network with default static IP configurations
  * Performance improvements
    * Dalvik VM + JIT compiler for ARMv7
    * ARM NEON optimizations for PixelFlinger
  * Theme Flexibility
    * Theme selector introduced
    * Flexible resolution support for Launcher
  * More and better peripheral support
    * External GSM modem for functional Android Telephony/RIL
    * Bluetooth OBEX OPush and FTP support
    * Motion sensor support
    * Camera capture / recording
  * Stability improvements with several issues fixed
    * Dalvik stability fix
    * Wifi signal strength with Linux Wireless Extension fix
    * Mouse stability fix

> For more detail, please reference our [roadmap and issues tracking](http://code.google.com/p/0xdroid/wiki/Roadmap)


## Related Documents ##
  * [USB\_Networking](http://code.google.com/p/0xdroid/wiki/USB_Networking)
  * [Launcher theme change](http://code.google.com/p/0xdroid/wiki/LauncherTheme)


## How to build from scratch ##
```
  $ repo init -u git://gitorious.org/0xdroid/manifest.git -b beagle-donut
  $ echo "TARGET_PRODUCT := beagleboard" > buildspec.mk
  $ echo "INSTALL_PREBUILT_DEMO_APKS := true" >> buildspec.mk ( optional for adding prebuilt demo apks )
  $ cd .repo/manifests/
  $ git checkout -b beagle-donut-0x3-release beagle-donut-0x3
  $ repo sync
  $ repo forall -c "git checkout -b beagle-donut-0x3-release beagle-donut-0x3"
  $ make (or make -j4 if there are 4 cores)
```


## Give us feedback ##
  * Join the [0xlab Development mailing-list](http://groups.google.com/group/0xlab-devel)
  * Join the [0xlab General discussion mailing-list](http://groups.google.com/group/0xlab-discuss)
  * [Issue tracking](http://code.google.com/p/0xdroid/issues)

