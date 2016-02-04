# Hsoconnect

This article covers using Hsoconnect with Option HSDPA modems (UMTS and EDGE/GPRS networks).

## Contents

*   [1 Hsoconnect Introduction](#Hsoconnect_Introduction)
*   [2 Installing](#Installing)
*   [3 Connecting to the Internet](#Connecting_to_the_Internet)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Firmware](#Firmware)
    *   [4.2 Permissions](#Permissions)
*   [5 External Resources](#External_Resources)

## Hsoconnect Introduction

HSOconnect is an easy to use connection manager that is designed to work with Option's latest HSDPA and HSUPA modems. Use HSOconnect to quickly connect to the Internet using your modem. Start up HSOconnect and it will keep looking for a device until you plug one in. If your SIM requires a PIN code; HSOconnect will ask you to enter it.

## Installing

HSOconnect can be [installed](/index.php/AUR#Installing_packages "AUR") with the package [hsoconnect](https://aur.archlinux.org/packages/hsoconnect/), available in the [AUR](/index.php/AUR "AUR").

Add your user to the 'network' group:

```
# gpasswd -a $USER network

```

## Connecting to the Internet

Click the Connect button and the program will automatically connect you to the Internet. While connected the amount of data sent and received is displayed. Click on the Connect button again to disconnect from the Internet. If you minimize HSOconnect move your mouse over the name to view how the connection is going. You cannot connect to the Internet until the modem is registered on a network.

As normal user, connect you Option modem and launch:

```
$ hsoconnect

```

## Troubleshooting

#### Firmware

HSOconnect will not connect using web'n'walk Surfstick (T-Mobile) which is identical to the Option iCON 225

VendorID= 0x0af0 ProductID= 0x6971

unless it is flashed to the latest Firmware.

#### Permissions

To run HSOconnect as user, the user has to be in the group "network". However the supplied udev-rules edit /dev/ttyHS* group permissions to group dialout. If there is no group dialout, group permissions will be set to root.

Edit

```
/etc/udev/rules.d/51-hso-udev.rules

```

and change "dialout" to "network".

```
ls -l /dev/ttyHS[0-2]

crw-rw---- 1 root network 252, 0 Aug 11 13:46 /dev/ttyHS0
crw-rw---- 1 root network 252, 1 Aug 11 13:46 /dev/ttyHS1
crw-rw---- 1 root network 252, 2 Aug 11 13:46 /dev/ttyHS2

```

## External Resources

*   [Hsoconnect](http://www.pharscape.org/hsoconnect.html)
*   [Icon 225 3G specifications](http://www.option.com/en/products/products/usb-modems/icon225/specifications/#start)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Hsoconnect&oldid=392236](https://wiki.archlinux.org/index.php?title=Hsoconnect&oldid=392236)"