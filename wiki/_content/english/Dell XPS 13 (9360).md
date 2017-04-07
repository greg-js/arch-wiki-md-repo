| **Device** | **Status** | **Modules** |
| Video | Working | i915 |
| Wireless | Working | ath10k |
| Bluetooth | Working | btusb |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | hid_multitouch (mousedev) |
| Webcam | Working | uvcvideo |
| USB-C / Thunderbolt 3 | Working |  ? |
| Wireless switch | Working | intel_hid |
| Function/Multimedia Keys | Working |  ? |

The Dell XPS 13 Late 2016 (9360) is the fourth-generation model of the XPS 13 line. The laptop is available since October in both a standard edition with Windows installed as well as a Developer Edition with Ubuntu installed. There is no hardware difference between them. Just like the older versions ([Dell XPS 13 (9333)](/index.php/Dell_XPS_13_(9333) "Dell XPS 13 (9333)"), [Dell XPS 13 (9343)](/index.php/Dell_XPS_13_(9343) "Dell XPS 13 (9343)") and [Dell XPS 13 (9350)](/index.php/Dell_XPS_13_(9350) "Dell XPS 13 (9350)")) it is available in different hardware configurations. This fourth gen model includes Intel's Kaby Lake CPU and configurable with up to 16GB LPDDR 1866 MHz RAM and a 1TB PCI SSD. It will now also be available in Rose Gold. Prior to previous information it won't be available with LPDDR 2133 MHz RAM.

The installation process for Arch on the XPS 13 does not differ from any other PC. For installation help, please see the [Installation guide](/index.php/Installation_guide "Installation guide") and [UEFI](/index.php/UEFI "UEFI"). This page covers the current status of hardware support on Arch, as well as post-installation recommendations.

As of kernel 4.5, the Intel Kaby Lake architecture is supported.

## Contents

*   [1 Content adaptive brightness control](#Content_adaptive_brightness_control)
*   [2 NVM Express SSD](#NVM_Express_SSD)
    *   [2.1 NVME Power Saving Patch](#NVME_Power_Saving_Patch)
*   [3 Video](#Video)
    *   [3.1 Module-based Powersaving Options](#Module-based_Powersaving_Options)
    *   [3.2 Blank screen issue after booting](#Blank_screen_issue_after_booting)
*   [4 Wireless](#Wireless)
*   [5 Bluetooth](#Bluetooth)
*   [6 Thunderbolt 3 / USB 3.1](#Thunderbolt_3_.2F_USB_3.1)
    *   [6.1 Ethernet repeatedly disconnects/reconnects with Dell USB-C adapter (DA200)](#Ethernet_repeatedly_disconnects.2Freconnects_with_Dell_USB-C_adapter_.28DA200.29)
    *   [6.2 USB-C Compatibility Chart](#USB-C_Compatibility_Chart)
    *   [6.3 Thunderbolt Firmware updates](#Thunderbolt_Firmware_updates)
*   [7 SATA controller](#SATA_controller)
*   [8 Touchpad](#Touchpad)
    *   [8.1 Remove psmouse errors from dmesg](#Remove_psmouse_errors_from_dmesg)
*   [9 Touchscreen](#Touchscreen)
    *   [9.1 Gestures](#Gestures)
    *   [9.2 Scrolling in Firefox](#Scrolling_in_Firefox)
*   [10 Keyboard Backlight](#Keyboard_Backlight)
*   [11 Hidden Keyboard Keys](#Hidden_Keyboard_Keys)
*   [12 Firmware Updates](#Firmware_Updates)
*   [13 Troubleshooting](#Troubleshooting)
    *   [13.1 EFISTUB does not boot](#EFISTUB_does_not_boot)
    *   [13.2 Not waking from suspend](#Not_waking_from_suspend)
    *   [13.3 Power Drain after waking from standby](#Power_Drain_after_waking_from_standby)
    *   [13.4 Popping Sound on headphones/external speakers](#Popping_Sound_on_headphones.2Fexternal_speakers)
    *   [13.5 Coil Whine](#Coil_Whine)
    *   [13.6 Freezing after waking from suspend](#Freezing_after_waking_from_suspend)
    *   [13.7 Continuous hissing sound with headphones](#Continuous_hissing_sound_with_headphones)
*   [14 See Also](#See_Also)

## Content adaptive brightness control

In the XPS 13 the display panels (both FHD and QHD+) come with adaptive brightness embedded in the panel firmware, this "content adaptive brightness control" (usually referred to as CABC or DBC) will adjust the screen brightness depending on the content displayed on the screen and will generally be found undesirable, especially for Linux users who are likely to be switching between dark and light screen content. Dell has issued a fix for this however it is only available to run in Windows and for the QHD+ model of the laptop so this precaution should be taken before installing Linux, the FHD model of the XPS 13 (9360) cannot be fixed. This is not a problem with the panel but rather a problem with the way the panels are configured for the XPS 13, as the same panel exists in the Dell's Latitude 13 7000 series (e7370) FHD model but with CABC disabled. The fix is available directly from [Dell](http://www.dell.com/support/home/de/de/debsdt1/Drivers/DriversDetails?driverId=20JWV&fileId=3574543510&osCode=WT64A&productCode=xps-13-9360-laptop&languageCode=ge&categoryId=AP).

## NVM Express SSD

### NVME Power Saving Patch

Andy Lutomirski has created a patchset which fixes powersaving for NVME devices in linux. Currently, this patch is not merged into mainline yet. Until it lands in mainline kernel use the AUR or repository linked below. **Linux-nvme** — Mainline linux kernel patched with Andy's patch for NVME powersaving APST.

	[https://github.com/damige/linux-nvme](https://github.com/damige/linux-nvme) || [linux-nvme](https://aur.archlinux.org/packages/linux-nvme/) (check out [[1]](http://linuxnvme.damige.net/) for compiled packages)

This patch is now in mainline (4.11rc1), so it is a matter of time before the standard kernel can be used instead.

## Video

The video should work with the `i915` driver of the current [linux](https://www.archlinux.org/packages/?name=linux) kernel. Consult [Intel graphics](/index.php/Intel_graphics "Intel graphics") for a detailed installation and configuration guide as well as for [Troubleshooting](/index.php/Intel_graphics#Troubleshooting "Intel graphics").

### Module-based Powersaving Options

For the HD 620 graphics card the following modules are working: (see [Intel graphics#Module-based Powersaving Options](/index.php/Intel_graphics#Module-based_Powersaving_Options "Intel graphics"))

```
modeset=1 enable_rc6=1 enable_fbc=1 

```

The first argument is to enable modesetting if it's not set by default. The second argument is needed to active power-saving C-States. Higher values than 1 are not available for kaby lake CPUs. The third argument is for frame buffer compression power savings. These values should work well!

```
enable_guc_loading=1 enable_guc_submission=1

```

These arguments are used to enable GuC updates. GuC is a small proprietary binary blob released by intel to update the GuC binary in faster intervals than the kernel release does. It is used for graphics workload scheduling on the various graphics parallel engines. More details at ([https://01.org/linuxgraphics/downloads/firmware](https://01.org/linuxgraphics/downloads/firmware)). The GuC binary for kaby lake is included since firmware release linux-firmware 20170217 in the official repository.

```
enable_huc=1

```

HuC is also an binary blob from intel. It's designed to offload some of the media functions from the CPU to GPU. More details at ([https://01.org/linuxgraphics/downloads/firmware](https://01.org/linuxgraphics/downloads/firmware)). The vanilla kernel doesn't load it at the moment! Patches to load HuC have to find their way into the i915 kernel graphic stack before this option will work. Maybe working for kernel 4.10 or 4.11.

```
enable_psr=1 disable_power_well=0 OR enable_psr=2 

```

Enable psr level 2 is working, while level 1 has a lot of problems. Setting it on level 2 doesn't give much energy saving at the moment. It's said that 'disable_power_well=0 enable_psr=1' is working in this combination.

```
NOT WORKING: semaphores=1 

```

The semaphore option is NOT working for kaby lake CPUs and won't enable even if you set the option to 1.

### Blank screen issue after booting

If using "late start" [KMS](/index.php/KMS "KMS") (the default) and the screen goes blank when loading modules, it may help to add `i915` and `intel_agp` to the initramfs or using a special [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"). Consult [Intel graphics#Blank screen during boot, when "Loading modules"](/index.php/Intel_graphics#Blank_screen_during_boot.2C_when_.22Loading_modules.22 "Intel graphics") for more information about the kernel parameter way and have a look at [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting") for a guide on how to setup the modules for the initramfs.

## Wireless

The Killer 1535 Wirless Adapter is functional and the ath10k firmware is included in recent linux kernel versions. The connection speed reported by iw is limited to 1-6Mbits/s. However this is just the output being wrong. The real connection speed is not limited to this value.

Some users are experiencing issues, where the connection is dropped under heavy load but reconnects within a brief moment. This might not be noticed during browsing at all but becomes apparent in online games. There is no know solution so far.

## Bluetooth

After following the instructions given at [Bluetooth](/index.php/Bluetooth "Bluetooth") tethering of internet connections via phone works immediately.

## Thunderbolt 3 / USB 3.1

The USB-C port supports Thunderbolt 3, Displayport-over-USB-C and USB power delivery as well as USB 3.1.

### Ethernet repeatedly disconnects/reconnects with Dell USB-C adapter (DA200)

Use of a power management package (such as [TLP](/index.php/TLP "TLP")) may cause the ethernet adapter to repeatedly disconnect and reconnect. If this happens, disable/blacklist USB autosuspend for the ethernet adapter. (On my laptop, this is the device <tt>Bus 004 Device 007: ID 0bda:8153 Realtek Semiconductor Corp</tt> in the output of <tt>lsusb</tt>.)

Also disabling or reducing power of wifi may help: [http://en.community.dell.com/support-forums/network-internet-wireless/f/3324/t/19995423](http://en.community.dell.com/support-forums/network-internet-wireless/f/3324/t/19995423)

### USB-C Compatibility Chart

| **Device** | **Ports** | **Status** |
| [Apple USB-C Digital AV Multiport Adapter](http://www.apple.com/uk/shop/product/MJ1K2ZM/A/usb-c-digital-av-multiport-adapter) | USB-C, USB-A, HDMI | Not Working |
| [Apple 29W USB-C Power Adapter](http://www.apple.com/uk/shop/product/MJ262B/A/apple-29w-usb-c-power-adapter?fnode=8b) | USB-C Power | Not Working |
| [Aukey USB C Hub HDMI 4 Port](https://www.amazon.co.uk/gp/product/B01H3K387Q/ref=oh_aui_search_detailpage?ie=UTF8&psc=1) | USB-C, 4xUSB-A, HDMI | Working |
| [Dell DA200](https://www.amazon.com/dp/B012DT6KW2) | USB-A, Ethernet, HDMI, VGA | Not Working |
| [StarTech.com tb32dp2 - Thunderbolt 3 Adapter](https://www.amazon.com/dp/B01ANR4CYE) | 2 x DP (4 K, 60 Hz) | Working |
| [Cable Matters USB-C Multiport Adapter](https://www.amazon.com/dp/B01C316EIK) | 4K HDMI or VGA, USB 3.0, Gigabit Ethernet | Working |
| [Juiced Systems BizHUB USB-C Multiport Gigabit HDMI Hub](https://www.amazon.com/Juiced-BizHUB-Multiport-Ethernet-Delivery/dp/B01J391C3W) | 4K@30Hz HDMI, 3x USB 3.0, Gigabit Ethernet, USB-C Power, SD, Micro-SD | Working |

### Thunderbolt Firmware updates

The thunderbolt controller in the laptop has an embedded firmware. The laptop ships with firmware version NVM 18, and the most recent available version from Dell's website is NVM 21\. If encountering compatibility problems with Thunderbolt accessories, the firmware may need to be updated. Dell maintains a [Github repository](https://github.com/dell/thunderbolt-nvm-linux) explaining the process to update the firmware, but unfortunately, does not provide the updated payload files. These can be extracted from the Windows firmware update files. Mainline support for the firmware update process is pending the inclusion of [these patches](https://github.com/01org/thunderbolt-software-kernel-tree/tree/networking) into the Linux kernel. The thunderbolt-icm kernel module is available in the AUR [thunderbolt-icm-dkms-git](https://aur.archlinux.org/packages/thunderbolt-icm-dkms-git/).

## SATA controller

When the SATA-controller is set to `RAID On` in Bios, the hard disk (at least the SSD) is not recognized. Set to `Off` or `AHCI` (`AHCI` is recommended) before attempting to install Arch.

## Touchpad

The touchpad has no explicit buttons. The buttons are built into the pads surface. There is a small line printed on the pad separating left from right click button. The pad has a **middle button** built in! (works with libinput without any configuration): To issue a middle click, simply press on the middle area right between the virtual left and click buttons - so on the small printed separator line.

### Remove psmouse errors from dmesg

If `dmesg | grep -i psmouse` returns an error, but your touchpad still works, then it might be a good idea to disable `psmouse`. First create a config file:

```
   # nano /etc/modprobe.d/modprobe.conf

   blacklist psmouse

```

Then add this file to `/etc/mkinitcpio.conf`:

```
   ...
   FILES="/etc/modprobe.d/modprobe.conf"
   ...

```

Rebuild your initial ramdisk image (see [Mkinitcpio#Image creation and activation](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio")).

## Touchscreen

The touchscreen works without additional configuration. The bug resulting in a disabled touchscreen after resume was fixed with kernel 4.8.5.

### Gestures

Refer to [libinput#Gestures](/index.php/Libinput#Gestures "Libinput") for information about the current development state and available methods.

### Scrolling in Firefox

See [Firefox/Tweaks#Pixel-perfect trackpad scrolling](/index.php/Firefox/Tweaks#Pixel-perfect_trackpad_scrolling "Firefox/Tweaks"). This enables both touchscreen scrolling and high-res trackpad scrolling.

## Keyboard Backlight

By default, the keyboard backlight turns off after 10 seconds of inactivity. Some users might find this too short and annoying. The delay can be increased (or decreased) by editing this file:

```
  /sys/devices/platform/dell-laptop/leds/dell\:\:kbd_backlight/stop_timeout

```

You can also change the brightness (0-2) by editing the following file. This is identical to pressing F10 on your keyboard:

```
   /sys/devices/platform/dell-laptop/leds/dell\:\:kbd_backlight/brightness

```

## Hidden Keyboard Keys

There are additional Fn+<Key> (sequences) that are not marked at all on the keyboard but underlying hardware generates them anyway. Here they are (if you find more add them to the table below):

<caption>Hidden Fn Keys</caption>
| Fn+<Key> | Resulting key (sequence) |
| Fn+Ins | XF86Sleep |
| Fn+Super_L | Super_R |
| Fn+B | Pause |
| Fn+R | Print |
| Fn+S | Scroll_Lock |
| Fn+A / D / E / F / G / T / Q / W | XF86Launch3 |

## Firmware Updates

Dell provides firmware updates via [fwupd](https://aur.archlinux.org/packages/fwupd/). See [Flashing BIOS from Linux#fwupd](/index.php/Flashing_BIOS_from_Linux#fwupd "Flashing BIOS from Linux"). Please note if you have used a bind mount partition for /boot, you will not be able to use the fwupd utility; Instead format a USB as FAT32 and put the bios update .exe on. Reboot into the one-time-boot menu and update the BIOS flash through there.

Alternatively, the BIOS update can be downloaded from the Dell website, and placed in a location accessible to the firmware. This could be the '/boot' folder, or a FAT32 formatted USB stick. Then restart your laptop and hit F12 while starting. In the boot menu choose firmware update and select the new file!

## Troubleshooting

### EFISTUB does not boot

The BIOS does not pass any boot parameters to the kernel. Use a UEFI [boot loader](/index.php/Boot_loader "Boot loader") instead.

### Not waking from suspend

Update the BIOS to 1.0.7 to patch this issue.

### Power Drain after waking from standby

Some users recognised ~2W more power consumption after waking up from standby. Go to the UEFI Firmware Settings (tap the F2 key when the Dell logo appears) and uncheck the 'Enable Thunderbolt Boot Support'. You may use [powertop](https://www.archlinux.org/packages/?name=powertop) or [powerstat-git](https://aur.archlinux.org/packages/powerstat-git/) to reproduce and check this behaviour yourself.

### Popping Sound on headphones/external speakers

Power saving being enabled on the audio chip will cause the hissing and popping to appear.

Have a look at [Advanced Linux Sound Architecture/Troubleshooting#Pops when starting and stopping playback](/index.php/Advanced_Linux_Sound_Architecture/Troubleshooting#Pops_when_starting_and_stopping_playback "Advanced Linux Sound Architecture/Troubleshooting") and [Advanced Linux Sound Architecture/Troubleshooting#Popping sound after resuming from suspension](/index.php/Advanced_Linux_Sound_Architecture/Troubleshooting#Popping_sound_after_resuming_from_suspension "Advanced Linux Sound Architecture/Troubleshooting").

If you are using [tlp](https://www.archlinux.org/packages/?name=tlp), it will activate power saving by default when on battery. Edit `/etc/default/tlp` and disable it.

### Coil Whine

Unfortunately Dell still did not fix this issue and the sound for my model was very loud. The issue seems to be connected to the graphic card. For some users, it is possible to reduce it a lot by activating frame buffer compression "enable_fbc=1" [Intel graphics#Module-based Powersaving Options](/index.php/Intel_graphics#Module-based_Powersaving_Options "Intel graphics"). The coil whine will then start again under heavy graphic load. For the touchscreen model, this may be very often, due to the high resolution screen. In a similar vein, the display can be run at a lower resolution, again reducing the load on the graphics card.

### Freezing after waking from suspend

Installing [xf86-video-intel-git](https://aur.archlinux.org/packages/xf86-video-intel-git/) is [reported](https://bbs.archlinux.org/viewtopic.php?pid=1698282#p1698282) to fix this.

### Continuous hissing sound with headphones

Open alsamixer and set "Headphone Mic Boost" gain to 10 dB: [https://www.reddit.com/r/Dell/comments/4j1zz4/headphones_have_static_noise_with_ubuntu_1604_on/](https://www.reddit.com/r/Dell/comments/4j1zz4/headphones_have_static_noise_with_ubuntu_1604_on/) Note that this does reduce the volume slightly.

## See Also

*   [Arch Forum thread for Dell XPS 13 (9360)](https://bbs.archlinux.org/viewtopic.php?id=217865)
*   [Service Manual for Dell XPS 13 (9360)](http://topics-cdn.dell.com/pdf/xps-13-9360-laptop_Service%20Manual_en-us.pdf)