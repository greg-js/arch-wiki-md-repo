| **Device** | **Status** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| [Wireless](/index.php/Wireless "Wireless") | Yes |
| [ALSA](/index.php/ALSA "ALSA") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| Camera | Yes |
| [Power management](/index.php/Power_management "Power management") | Yes |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes |
| SD card reader | Yes |

This page contains instructions, tips, pointers, and links for installing and configuring Arch Linux on the [ASUS Zenbook UX305](https://www.asus.com/Notebooks/ASUS-ZenBook-UX305FA/specifications/).

Hardware reference from UX305-FB041H. Model available since **12 feb 2015**.

## Contents

*   [1 Hardware lists](#Hardware_lists)
*   [2 Compatibility](#Compatibility)
    *   [2.1 Touchpad](#Touchpad)
        *   [2.1.1 Palm detection](#Palm_detection)
        *   [2.1.2 Middle click](#Middle_click)
    *   [2.2 Wifi](#Wifi)
    *   [2.3 Graphics](#Graphics)
    *   [2.4 QHD+ Pentile Display](#QHD.2B_Pentile_Display)
    *   [2.5 Function Keys](#Function_Keys)
*   [3 See also](#See_also)

## Hardware lists

See [[1]](https://gist.github.com/anonymous/6363a5462af10ee18c0c) for specific hardware information.

See [[2]](https://gist.github.com/precurse/6dc1990cd000551c8f11) for UX305CA (Skylake) hardware information. Physically labelled with UX305C on laptop, but UX305CA shows in dmesg. See and contribute to discussion tab of this page for fixes.

## Compatibility

### Touchpad

Works after installing [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput).

#### Palm detection

If default Palm Detection doesn't work well, one can manually disable part of the trackpad by setting AreaEdge properties.

You can do this on the fly or add these parameters in the config file:

```
 $ synclient AreaLeftEdge=500
 $ synclient AreaRightEdge=2500

```

#### Middle click

Three finger tap for middle click simulation should work under [libinput](/index.php/Libinput "Libinput") by default.

If you are still using the old [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) driver, you can enable Middle click by running:

```
$ synclient TapButton1=1 TapButton2=3 TapButton3=2

```

### Wifi

Intel Dual Band wifi. Should work with recent kernels. 3.10+ with iwlwifi. See [Wireless network configuration#iwlwifi](/index.php/Wireless_network_configuration#iwlwifi "Wireless network configuration") for details.

### Graphics

As of [linux](https://www.archlinux.org/packages/?name=linux) 3.16, virtual terminals show a blank screen.

UEFI results with memory changes for the Intel graphic card:

```
 With 32-256MB memory assignment in bios: Works.
 With 512MB memory assignment: **X11 breaks**. 1/3th upper-part of screen semi works (swapped and mis-alligned), rest is noise/snow.

```

Bug: [https://bugzilla.redhat.com/show_bug.cgi?id=1151757](https://bugzilla.redhat.com/show_bug.cgi?id=1151757)

```
 Kernel 3.16 boots with usable tty/x11 via bootparam: nomodeset

```

See also [Intel graphics#SNA issues](/index.php/Intel_graphics#SNA_issues "Intel graphics").

### QHD+ Pentile Display

Some models include a 3200x1800 (faux-3200x1800 RG/BW Pentile) screen, which displays very tiny characters, and can make them difficult to read due to its incomplete subpixel matrix.

For Firefox and Thunderbird, add the below property in the about:config area

```
 layout.css.devPixelsPerPx=2.

```

### Function Keys

As of [linux](https://www.archlinux.org/packages/?name=linux) 4.10, pressing `Fn+F5` (brightness down) and `Fn+F6` (brightness up) works without additional configuration on the UX305CA.

Kernel 3.16 with `acpi_listen`, when pressing `Fn+F12` (volup), `Fn+F11` (voldown), `Fn+F10` (mute), `F9` (disable mousepad):

```
 button/volumeup VOLUP 00000080 00000000 K
 button/volumedown VOLDN 00000080 00000000 K
 button/mute MUTE 00000080 00000000 K
 PNP0C14:00 000000ff 00000000

```

The light(sensor?) button (fn+a) returns:

```
 PNP0C14:00 000000ff 00000000

```

Tested with:

```
# modprobe -D asus-laptop

```

And/Or:

```
# modprobe -D asus-nb-wmi

```

No effect so far. Investigate.

## See also

*   [ASUS Zenbook UX303](/index.php/ASUS_Zenbook_UX303 "ASUS Zenbook UX303")
*   [https://wiki.debian.org/InstallingDebianOn/Asus/UX31a](https://wiki.debian.org/InstallingDebianOn/Asus/UX31a)
*   [https://wiki.debian.org/InstallingDebianOn/Asus/UX301LA](https://wiki.debian.org/InstallingDebianOn/Asus/UX301LA)