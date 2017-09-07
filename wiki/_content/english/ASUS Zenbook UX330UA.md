This article covers configuration specific to this laptop's hardware.

| **Device** | **Status** | **Kernel modules** | **X.org modules** |
| Bluetooth adapter | does not work |
| GPU | Works | i915 | modesetting |
| Touchpad | Works | libinput |
| Wireless NIC | Works (5GHz doesn't) | iwl |

This page contains instructions, tips, pointers, and links for installing and configuring Arch Linux on the [Asus ZenBook UX330UA](https://www.asus.com/Laptops/ASUS-ZenBook-UX330UA/specifications/). As of this time Asus' UX330UA page is outdated. [Use Amazon's page for reference till Asus updates they site info.](https://www.amazon.com/UX330UA-AH54-13-3-inch-Ultra-Slim-Processor-Fingerprint/dp/B01M18UZF5)

Hardware reference from UX330UA-AH54 (2017 variant). 2017 Model available since **24 feb 2017**.

## Contents

*   [1 Hardware lists](#Hardware_lists)
*   [2 Compatibility](#Compatibility)
    *   [2.1 Touchpad](#Touchpad)
        *   [2.1.1 Middle click](#Middle_click)
    *   [2.2 Wifi](#Wifi)
    *   [2.3 Graphics](#Graphics)
    *   [2.4 QHD+ Pentile Display](#QHD.2B_Pentile_Display)
    *   [2.5 Function Keys](#Function_Keys)
*   [3 See also](#See_also)

## Hardware lists

See [[1]](https://gist.github.com/Archerious/d1511100e6c128dde2d63ea9ce863b3e) for specific hardware information.

See [[2]](https://gist.github.com/Archerious/0efdba649f02262c7c5ed2a8c197b970) for UX330UAK (Kaby Lake) hardware information. Physically labelled with UX330UA-AH54 on laptop, but shows UX330UAK in dmesg. See and contribute to discussion tab of this page for fixes.

## Compatibility

### Touchpad

Works after installing [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput).

If default Palm Detection doesn't work well, one can manually disable part of the trackpad by setting AreaEdge properties.

You can do this on the fly or add these parameters in the config file:

```
 $ synclient AreaLeftEdge=500
 $ synclient AreaRightEdge=2500

```

#### Middle click

Works Perfectly as of Kernel: 4.11.2-1-ARCH and [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput).

### Wifi

Intel Dual Band wifi. Should work with recent kernels. 3.10+ with iwlwifi. See [Wireless network configuration#iwlwifi](/index.php/Wireless_network_configuration#iwlwifi "Wireless network configuration") for details.

There is a kernel panic with 5GHz frequencies: [https://bugs.archlinux.org/task/53317](https://bugs.archlinux.org/task/53317) [https://bugzilla.kernel.org/show_bug.cgi?id=195299](https://bugzilla.kernel.org/show_bug.cgi?id=195299)

### Graphics

No issues to report so far. Working perfectly with Intel HD620.

See also [Intel graphics#SNA issues](/index.php/Intel_graphics#SNA_issues "Intel graphics").

### QHD+ Pentile Display

Some models include a 3200x1800 (faux-3200x1800 RG/BW Pentile) screen, which displays very tiny characters, and can make them difficult to read due to its incomplete subpixel matrix.

For Firefox and Thunderbird, add the below property in the about:config area

```
 layout.css.devPixelsPerPx=2.

```

### Function Keys

Kernel 4.11.2-1-ARCH FN+f5 lowers brightness, fn+f6 increases brightness, fn+f11 lowers sound, fn+f12 increases sound. Working fine with Arch and gnome without tweaking anything.

## See also

*   <a class="mw-selflink selflink">ASUS Zenbook UX330UA</a>
*   [https://forums.linuxmint.com/viewtopic.php?t=243645](https://forums.linuxmint.com/viewtopic.php?t=243645)
*   [https://www.reddit.com/r/linuxhardware/comments/6aylzz/asus_zenbook_ux330uaah5q_good_for_gnulinux/](https://www.reddit.com/r/linuxhardware/comments/6aylzz/asus_zenbook_ux330uaah5q_good_for_gnulinux/)
*   [https://www.reddit.com/r/linuxhardware/comments/5eqpyt/asus_ux330uaah54_anyone_running_linux_on_this_one/](https://www.reddit.com/r/linuxhardware/comments/5eqpyt/asus_ux330uaah54_anyone_running_linux_on_this_one/)
*   Debian Wiki has yet to create a thread on UX330UA-AH54.
*   [https://groups.google.com/forum/#!topic/nairobi-gnu/U8-8vHE3_H8](https://groups.google.com/forum/#!topic/nairobi-gnu/U8-8vHE3_H8)