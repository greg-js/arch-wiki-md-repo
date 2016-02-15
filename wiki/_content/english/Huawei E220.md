## Contents

*   [1 Introduction](#Introduction)
*   [2 Plugging In](#Plugging_In)
    *   [2.1 Quick Start](#Quick_Start)
        *   [2.1.1 Easy Install using Network Manager](#Easy_Install_using_Network_Manager)
        *   [2.1.2 Bare Naked](#Bare_Naked)
        *   [2.1.3 Configure n' Dial](#Configure_n.27_Dial)
        *   [2.1.4 If using PIN code add this before Init2](#If_using_PIN_code_add_this_before_Init2)
    *   [2.2 Slow Start](#Slow_Start)
*   [3 Extras](#Extras)
    *   [3.1 Port Testing](#Port_Testing)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Hal](#Hal)
    *   [4.2 Route](#Route)
*   [5 Links](#Links)

# Introduction

Marketed by various telecommunications companies in several countries, the [E220](http://en.wikipedia.org/wiki/Huawei_E220) is a 3.5G HSDPA USB modem used mainly for wireless Internet access via mobile telephony networks. Technically it is a modem, USB and (due to the CDFS format) CD-ROM device. With a kernel version older than 2.6.20, getting Linux to recognize the device as a modem and accessing its functions requires a workaround.

_"Linux kernel versions prior to 2.6.20 have some problems with it, as the SCSI CDROM fakevolume with drivers for Microsoft systems gets automounted by usbstorage.ko module, preventing serial device /dev/ttyUSB0 from working properly."_

However, as support for it was added in 2.6.20 via modules _usb-storage_ and _usbserial_, getting it to work is as simple as plugging it in and dialling up (the above statement is of no concern to us as we can load and unload modules at will, it was probably meant for pre-packaged GNU and Linux distributions). In fact, using the modem under Linux proves to be more reliable as there are no uncalled-for disconnections. This is probably due to the fact that we are communicating directly with the modem, whereas in Windows or Mac OS X drivers are installed on first run (that is what the storage portion is for) and connection is achieved through a thick software layer every time, leaving room for possible interferences and conflicts.

# Plugging In

## Quick Start

### Easy Install using Network Manager

If you are using network-manager then this modem should be plug 'n play. I tested using Huawei E270, but since lsusb said that my modem is E220/E270, I assume it is the same. (Note: You can follow these instructions too if lsusb detects your Huawei E180 as E220.)

The required packages are modemmanager and network-manager-applet from extra. Install them if you haven't.

Start the networkmanager daemon from rc.conf or manually using /etc/rc.d/networkmanager start. Start the nm-applet if it hasn't started yet. Make sure the modem is connected; I used a cable with two usb port like the one for an external harddrive. Then, from nm-applet add a Mobile Broadband config via 'Edit Connections...'. Set the config according your network; usually apn, username, and password.

Activate the connection by choosing it on the Network Manager applet. If it is not showing up, unplug and plug in the modem again to refresh the connection. Now you should see it listed in the Network Manager applet. Click on it and it will try to connect. Once connected, the icon will change. You're good to go then.

For _Vodafone_ brands of this device, you can use [vodafone-mccd](https://aur.archlinux.org/packages.php?ID=32986) which is the [Vodafone Mobile Connect Card Driver for Linux](http://forge.vodafonebetavine.net/projects/vodafonemobilec/). The official name is very long, yes.

### Bare Naked

You can just try _Plug 'n Dial_ first to see if it works (I will give you free beer if it does!). After hooking up to the USB port (some say an upright position is best; let it hang over the edge of the desk), check to make sure it is detected.

```
$ cat /proc/bus/usb/devices

```

You should see **Huawei** somewhere there. If not, you are on your own. The _usb-storage_ and/or _usbserial_ modules must be loaded, whether manually or by [HAL](/index.php/HAL "HAL") is up to you and/or your system.

```
# modprobe usb-storage
# modprobe usbserial
$ sleep 6 # the modem may take a while to initialize
$ ls /dev/ttyUSB*

```

You should see three renditions of **ttyUSB**. If not, we will get to that later. This _is_ a "Quick Start" after all, no? The ports:

*   ttyUSB0 - Modem
*   ttyUSB1 - USB?
*   ttyUSB2 - Nothing

Now you need a dialler. Most convenient of all would be [wvdial](/index.php/Wvdial "Wvdial"), so install it. You should have _ppp_ already, if not just pull them both in.

```
# pacman -S wvdial ppp

```

### Configure n' Dial

Most SIM and data services provided together with the device do not require special settings and work with similar configuration to get connected. They are almost "Plug n' Play", a special trait of Linux. Edit _/etc/wvdial.conf_ and use something like the following:

```
[Dialer hsdpa]
Phone = *99***16#
Username = 65
Password = user123
Stupid Mode = 1
Dial Command = ATDT
Modem = /dev/ttyUSB0
Baud = 460800
Init2 = ATZ
Init3 = ATQ0 V1 E1 S0=0 &C1 &D2 +FCLASS=0
ISDN = 0
Modem Type = Analog Modem

```

For providers that do require a specific Init string and user/password combination, [mkwvconf-git](https://aur.archlinux.org/packages/mkwvconf-git/) in AUR can help generate a wvdial configuration (based on the [mobile-broadband-provider-info-git](https://aur.archlinux.org/packages/mobile-broadband-provider-info-git/) package).

### If using PIN code add this before Init2

```
 Init1 = AT+CPIN=9999

```

where 9999 is changed for your PIN-code

There is an example [here](http://www.insync.za.net/3g_docs/wvdial.conf) by a "Linux Guru". Then load the PPP module.

```
# modprobe ppp-generic

```

You can now connect immediately, but probably only as root, which is **not** a disadvantage.

```
# wvdial hsdpa

```

## Slow Start

_Edit: This section is nullified if you have UDEV and HAL workarounds, or a script, or a package from AUR._

So why then? Well, for some reason those of us on newer kernels still have to ride the old ways. In some cases, all that is needed to be done is to remove the _usb-storage_ module first, then load _usbserial_ with the device IDs. The first _cat_ command on this page will have that information, while _lsusb_ is an alternative. Anyhow, the IDs are the same for almost all E220s, so you can copy wholesale.

```
# modprobe -r usb-storage usbserial
# modprobe usbserial vendor=0x12d1 product=0x1003

```

In other cases, where the _option_ module gets autoloaded for use by _usbserial_, you just have to blacklist it in [rc.conf](/index.php/Rc.conf "Rc.conf"):

```
MOD_BLACKLIST=(option) 

```

When you cannot salvage anything from this either, you have to _go Gentoo_ and compile something. Do not worry, it is only a script and we do things like this almost everyday, albeit in _bash_.

```
$ mkdir ~/huawei-e220 && cd ~/huawei-e220
$ wget [http://www.kanoistika.sk/bobovsky/archiv/umts/huaweiAktBbo.c](http://www.kanoistika.sk/bobovsky/archiv/umts/huaweiAktBbo.c)
$ gcc -lusb -o e220 *.c
# ./e220

```

This gets around the kernel to recognize the modem functionalities of the device. You can now carry on and connect using the above methods. If you had to follow this step, you will always need the script unless you set _udev_ rules and such (package link below). So move it to a global _PATH_.

```
$ cd ~/huawei-e220
# mv e220 /usr/bin/e220

```

Now it is easier.

# Extras

_Note: It seems some people get it to work using ttyUSB1, which should not be the case, but rest assured that at least on recent kernels and systems ttyUSB0 is the correct port to dial with._

## Port Testing

To check if the device is functioning alright on a particular serial port, there is a program for probing serial devices.

```
# pacman -S minicom

```

Now run it.

```
# minicom -s

```

Change the serial port to _/dev/ttyUSB1_ and exit from the page, this will open the main program. When it initializes the modem, issue the command _AT_. The answer should be _OK_, which means the modem is working well on that port.

# Troubleshooting

## Hal

The hald daemon detects the SCSI CD-ROM drive and because of that it will try to change the modem to storage mode. To prevent this you need to create a Hal policy so it ignores the device.

Create a file the /usr/share/hal/fdi/preprobe/20thirdparty/10-huawei-e220.fdi and putt this in it

```
<?xml version="1.0" encoding="UTF-8"?>
<deviceinfo version="0.2">
  <device>
    <match key="usb.vendor_id" int="0x12d1"> 
      <match key="usb.product_id" int="0x1003"> 
        <merge key="info.ignore" type="bool">true</merge>
      </match>
    </match>
  </device>
</deviceinfo>

```

With this, for my experience, only two USB serial ports are created and them vodafone-mccd doesn't recognize correctly the modem but you can connect correctly with wvdial.

## Route

If problem with connection through ppp0 one might need to add the network manually:

```
 # ip route add ip route add 10.0.0.0/8 dev ppp0

```

if the remote adress starts on 10.

Then you add default route and dns as usually:

```
# ip route add default via 10.x.x.x

```

(change to remote adress recieved and viewed with command `ip a`)

# Links

[http://wwwu.uni-klu.ac.at/agebhard/HuaweiE220/](http://wwwu.uni-klu.ac.at/agebhard/HuaweiE220/)
[http://oozie.fm.interia.pl/pro/huawei-e220/](http://oozie.fm.interia.pl/pro/huawei-e220/)
[http://mybroadband.co.za/vb/showthread.php?t=21726](http://mybroadband.co.za/vb/showthread.php?t=21726)
[USB 3G Modem](/index.php/USB_3G_Modem "USB 3G Modem")