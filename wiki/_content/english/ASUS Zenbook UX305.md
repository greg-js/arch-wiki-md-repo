This page contains instructions, tips, pointers, and links for installing and configuring Arch Linux on the [ASUS Zenbook UX305](http://www.asus.com/Notebooks_Ultrabooks/ASUS_ZENBOOK_UX305/Features/).

Hardware reference from UX305-FB041H. Model available since **12 feb 2015**.

## Contents

*   [1 Hardware lists](#Hardware_lists)
*   [2 Compatibility](#Compatibility)
    *   [2.1 Touchpad](#Touchpad)
    *   [2.2 Wifi](#Wifi)
    *   [2.3 Graphics](#Graphics)
    *   [2.4 QHD monitor](#QHD_monitor)
    *   [2.5 Function Keys](#Function_Keys)
        *   [2.5.1 Brightness Keys](#Brightness_Keys)
*   [3 See also](#See_also)

## Hardware lists

See [[1]](https://gist.github.com/anonymous/6363a5462af10ee18c0c) for specific hardware information.

See [[2]](https://gist.github.com/precurse/6dc1990cd000551c8f11) for UX305CA (Skylake) hardware information. Physically labelled with UX305C on laptop, but UX305CA shows in dmesg. See and contribute to discussion tab of this page for fixes.

## Compatibility

### Touchpad

See [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") for details.

Multi-touch scrolling works as of kernel 3.16.

If default Palm Detection doesn't work well, one can manually disable part of the trackpad by setting AreaEdge properties.

You can do this on the fly or add these parameters in the config file:

```
 $ synclient AreaLeftEdge=500
 $ synclient AreaRightEdge=2500

```

**UX305C:**

Touchpad will only work by default with Linux 4.5.0-rc1 or later. Can currently be used by installing [linux-mainline](https://aur.archlinux.org/packages/linux-mainline/).

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

### QHD monitor

Some models include a 3200x1800 screen, which display very tiny characters.

For Firefox and Thunderbird, add the below property in the about:config area

```
 layout.css.devPixelsPerPx=2.

```

### Function Keys

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

#### Brightness Keys

For whatever reason, `xev` does not return any events for the standard brightness keys, but `F3` and `F4` seem to be detected as `XF86KbdBrightnessDown` and `XF86KbdBrightnessUp`, respectively.

## See also

*   [ASUS Zenbook UX303](/index.php/ASUS_Zenbook_UX303 "ASUS Zenbook UX303")
*   [https://wiki.debian.org/InstallingDebianOn/Asus/UX31a](https://wiki.debian.org/InstallingDebianOn/Asus/UX31a)
*   [https://wiki.debian.org/InstallingDebianOn/Asus/UX301LA](https://wiki.debian.org/InstallingDebianOn/Asus/UX301LA)