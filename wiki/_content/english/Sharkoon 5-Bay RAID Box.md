Sharkoon 5-Bay RAID Box external Raid USB3/eSata case [[1]](http://www.sharkoon.com/?q=en/node/1809).

## Known issues

The SMART values of the top most HDD can't be accessed. When using the HDDs without the hardware RAID they don't hibernate or switch off when the computer or USB is powered off. When using the hdds separately with a software RAID the RAID fails a lot especially when hibernation of disks is activated [[2]](https://lycabettus.wordpress.com/2012/01/26/a-softraid-setup-in-osx-lion-using-the-sharkoon-esata-enclosure/) (this can be fixed by installing a non official firmware update for the JMS539 Sata/USB 3.0 Controller )

## Updating the JMS539 Sata/USB 3.0 Controller's firmware

For updating the driver the easyest way is to use the windows installer. download the latest firmware+installer for windows from station-drivers.com [[3]](http://www.station-drivers.com/index.php/downloads/Drivers/Jmicron/JMS539-Sata-USB-3.0-Controller/JMS-539-Firmware-Version-255.31.3.41.22/) Plug the Sharkoon 5-Bay RAID Box in a USB2 socket at your windows computer (a USB3 socket should not work for the updating process after that it can be used with USB3 again of course). Install the new firmware with the downloaded installer.