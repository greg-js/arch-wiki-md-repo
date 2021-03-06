**Note:** This page refers to the early 2016 model of XPS 13\. For the late 2016 model see [Dell XPS 13 (4th Gen)](/index.php/Dell_XPS_13_(4th_Gen) "Dell XPS 13 (4th Gen)").

| **Device** | **Status** | **Modules** |
| Video | Works after configuration | i915 |
| Wireless | Works after configuration | brcmfmac |
| Bluetooth | Works after installing firmware | btbcm |
| Audio | Working | snd_hda_intel |
| Touchpad | Works after configuration |  ? |
| Webcam | Working | uvcvideo |
| Card Reader | Working | rtsx_pci |
| Wireless switch | Working | intel_hid |
| Function/Multimedia Keys | Working |  ? |

The Dell XPS 13 2016 (9350) is the third-generation model of the XPS 13 line. The laptop is available in both a standard edition with Windows installed as well as a Developer Edition which only differs in that it comes with Ubuntu installed as well as the Broadcom WiFi card replaced with an Intel WiFi card. Just like the older versions ([Dell XPS 13](/index.php/Dell_XPS_13 "Dell XPS 13") and [Dell XPS 13 (2015)](/index.php/Dell_XPS_13_(2015) "Dell XPS 13 (2015)")) it can be bought in different hardware configurations.

The installation process for Arch on the XPS 13 does not differ from any other PC. For installation help, please see the [Installation guide](/index.php/Installation_guide "Installation guide") and [UEFI](/index.php/UEFI "UEFI"). This page covers the current status of hardware support on Arch, as well as post-installation recommendations.

As of kernel 4.3, the Intel Skylake architecture is supported.

## Contents

*   [1 Content adaptive brightness control](#Content_adaptive_brightness_control)
*   [2 BIOS](#BIOS)
    *   [2.1 USB not found](#USB_not_found)
    *   [2.2 No UEFI system found](#No_UEFI_system_found)
    *   [2.3 Updates](#Updates)
*   [3 Thunderbolt 3 / USB 3.1](#Thunderbolt_3_.2F_USB_3.1)
*   [4 SATA controller](#SATA_controller)
    *   [4.1 Dual booting Linux and Windows](#Dual_booting_Linux_and_Windows)
*   [5 NVM Express SSD](#NVM_Express_SSD)
    *   [5.1 Cannot find root device](#Cannot_find_root_device)
    *   [5.2 Note on Mount Options](#Note_on_Mount_Options)
    *   [5.3 NVME Power Saving Patch](#NVME_Power_Saving_Patch)
*   [6 Wireless](#Wireless)
*   [7 Bluetooth](#Bluetooth)
    *   [7.1 Intel WiFi](#Intel_WiFi)
    *   [7.2 Broadcom Wifi](#Broadcom_Wifi)
        *   [7.2.1 Wireless headset: strange bluetooth behavior](#Wireless_headset:_strange_bluetooth_behavior)
*   [8 Video](#Video)
    *   [8.1 Blank screen issue after booting](#Blank_screen_issue_after_booting)
    *   [8.2 Linux kernel 4.3 or earlier](#Linux_kernel_4.3_or_earlier)
    *   [8.3 Linux kernel 4.5 or earlier](#Linux_kernel_4.5_or_earlier)
*   [9 Touchpad](#Touchpad)
    *   [9.1 Remove psmouse errors from dmesg](#Remove_psmouse_errors_from_dmesg)
    *   [9.2 Gestures](#Gestures)
*   [10 Sound](#Sound)
    *   [10.1 Hissing/Crackling noises when using headphones](#Hissing.2FCrackling_noises_when_using_headphones)
    *   [10.2 Loud popping-noises when sound was not playing](#Loud_popping-noises_when_sound_was_not_playing)
*   [11 Microphone](#Microphone)
*   [12 CPU slowdown after resume from suspend](#CPU_slowdown_after_resume_from_suspend)
*   [13 Diverting models](#Diverting_models)
    *   [13.1 XPS 12](#XPS_12)
    *   [13.2 Dell XPS 15](#Dell_XPS_15)
    *   [13.3 Dell XPS 13 (2015)](#Dell_XPS_13_.282015.29)
    *   [13.4 Dell XPS 13 9360 (4th Gen - late 2016)](#Dell_XPS_13_9360_.284th_Gen_-_late_2016.29)
*   [14 lspci and lsusb](#lspci_and_lsusb)
    *   [14.1 lspci](#lspci)
    *   [14.2 lsusb](#lsusb)
*   [15 See also](#See_also)

## Content adaptive brightness control

In the XPS 13 the display panels (both FHD and QHD+) come with adaptive brightness embedded in the panel firmware, this "content adaptive brightness control" (usually referred to as CABC or DBC) will adjust the screen brightness depending on the content displayed on the screen and will generally be found undesirable, especially for Linux users who are likely to be switching between dark and light screen content. Dell has issued a fix for this however it is only available to run in Windows and for the QHD+ model of the laptop so this precaution should be taken before installing Linux, the FHD model of the XPS 13 (9350) cannot be fixed. This is not a problem with the panel but rather a problem with the way the panels are configured for the XPS 13, as the same panel exists in the Dell's Latitude 13 7000 series (e7370) FHD model but with CABC disabled. The fix is available directly from [Dell](http://www.dell.com/support/home/uk/en/ukdhs1/Drivers/DriversDetails?driverId=PWD5K&fileId=3505631210&osCode=W764&productCode=xps-13-9350-laptop&languageCode=en&categoryId=AP).

## BIOS

### USB not found

It may happen that the Arch Linux USB won't be recognized. You have to disable secure boot (Secure Boot > Disable) and then enable the legacy (General > Advanced Boot Options > Enable Legacy Option ROMs).

### No UEFI system found

Sometimes the BIOS UEFI does not respect the efivars. In this case you have manually add your efi file in BIOS boot options by going to General > Boot Sequence > Add Boot Option.

### Updates

[BIOS update 1.4.4](http://downloads.dell.com/FOLDER03769593M/1/XPS_9350_1.4.4.exe) was released on 2016-06-30\. Store the update binary on your EFI partition (`/boot/EFI`) or on a USB flash drive, reboot, and choose BIOS Update in the F12 boot menu. This might also help if your machine will not resume after suspend.

## Thunderbolt 3 / USB 3.1

The USB-C port supports Thunderbolt 3, Displayport-over-USB-C and USB power delivery as well as USB 3.1.

In the event of devices not working correctly, ensure that you have updated to the latest BIOS (above) and Thunderbolt firmware (below).

[Thunderbolt 3 Firmware Update 2.16.01.003, A04](http://downloads.dell.com/FOLDER03798029M/1/Intel_TBT3_FW_UPDATE_NVM16_A04_2.16.01.003.exe) was released on 2016-08-10\. Unlike the BIOS update, this is a graphical application which must be run in a modern Windows environment (MS-DOS will not suffice).

Hotplug support for this port requires a [bug fix](https://bugzilla.kernel.org/show_bug.cgi?id=115121) which landed in kernel version 4.7\. It also requires the kernel to be built with <tt>CONFIG_PCI_HOTPLUG=y</tt>.

## SATA controller

When the SATA-controller is set to `RAID On` in Bios, the hard disk (at least the SSD) is not recognized. Set to `Off` or `AHCI` (`AHCI` is recommended) before attempting to install Arch.

### Dual booting Linux and Windows

In order to boot into Windows properly without getting an `INACCESSIBLE_BOOT_DEVICE` error with disabled `RAID` you must configure Windows to use the `AHCI`-speaking SATA storage controller, assuming you used `AHCI` for installing Linux. The driver is effectively disabled even though it is installed. Either of the following methods were reported to activate the drivers without reinstallation (your mileage may vary):

*   [booting into safe mode and back](http://www.tenforums.com/drivers-hardware/15006-attn-ssd-owners-enabling-ahci-mode-after-windows-10-installation.html)
*   [Selecting `Microsoft Storage Spaces Controller` in Windows Device Manager](https://samnicholls.net/2016/01/14/how-to-switch-sata-raid-to-ahci-windows-10-xps-13/)
*   [Modifying registry entries](http://www.tenforums.com/tutorials/22631-ahci-enable-windows-8-windows-10-after-installation.html)
*   [Modifying other registry entries](http://superuser.com/questions/471102/change-from-ide-to-ahci-after-installing-windows-8/471108#471108)

Consult the [microsoft support](https://support.microsoft.com/en-us/kb/2795397) page for additional information. Be aware that some manufactures propagate reinstalling Windows to be the only solution, which it is not.

## NVM Express SSD

### Cannot find root device

The location of the `nvme` module for ["NVM Express"](https://en.wikipedia.org/wiki/NVM_Express "wikipedia:NVM Express") SSD has changed between [linux](https://www.archlinux.org/packages/?name=linux) kernel version 4.3 and 4.4\. If you experience "cannot find root device" on boot, it may be due to the [`nvme` module not being present in `initramfs`](https://bugs.archlinux.org/task/47761). In this case, the following may resolve your issue.

Edit your `/etc/mkinitcpio.conf` file:

```
   ...
   MODULES="... nvme"
   ...

```

Then update the bootloader.

```
   # mkinitcpio -p linux

```

where `linux` is the name of the image loaded on boot. If you installed [linux-mainline](https://aur.archlinux.org/packages/linux-mainline/) then change that to `linux-mainline`.

### Note on Mount Options

Using the `discard` mount option for your filesystem is not recommended, as mentioned in [this warning](/index.php/Solid_State_Drives#Continuous_TRIM "Solid State Drives") and [the forum](https://bbs.archlinux.org/viewtopic.php?pid=1593544#p1593544). See also [Solid State Drives/NVMe#Discards](/index.php/Solid_State_Drives/NVMe#Discards "Solid State Drives/NVMe") for further information.

### NVME Power Saving Patch

Andy Lutomirski has released version 4 of his patchset which fixes powersaving for NVME devices in linux. Currently, this patch is not merged into mainline yet. Until it lands in mainline kernel use the AUR package below. **Linux-nvme** — Mainline linux kernel patched with Andy's patch for NVME powersaving APST.

	[https://github.com/damige/linux-nvme](https://github.com/damige/linux-nvme) || [linux-nvme](https://aur.archlinux.org/packages/linux-nvme/)

## Wireless

For the non-developer edition, the built-in Broadcom BCM4350 is now supported in the current [linux](https://www.archlinux.org/packages/?name=linux) kernel (as of version 4.4.1-1). The wireless module `brcmfmac` also needs the firmware `brcmfmac4350-pcie.bin` from the related [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) package.

The Broadcom adapter does not report its regulatory country and so, by default, the global settings for channels and frequencies will be set. See [Wireless network configuration#Respecting the regulatory domain](/index.php/Wireless_network_configuration#Respecting_the_regulatory_domain "Wireless network configuration") for more information about how this can be changed.

## Bluetooth

### Intel WiFi

If your WiFi card supports Bluetooth, then the BT interface should be available out-of-the-box, as the required firmware is included in [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware).

### Broadcom Wifi

Bluetooth should work right away. Load the module `btusb` and `bluetooth` if it was not already and [start](/index.php/Start "Start")/[enable](/index.php/Enable "Enable") `bluetooth.service`. Refer to [Bluetooth](/index.php/Bluetooth "Bluetooth") for more information and configuration options.

#### Wireless headset: strange bluetooth behavior

If your Bluetooth behaves unstable, such as connection loss, stuttering sound. being able to connect but not to listen through it, etc. you probably need the proprietary firmware.

The Broadcom Bluetooth firmware is not available in the kernel (the same as for the 2015 model [source](http://tech.sybreon.com/2015/03/15/xps13-9343-ubuntu-linux/)), therefore you will have to retrieve it from a Windows [.exe](http://downloads.dell.com/FOLDER03272920M/1/9350_Network_Driver_XMJK7_WN32_12.0.1.720_A00.EXE). You need to extract the `.exe` file with [p7zip](https://www.archlinux.org/packages/?name=p7zip) and then convert it to a `.hcd` file with *hex2hcd* from [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils):

```
$ 7z x 9350_Network_Driver_XMJK7_WN32_12.0.1.720_A00.EXE
$ cp Win32/BCM4350C5_003.006.007.0095.1703.hex ./
$ hex2hcd BCM4350C5_003.006.007.0095.1703.hex
# mv BCM4350C5_003.006.007.0095.1703.hcd /lib/firmware/brcm/BCM-0a5c-6412.hcd

```

After reboot, the firmware should be available for your Bluetooth interface.

## Video

The video should work with the `i915` driver of the current [linux](https://www.archlinux.org/packages/?name=linux) kernel. Consult [Intel graphics](/index.php/Intel_graphics "Intel graphics") for a detailed installation and configuration guide as well as for [Troubleshooting](/index.php/Intel_graphics#Troubleshooting "Intel graphics").

### Blank screen issue after booting

If using "late start" [KMS](/index.php/KMS "KMS") (the default) and the screen goes blank when loading modules, it may help to add `i915` and `intel_agp` to the initramfs or using a special [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"). Consult [Intel graphics#Blank screen during boot, when "Loading modules"](/index.php/Intel_graphics#Blank_screen_during_boot.2C_when_.22Loading_modules.22 "Intel graphics") for more information about the kernel paramter way and have a look at [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting") for a guide on how to setup the modules for the initramfs.

### Linux kernel 4.3 or earlier

If you are using an older kernel 4.3 or earlier, you also require the kernel parameter `i915.preliminary_hw_support=1`, see [Intel graphics#Skylake support](/index.php/Intel_graphics#Skylake_support "Intel graphics"). (For later kernels 4.3+ or [linux-bcm4350](https://aur.archlinux.org/packages/linux-bcm4350/) the parameter is unnecessary.)

### Linux kernel 4.5 or earlier

If you have the newer i7-6560 CPU with Iris 540 graphics, the GPU hangs every few minutes with kernel versions before 4.6\. This is probably due to this bug [https://bugs.freedesktop.org/show_bug.cgi?id=94161](https://bugs.freedesktop.org/show_bug.cgi?id=94161) and can be countered by either disabling DRI in your Xorg configuration:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
	Identifier  "Intel Graphics"
	Driver      "intel"
	Option	    "DRI"	"false"
EndSection

```

or by adding `i915.enable_rc6=0` to the kernel boot parameters.

## Touchpad

Only key-presses work out of the box. Installing [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) is sufficient for proper mouse support plus it also handles the touchscreen - see [libinput](/index.php/Libinput "Libinput") for configuration. Features such as tap-to-click are usually adjustable within the [desktop environment](/index.php/Desktop_environment "Desktop environment").

Alternatively you may want to install [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) as driver but "it is on maintenance mode and [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) must be preferred over" (installation note from the package itself). Plus it may lack the ability to be easily adjustable within your [desktop environment](/index.php/Desktop_environment "Desktop environment") (see [Dell Studio XPS 13](/index.php/Dell_Studio_XPS_13 "Dell Studio XPS 13")). Restarting the X server might be required.

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

### Gestures

Refer to [libinput#Gestures](/index.php/Libinput#Gestures "Libinput") for information about the current development state and available methods.

## Sound

### Hissing/Crackling noises when using headphones

Some people reported white hissing/crackling noises when using headphones. To get rid of them you can run `alsamixer` from [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils). Select your soundcard with F6 and set the headset-gain to 22 (3rd lever from the left) or use the `amixer` command:

```
 $ amixer -c 0 cset 'numid=10' 1
 numid=10,iface=MIXER,name='Headphone Mic Boost Volume'
   ; type=INTEGER,access=rw---R--,values=2,min=0,max=3,step=0
   : values=1,1
   | dBscale-min=0.00dB,step=10.00dB,mute=0

```

Unfortunately [PulseAudio](/index.php/PulseAudio "PulseAudio") will override the above setting every time you log in/out of your environment (or every time the PulseAudio service is restarted), even if the `alsa-restore.service` is enabled at [start](/index.php/Start "Start") up.

To work around this issue, edit `/usr/share/pulseaudio/alsa-mixer/paths/analog-input-headphone-mic.conf` and comment out the section `[Element Headphone Mic Boost]`:

```
 ---
 #[Element Headphone Mic Boost]
 #required-any = any
 #switch = select
 #volume = merge
 #override-map.1 = all
 #override-map.2 = all-left,all-right
 ---

```

Similarly in `/usr/share/pulseaudio/alsa-mixer/paths/analog-input-internal-mic.conf`, comment out the same section:

```
 ---
 #[Element Headphone Mic Boost]
 #switch = off
 #volume = off
 ---

```

This will prevent PulseAudio to fiddle with the gain setting at all.

**Note:** Unfortunately, you must make the same modifications every time the PulseAudio package is updated. Additionally, this will entirely disable the internal microphone.

### Loud popping-noises when sound was not playing

Also people noticed loud popping-noises when sound was not playing. You can turn off the sound_power_save in through e.g. `tlp`

```
   # nano /etc/default/tlp
   ...
   SOUND_POWER_SAVE_ON_BAT = 0 
   ...

```

## Microphone

**Note:** Not all hardware has the "Digital" channel

For ALSA, increase "Digital" channel for microphone to work.

## CPU slowdown after resume from suspend

If you are experiencing a very slow computer after resume from suspend, you may be subject to a bug where your CPU frequency is capped to a very low value. Use `cpupower frequency-info` to check. If so, please read [this forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1558948#p1558948) for debug information, and a workaround.

## Diverting models

### XPS 12

### Dell XPS 15

Despite the similarities between the two devices they have quite different solutions for various problems, refer to [Dell XPS 15](/index.php/Dell_XPS_15 "Dell XPS 15") for more information.

### Dell XPS 13 (2015)

Information about the predecessor is available at [Dell XPS 13 (2015)](/index.php/Dell_XPS_13_(2015) "Dell XPS 13 (2015)").

### Dell XPS 13 9360 (4th Gen - late 2016)

Information about the successor is available at [Dell XPS 13 (4th Gen)](/index.php/Dell_XPS_13_(4th_Gen) "Dell XPS 13 (4th Gen)").

## lspci and lsusb

The <tt>lspci</tt> and <tt>lsusb</tt> below were take from the following system:

```
[    0.000000] DMI: Dell Inc. XPS 13 9350/0PWNCR, BIOS 1.3.3 03/01/2016

```

on kernel:

```
Linux marv 4.5.4-1-ARCH #1 SMP PREEMPT Wed May 11 22:21:28 CEST 2016 x86_64 GNU/Linux

```

### lspci

```
00:00.0 Host bridge: Intel Corporation Skylake Host Bridge/DRAM Registers (rev 08)
00:02.0 VGA compatible controller: Intel Corporation Skylake Integrated Graphics (rev 07)
00:04.0 Signal processing controller: Intel Corporation Skylake Processor Thermal Subsystem (rev 08)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:15.0 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #0 (rev 21)
00:15.1 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #1 (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:1c.0 PCI bridge: Intel Corporation Device 9d10 (rev f1)
00:1c.4 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #5 (rev f1)
00:1c.5 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #6 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Device 9d18 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point-LP LPC Controller (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
3a:00.0 Network controller: Broadcom Corporation BCM4350 802.11ac Wireless Network Adapter (rev 08)
3b:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS525A PCI Express Card Reader (rev 01)
3c:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller (rev 01)

```

[Full output from sudo lspci -v](https://gist.github.com/mgalgs/a903e3528f48aa25b5c0b9ae9c09a07f)

After plugging in a USB-C hub, a number of new PCI devices appear:

```
01:00.0 PCI bridge: Intel Corporation Device 1576
02:00.0 PCI bridge: Intel Corporation Device 1576
02:01.0 PCI bridge: Intel Corporation Device 1576
02:02.0 PCI bridge: Intel Corporation Device 1576
39:00.0 USB controller: Intel Corporation Device 15b5

```

### lsusb

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 004: ID 0c45:670c Microdia 
Bus 001 Device 003: ID 04f3:20d0 Elan Microelectronics Corp. 
Bus 001 Device 002: ID 0a5c:6412 Broadcom Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

[Full output from sudo lsusb -v](https://gist.github.com/mgalgs/15fb0d19795f700d60f061f67dddbefc)

## See also

*   [Arch Forum thread for XPS 13](https://bbs.archlinux.org/viewtopic.php?pid=1579113)
*   [Dell XPS 13 9350 driver and firmware updates](http://www.dell.com/support/home/us/en/19/product-support/product/xps-13-9350-laptop/drivers)