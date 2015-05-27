# Profiling 0xdroid #

This page describes how to do system-wide profiling via oprofile in 0xdroid.  Original Android supports oprofile.  However it only supports ARMv6.  Our reference hardware is Beagleboard, which is powered by TI OMAP353x SoC (ARMv7 architecture).  Therefore 0xlab developers did some hacks around the files inside directory external/oprofile and update new prebuilt 'oprofile' utilities in order to let oprofile support ARMv7.  The prebuilt files change nothing but using the same architecture table in external/oprofile.  Thus, you will need to use the prebuilt 'opreport' to analysis the logs.

The following is a mini how-to of using it.

## Kernel setting ##

0xdroid kernel does not enable oprofile flag by default, and you need to turn it on first.
You can refer to wiki [build Linux kernel from scratch](Source.md) and build the custom kernel.  To enable OPROFILE, you will need to set the following flags:
```
 + CONFIG_OPROFILE_ARMV7=y
 + CONFIG_OPROFILE=y
 + CONFIG_PROFILING=y
 + CONFIG_HAVE_OPROFILE=y
 + CONFIG_TRACEPOINTS=y
```
Run on Beagleboard.

You can use 'opcontrol' to trigger start/stop profiling on Beagleboard. You can also choose logging kernel symbols or not.  If you want to log kernel symbols, you need to put the vmlinux into beagleboard.  To be easily deploy, using USB mass storage is a good idea.  0xdroid should be able to mount USB disk automatically on directory /sdcard.  If not, do the following commands:
```
/system/bin/mount -t vfat /dev/block/sda1 /sdcard
setprop EXTERNAL_STORAGE_STATE mounted
am broadcast -a android.intent.action.MEDIA_MOUNTED —ez read-only false -d file:///sdcard
```

Before starting profiling, you need to setup the oprofile.  Please refer to oprofile manual in advance.  Here are the reference instructions to set up oprofile:
```
opcontrol —setup —event=CPU_CYCLES:15000:::1:1 —vmlinux=/sdcard/vmlinux —kernel-range=0xc0008000,0xcfffffff
echo 16 > /dev/oprofile/backtrace_depth
opcontrol —start
```

Then do activity you want to be profiled.
After finish do the following command to stop profiling.

```
opcontrol —stop
```

## Analysis ##

After profiling, you will need to move all the data to host to do analysis. Therefore you can choose use usb ethernet to do such task.
Connecting beagleboard

On device:
  * plug in usb line between laptop and beagleboard (OTG port)
  * netcfg usb0 up
  * ifconfig usb0 192.168.0.202
On laptop:
  * sudo ifconfig usb0 192.168.0.200 # beware nm-applet may breaks it, you can set it up.
  * export ADBHOST=192.168.0.202
  * export PATH={Where you put 0xdroid}/out/host/linux-x86/bin:$PATH
  * pkill adb
  * adb devices # If you can see the device then you can do next step, or you may need to checkout what’s wrong.
opimport\_pull

Using the script **external/oprofile/opimport\_pull** to pull down samples and analysis them.

```
cd {Where you put 0xdroid}
. build/envsetup.sh
setpaths
export OPROFILE_EVENTS_DIR=${PWD}/prebuilt/linux-x86/oprofile/
cd external/oprofile
./opimport_pull /tmp/beagle-cupcake-oprofile
```

Then the script will pull down samples from beagleboard and do the symbol analysis once for you.
If you want to dig out more information, you can use:

```
cp ${Where you build your kernel}/vmlinux ${OUT}/symbols
${OPROFILE_EVENTS_DIR}/bin/opreport —session-dir=/tmp/beagle-cupcake-oprofile -p ${OUT}/symbols -d
```

Enjoy it!

## Appendix ##

You can check the script of opimport\_pull and do whatever you want, even add graphvis supports.
You can also move out the /data/oprofile to other SD card and so that you can not using opimport\_pull.