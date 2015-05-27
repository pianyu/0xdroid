![http://beagleboard.org/static/images/2708776217_9f660db58d_o_d.png](http://beagleboard.org/static/images/2708776217_9f660db58d_o_d.png)

To work with Beagleboard, you will need the following:
  * Board
  * Host machine (Linux Ubuntu 8.x/9.x) with Ethernet card and serial port
  * Serial cable (null-modem)
  * Power supply (5V)
  * USB Hub
  * USB Mouse / Keyboard
  * Ethernet cross cable or Ethernet Switch/Hub+2 cables
  * Card Reader
  * 2Gb SD or MMC Card
  * 4:3 or 16:9 capable Display with DVI input
  * HDMI to DVI cable

## RS232 ##
  * Easy way: [Buy from digikey](http://www.digikey.com/scripts/DkSearch/dksus.dll?Detail?lang=en&site=US&name=BBC01-ND).
  * Geek way:
    * Make your our own RS232 lines as the following instructions:
      * USB to RS232 line [http://lh3.ggpht.com/\_uSgEb50CjDE/SnavUSqzYdI/AAAAAAAAA-k/qZLdOx4OCUE/s144/DSCF0789.JPG](http://picasaweb.google.com/lh/photo/Mzub6JE3co2hg6k-eYy5bg?feat=embedwebsite)
      * one RS232 male solider head (A) [http://lh4.ggpht.com/\_uSgEb50CjDE/SnavURQoIjI/AAAAAAAAA-o/SlhbKvnc-L4/s144/DSCF0790.JPG](http://picasaweb.google.com/lh/photo/oqzDSa79BLv7tS7kw1HSkQ?feat=embedwebsite) [http://lh6.ggpht.com/\_uSgEb50CjDE/SnavUnaFGbI/AAAAAAAAA-s/fUmoJJS137o/s144/DSCF0791.JPG](http://picasaweb.google.com/lh/photo/WyvxEpE4UX3D3BrUB1FE1Q?feat=embedwebsite)
      * Three lines [http://lh4.ggpht.com/\_uSgEb50CjDE/SnavUn3Db-I/AAAAAAAAA-w/BXRS9WWPcpE/s144/DSCF0792.JPG](http://picasaweb.google.com/lh/photo/bN421_2GssoMBHB09neH9Q?feat=embedwebsite)
      * one 2.5mm 2x5 10 pin header (B) [http://lh4.ggpht.com/\_uSgEb50CjDE/SnavUkxb5LI/AAAAAAAAA-0/hNGVMrpKpNM/s144/DSCF0793.JPG](http://picasaweb.google.com/lh/photo/pFQa9gzzHZvViBLV5Eod_Q?feat=embedwebsite)
      * Connecting A to B as below:
        * A <——> B
        * 2 <——–> 3
        * 3 <——–> 2
        * 5 <——–> 5
    * You can also check [Beagleboard RS232 Adapter Board](http://elinux.org/upload/2/2c/Flyswatter-ti-uart.pdf) [http://lh5.ggpht.com/\_uSgEb50CjDE/Sc02IkVpXdI/AAAAAAAAAls/noEeBdB4vhI/s144/DSCF0401.JPG](http://picasaweb.google.com/lh/photo/m4xp2JZKPEgrDnQXnF0SPg?feat=embedwebsite)

## USB OTG Lines ##

EHCI port on Beagleboard is USB 2.0 only, and you need extra USB hub to use low speed USB 1.x devices, such as USB keyboard and mouse.  Instead, you can use the OTG port for input devices.
  * Easy way: [Buy from digikey](http://search.digikey.com/scripts/DkSearch/dksus.dll?lang=en&site=US&KeyWords=10-00003-ND)
  * Geek way
    * Buy a normal mini male to USB type A male line (Generally speaking, most A male to mini male lines are in this type). Then cut the cover of mini male’s head, and short pin 4 and 5. Recover the mini male’s head.

Then you can use this line to play with USB OTG.
[http://lh6.ggpht.com/\_uSgEb50CjDE/Sc02CoGaQUI/AAAAAAAAAko/uY9CBlSNNbc/s144/DSCF0393.JPG](http://picasaweb.google.com/lh/photo/oiOHhf-eiD47gfHC9xAQkg?feat=embedwebsite)

## USB hub ##

We play with more than one devices, therefore we need a USB hub to play with. You can buy
  * [A female to female head](http://search.digikey.com/scripts/DkSearch/dksus.dll?lang=en&site=US&KeyWords=ae1474-nd) (easy to find)
  * a self-powered USB hub
Please note that you will need self-powered USB hub because the usb OTG port may not have sufficient current for all devices.

## HDMI monitor ##
  * find a monitor with HDMI or DVI-D interface (You can try TV as a monitor, but do NOT expect too much)
  * find a HDMI to HDMI or DVI-D line