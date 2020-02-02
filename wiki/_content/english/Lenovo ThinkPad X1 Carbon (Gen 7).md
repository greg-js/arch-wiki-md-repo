Related articles

*   [Lenovo ThinkPad X1 Carbon](/index.php/Lenovo_ThinkPad_X1_Carbon "Lenovo ThinkPad X1 Carbon")
*   [Lenovo ThinkPad X1 Carbon (Gen 2)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_2) "Lenovo ThinkPad X1 Carbon (Gen 2)")
*   [Lenovo ThinkPad X1 Carbon (Gen 3)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_3) "Lenovo ThinkPad X1 Carbon (Gen 3)")
*   [Lenovo ThinkPad X1 Carbon (Gen 4)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_4) "Lenovo ThinkPad X1 Carbon (Gen 4)")
*   [Lenovo ThinkPad X1 Carbon (Gen 5)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_5) "Lenovo ThinkPad X1 Carbon (Gen 5)")
*   [Lenovo ThinkPad X1 Carbon (Gen 6)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_6) "Lenovo ThinkPad X1 Carbon (Gen 6)")
*   [Lenovo ThinkPad X1 Yoga (Gen 3)](/index.php/Lenovo_ThinkPad_X1_Yoga_(Gen_3) "Lenovo ThinkPad X1 Yoga (Gen 3)")
*   [Lenovo ThinkPad X1 Yoga (Gen 4)](/index.php/Lenovo_ThinkPad_X1_Yoga_(Gen_4) "Lenovo ThinkPad X1 Yoga (Gen 4)")

**Tip:** A great resource for thinkpads is [https://www.thinkwiki.org/wiki/ThinkWiki](https://www.thinkwiki.org/wiki/ThinkWiki)

The Lenovo ThinkPad X1 Carbon, 7th generation is an ultrabook introduced in early 2019\. It features a 14" screen, 8th-gen or 10th-gen Intel Core processors and integrated [Intel UHD 620 graphics](/index.php/Intel_graphics "Intel graphics").

To ensure you have this version, [install](/index.php/Install "Install") the package [dmidecode](https://www.archlinux.org/packages/?name=dmidecode) and run:

```
# sudo dmidecode -s system-version
ThinkPad X1 Carbon 7th

```

| **Device** | **Working** | **Modules** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes | i915, (intel_agp) |
| [Wireless network](/index.php/Wireless_network_configuration#iwlwifi "Wireless network configuration") | Yes | iwlmvm |
| Native Ethernet with [dongle](https://www.lenovo.com/us/en/accessories-and-monitors/cables-and-adapters/adapters/CABLE-BO-Ethernet-Extension-Adapter-2/p/4X90Q84427) | Yes | ? |
| Mobile broadband Fibocom | Yes¹ | ? |
| Audio | Yes | snd_hda_intel |
| Microphone | No⁴ | snd_sof, snd_sof_intel_hda |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes | psmouse, rmi_smbus, i2c_i801 |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes | psmouse, rmi_smbus, i2c_i801 |
| Camera | Yes | uvcvideo |
| [Fingerprint reader](/index.php/Fprint "Fprint") | Yes² | ? |
| [Power management](/index.php/Power_management "Power management") | Yes³ | ? |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes | btusb |
| Keyboard backlight | Yes | thinkpad_acpi |
| Function/Multimedia keys | Yes | ? |
| 

1.  The Fibocom LTE module has Linux support once switched to USB mode; see [[1]](https://forums.lenovo.com/t5/Other-Linux-Discussions/How-To-Configure-X1-Carbon-Gen-7-on-Debian-FingerPrint-4G-Modem/td-p/4550327) and [[2]](https://github.com/abrasive/xmm7360)
2.  An official driver and a reverse engineered driver are in the works [[3]](https://gitlab.freedesktop.org/libfprint/libfprint/issues/181) (*06cb:00bd*).
3.  S3 suspend requires changes to BIOS settings, see section on [#Sleep/Suspend](#Sleep/Suspend).
4.  The internal microphone doesn't work on versions of the [linux](https://www.archlinux.org/packages/?name=linux) kernel before 5.3\. On version 5.3 and newer the SOF firmware can be enabled, see [Talk#Microphone](/index.php/Talk:Lenovo_ThinkPad_X1_Carbon_(Gen_7)#Microphone "Talk:Lenovo ThinkPad X1 Carbon (Gen 7)").

 |

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware](#Hardware)
*   [2 BIOS](#BIOS)
    *   [2.1 Updates](#Updates)
        *   [2.1.1 Automatic (Linux Vendor Firmware Service)](#Automatic_(Linux_Vendor_Firmware_Service))
        *   [2.1.2 Manual (fwupdmgr)](#Manual_(fwupdmgr))
    *   [2.2 Sleep/Suspend](#Sleep/Suspend)
    *   [2.3 S3 Suspend Bug with Bluetooth Devices](#S3_Suspend_Bug_with_Bluetooth_Devices)
    *   [2.4 BIOS configurations](#BIOS_configurations)
*   [3 Touchpad issues](#Touchpad_issues)
*   [4 Power management/Throttling issues](#Power_management/Throttling_issues)
    *   [4.1 throttled](#throttled)
*   [5 Audio](#Audio)
    *   [5.1 Volume controls](#Volume_controls)
        *   [5.1.1 Persistent fix](#Persistent_fix)
    *   [5.2 Microphone](#Microphone)
*   [6 Disabling red LED in ThinkPad logo](#Disabling_red_LED_in_ThinkPad_logo)
*   [7 Additional resources](#Additional_resources)

## Hardware

Additional hardware information from `lsusb` and `lspci` can be found bellow when using the [linux](https://www.archlinux.org/packages/?name=linux) kernel 5.2.7:

`lsusb`

```
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 06cb:00bd Synaptics, Inc. 
Bus 001 Device 002: ID 04f2:b67c Chicony Electronics Co., Ltd 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

`lspci`

```
00:00.0 Host bridge: Intel Corporation Device 3e34 (rev 0c)
00:02.0 VGA compatible controller: Intel Corporation UHD Graphics 620 (Whiskey Lake) (rev 02)
00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 0c)
00:08.0 System peripheral: Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th Gen Core Processor Gaussian Mixture Model
00:12.0 Signal processing controller: Intel Corporation Cannon Point-LP Thermal Controller (rev 11)
00:14.0 USB controller: Intel Corporation Cannon Point-LP USB 3.1 xHCI Controller (rev 11)
00:14.2 RAM memory: Intel Corporation Cannon Point-LP Shared SRAM (rev 11)
00:14.3 Network controller: Intel Corporation Cannon Point-LP CNVi [Wireless-AC] (rev 11)
00:15.0 Serial bus controller [0c80]: Intel Corporation Cannon Point-LP Serial IO I2C Controller #0 (rev 11)
00:15.1 Serial bus controller [0c80]: Intel Corporation Cannon Point-LP Serial IO I2C Controller #1 (rev 11)
00:16.0 Communication controller: Intel Corporation Cannon Point-LP MEI Controller #1 (rev 11)
00:1d.0 PCI bridge: Intel Corporation Cannon Point-LP PCI Express Root Port #9 (rev f1)
00:1d.4 PCI bridge: Intel Corporation Cannon Point-LP PCI Express Root Port #13 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Cannon Point-LP LPC Controller (rev 11)
00:1f.3 Audio device: Intel Corporation Cannon Point-LP High Definition Audio Controller (rev 11)
00:1f.4 SMBus: Intel Corporation Cannon Point-LP SMBus Controller (rev 11)
00:1f.5 Serial bus controller [0c80]: Intel Corporation Cannon Point-LP SPI Controller (rev 11)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (6) I219-V (rev 11)
03:00.0 Non-Volatile memory controller: Sandisk Corp WD Black 2018/PC SN720 NVMe SSD
05:00.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
06:00.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
06:01.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
06:02.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
06:04.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
07:00.0 System peripheral: Intel Corporation JHL6540 Thunderbolt 3 NHI (C step) [Alpine Ridge 4C 2016] (rev 02)
2d:00.0 USB controller: Intel Corporation JHL6540 Thunderbolt 3 USB Controller (C step) [Alpine Ridge 4C 2016] (rev 02)

```

## BIOS

**Warning:** Don't enrolling customized Secure Boot keys now. Because of the buggy firmware, various users have reported that doing so bricks their machines.

The most convenient way to install Arch Linux is by disabling "Secure Boot" `Security -> Secure Boot - Set to "Disabled"`. However it is possible to self-sign your kernel and boot with it enabled. For further information have a look at the [Secure Boot](/index.php/Secure_Boot "Secure Boot") article.

In case your `efivars` are not properly set it is most likely due to you not being booted into [UEFI](/index.php/UEFI "UEFI"). Should the problem persist be sure to consult the [UEFI#UEFI variables](/index.php/UEFI#UEFI_variables "UEFI") section.

### Updates

#### Automatic (Linux Vendor Firmware Service)

[In August of 2018 Lenovo has joined](https://blogs.gnome.org/hughsie/2018/08/06/please-welcome-lenovo-to-the-lvfs/) the [Linux Vendor Firmware Service (LVFS)](https://fwupd.org/) project, which enables firmware updates from within the OS. BIOS updates (and possibly other firmware such as the Thunderbolt controller) can be queried for and installed through [fwupd](/index.php/Fwupd "Fwupd").

#### Manual (fwupdmgr)

Lenovo may in the future provide cabinet files that can be directly installed with fwupdmgr. Check for Linux `.cab` files from the [Lenovo ThinkPad X1 Carbon (Gen 7) driver website](https://pcsupport.lenovo.com/us/en/products/laptops-and-netbooks/thinkpad-x-series-laptops/thinkpad-x1-carbon-7th-gen-type-20qd-20qe/downloads).

1.  Make sure the AC adapter is firmly connected to the target computer.
2.  Launch Terminal.
3.  Move to the directory where the cabinet file was placed.
4.  Run `fwupdmgr install xxxxxxxx.cab` to schedule firmware update.
5.  Restart the system.
6.  The computer will be restarted and the UEFI BIOS will be updated.

### Sleep/Suspend

The BIOS has two "Sleep State" options, Windows and Linux, which you can find in at `Config -> Power -> Sleep State`. The Linux option is the traditional S3 power state where all hardware components are turned off except for the RAM, and it should work normally. The Windows option is a newer software-based "modern standby" which works on Linux (despite the name). One possible benefit to the Windows sleep state is faster wake up time, and one possible drawback is increased power usage.

### S3 Suspend Bug with Bluetooth Devices

Occasionally your Thinkpad will wake up immediately after suspending with certain [bluetooth](/index.php/Bluetooth "Bluetooth") devices added. To prevent this, remove the devices or disable [bluetooth](/index.php/Bluetooth "Bluetooth") before suspending.

### BIOS configurations

*   `Config -> Thunderbolt BIOS Assist Mode - Set to "Enabled"`. When disabled, on Linux, power usage appears to be significantly higher because of a substantial number of CPU wakeups during s2idle.

## Touchpad issues

Due to a bug in a touchpad firmware, the touchpad might not work with following logs in dmesg:

```
[    4.499490] i2c_designware i2c_designware.1: i2c_dw_handle_tx_abort: lost arbitration
[...]
[   12.668795] i2c_hid i2c-SYNA8005:00: failed to set a report to device.
[   13.678765] i2c_designware i2c_designware.1: controller timed out

```

The solution is to update touchpad firmware (version `1.3.3013412` works correctly).

## Power management/Throttling issues

A [bug](https://forums.lenovo.com/t5/Other-Linux-Discussions/X1C6-T480s-low-cTDP-and-trip-temperature-in-Linux/td-p/4028489/highlight/true) causes the CPU to consume less power than under Windows and throttle at 80°C instead of 97°.

Lenovo has confirmed the issue, [explained the cause](https://forums.lenovo.com/t5/Other-Linux-Discussions/X1C6-T480s-low-cTDP-and-trip-temperature-in-Linux/m-p/4534535/highlight/true#M13642) and published [updates for the embedded controller and the BIOS](https://forums.lenovo.com/t5/Other-Linux-Discussions/X1C6-T480s-low-cTDP-and-trip-temperature-in-Linux/m-p/4535310/highlight/true#M13653) to LVFS (*see [#BIOS Updates](#Updates)*).

### throttled

If you are stuck on an earlier version of the firmware and BIOS (or do not want to upgrade), you can install [throttled](https://www.archlinux.org/packages/?name=throttled), then run

```
sudo systemctl enable --now lenovo_fix.service

```

## Audio

As there are physically four loudspeakers, you need to configure to 4.0 audio output. When using PulseAudio there are various [configuration utilities](/index.php/PulseAudio#Front-ends "PulseAudio").

### Volume controls

In order for volume controls to work correctly you must edit `/usr/share/pulseaudio/alsa-mixer/paths/analog-output.conf.common` by adding the following above `[Element PCM]`:

```
[Element Master]
switch = mute
volume = ignore

```

A PulseAudio restart is required for this change to take effect. Make sure to increase the "*Master*" channel volume to 100% for the top-firing speakers to work (using amixer or alsamixer, found in [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils)).

#### Persistent fix

Upgrading or reinstalling [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) will overwrite this file, and [PulseAudio doesn't appear to offer another way](https://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/PulseAudioStoleMyVolumes/) to make this configuration change. To prevent pacman from overwriting the file, add the following line under `[options]` in `/etc/pacman.conf`:

```
NoUpgrade = usr/share/pulseaudio/alsa-mixer/paths/analog-output.conf.common

```

### Microphone

On kernel up to 5.2, the internal microphones are detected but [no audio is captured](/index.php/Advanced_Linux_Sound_Architecture/Troubleshooting#Microphone "Advanced Linux Sound Architecture/Troubleshooting"). Unfortunately even on the 5.3 kernels, the microphones still don't work out of the box.

You might be able to get the microphones working by following the instructions in this [docx file](https://forums.lenovo.com/lnv/attachments/lnv/lx02_en/3061/1/sof-driver-guide.docx) from the Lenovo Forums. Also check out [this post](https://bbs.archlinux.org/viewtopic.php?id=249900) from the Arch Forums.

## Disabling red LED in ThinkPad logo

You can temporarily disable the red LED in the ThinkPad logo on the cover:

1\. Enable writing to the embedded controller registers by adding the kernel parameter `ec_sys.write_support=1`. If you use UEFI boot, you can add this parameter in `/boot/efi/loader/entries/arch.conf` under "options".

2\. Disable the LED with this command:

```
# echo -n -e "\x0a" | sudo dd of="/sys/kernel/debug/ec/ec0/io" bs=1 seek=12 count=1 conv=notrunc 2> /dev/null

```

This would need to be run after each suspend/reboot to be permanent.

## Additional resources

*   [ThinkWiki X1 Carbon 7th Gen page](https://www.thinkwiki.org/wiki/Category:X1_Carbon_(7th_Gen))
*   [Dell XPS 13 9370 quirks](https://gist.github.com/greigdp/bb70fbc331a0aaf447c2d38eacb85b8f): Some pointers on getting Watt usage down to ~2W, Intel video powersaving features might be interesting, see also the [Intel graphics](/index.php/Intel_graphics "Intel graphics") page for interesting power-saving options.
*   [Intel Blog: Best practice to debug Linux* suspend/hibernate issues](https://01.org/blogs/rzhang/2015/best-practice-debug-linux-suspend/hibernate-issues), including the [pm-graph](https://github.com/01org/pm-graph) tool to analyze power usage during suspend
*   [How to fix volume control (ALSA problem)](https://forums.linuxmint.com/viewtopic.php?t=91453) This is where the volume fix came from originally.
*   [Windows System Power States](https://docs.microsoft.com/en-us/windows/win32/power/system-power-states)
*   [System Power Management Sleep States at kernel.org](https://www.kernel.org/doc/Documentation/power/states.txt)