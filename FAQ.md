# Frequently Asked Questions

# Frequently Asked Questions #

## General Questions ##

### After flashing the u-boot I can't use saveenv? ###

You may have downloaded a wrong u-boot image that accidentally uploaded by developer. This u-boot image disables all NAND access and enforces default boot environment.

Download the new flash-uboot.bin and flash again.

### The installer always set wrong bootargs? ###

This might caused by a bug in the installer ([Issue #98](https://code.google.com/p/0xdroid/issues/detail?id=#98))

Try comment out unused parts in install.conf

### The flashing failed and I can't boot again? ###

If you saw
```
Mounting SD card... 
Copying files.. 
        * 0xkernel.bin 
        * android.ubi 
Writing android.ubi into NAND flash... 
File System :: Done! 
Check point 
Erase NAND flash (Kernel) 
Writing 0xkernel.bin into NAND flash... 
starting from 0 
Kernel :: Done! 
Check point 
nandwrite: File I/O error on input: Is a directory 
nandwrite: Data was only partially written due to error 
: Is a directory 
Erase NAND flash (U-Boot) 
Writing into NAND flash... 
starting from 0 
Failed to flash 
Exit.. 
```
And subsequence reboot you got
```
Texas Instruments X-Loader 1.41 
Starting OS Bootloader... 
```
And stuck here,

You must download the release image very early because the original release image had a serious bug that erase the bootloader silently. We are sorry about this, try download again and see if the problem is gone.

## Devkit8000 ##
### The LCD flickers and displays nothing ###

If you saw a lots errors like
```
omapdss DISPC error: GFX_FIFO_UNDERFLOW, disabling GFX
omapdss DISPC error: SYNC_LOST, disabling LCD
```

There are two possible reasons:

  1. The display resolution was wrong
  1. Framebuffer rotation enabled on big screen.

The 4.3 inch panel should have
```
omapfb.mode=lcd:480x272 omapfb.rotate=1
```

The 7 inch panel should have
```
omapfb.mode=lcd:800x480 omapfb.rotate=0
```

### Can I rotate the 7 inch LCD panel? ###

Currently we can only use landscape mode on bigger panel.

It's due to OMAP's DMA engine isn't fast enough to handle the big rotation area and the VRFB subsystem is quite unstable ATM.