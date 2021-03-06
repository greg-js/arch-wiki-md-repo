**Acer Aspire Timeline 1810tz**

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 lspci](#lspci)
*   [2 Fan control](#Fan_control)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Touchpad](#Touchpad)
*   [4 See also](#See_also)

## lspci

```
00:00.0 Host bridge: Intel Corporation Mobile 4 Series Chipset Memory Controller Hub (rev 07)
00:02.0 VGA compatible controller: Intel Corporation Mobile 4 Series Chipset Integrated Graphics Controller (rev 07)
00:02.1 Display controller: Intel Corporation Mobile 4 Series Chipset Integrated Graphics Controller (rev 07)
00:1a.0 USB Controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #4 (rev 03)
00:1a.7 USB Controller: Intel Corporation 82801I (ICH9 Family) USB2 EHCI Controller #2 (rev 03)
00:1b.0 Audio device: Intel Corporation 82801I (ICH9 Family) HD Audio Controller (rev 03)
00:1c.0 PCI bridge: Intel Corporation 82801I (ICH9 Family) PCI Express Port 1 (rev 03)
00:1c.3 PCI bridge: Intel Corporation 82801I (ICH9 Family) PCI Express Port 4 (rev 03)
00:1d.0 USB Controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #1 (rev 03)
00:1d.1 USB Controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #2 (rev 03)
00:1d.2 USB Controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #3 (rev 03)
00:1d.7 USB Controller: Intel Corporation 82801I (ICH9 Family) USB2 EHCI Controller #1 (rev 03)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev 93)
00:1f.0 ISA bridge: Intel Corporation ICH9M-E LPC Interface Controller (rev 03)
00:1f.2 SATA controller: Intel Corporation ICH9M/M-E SATA AHCI Controller (rev 03)
00:1f.3 SMBus: Intel Corporation 82801I (ICH9 Family) SMBus Controller (rev 03)
01:00.0 Ethernet controller: Atheros Communications Device 1063 (rev c0)
02:00.0 Network controller: Intel Corporation WiFi Link 1000 Series

```

## Fan control

**Acerhdf** [[1]](http://piie.net/?section=acerhdf) is a module you can load to control the fan-speed. Download the latest version, unpack it and follow instructions in the readme file. You probably need to add your bios-version in the config-file. Your bios-version is in the error message when you load the module. Add acerhdf in your rc.conf. If it doesn't work, you can also follow these instructions: [Acer Aspire One#acerhdf](/index.php/Acer_Aspire_One#acerhdf "Acer Aspire One")

## Troubleshooting

### Touchpad

If the touchpad becomes unresponsive, add the following: [[2]](https://bbs.archlinux.org/viewtopic.php?id=107583)

 `~/.xinitrc` 
```
xinput --set-prop "SynPS/2 Synaptics TouchPad" "Synaptics Two-Finger Pressure" 280

```

## See also

*   [Linux Laptop](http://www.linlap.com/wiki/acer+aspire+1410)
*   [lesswatts.org](http://www.lesswatts.org)
*   [Ubuntu wiki](https://help.ubuntu.com/community/Aspire1810TZ/Karmic)
*   [Timeline on Notebookcheck](http://www.notebookcheck.net/Review-Acer-Aspire-Timeline-1810TZ-Subnotebook.21322.0.html)