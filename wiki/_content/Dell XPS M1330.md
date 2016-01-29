# Dell XPS M1330

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** references to [initscripts](/index.php?title=Initscripts&action=edit&redlink=1 "Initscripts (page does not exist)") (Discuss in [Talk:Dell XPS M1330#](https://wiki.archlinux.org/index.php/Talk:Dell_XPS_M1330))

Dell XPS M1330 works quite well out of the box with Arch and GNU/Linux in general, just like his big brother Dell XPS M1530\.

## Contents

*   [1 Sound](#Sound)
*   [2 Touchpad Synaptics](#Touchpad_Synaptics)
*   [3 Fingerprint reader](#Fingerprint_reader)
*   [4 Network](#Network)
    *   [4.1 Ethernet Setup](#Ethernet_Setup)
    *   [4.2 Wireless Setup](#Wireless_Setup)
    *   [4.3 Bluetooth](#Bluetooth)
*   [5 nVidia Graphics](#nVidia_Graphics)
    *   [5.1 Compiz Fusion](#Compiz_Fusion)
    *   [5.2 GPU Temperature](#GPU_Temperature)
*   [6 Suspend](#Suspend)
*   [7 Hard Drive](#Hard_Drive)
*   [8 SD Card Reader](#SD_Card_Reader)
*   [9 Webcam](#Webcam)
*   [10 Sensors / Hardware info](#Sensors_.2F_Hardware_info)
*   [11 Extra media keys](#Extra_media_keys)
*   [12 BIOS](#BIOS)
    *   [12.1 History of BIOS Revisions](#History_of_BIOS_Revisions)
*   [13 Battery Usage](#Battery_Usage)
*   [14 External Resources](#External_Resources)

## Sound

Sound should now work out of the box. Just be sure to unmute all channels in **alsamixer**. To get the microphone working, you may have to change the digital input source (right now I have Digital Mic 1 but this could change in a new alsa version).

I suggest muting the PC speaker using alsamixer, as it makes an annoying squeak otherwise.

With the current Linux kernel 3.0 and [ALSA](/index.php/ALSA "ALSA") 1.0.24, do not mess around with the snd-hda-intel module, like supposed in different Threads ( model=3stack etc. ). Automatic detection works fine.

## Touchpad Synaptics

To configure the touchpad, you can refer to: [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") Page.

## Fingerprint reader

As of today, the device manufacturer is SGS Thomson Microelectronics (you can check with a `lsusb`). Install it using [ThinkFinger](/index.php/ThinkFinger "ThinkFinger").

If you can't get thinkfinger going, try [fprint](/index.php/Fprint "Fprint").

## Network

#### Ethernet Setup

the ethernet card is recognized by the kernel, simply load the network module to use it, or use a connection manager (see [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") for a list of programs)

#### Wireless Setup

**Note:** M1330 has been shipped with many different wireless chipset. You can find out what your card is with 'hwdetect --show-net' or 'lshwd'. Check also [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

*   **Intel chipset: 3945abg or 4965agn**

The driver is included in the Linux kernel, should work out of the box.

*   **Broadcom chipset : bcm43xx or b43 or bcm4312**

See [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless").

#### Bluetooth

**Warning:** If you have had Windows Vista installed, MAKE SURE YOU SWITCH THE BLUETOOTH MODULE 'ON' IN VISTA! Failure to do this can render the bluetooth device (Wireless 355 Bluetooth Module) unuseable in Arch or any other O/S such as Windows 7 or XP. This is despite enabling the module in the BIOS, or even reflashing the BIOS. The Bluetooth module remains firmly 'off'. Annoying.

Before taking drastic measures however, ensure the transmitter switch is 'On' - it's the switch on the right-hand side of the laptop next to the slot loading DVD Drive. If this switch is 'off' then wifi won't work either.

If you're unfortunate to find yourself with Arch installed and a 'switched off' bluetooth device your only solution may be to reinstall Vista and switch the module back on before re-installing Linux. You can safely delete Vista again once you have switched the module back on. Another option is to install Windows 7 or XP then re-enable the module using the Dell patch (R159805.EXE) as described here: [http://codereflect.com/2009/01/17/what-you-can-do-if-your-dell-laptop-doesnt-show-bluetooth-device-after-re-installing-windows-vista/](http://codereflect.com/2009/01/17/what-you-can-do-if-your-dell-laptop-doesnt-show-bluetooth-device-after-re-installing-windows-vista/)

Once you've enabled your Bluetooth module, you can then install the relevant software.

Install [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils) & [bluez-libs](https://www.archlinux.org/packages/?name=bluez-libs) from extra repository.

Edit /etc/conf.d/bluetooth:

```
DAEMON_ENABLE="true"
HIDD_ENABLE="true"

```

Restart bluetooth service:

```
# rc.d restart bluetooth

```

A list of utilities for bluetooth managing is present in AUR database.

If the above solutions do not work, for example, your Logitech BT Travel Mouse is detected the first time only, then fails to be detected, you can try removing `bluez-utils` and installing [blueman](/index.php/Blueman "Blueman") instead.

## nVidia Graphics

For those of you with the nVidia 8400GM chipset, using the [nVidia](/index.php/NVIDIA "NVIDIA") driver package works fine.

#### Compiz Fusion

Works just great with the nVidia chipset. You might like to tweak the nVidia Powermizer for maximum battery life. I have forced my graphics chipset to the lowest performance level and Compiz-Fusion runs satisfactorily with a little slowdown here and there. See [NVIDIA#Force Powermizer performance level (for laptops)](/index.php/NVIDIA#Force_Powermizer_performance_level_.28for_laptops.29 "NVIDIA") for more details on how to set this up.

To have better performance with nVidia drivers, you should try "loose binding" in Compiz Fusion (bug with Geforce 8 series). If you use Fusion Icon, just right click it, then "Compiz Options"->"Loose Binding".

#### GPU Temperature

Starting with drives > 256.53 the reported GPU Temperature is about 10° higher then before. It *may* be a driver problem resulting in higher battery usage, as higher Temperature = More Power, but it also may be something else. Hope that it doesn't shorten the life of the card. Using the 256.53 driver with Kernels newer X-Servers > 1.10 does not work, so there is a problem.

## Suspend

**Note:** If you have suspend problems, try [nvidia-prerelease driver 180.25](ftp://download.nvidia.com/XFree86/Linux-x86/180.25/), it seems to solve the problem described below.

With 180.x series of proprietary NVidia driver, suspend does not work properly, using 177.x series helps but it's slower in 2d rendering. Hibernate also works with 180.x series.

**Note:** This only works since kernel 2.6.25.x (stock Arch kernel). In former versions, force unloading modules is not provided and you have to recompile your kernel with this option.

With acpi-freq running, you might notice that CPU1 is deactivated after using pm-suspend. To fix this you have to unload acpi-freq module each time pm-suspend is called.

Put this in `/etc/pm/sleep.d/66dummy`:

```
#!/bin/bash
case $1 in
    suspend)
        rmmod -f acpi_cpufreq
        ;;
    resume)
        modprobe acpi_cpufreq
        ;;
    *)  echo "somebody is calling me totally wrong."
        ;;
esac

```

Then make it executable :

```
# chmod +x /etc/pm/sleep.d/66dummy

```

Solution was provided by this [forum topic](https://bbs.archlinux.org/viewtopic.php?id=44500).

## Hard Drive

If your hard drive clicks regurlarly, you may suffer from this [problem](https://bbs.archlinux.org/viewtopic.php?id=39258). To fix it, add these lines to your `/etc/rc.local`:

```
hdparm -B 254 /dev/sdX >> /dev/null

```

or :

```
hdparm -B 224 /dev/sdX >> /dev/null

```

(replace X in `sdX` by the letter of your drive, e.g. `sda`)

When resuming from a pm-suspend, you might notice that the hard drive is clicking again. To fix this, modify your `/etc/pm/sleep.d/66dummy` to put the lines above. Following the last example in previous suspend section:

```
case $1 in
    suspend)
        rmmod -f acpi_cpufreq
        ;;
    resume)
        modprobe acpi_cpufreq
        hdparm -B 224 /dev/sda >> /dev/null
        ;;
    *)  echo "somebody is calling me totally wrong."
        ;;
esac

```

If not already done, make the file executable.

## SD Card Reader

The device is recognized by the kernel. The Adapter module is: sdhci

The card will be availabe for mounting under the device:

```
/dev/mmcblk0p1

```

## Webcam

See [Webcam setup](/index.php/Webcam_setup "Webcam setup") for details.

Some m1330's come without a webcam, or the camera cable may be damaged or have become detached internally. If in doubt (and before pulling your hair out trying to figure out why the camera won't work despite trying every software trick), run the built-in diagnostics (available by pushing 'F12' during the POST screen, then selecting 'Diagnostics'). If no camera is hooked up or the cable is damaged, you'll receive the following message: "Hardware Detect Error - Auxiliary LCD cable not detected."

If this is the case, you can try to fix / replace / install the needed hardware according the following: [[1]](http://ahwee.com/how-to-disassemble-laptop-dell-xps-m1330), [[2]](http://support.dell.com/support/edocs/systems/xpsm1330/en/sm/display.htm), [[3]](http://support.dell.com/support/edocs/systems/xpsm1330/en/sm/camera.htm#wp1084976)

## Sensors / Hardware info

Install i8k packages: [i8kmonitor](https://aur.archlinux.org/packages/i8kmonitor/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/i8kmonitor)]</sup> and [i8kutils](https://aur.archlinux.org/packages/i8kutils/)<sup><small>AUR</small></sup>.

This will provide many useful information (temperature, fan speed, BIOS...) and utilities (fan monitor, BIOS update...). For CPU temps, use [lm_sensors](/index.php/Lm_sensors "Lm sensors").

## Extra media keys

See [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys").

## BIOS

**Note:** Updating your BIOS is always a dangerous operation (even if it is safer on a laptop with a battery). **Perform it at your own risks.**

You can perform BIOS updates under GNU/Linux! Just install [i8kutils](https://aur.archlinux.org/packages/i8kutils/)<sup><small>AUR</small></sup>!

Download latest BIOS (A15) [here (.hdr file)](http://linux.dell.com/repo/firmware/bios-hdrs/system_bios_ven_0x1028_dev_0x0209_version_a15/bios.hdr). This BIOS is for device ID 0x0209\. You can check your device ID by installing [libsmbios](https://www.archlinux.org/packages/?name=libsmbios) and then running:

```
smbios-sys-info-lite

```

You can find other bios fitting your system ID [there](http://linux.dell.com/repo/firmware/bios-hdrs/).

Then go in the directory where you downloaded the BIOS file and type as root:

```
modprobe dell_rbu

```

```
dellBiosUpdate-combat -u -f bios.hdr

```

Reboot, stare at the white frightening screen saying "BIOS update" for an endless minute. Listen to the sweet vacuum-like full speed sound of your fans just before it reboots automatically. Then observe the boot screen with Dell logo displayed much longer than usual. Sweep the sweat on your forehead. You are done!

### History of BIOS Revisions

Check this **[thread](http://forum.notebookreview.com/showthread.php?t=324392)** from NoteBook Review for detailed info.

**A10** : _May '08_

*   The only enhancement I noticed with this bios is that you can now eject a CD/DVD without freezing your system (this was really a weird behaviour !). **Please upgrade to A11 or A12 if you are currently using A10 !**

**A11** : _Jun '08_

*   Fixing [overheating issues](http://forum.notebookreview.com/showthread.php?t=264653) introduced with A10 bios.

**A12** : _Jul '08_

*   Other thermal enhancements. Temperatures are lower for me but the fan is always running.

**A13** : _Oct '08_ (removed-from-the-official-list)

*   Added support for new versions of Intel CPUs.
*   Added support for 8GB memory.

**A14** : _Nov '08_

*   Added enhancement for Wifi sniffer function.

**A15** : _Jan '09_

*   Enhance `Fn+F8` function (probably only for Intel integrated graphics)
*   Support for 8GB memory is... back!

## Battery Usage

I have been monitoring the battery usage for while. Test setting is quite easy: Get as Low as Possible with display on and X-Server running, values are reported by Powertop.

```
Kernel 3.4.4-3-ARCH and NVidia Driver 304.37, 2,4 Ghz undervolted, Crucial M4 SSD, 9,75 W. Device is 5 years old now.
Kernel 3.0-ARCH and NVidia Driver 275.xx 2,4 Ghz, OCZ SSD, pci_aspm=force on kernel line, 10,8 W. Guess that is near the technical minimum.
Kernel 2.6.37-ARCH and NVidia Driver 270.xx, 2.4 Ghz, OCZ SSD: 11,6 W
Kernel 2.6.36-ARCH and NVidia Driver 256.xx, 1.8 Ghz, Samsung HDD: 11,0 W

```

## External Resources

[This page](http://intr.overt.org/blog/?page_id=56) describes all of the various driver modules required to make the hardware in the XPS M1330 work.

French speaking people can also refer to [these articles](http://www.atlas95.com/blog/category/dell/xps-1330/).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dell_XPS_M1330&oldid=400580](https://wiki.archlinux.org/index.php?title=Dell_XPS_M1330&oldid=400580)"