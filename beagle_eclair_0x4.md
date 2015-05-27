# Release notes page for beagle-eclair-0x4 and devkit8k-eclair-0x4

# Release Note: beagle-eclair-0x4, devkit8k-eclair-0x4 #

0xlab team is glad to announce the forth release of 0xdroid that is based on the eclair branch. In this new release we introduced new hardware support, better softare graphics performance on eclair and brand new happy installer.


  * Version: beagle-donut-0x3
  * Date: April 25, 2010
  * Release Image:
    * [beagle-eclair-0x4.zip](http://downloads.0xlab.org/release/beagle-eclair-0x4/beagle-eclair-0x4.zip)
    * [devkit8k-eclair-0x4.zip](http://downloads.0xlab.org/release/devkit8k-eclair-0x4/devkit8k-eclair-0x4.zip)
  * MD5 sum:
    * [beagle-eclair-0x4](http://downloads.0xlab.org/release/beagle-eclair-0x4/md5sum.txt)
    * [devkit8k-eclair-0x4](http://downloads.0xlab.org/release/devkit8k-eclair-0x4/md5sum.txt)

# Release Details #

  * Eclair codebase
  * Improve software graphics performance in Eclair
  * New hardware: DevKit8000
  * Touchscreen support along with calibration UI
  * 3G modem / Data card support
  * Refined system image installer
  * Small screen support
  * ARM optimized string operations
  * ARMv6 atomic operation improvement
  * Merge skia ARMv6/ARMv7 optimization from QuIC

For more detail, please reference our [roadmap and issues tracking](http://code.google.com/p/0xdroid/wiki/Roadmap)

## How to build from scratch ##
```
  $ repo init -u git://gitorious.org/0xdroid/manifest.git -b beagle-eclair -m beagle-eclair-0x4.xml
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