# Dell XPS 13 (2016)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** This page is a work in progress; you're warmly invited to contribute! (Discuss in [Talk:Dell XPS 13 (2016)#](https://wiki.archlinux.org/index.php/Talk:Dell_XPS_13_(2016)))

<table class="wikitable" style="float: right;">

<tbody>

<tr>

<td>**Device**</td>

<td>**Status**</td>

<td>**Modules**</td>

</tr>

<tr>

<td>Video</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Works after configuration</td>

<td>i915</td>

</tr>

<tr>

<td>Wireless</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Works after configuration</td>

<td>brcmfmac</td>

</tr>

<tr>

<td>Bluetooth</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Works after installing firmware</td>

<td>btbcm</td>

</tr>

<tr>

<td>Audio</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>snd_hda_intel</td>

</tr>

<tr>

<td>Touchpad</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Works after configuration</td>

<td> ?</td>

</tr>

<tr>

<td>Webcam</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>uvcvideo</td>

</tr>

<tr>

<td>Card Reader</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>rtsx_pci</td>

</tr>

<tr>

<td>Wireless switch</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">Not supported yet</td>

<td> ?</td>

</tr>

<tr>

<td>Function/Multimedia Keys</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td> ?</td>

</tr>

</tbody>

</table>

The Dell XPS 13 2016 (9350) is the third-generation model of the XPS 13 line. Unlike its predecessor, it has no official Linux support yet. Just like the older versions ([Dell XPS 13](/index.php/Dell_XPS_13 "Dell XPS 13") and [Dell XPS 13 (2015)](/index.php/Dell_XPS_13_(2015) "Dell XPS 13 (2015)")) it can be bought in different hardware configurations.

The installation process for Arch on the XPS 13 does not differ from any other PC. For installation help, please see the [Installation guide](/index.php/Installation_guide "Installation guide"), [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") and [UEFI](/index.php/UEFI "UEFI"). This page covers the current status of hardware support on Arch, as well as post-installation recommendations.

As of kernel 4.3, the Intel Skylake architecture is supported.

## Contents

*   [1 BIOS updates](#BIOS_updates)
*   [2 SATA controller](#SATA_controller)
*   [3 NVM Express SSD](#NVM_Express_SSD)
*   [4 Wireless](#Wireless)
*   [5 Bluetooth](#Bluetooth)
*   [6 Video](#Video)
*   [7 Touchpad](#Touchpad)
*   [8 Sound](#Sound)
*   [9 Microphone](#Microphone)
*   [10 Kernel specific notes](#Kernel_specific_notes)
*   [11 Links](#Links)

## BIOS updates

[BIOS update 1.1.9](http://www.dell.com/support/home/us/en/04/Drivers/DriversDetails?driverId=376N9) was released on 2016-01-13\. Store the update binary on your EFI partition (`/boot/efi`) or on a USB flash drive, reboot, and choose BIOS Update in the F12 boot menu.

## SATA controller

When the SATA-controller is set to "RAID On" in Bios, the hard disk (at least the SSD) is not recognized. Set to "Off" or "AHCI" before attempting to install Arch. If dual boot to Windows is intended, follow [[1]](https://support.microsoft.com/en-us/kb/2795397) to work around the "INACCESSIBLE_BOOT_DEVICE" error.

## NVM Express SSD

The ["NVM Express"](https://en.wikipedia.org/wiki/NVM_Express) SSD requires adding "nvme" in modules to detect the PCIe SSD.

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

where `linux` is the name of the image loaded on boot. If you installed [linux-mainline](https://aur.archlinux.org/packages/linux-mainline/)<sup><small>AUR</small></sup> then change that to `linux-mainline`.

## Wireless

The built-in Broadcom BCM4350 is now supported in the current [linux](https://www.archlinux.org/packages/?name=linux) kernel in the testing repository (version 4.4.0-3). The wireless module `brcmfmac` also needs the firmware `brcmfmac4350-pcie.bin` from the related [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) package.

If you have not already done so, enable the testing repository to retrieve the package in `/etc/pacman.conf`:

```
 # The testing repositories are disabled by default. To enable, uncomment the
 # repo name header and Include lines. You can add preferred servers immediately
 # after the header, and they will be used before the default mirrors.

 [testing]
 Include = /etc/pacman.d/mirrorlist

 [core]
 Include = /etc/pacman.d/mirrorlist

```

## Bluetooth

**Note:** **Intel WiFi users:** If your WiFi card supports Bluetooth, then the BT interface should be available out-of-the-box, as the required firmware is included in [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware).

The Broadcom Bluetooth firmware is not available in the kernel (the same as for 2015 model [source](http://tech.sybreon.com/2015/03/15/xps13-9343-ubuntu-linux/)), so you will have to retrieve it from the [[2]](http://downloads.dell.com/FOLDER03272920M/1/9350_Network_Driver_XMJK7_WN32_12.0.1.720_A00.EXE). You need to extract the `.exe` file with [p7zip](https://www.archlinux.org/packages/?name=p7zip) and then convert it to a `.hcd` file with _hex2hcd_ from [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils):

```
$ 7z x 9350_Network_Driver_XMJK7_WN32_12.0.1.720_A00.EXE
$ cp Win32/BCM4350C5_003.006.007.0095.1703.hex ./
$ hex2hcd BCM4350C5_003.006.007.0095.1703.hex
# mv BCM4350C5_003.006.007.0095.1703.hcd /lib/firmware/brcm/BCM-0a5c-6412.hcd

```

After reboot, the firmware should be available for your Bluetooth interface.

## Video

**Note:** some hardware only needs `i915`

Works with kernel parameter `i915.preliminary_hw_support=1` [Intel graphics#Driver not working for Intel Skylake chips](/index.php/Intel_graphics#Driver_not_working_for_Intel_Skylake_chips "Intel graphics"). For kernels 4.3+ ([linux-bcm4350](https://aur.archlinux.org/packages/linux-bcm4350/)<sup><small>AUR</small></sup>) the parameter is unnecessary, but you may face blank screen problem after booting - adding `i915` and `intel_agp` to the kernel modules fixes the problem, see [Intel graphics#Blank screen during boot, when "Loading modules"](/index.php/Intel_graphics#Blank_screen_during_boot.2C_when_.22Loading_modules.22 "Intel graphics")

```
   # nano /etc/mkinitcpio.conf
   ...
   MODULES="... intel_agp i915"
   ...

```

Then update the bootloader.

```
   # mkinitcpio -p linux

```

where `linux` is the name of the image loaded on boot. If you installed [linux-mainline](https://aur.archlinux.org/packages/linux-mainline/)<sup><small>AUR</small></sup> then change that to `linux-mainline`.

## Touchpad

Only key-presses work out of the box. Installing `xf86-input-synaptics` and restarting X fixes the problem (see [Dell Studio XPS 13](/index.php/Dell_Studio_XPS_13 "Dell Studio XPS 13")). `xf86-input-libinput` may be a good alternative that also handles touchscreen - see [libinput](/index.php/Libinput "Libinput") for configuration.

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

Then update the bootloader.

```
   # mkinitcpio -p linux

```

where `linux` is the name of the image loaded on boot. If you installed [linux-mainline](https://aur.archlinux.org/packages/linux-mainline/)<sup><small>AUR</small></sup> then change that to `linux-mainline`.

## Sound

Some people reported white hissing/crackling noises when using headphones. To get rid of them you can run `alsamixer` from [alsa-tools](https://www.archlinux.org/packages/?name=alsa-tools). Select your soundcard with F6 and set the headset-gain to 22 (3rd lever from the left) or use the `amixer` command:

```
 $ amixer -c 0 cset 'numid=10' 1
 numid=10,iface=MIXER,name='Headphone Mic Boost Volume'
   ; type=INTEGER,access=rw---R--,values=2,min=0,max=3,step=0
   : values=1,1
   | dBscale-min=0.00dB,step=10.00dB,mute=0

```

Also people noticed loud popping-noises when sound was not playing. You can turn off the sound_power_save in `tlp`

```
   # nano /etc/default/tlp
   ...
   SOUND_POWER_SAVE_ON_BAT = 0 
   ...

```

## Microphone

**Note:** Not all hardware has the "Digital" channel

For ALSA, increase "Digital" channel for microphone to work.

## Kernel specific notes

The [linux](https://www.archlinux.org/packages/?name=linux) kernel in the core repository (4.3) does not support wifi. It is recommended to install the patch kernel from [linux-bcm4350](https://aur.archlinux.org/packages/linux-bcm4350/)<sup><small>AUR</small></sup> or use the kernel from the testing repository.

The linux kernel in testing repository (4.4) supports wifi out-of-the-box, see [#Wireless](#Wireless).

## Links

General Discussion Thread on Arch Forum [[3]](https://bbs.archlinux.org/viewtopic.php?pid=1579113)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dell_XPS_13_(2016)&oldid=416295](https://wiki.archlinux.org/index.php?title=Dell_XPS_13_(2016)&oldid=416295)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Dell](/index.php/Category:Dell "Category:Dell")

Hidden category:

*   [Pages flagged with Template:Stub](/index.php/Category:Pages_flagged_with_Template:Stub "Category:Pages flagged with Template:Stub")