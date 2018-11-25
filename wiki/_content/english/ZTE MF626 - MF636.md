Related articles

*   [USB 3G Modem](/index.php/USB_3G_Modem "USB 3G Modem")

The ZTE MF626 / MF636 is a USB modem which combines 3G+/3G with EDGE/GPRS in one compact device. It has an integrated micro-SD card reader. It can send data at speeds up to 4.5 Mbps on 3G+ networks and receive data at speeds of up to 7.2 Mbps.  It is also known as the Rogers (Canadian cellular carrier) red stick USB dongle.

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Disable CD mode on the device](#Disable_CD_mode_on_the_device)
    *   [1.2 Disable CD mode on the device with wvdial](#Disable_CD_mode_on_the_device_with_wvdial)
    *   [1.3 Setup udev rules](#Setup_udev_rules)
    *   [1.4 Create a wvdial configuration](#Create_a_wvdial_configuration)
*   [2 Connect to the internet](#Connect_to_the_internet)
*   [3 Tips and tricks](#Tips_and_tricks)
*   [4 See also](#See_also)

## Configuration

### Disable CD mode on the device

Using a Windows machine, plug in the USB device and go through the short install wizard. Once done, close the Rogers app that starts up, then head into the Device Manager (*Control Panel > System > Hardware > Device Manager*). Under the Ports section, find the COM port that's connected to the USB modem (ignore the Diagnostics mode). Connect to that COM port through Hyperterminal, found in the Accessories area of the Start Menu. Connection parameters are:

```
Bits per Second: 115200
Data bits: 8
Parity: None
Stop bits: 1
Flow Control: None

```

Once connected, type the following commands:

```
AT+ZOPRT=5
AT+ZCDRUN=8

```

This tells the modem not to use CD mode when it is first plugged into a computer. Now exit Hyperterminal and remove the USB modem. You are done with Windows.

### Disable CD mode on the device with wvdial

First, remove the module `usb-storage` then load the `usbserial` module:

```
# rmmod usb_storage
# modprobe usbserial

```

Edit `/etc/wvdial.conf`:

```
[Dialer Defaults]
Modem = /dev/ttyUSB0
Modem Type = Analog Modem
ISDN = 0
Init1 = AT+ZOPRT=5
Init2 = AT+ZCDRUN=8

```

Execute *wvdial*, it should use those commands and fail to connect. Once it exits, unplug the stick and plug it back in and it should be recognized as a modem.

### Setup udev rules

Create the following [udev](/index.php/Udev "Udev") rule:

 `/etc/udev/rules.d/90-zte.conf.rules`  `ACTION=="add", SUBSYSTEM=="usb", ATTRS{idVendor}=="19d2", ATTRS{idProduct}=="0031", RUN+="/sbin/modprobe usbserial vendor=0x19d2 product=0x0031", MODE="660", GROUP="network"` 

### Create a wvdial configuration

[Wvdial](/index.php/Wvdial "Wvdial") is an easy-to-use frontend to PPPd. Make sure you replace the `/dev/ttyUSB0` line with the node that your USB modem is connected to, you can see that with dmesg. Save as `/etc/wvdial.conf`.

```
[Dialer Defaults]
Modem = /dev/ttyUSB0
ISDN = off
Modem Type = USB Modem
Baud = 7200000
Init = ATZ
Init2 =
Init3 =
Init4 =
Init5 =
Init6 =
Init7 =
Init8 =
Init9 =
Phone = *99#
Phone1 =
Phone2 =
Phone3 =
Phone4 =
Dial Prefix =
Dial Attempts = 1
Dial Command = ATM1L3DT
Ask Password = off
Password = off
Username = na
Auto Reconnect = off
Abort on Busy = off
Carrier Check = off
Check Def Route = off
Abort on No Dialtone = off
Stupid Mode = on
Idle Seconds = 0
Auto DNS = on

```

If the above does not work, try the following (extracted from sakis3g):

This is for Etisalat Misr, but should work for all the other networks that use the same device.

```
[Dialer Defaults]
Modem = /dev/ttyUSB2
Modem Type = Analog Modem
ISDN = 0
Baud = 7200000
Dial Attempts = 3
Username = apn
Password = apn
Phone = *99#
Auto Reconnect = off
Stupid Mode = 1
Init1 = ATZ
Init6 = AT+CGEQMIN=1,4,64,640,64,640
Init7 = AT+CGEQREQ=1,4,64,640,64,640

```

## Connect to the internet

Now just run *wvdial* to connect

```
# wvdial

```

If you see output reporting your PPP local and endpoint IP addresses, then it worked.

## Tips and tricks

All steps above may be obsolete if the modem stick is supported by [sakis3g](http://www.sakis3g.org/) which is an all in one command line script and automatises all the steps above. The installation steps are as follows:

```
wget "[http://www.sakis3g.org/versions/latest/$ARCH/sakis3g.gz](http://www.sakis3g.org/versions/latest/$ARCH/sakis3g.gz)" # where $ARCH is either i386 or amd64
gunzip sakis3g.gz
chmod +x sakis3g
./sakis3g --interactive

```

## See also

*   [Ubuntu forum post 1](http://ubuntuforums.org/showthread.php?t=1005910) - further details
*   [Ubuntu forum post 2](http://ubuntuforums.org/showthread.php?t=1065934) - further details