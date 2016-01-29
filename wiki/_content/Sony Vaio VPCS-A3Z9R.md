# Sony Vaio VPCS-A3Z9R

## Contents

*   [1 Installation](#Installation)
*   [2 Issues](#Issues)
*   [3 Switchable graphics](#Switchable_graphics)
*   [4 What works](#What_works)

## Installation

To install Arch Linux to Sony Vaio VPCS-A3Z9R you need to make fake RAID work first:

```
# modprobe dm_mod
# ls -l /dev/md

```

You'll find all mdXXX device created. This prevents fakeraid from working properly, so we will fix it:

```
# mdadm -S /dev/mdXXX

```

Replace XXX by the values from ls command and start dmraid:

```
# dmraid -ay

```

All should work now and you can proceed with usual Arch Linux installation routine.

## Issues

If you have any issues with screen not enabling after it gone blank try disabling display auto switch off in power management settings of your favorite desktop environment.

## Switchable graphics

It is remommended to use opensource drivers from xf86-video-ati package. Somehow, vgaswitcheroo is not working, but switching graphics with PRIME works well:

```
# xrandr --setprovideroffloadsink radeon Intel

```

Use

```
# DRI_PRIME=1 mycommand

```

to enable ATI graphics card for mycommand

## What works

WiFi, HDMI output port and Fn hotkeys (display brightness, volume) are working out of the box.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Sony_Vaio_VPCS-A3Z9R&oldid=375245](https://wiki.archlinux.org/index.php?title=Sony_Vaio_VPCS-A3Z9R&oldid=375245)"