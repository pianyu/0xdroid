# Our focus #

The focus of this Wiki is to centralize 0xdroid specific information and how to get it running on the Beagleboard / Beagleboard-xM / Pandaboard / TI OMAP SoC derived boards.  The Wiki includes information on how to [download and install 0xdroid](UsingPreBuiltImages.md), how to use specific parts (like the [mouse actions](MouseAction.md) and [USB networking](USB_Networking.md)), what features of the 0xdroid are currently functional and how you can contribute to improve the releases.

Browse through the menu section on your left to find those details you are looking for.

# Development Goal #

The reason why [0xlab](http://0xlab.org/) has to construct yet another project derived from Android is that we wish to exploit the ability of certain hardware SoC and leverage the existing open source software work.  So, 0xdroid is not only regarded as Android porting project but also an open environment to introduce several new features, improvement, and community-driven feedbacks, that implies it is fairly possible to facilitate more hardware peripherals, extended devices, and improve software re-usability.
  * ARM SoC: dedicated to Beaglboard, Beagleboard, Pandaboard and TI OMAP derived platforms
  * Peripheral support
    * Device: WiFi, Bluetooth, WebCam, Accelerometer, GSM modem / 3G data card
    * Software: corresponding software development such as Bluetooth OBEX.
  * Performance: use NEON instruction set introduced in ARM Cortex A8, and enable SoC specific functionality such as DSP.
  * Multimedia compatibility and stability
  * Usability and visual enhancements

For detailed 0xdroid development roadmap and status, please check wiki page: [Roadmap](Roadmap.md).

# Get Involved #

  * Give feedbacks via IRC [#0xlab](http://webchat.freenode.net/?channels=0xlab) or join the 0xlab mailing list:
    * General discussion: http://groups.google.com/group/0xlab-discuss
    * Technical / Development: http://groups.google.com/group/0xlab-devel
  * If you find an issue or bug, please file a project issue: http://code.google.com/p/0xdroid/issues/list