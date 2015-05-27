# Introduction #

In order to communicate via TCP/IP to Beagleboard, a basic understanding of the networking expectations is required. Each end of the USB connection forms a LAN (local area network) segment, with the Beagleboard's USB networking device at one end (default 192.168.0.202) and your laptop or desktop at the other end (192.168.0.200 in this guide).

Normally, your desktop machine will know how to reach the Internet, having had its gateway (the IP address of the machine or device which knows how to send packets to machines beyond your subnet) configured via DHCP or statically (probably via a router). For the Beagleboard to reach the Internet, your desktop will have to be configured to route and masquerade (NAT) packets from it.

Normally, none of this is an issue, but problems can arise when the subnet between the Beagleboard and your desktop overlap with the desktop to the router (which forms a second LAN), since your desktop might not know how to route traffic properly.

In other words: if your existing router and desktop have addresses 192.168.0.(something) changing them to e.g. 192.168.1.(something) might save you a lot of troubleshooting later.

# Using network-manager on Linux distributions using udev #

It is possible to use network-manager to automatically connect to the Beagleboard using udev. The process uses udev to run a script when the Beagleboard is plugged in.

Then, it will show as usb0 from Linux host side.  The script uses the 'ifconfig' command to set the mac address of the usb network interface.  Also, it invokes 'iptables' for NAT configurations.

To begin, create /etc/udev/rules.d/80-beagleboard.rules :
```
KERNEL=="usb[0-9]*", DRIVERS=="cdc_ether", ACTION=="add", RUN+="/usr/local/sbin/beagleboard-usb-add.sh %k"
```

Next, create the file /usr/local/sbin/beagleboard-usb-add.sh :
```
#!/bin/sh

sysctl net.netfilter.nf_conntrack_acct=1

ifconfig $1 192.168.0.200 netmask 255.255.255.0
iptables -A POSTROUTING -t nat -j MASQUERADE -s 192.168.0.0/24
echo 1 > /proc/sys/net/ipv4/ip_forward
iptables -P FORWARD ACCEPT
```


# USB Ethernet Gadget with Windows HOST machine #

If you have not done the setup required for Microsoft Window RNDIS configuration, then Host machine will prompt for USB new hardware found screen, go through the steps below to do the same, otherwise continue by skipping this step

  * Select the Linux.inf as the driver "linux.inf".
  * On the Windows PC, bring up Network Connections and look for the Device Name:
```
Linux USB Ethernet/RNDIS Gadget. 
```
> Right-mouse click for Properties. Scroll down to Internet Protocol (TCP/IP), select it, and press the Properties button.
  * Select an IP address close to the one selected for the Beagleboard. It should be IP address of 192.168.0.200 and subnet mask of 255.255.255.0.