This document is written to help a new user set up a Palm Pilot in Evolution. It has been tested with my Zire 71 (USB connection) and a Palm T/X (Wifi connection), but should work with most Palm Pilot devices.

Additions for anyone using different devices are appreciated. I have put in what I *think* will work, but as I only have the one device I can't test anything other than that device.

## Checking the Hardware

If you have a USB connection you can test it by typing

```
lsusb

```

into a terminal, which lists all the devices connected to the ports. If your device is missing it may be one of those Palm Pilots (like the Zire 71) that only 'appears' on the system when it is actually transferring. In this case, press the transfer button on the cradle or "Hotsync" from the Palm Menus, type lsusb again, and you should get a display which resembles this.

```
[paulr@myhost aux]$ lsusb
Bus 002 Device 001: ID 0000:0000  
Bus 005 Device 001: ID 0000:0000  
Bus 003 Device 003: ID 055f:0006 Mustek Systems, Inc. ScanExpress 1200 UB
Bus 003 Device 002: ID 04e8:3242 Samsung Electronics Co., Ltd 
Bus 003 Device 001: ID 0000:0000  
Bus 004 Device 001: ID 0000:0000  
Bus 001 Device 005: ID 0830:0060 Palm, Inc. Palm Tungsten T / Zire 71
Bus 001 Device 004: ID 06d6:0025 Aashima Technology B.V. 
Bus 001 Device 001: ID 0000:0000  

```

Then cancel the Hotsync on the Palm.

If you have a Serial Zire, it should be possible to test it by putting the Palm into hotsync and typing

```
cat </dev/ttyS0

```

which should display reams of gobbledegook.

To test the network link is difficult ; the simplest way is to see if your Palm is talking to the same Wifi system as your computer.