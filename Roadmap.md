## 0x7-LEB-Gingerbread ##

  * Release date: June 8, 2011
  * Summary: customized Linaro Evaluation Build for ARM Cortex-A8/A9
  * Target hardware: Pandaboard and Beagleboard-xM
  * Changes:
    * Rebase Linaro Kernel tree for consolidation development ([Issue #166](https://code.google.com/p/0xdroid/issues/detail?id=#166))
    * Adapt optimization efforts from Linaro
      * linaro toolchain ([Issue #164](https://code.google.com/p/0xdroid/issues/detail?id=#164)), cortex-strings ([Issue #165](https://code.google.com/p/0xdroid/issues/detail?id=#165)), etc.
    * Generic graphics performance improvements
    * zlib NEON improvement ([Issue #161](https://code.google.com/p/0xdroid/issues/detail?id=#161)). Useful to APK manipulation and PNG
    * libpng: Add ARM NEON optimization
    * Use tweaked ADWLauncher ([Issue #163](https://code.google.com/p/0xdroid/issues/detail?id=#163))
    * Enable software cursor for Gingerbread ([Issue #167](https://code.google.com/p/0xdroid/issues/detail?id=#167))
    * frameworks/base: Compute cursor dirty region aggressively
    * libagl: Optimize matrix multiply using ARM VFP
    * packages/apps: Replace Launcher2 with faster and powerful ADW.Launcher
    * frameworks/base: Improve efficiency of SoftKeyboard
    * webkit: Add optimizations done by QuIC: Adaptive request reordering, Memory Cache optimization, Efficient image caching
    * skia: Switch from VFP back to fixed scalar based calculation for performance considerations
    * skia: optimize blit routines
    * skia: Merge NEON optimizations from QuIC and ST-Ericsson
    * libpixelflinger: Re-enable ARM NEON optimizations
    * bionic: Use ARMv6 instruction for handling byte order
    * libcore: Optimize byte-swapped accesses. Known to bring better floating-point performance

## Beagle-eclair-0x5 ##

  * Release date: July 30, 2010
  * Changes:
    * Feature: Major Linux kernel upgrade: from 2.6.29 to 2.6.32 (issue tracked on [0xlab-kernel](http://code.google.com/p/0xlab-kernel/issues/list))
    * Feature: Support TI's Android PowerVR SGX (hardware 2D/3D engine)
    * Feature: Support Android USB gadget: adb and mass-storage ([Issue #95](https://code.google.com/p/0xdroid/issues/detail?id=#95))
      * Note: 0xdroid no longer support usbnet gadget driver.  Use adb or USB Ethernet instead.
    * Feature: new Bluetooth Extensions -- HID ([Issue #102](https://code.google.com/p/0xdroid/issues/detail?id=#102))
    * Feature: Make Launcher2 really usable ([Issue #76](https://code.google.com/p/0xdroid/issues/detail?id=#76))
    * Feature: Make Gallery3D workable by fixing PixelFlinger regressions ([Issue #107](https://code.google.com/p/0xdroid/issues/detail?id=#107))
    * Feature: Touchscreen Calibration shouldn't require reboot ([Issue #94](https://code.google.com/p/0xdroid/issues/detail?id=#94), [Issue #99](https://code.google.com/p/0xdroid/issues/detail?id=#99))
    * Feature: Robocat i2c port support ([Issue #134](https://code.google.com/p/0xdroid/issues/detail?id=#134))
    * Feature: Support NTFS mounting ([Issue #117](https://code.google.com/p/0xdroid/issues/detail?id=#117))
    * Feature: Improved libgralloc for non HW accelerated targets ([Issue #108](https://code.google.com/p/0xdroid/issues/detail?id=#108), [Issue #133](https://code.google.com/p/0xdroid/issues/detail?id=#133))
    * Bugfix: USB Camera support is broken due to API changes ([Issue #126](https://code.google.com/p/0xdroid/issues/detail?id=#126))
    * Bugfix: 0xdroid Installer reads configurations incorrectly. ([Issue #98](https://code.google.com/p/0xdroid/issues/detail?id=#98))
    * Bugfix: UI doesn't respond to KEY\_MENU reported from kernel ([Issue #91](https://code.google.com/p/0xdroid/issues/detail?id=#91))
    * Bugfix: HOME key does not work ([Issue #105](https://code.google.com/p/0xdroid/issues/detail?id=#105))
    * Bugfix: KeyGuard blocks the whole screen in landscape mode ([Issue #106](https://code.google.com/p/0xdroid/issues/detail?id=#106))
    * Bugfix: Gallery3D backgrounnd shadowed the thumbnail ([Issue #111](https://code.google.com/p/0xdroid/issues/detail?id=#111))
    * Bugfix: MediaPlayer video/audio out of sync ([Issue #123](https://code.google.com/p/0xdroid/issues/detail?id=#123), [Issue #124](https://code.google.com/p/0xdroid/issues/detail?id=#124))
    * Bugfix: Audio recording can't be successful as stopping the recording ([Issue #127](https://code.google.com/p/0xdroid/issues/detail?id=#127))
    * Bugfix: Touchscreen calibration UI doesn't start at all ([Issue #129](https://code.google.com/p/0xdroid/issues/detail?id=#129))
    * Bugfix: Apply Thumb2 optimizations to bionic ([Issue #103](https://code.google.com/p/0xdroid/issues/detail?id=#103))
    * Bugfix: Install to SD card failed ([Issue #97](https://code.google.com/p/0xdroid/issues/detail?id=#97))

## Beagle-eclair-0x4 ##

  * Release date: Apr 25, 2010
  * Changes:
    * Eclair codebase ([Issue #62](https://code.google.com/p/0xdroid/issues/detail?id=#62), [Issue #66](https://code.google.com/p/0xdroid/issues/detail?id=#66))
    * Improve software graphics performance in Eclair ([Issue #73](https://code.google.com/p/0xdroid/issues/detail?id=#73))
    * New hardware: DevKit 8000 ([Issue #72](https://code.google.com/p/0xdroid/issues/detail?id=#72), [Issue #74](https://code.google.com/p/0xdroid/issues/detail?id=#74), [Issue #77](https://code.google.com/p/0xdroid/issues/detail?id=#77))
    * Touchscreen support along with calibration UI ([Issue #7](https://code.google.com/p/0xdroid/issues/detail?id=#7), [Issue #59](https://code.google.com/p/0xdroid/issues/detail?id=#59))
    * 3G modem / Data card support ([Issue #80](https://code.google.com/p/0xdroid/issues/detail?id=#80))
    * Refined system image installer ([Issue #60](https://code.google.com/p/0xdroid/issues/detail?id=#60), [Issue #52](https://code.google.com/p/0xdroid/issues/detail?id=#52))
    * Small screen support ([Issue #70](https://code.google.com/p/0xdroid/issues/detail?id=#70))
    * ARM optimized string operations ([Issue #78](https://code.google.com/p/0xdroid/issues/detail?id=#78))
    * ARMv6 atomic operation improvement ([Issue #88](https://code.google.com/p/0xdroid/issues/detail?id=#88))
    * Merge skia ARMv6/ARMv7 optimization from QuIC ([Issue #83](https://code.google.com/p/0xdroid/issues/detail?id=#83))
    * Enable Launcher2 and LiveWallpaper on smaller size screen ([Issue #76](https://code.google.com/p/0xdroid/issues/detail?id=#76))

## Beagle-donut-0x3 ##

  * Release date: Dec 18, 2009
  * Changes:
    * External GSM modem for functional Android Telephony/RIL ([Issue #3](https://code.google.com/p/0xdroid/issues/detail?id=#3), [Issue #43](https://code.google.com/p/0xdroid/issues/detail?id=#43))
    * Bluetooth OBEX/OPP/FTP support ([Issue #49](https://code.google.com/p/0xdroid/issues/detail?id=#49))
    * Motion sensor support ([Issue #50](https://code.google.com/p/0xdroid/issues/detail?id=#50))
    * New Android theme ([Issue #30](https://code.google.com/p/0xdroid/issues/detail?id=#30)) along with theme selector ([Issue #48](https://code.google.com/p/0xdroid/issues/detail?id=#48))
    * Flexible resolution support for Launcher ([Issue #29](https://code.google.com/p/0xdroid/issues/detail?id=#29))
    * Ethernet support + USB OTG network ([Issue #38](https://code.google.com/p/0xdroid/issues/detail?id=#38), [Issue #39](https://code.google.com/p/0xdroid/issues/detail?id=#39), [Issue #44](https://code.google.com/p/0xdroid/issues/detail?id=#44), [Issue #53](https://code.google.com/p/0xdroid/issues/detail?id=#53), [Issue #58](https://code.google.com/p/0xdroid/issues/detail?id=#58))
    * Dalvik VM + JIT compiler for ARMv7. CaffeineMark Embedded results up to 2.7x speedup. ([Issue #56](https://code.google.com/p/0xdroid/issues/detail?id=#56))
    * ARM NEON/SIMD optimizations for PixelFlinger up to 5x speedup ([Issue #57](https://code.google.com/p/0xdroid/issues/detail?id=#57))
    * Camera / OpenCORE HAL migration to Donut ([Issue #32](https://code.google.com/p/0xdroid/issues/detail?id=#32), [Issue #34](https://code.google.com/p/0xdroid/issues/detail?id=#34))
    * Camera capture / recording fixes ([Issue #35](https://code.google.com/p/0xdroid/issues/detail?id=#35), [Issue #40](https://code.google.com/p/0xdroid/issues/detail?id=#40), [Issue #41](https://code.google.com/p/0xdroid/issues/detail?id=#41), [Issue #45](https://code.google.com/p/0xdroid/issues/detail?id=#45))
    * Audio initialization cleanup ([Issue #36](https://code.google.com/p/0xdroid/issues/detail?id=#36))
    * Fix signal strength issues with Linux Wireless Extension ([Issue #28](https://code.google.com/p/0xdroid/issues/detail?id=#28))
    * Mouse stability fix ([Issue #26](https://code.google.com/p/0xdroid/issues/detail?id=#26))
    * Dalvik stability fix ([Issue #25](https://code.google.com/p/0xdroid/issues/detail?id=#25))
    * elfcopy .debug section reordering ([Issue #20](https://code.google.com/p/0xdroid/issues/detail?id=#20))
    * Tweak web browser preference to use desktop services instead of mobile ones


## Beagle-cupcake-0x2 ##

  * Release Date: Oct 9. 2009
  * Changes:
    * Brand-new Home/Launcher with visual enhancement
    * New Camera HAL with performance tweaks
    * OMAP3 hardware video overlays support for OpenCORE rendering
    * Automatic video output scaling
    * Revised Audio In/Out support
    * New software cursor from android-x86
    * Volume manager supports SD/MMC and USB Mass Storage
    * Dalvik VM performance improvement
    * Memory leaks and race condition fixes
    * ARM NEON and Thumb2 optimized bionic/libcutils
    * ARM NEON optimizations for skia
    * Enable oprofile for ARMv7 architecture
    * early-stage porting for Busybox (linked to bionic) experiments
    * Adjust memory constraints to fit high resolution display
    * Introduce virtual touchscreen device on Beagleboard to satisfy more touch-driven applications
    * experimental package management system

## Beagle-cupcake-0x1 ##

  * Release Date: Aug 7, 2009
  * Changes:
    * Product for beagleboard
    * Revised initialization sequence for Beagleboard related settings
    * Replace yaffs2 with new and fast flash file system -- ubifs
    * Add software cursor and new keyboard layouts
    * ARMv7 tuned GNU toolchain based on gcc 4.4.1 (ARM NEON and Thumb2)
    * Tweaked memory operation routines for Cortex A8 to gain better performance
    * Enable ALSA for sound.
    * Provide GPIO keyboard
    * Fix the framebuffer flipping issue
    * Disable battery check for beagleboard
    * Disable unusable camera/video force rotation
    * Dalvik backports from donut
    * Several bug fixes.