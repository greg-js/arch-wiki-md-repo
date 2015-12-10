# Touchatag RFID Reader

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Touchatag is a RFID Reader

## Contents

*   [1 About Touchatag](#About_Touchatag)
*   [2 Check hardware version](#Check_hardware_version)
*   [3 Disable pn533 and nfc driver in kernel](#Disable_pn533_and_nfc_driver_in_kernel)
*   [4 Install Touchatag](#Install_Touchatag)
*   [5 Test Touchatag](#Test_Touchatag)
*   [6 Optional: Test tags](#Optional:_Test_tags)
*   [7 Install tagEventor](#Install_tagEventor)

## About Touchatag

Touchatag is a RFID tag reader from [Touchatag](http://www.touchatag.com/). It is a cheap set consisting of an ACR122U USB tag reader and MiFare Ultralight RFID tags.

It is available [here](http://www.getdigital.de/products/Touchatag/lng/en).

**Remember: Always put a tag on the reader, otherwise you might encounter problems!**

## Check hardware version

lsusb shows the device:

```
Bus 003 Device 004: ID 072f:2200 Advanced Card Systems, Ltd 

```

lsusb -v shows also the firmware version bcdDevice:

```
idVendor           0x072f Advanced Card Systems, Ltd
idProduct          0x2200 
bcdDevice            1.00

```

The Version this howto is about is the above ACS ACR122U PICC firmware 1.0.

## Disable pn533 and nfc driver in kernel

When the ACR122U plug in, kernel(>3.5) will automatic load the pn533 driver. With the pn533 driver, pcscd will report "Can't claim interface" error. use below command to disable pn533 and nfc driver in kernel.

```
# echo "install nfc /bin/false" >> /etc/modprobe.d/blacklist.conf
# echo "install pn533 /bin/false" >> /etc/modprobe.d/blacklist.conf

```

## Install Touchatag

First install this:

```
# pacman -S pcsclite ccid

```

## Test Touchatag

To test the device run:

```
# pcscd -f

```

If you encounter a problem like this:

```
ccid_usb.c:859:ccid_check_firmware() Firmware (1.00) is bogus! Upgrade the reader firmware or get a new reader.
ifdhandler.c:104:IFDHCreateChannelByName() failed
readerfactory.c:1050:RFInitializeReader() Open Port 200000 Failed (usb:072f/2200:libusb:006)
readerfactory.c:233:RFAddReader() ACS ACR122U PICC Interface init failed.

```

The [libnfc README](http://libnfc.googlecode.com/git/README) suggests to do this:

```
If your Touchatag or ACR122 device fails being detected by PCSC-lite daemon (pcsc_scan doesn't see anything) 
then try removing the bogus firmware detection of libccid: edit libccid_Info.plist configuration file 
(usually /etc/libccid_Info.plist) and locate "<key>ifdDriverOptions</key>", turn "<string>0x0000</string>" 
value into 0x0004 to allow bogus devices and restart pcscd daemon.

Warning: if you use ACS CCID drivers (acsccid), configuration file is located in something like: 
/usr/lib/pcsc/drivers/ifd-acsccid.bundle/Contents/Info.plist
or
/usr/lib/pcsc/drivers/ifd-ccid.bundle/Contents/Info.plist

```

## Optional: Test tags

[Install](/index.php/Install "Install") [pcsc-tools](https://www.archlinux.org/packages/?name=pcsc-tools), [start](/index.php/Start "Start") `pcscd.service`, then put a tag on the reader and try to scan with:

```
# pcsc_scan

```

You should get something like this:

```
PC/SC device scanner
V 1.4.17 (c) 2001-2009, Ludovic Rousseau <ludovic.rousseau@free.fr>
Compiled with PC/SC lite version: 1.6.6
Scanning present readers...
0: ACS ACR122U 00 00

Mon Mar 21 18:16:07 2011
 Reader 0: ACS ACR122U 00 00
  Card state: Card inserted, Shared Mode, 
  ATR: 3B BE 95 00 00 41 03 00 00 00 00 00 00 00 00 00 02 90 00 

ATR: 3B BE 95 00 00 41 03 00 00 00 00 00 00 00 00 00 02 90 00
+ TS = 3B --> Direct Convention
+ T0 = BE, Y(1): 1011, K: 14 (historical bytes)
  TA(1) = 95 --> Fi=512, Di=16, 32 cycles/ETU
    125000 bits/s at 4 MHz, fMax for Fi = 5 MHz => 156250 bits/s                                                                
  TB(1) = 00 --> VPP is not electrically connected
  TD(1) = 00 --> Y(i+1) = 0000, Protocol T = 0 
-----
+ Historical bytes: 41 03 00 00 00 00 00 00 00 00 00 02 90 00
  Category indicator byte: 41 (proprietary format) 

Possibly identified card (using /usr/share/pcsc/smartcard_list.txt):
3B BE 95 00 00 41 03 00 00 00 00 00 00 00 00 00 02 90 00
        touchatag SAM card

```

## Install tagEventor

[tagEventor](http://code.google.com/p/tageventor/) runs in the background and executes scripts when a tag enters or leaves your tag reader.

Download a [binary version](http://code.google.com/p/tageventor/downloads/list) or [compile](http://code.google.com/p/tageventor/source/checkout) your own.

Run tagEventor to test your installation:

```
# tagEventor -v 1

```

The scripts are located in /etc/gtagEventor. Read the [tagEventor documentation](http://code.google.com/p/tageventor/) on how to use them.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Touchatag_RFID_Reader&oldid=368766](https://wiki.archlinux.org/index.php?title=Touchatag_RFID_Reader&oldid=368766)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Other hardware](/index.php/Category:Other_hardware "Category:Other hardware")