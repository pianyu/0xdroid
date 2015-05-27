WIP

# Install.conf #

0xdroid's new installer reads options from install.conf. Modifying install.conf changes the installer's behavior.

```
[installer]

# Name your image files
KERNEL_IMAGE  = 0xkernel-beagle.bin
ROOTFS_IMAGE  = android-beagle.ubi
U_BOOT_IMAGE  = flash-uboot.bin

# To install to your SD card, uncomment the following line
# INSTALL_TO_SD = y

# To fetch images from net, uncomment the following lines
#    IPADDRESS is the ip address of the target device
# NET_INSTALL=y
# IPADDRESS=192.168.0.202
# REMOTE_KERNEL_IMAGE=http://192.168.0.201/0xkernel-beagle.bin
# REMOTE_ROOTFS_IMAGE=http://192.168.0.201/android-beagle.ubi

# Enable verbose debug message
# DEBUG=y

[beagleboard]

DEFAULT_DISPLAY = dvi
DEFAULT_VIDEOMODE = dvi:1024x768MR-24@60

[devkit8000]

# Bootargs for 7 inch LCD panel
DEFAULT_DISPLAY = lcd
DEFAULT_VIDEOMODE = lcd:800x480

# Bootargs for 4.3 inch LCD panel
# DEFAULT_DISPLAY = lcd
# DEFAULT_VIDEOMODE = lcd:480x272
# OPTION_ARGS = omapfb.rotate=1
```