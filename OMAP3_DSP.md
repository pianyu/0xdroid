# Introduction #

OMAP3530 has C46x+ DSP core embedded in the SoC.  [Rowboat](http://code.google.com/p/rowboat/)  DSP support is based on
TI Linux Digital Video Software Development Kit (DVSDK) for OMAP3530, and 0xdroid extends the efforts of [Rowboat](http://code.google.com/p/rowboat/).

## Instructions ##

For giving a try and following this, please use beagle-donut-dsp branch:
```
# repo init -u git://gitorious.org/0xdroid/manifest.git -b beagle-donut-dsp -m ti-dsp.xml
```

and for building with dsp stack, there is a step that we need to download codec engine and specify the GStreamer/DSP support:
```
# make TARGET_PRODUCT=beagleboard BUILD_WITH_GST=true dvsdk
```

For getting more info, please check http://code.google.com/p/rowboat/wiki/DSP as well and rowboat project.