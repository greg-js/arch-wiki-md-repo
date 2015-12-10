# Lenovo ThinkPad T410

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

The ThinkPad T410 is a laptop with little to no hardware issues.

## Contents

*   [1 Trackpoint](#Trackpoint)
*   [2 Fingerprint reader](#Fingerprint_reader)
*   [3 Graphics](#Graphics)
*   [4 Modules](#Modules)

## Trackpoint

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [TrackPoint](/index.php/TrackPoint "TrackPoint").**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:Lenovo ThinkPad T410#](https://wiki.archlinux.org/index.php/Talk:Lenovo_ThinkPad_T410))

To make the trackpoint able to scroll while holding down the middle button, make a xorg configuration file `/etc/X11/xorg.conf.d/20-trackpoint.conf` with the following contents:

```
Section "InputClass"
	Identifier	"Trackpoint Wheel Emulation"
	MatchProduct	"TPPS/2 IBM TrackPoint|DualPoint Stick|Synaptics Inc. Composite TouchPad / TrackPoint|ThinkPad USB Keyboard with TrackPoint|USB Trackpoint pointing device|Composite TouchPad / TrackPoint"
	MatchDevicePath	"/dev/input/event*"
	Option		"EmulateWheel"		"true"
	Option		"EmulateWheelButton"	"2"
	Option		"Emulate3Buttons"	"false"
	Option		"XAxisMapping"		"6 7"
	Option		"YAxisMapping"		"4 5"
EndSection

```

## Fingerprint reader

The fingerprint reader works, just follow the setup guide in [Fprint](/index.php/Fprint "Fprint").

```
Bus 001 Device 004: ID 147e:2016 Upek Biometric Touchchip/Touchstrip Fingerprint Sensor

```

## Graphics

See [NVIDIA](/index.php/NVIDIA "NVIDIA") or [intel](/index.php/Intel "Intel").

## Modules

The tp_smapi module is available in the AUR. After installation put the following in `/etc/modules-load.d/thinkpad.conf` to load the module on boot.

```
tp_smapi

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_T410&oldid=399398](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_T410&oldid=399398)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")