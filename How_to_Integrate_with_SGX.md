# Introduction #

The Graphics SDK (with the associated drivers) for the PowerVR SGX graphics core on OMAP35x supports several methods for sharing 2D images between OpenGL ES 1.1, 2.0, OpenVG and native OS windowing systems. The terminology and use of these various approaches for the SGX is difficult to discern from the standard documents that define them because the PowerVR implementation is not comprehensive and there are many issues in their application that dramatically affect performance.
Those that are new to OpenGL ES might think that PixelBuffers, Texture Maps, Pixmaps and/or Frame Buffer Objects are interchangeable or compatible, but that is generally not true. These constructs have been defined over time as OpenGL has evolved and their intended uses and level of support on the SGX differ significantly. ([from its WiKi page](http://processors.wiki.ti.com/index.php/Render_to_Texture_with_OpenGL_ES#Introduction))

# Install the Android Graphics SGX SDK on Host Machine #

#### Download the code ####
```
$ git clone git://gitorious.org/rowboat/ti_android_sgx_sdk.git
```

#### Execute the installer (quiet mode) ####
```
$ cd ti_android_sgx_sdk
$ echo -e "Y\nY\nqY\n/tmp/sgx-dir\n" | DISPLAY=:9999 ./OMAP35x_Android_Graphics_SDK_setuplinux_3_01_00_03.bin
```

#### Edit Rules.make to configure the SGX source build ####
```
$ cd /tmp/sgx-dir
$ vi Rules.make
```

```
 # set home area HOME (relative location for all SDK operations)
  HOME=INVALIDVAL
  Example: HOME=/home/user/

 # Path of Android Root FS*
  ANDROID_ROOT=$(HOME)/INVALIDVAL
  Example: ANDROID_ROOT=$(HOME)/beagle-eclair/out/target/product/beagleboard

 # set toolchain root path for arm-eabi*
  CSTOOL_DIR=INVALIDVAL
  Example: CSTOOL_DIR=/home/user/beagle-eclair/prebuilt/linux-x86/toolchain/arm-eabi-4.4.0

 #set the kernel installation path*
  KERNEL_INSTALL_DIR=$(HOME)/INVALIDVAL
  Example: KERNEL_INSTALL_DIR=$(HOME)/kernel
```

#### disable some code as below ####
```
diff --git a/GFX_Linux_KM/services4/system/omap3/sysutils_linux.c b/GFX_Linux_KM/services4/system/omap3/sysutils_linux.c
index 8ce39c1..84dca3d 100755
--- a/GFX_Linux_KM/services4/system/omap3/sysutils_linux.c
+++ b/GFX_Linux_KM/services4/system/omap3/sysutils_linux.c
@@ -65,6 +65,7 @@ static PVRSRV_ERROR ForceMaxSGXClocks(SYS_SPECIFIC_DATA *psSysSpecData)
 {
        PVR_UNREFERENCED_PARAMETER(psSysSpecData);
 
+#if 0
        /* Pin the memory bus bw to the highest value according to CORE_REV */
 #if defined(SGX530) && (SGX_CORE_REV == 125)
        if(cpu_is_omap3630())
@@ -72,6 +73,7 @@ static PVRSRV_ERROR ForceMaxSGXClocks(SYS_SPECIFIC_DATA *psSysSpecData)
 #else
        omap_pm_set_min_bus_tput(&gpsPVRLDMDev->dev, OCP_INITIATOR_AGENT, 664000);
 #endif
+#endif
        return PVRSRV_OK;
 }
 
@@ -291,7 +293,7 @@ IMG_VOID DisableSGXClocks(SYS_DATA *psSysData)
                clk_disable(psSysSpecData->psSGX_FCK);
        }
 
-       omap_pm_set_min_bus_tput(&gpsPVRLDMDev->dev, OCP_INITIATOR_AGENT, 0);
+       //omap_pm_set_min_bus_tput(&gpsPVRLDMDev->dev, OCP_INITIATOR_AGENT, 0);
 
        atomic_set(&psSysSpecData->sSGXClocksEnabled, 0);
```

#### Build the Kernel Module sources ####
```
$ make

building the sgx kernel modules...
copying the sgx kernel modules to appropriate folder...
```


#### Install the drivers in Target filesystem ####
```
$ make install OMAPES=3.x

Installing PowerVR Consumer/Embedded DDK 1.5.15.2766 on host

File system installation root is /home/user/beagle-eclair/out/target/product/beagleboard/
Installation complete!
```

**More details?! [Check SGX WiKi page!](http://code.google.com/p/rowboat/wiki/ConfigureAndBuild#Install_the_Android_Graphics_SGX_SDK_on_Host_Machine)**



# Build Android kernel and system image with SGX #

Follow [source](Source.md) wiki page to get 0xdroid source code

```
$ mkdir beagle-eclair
$ cd beagle-eclair
$ repo init -u git://gitorious.org/0xdroid/manifest.git -b beagle-eclair
$ repo sync
```

### make sure few patches about SGX ###

  * init.sgx.sh (a shell script to start SGX service)
http://gitorious.org/0xdroid/system_core/commit/cf6db85b308be32f100f7b134d0c6350e5edc504.patch

  * init.rc (put SGX service in init)

http://gitorious.org/0xdroid/vendor_0xlab/commit/26ee500e459982eca381edbe1d47c38b8ed90cc4.patch