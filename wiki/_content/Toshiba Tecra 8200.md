# Toshiba Tecra 8200

## Contents

*   [1 INSTALL in a toshiba tecra 8200](#INSTALL_in_a_toshiba_tecra_8200)
*   [2 Audio](#Audio)
*   [3 Video](#Video)
*   [4 Network](#Network)
*   [5 Modem](#Modem)
*   [6 Some tweaking](#Some_tweaking)
*   [7 Some references](#Some_references)

## INSTALL in a toshiba tecra 8200

Install goes pretty smooth and error-free. All my recommendations are provided to make your install process easier. If you do not need them, or find ways to make a certain process easier or better, please edit this document.

## Audio

Use the ALSA module: snd-ymfpci

## Video

Use xorg.

In `Xorg.conf`, these parameters work.

```
Section "InputDevice"
	Identifier  "Mouse0"
	Driver      "mouse"
	Option	    "Protocol" "PS/2"
	Option	    "Emulate3Buttons"
	Option	    "Device" "/dev/psaux"
	Option      "ZAxisMapping" "4 5"
EndSection
Section "Monitor"
	Identifier   "lcdhard"
	HorizSync    31.5 - 48.5
	VertRefresh  55.0 - 90.0
EndSection
Section "Device"
	Identifier  "tridentXP"
	Driver      "trident"
	ChipSet     "bladeXP"
	Card        "trident bladeXP"
EndSection

```

Do not forget to install the window manager of your choice. it could be xfce or gnome or kde. and to pacman the trident driver

## Network

*   Wired

in `/etc/modprobe.d/modprobe.conf`

```
alias eth0 eepro100

```

and in `rc.conf`, configure your network as you want. in my case eth0 is like

```
eth0="192.168.0.2 netmask 255.255.255.0 broadcast 192.168.0.255"
gateway="default gw 192.168.0.1"
ROUTES=(gateway)

```

*   Wireless

if i follow other persons, it would be run with orinoco_cs. you must install pcmcia_cs and wirelesstools

## Modem

The modem appears to be working. The drivers for the modem are no longer available from the official source. You can find a collection of them [here](http://linmodems.technion.ac.il/packages/smartlink/) from an unofficial source.

## Some tweaking

[Install](/index.php/Install "Install") the [hwd](https://www.archlinux.org/packages/?name=hwd) package. This is a nice hardware detection script.

comment or remove in rc.sysinit the last line, it's a screensaver but usually, you have another one

```
/usr/bin/setterm -blank 15

```

*   permit to the user to halt or reboot the system

*   using nano to change the config file, it's very simple to use but to prevent the problem of wraping add in `/etc/nanorc`

```
set nowrap

```

*   time

to synchronise your time use ntpclient. install the npt package, then when you want update time

```
ntpdate pool.ntp.org

```

## Some references

*   installation report
    *   [Mandrake Linux 9.0/9.1 on Toshiba Tecra 8200](http://www.justobjects.nl/just/linux/linux-tecra-8200-all.html)
    *   [Mandrake Linux 8.2 (Bluebird) and Win 2000 on Toshiba Tecra 8200 mini-HOWTO](http://home.sprintmail.com/~khollenshead/linux/linux-winnt-tecra8200.html)
    *   [Redhat 7.2 on Toshiba Tecra 8200 HOWTO](http://sandroboscaro.tripod.com/tecra-redhat-howto.html)

*   [toshiba website](http://linux.toshiba-dme.co.jp/linux/eng/pc/tecra8200_memo.htm)
*   [specs](http://linux.toshiba-dme.co.jp/linux/eng/spec.php3?model=PT820xxx)
*   [pdf specs](http://cdgenp01.csd.toshiba.com/content/product/pdf_files/detailed_specs/tecra_8200.pdf)

*   specifiq software
    *   modem pctel Toshiba Satellite 1100- S101.
        *   [pctel-linux](http://linmodems.technion.ac.il/pctel-linux/)
        *   [fnfx](http://fnfx.sourceforge.net/)
*   [ifplugd](http://0pointer.de/lennart/projects/ifplugd/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Toshiba_Tecra_8200&oldid=392741](https://wiki.archlinux.org/index.php?title=Toshiba_Tecra_8200&oldid=392741)"