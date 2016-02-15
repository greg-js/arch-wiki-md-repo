[Asus Trio TX201LA](http://www.asus.com/Notebooks_Ultrabooks/ASUS_Transformer_Book_Trio_TX201LA/specifications/) is a good piece of recent (for 2014) hardware, which allows one to combine desktop, laptop and tablet in a single piece. In fact the tablet is a different story - detachable screen runs Android and is out of scope. Nevertheless the base itself (which can serve as desktop) or with attached tablet (forming laptop) can boast Intel Haswell Core i7 or Core i5 CPU, 4G RAM and 500G HDD. And that is what running Linux, almost smoothly.

## Contents

*   [1 Install](#Install)
    *   [1.1 WiFi](#WiFi)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 SATA](#SATA)
    *   [2.2 Kernel](#Kernel)
    *   [2.3 ACPI](#ACPI)
    *   [2.4 Backlight](#Backlight)
    *   [2.5 Wireless Switch](#Wireless_Switch)
    *   [2.6 Other Keys](#Other_Keys)
*   [3 See also](#See_also)

### Install

You can follow standard [Installation](/index.php/Installation "Installation") process. No problems with [UEFI](/index.php/UEFI "UEFI") spotted.

#### WiFi

When installing from 2014.12 image running on 3.17 kernel wifi for some reason doesn't work. It seems it works for some older versions, and for 3.18+ but with 3.17 you'd probably need some USB wifi. WIFI is detected, wpa_supplicant runs on it however it cannot associate in any band. It seems it's caused by way too restrictive regulation settings, so you may also try to adjust AP settings for safe channels (1-11, 36-44) and sit closer to AP to get it working.

Don't forget to install crda among other required wireless packages to apply less restrictive regional regulation domain settings.

```
pacman -Syu iw iwconfig wpa_supplicant crda dhcpcd

```

This together with 3.18 or newer kernel make wifi work somehow. To improve WiFi quality even better adjust power management settings, effectively disabling any kind of power management for wifi. E.g.

```
echo 'options rtl8821ae ips=N fwlps=N swlps=Y' > /etc/modprobe.d/wifi.conf

```

to switch to software PM. If even that doesn't help you may switch off PM now by

```
iwconfig wlp2s0 power off

```

It's really about power management, not power supply for the card (which is managed by rfkill). Or to preserve it permanently across reboots

```
echo 'ACTION=="add",SUBSYSTEM=="net",ENV{ID_NET_DRIVER}=="rtl8821ae", RUN+="iwconfig $name power off"' > /etc/udev/rules.d/wifi.rules

```

### Troubleshooting

#### SATA

You may notice during installation or on initial reboot ATA errors, such as `CRC` or `READ FPDMA QUEUED` - those are result of SATA speed mismatches. The controller is capable of 6Gbps while the internal HDD can only run at 3Gbps. This will add a boot delay until `libata` finds the correct speed by probing and resetting.

It is likely better to enforce 3Gbps by adding `libata.force=3.0Gbps` to the [kernel command line](/index.php/Kernel_command_line "Kernel command line"). Remove this restriction after migrating to an SSD drive.

#### Kernel

Even though system is capable of running current stable kernel it maybe worth spending some time compiling newer rc+ kernel until it is packaged. With 3.18 kernel you may experience various lock-outs, hang-outs and even kernel panics - due to inadequate memory and resource management. On the other hand 3.19 or 4.0+ is running much more smoothly, although not fully fixed even that. The hardware is heavily dependent on ACPI management which in turn mostly relies on certain driver feedback so be ready to expect various oops and kernel thread hangups until proper hooks are installed by kernel and drivers.

When configuring kernel don't forget to enable drivers/options for following device specific components:

| Component | HW Name | Kernel menu item |
| WIFI | Realtek 8821AE | Device Drivers -> Network Device Support -> Realtek rtlwifi family -> Realtek 8821AE |
| Touchpad | Elantech EPS/2 Touchpad | Device Drivers -> Input device support -> Mice -> PS/2 Mouse -> Elantech PS/2 Protocol extension |
| Touchscreen | Atmel maXTouch Digitizer | Device Drivers -> HID Support -> Special HID Drivers -> HID Multitouch Pannels |
| Bluetooth | Realtek USB HCI | Networking Support -> Bluetooth Subsystem Support -> Bluetooth Device Drivers -> HCI USB Driver |
| Audio | Intel HD + Conexant | Device Drivers -> Sound card support -> Advanced Linux Sound Architecture -> HD Audio -> Conexant and HDMI |
| WebCAM | Chicony HD USB Video | Device Drivers -> Multimedia Support -> Media USB Adapters -> USB Video Class |

#### ACPI

#### Backlight

Backlight does not work by default in Linux due to missing Ambient Light Sensor (ALS) driver. ACPI handler for backlight is hooked to ALS probe and when driver is absent it generates ACPI Error:

```
ACPI Exception: AE_AML_PACKAGE_LIMIT, Index (0xFFFFFFFFFFFFFFFF) is beyond end of object (length 0x10) (20140926/exoparg2-420)
ACPI Error: Method parse/execution failed [\_SB_.PCI0.LPCB.EC0_._Q0E] (Node ffff88011a448820), AE_AML_PACKAGE_LIMIT (20140926/psparse-536)

```

One way then which seems to be somehow working to deal with backlight is using [xrandr](/index.php/Xrandr "Xrandr"), but even that is not really decreasing backlight, rather as command says changes brightness:

```
xrandr --output eDP1 --brightness 1.0

```

It accepts values from 0(off) to 1 and above, but above 1.5 it becomes overexposed. Workable range 0.0 to 1.2, good default would be 0.5 (which you can put into your local xsession rc file.

Also you can turn backlight on and off and that either by setting brightness to 0 or bl_power to 1 in the sys/class/backlight/* knobs.

To make the backlight keys work you need to load ALS driver. That could be achieved by booting Windows and rebooting to Linux - but that will work until power-off or suspend.

If you don't mind compiling kernel module you may try to use off-the-tree driver for ALS by [Viktar Vaŭčkievič](https://github.com/victorenator/als.git). With the driver ACPI handler works properly so you don't need any other scripts.

If the driver still doesn't work (most of the time it doesn't - certain hardware initialisation for ALS seems to be still missing) you may try instead [this fork](https://github.com/rufferson/als) which by default disabled ALS allowing manual backlight management via ACPI with fn keys.

#### Wireless Switch

Wireless switch does not work by default on linux. ACPI handler detects Win8 OS and delegates rfkill management to software driver, which is missing. One way to handle this is to remove Windows 2012 OSI string - which may affect other ACPI handlers though. When OSI is below Win8 - asus-nb-wmi's wapf parameter influences how hardware switch is acting. WAPF handling is different from the one documented in asus-nb-wmi.c - the implementation states following:

	Bit 3 is set (0x4)

	Full software control, only keypress is sent (0x88) and handler terminates.

	Bit 1 is set (0x1)

	Fn switch toggles both radios (toggling airplane mode), sending corresponding ACPI key event when they are on or off.

	Any other values

	Toggles radios in a sequence - both off, WL on/BT off, WL off/BT on, both on.

If OSI string is required to be preserved - the only way out is using driver for ACPI device ([ASHS](https://github.com/rufferson/ashs)) which will handle events and do radio management.

#### Other Keys

There are multiple special keys available under the same ACPI event key: Display-Off key (fn+F7), Camera key (fn+V), Screen-profile (fn+C), Auto-backlight (fn+A) and Touchpad-Off (fn+F9). All of them are generating

```
PNP0C14:00 000000ff 00000000

```

which makes them useless for acpid. Screen profile key though generates in addition another event (eg, two events are emitted)

```
button/prog1 PROG1 00000080 00000000 K

```

so you can bind toggle script which enables/disables backlight using both knobs (in case you turn it off by one of them while debugging). Something like

```
#!/usr/bin/bash

SYS=/sys/class/backlight
BLD=intel_backlight

PWR_KNOB=$SYS/$BLD/bl_power
BRT_KNOB=$SYS/$BLD/brightness

PWR_VAL=`cat $PWR_KNOB`
BRT_VAL=`cat $BRT_KNOB`

if [ $BRT_VAL -eq 0 -o $PWR_VAL -eq 1 ]; then
  echo 0 > $PWR_KNOB
  echo 99 > $BRT_KNOB
else
  echo 1 > $PWR_KNOB
  echo 0 > $BRT_KNOB
fi
```

which could be hooked into system by simple file like /etc/acpi/events/bl

```
event=button/prog1.*
action=/etc/acpi/bl.sh

```

Additionally volume keys are sending proper acpi events (MUTE/VOLUP/VOLDOWN) so could be bound to the system or left for app to react since they are also sending proper XF86 scancodes.

Other keys sending proper scancodes are XF86TouchpadToggle (fn+F9), XF86WebCam (fn+V), XF86Launch1 (fn+C), XF86Launch6 (fn+Space) and undefined NoSymbol with keycode 248(fn+A) - AutoBacklight. Even though not labeled on the keyboard - fn+F3 and fn+F4 are generating XF86Mail and XF86WWW correspondingly.

Useless keys then are Wireless/Airplane-Mode(fn+F2), Backlight (fn+F5-F7) and DisplaySwitch (fn+F8) as they are not generating any events.

## See also

*   [ASUS Zenbook Prime UX31A](/index.php/ASUS_Zenbook_Prime_UX31A "ASUS Zenbook Prime UX31A")

*   [ASUS Transformer Book Trio](http://www.asus.com/Notebooks_Ultrabooks/ASUS_Transformer_Book_Trio_TX201LA/)

*   [NotebookCheck Test](http://www.notebookcheck.com/Test-Asus-Transformer-Book-Trio-TX201LA-Convertible.108616.0.html)

*   [Linux Laptop Usability Matrix](http://www.linlap.com/asus_transformer_book_trio_tx201la)