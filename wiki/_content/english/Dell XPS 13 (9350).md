**Note:** This page refers to the early 2016 model of XPS 13\. For the late 2016 model see [Dell XPS 13 (9360)](/index.php/Dell_XPS_13_(9360) "Dell XPS 13 (9360)").

| **Device** | **Status** | **Modules** |
| Video | Working | i915 |
| Wireless | Working | brcmfmac |
| Bluetooth | Works after installing firmware | btbcm |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | ? |
| Webcam | Working | uvcvideo |
| Card Reader | Working | rtsx_pci |
| Wireless switch | Working | intel_hid |
| Function/Multimedia Keys | Working | ? |
| TPM 1.2/2.0 | Working | tpm |

Related articles

*   [Dell XPS 13 (9333)](/index.php/Dell_XPS_13_(9333) "Dell XPS 13 (9333)")
*   [Dell XPS 13 (9343)](/index.php/Dell_XPS_13_(9343) "Dell XPS 13 (9343)")
*   [Dell XPS 13 (9360)](/index.php/Dell_XPS_13_(9360) "Dell XPS 13 (9360)")
*   [Dell XPS 13 (9370)](/index.php/Dell_XPS_13_(9370) "Dell XPS 13 (9370)")
*   [Dell XPS 13 2-in-1 (9365)](/index.php/Dell_XPS_13_2-in-1_(9365) "Dell XPS 13 2-in-1 (9365)")

The Dell XPS 13 2016 (9350) is the third-generation model of the XPS 13 line. The laptop is available in both a standard edition with Windows installed as well as a Developer Edition which only differs in that it comes with Ubuntu installed as well as the Broadcom WiFi card replaced with an Intel WiFi card. Just like the older versions ([Dell XPS 13 (9333)](/index.php/Dell_XPS_13_(9333) "Dell XPS 13 (9333)") and [Dell XPS 13 (9343)](/index.php/Dell_XPS_13_(9343) "Dell XPS 13 (9343)")) it can be bought in different hardware configurations.

The installation process for Arch on the XPS 13 does not differ from any other PC. For installation help, please see the [Installation guide](/index.php/Installation_guide "Installation guide") and [UEFI](/index.php/UEFI "UEFI"). This page covers the current status of hardware support on Arch, as well as post-installation recommendations.

As of kernel 4.3, the Intel Skylake architecture is supported.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Content adaptive brightness control](#Content_adaptive_brightness_control)
*   [2 BIOS](#BIOS)
    *   [2.1 Updates](#Updates)
    *   [2.2 Firmware Updates](#Firmware_Updates)
*   [3 Thunderbolt 3 / USB 3.1](#Thunderbolt_3_/_USB_3.1)
    *   [3.1 Doing Thunderbolt firmware updates without fwupd or Windows](#Doing_Thunderbolt_firmware_updates_without_fwupd_or_Windows)
    *   [3.2 External screen](#External_screen)
*   [4 SATA controller](#SATA_controller)
    *   [4.1 Dual booting Linux and Windows](#Dual_booting_Linux_and_Windows)
*   [5 NVM Express SSD](#NVM_Express_SSD)
    *   [5.1 Cannot find root device](#Cannot_find_root_device)
    *   [5.2 Note on Mount Options](#Note_on_Mount_Options)
*   [6 Wireless](#Wireless)
*   [7 Bluetooth](#Bluetooth)
    *   [7.1 Intel WiFi](#Intel_WiFi)
    *   [7.2 Broadcom Wifi](#Broadcom_Wifi)
        *   [7.2.1 Wireless headset: strange bluetooth behavior](#Wireless_headset:_strange_bluetooth_behavior)
*   [8 Video](#Video)
    *   [8.1 Blank screen issue after booting](#Blank_screen_issue_after_booting)
    *   [8.2 Linux kernel 4.8 or later power savings](#Linux_kernel_4.8_or_later_power_savings)
        *   [8.2.1 RC6](#RC6)
        *   [8.2.2 Panel Self Refresh](#Panel_Self_Refresh)
        *   [8.2.3 Frame Buffer Compression](#Frame_Buffer_Compression)
        *   [8.2.4 GuC](#GuC)
    *   [8.3 Linux kernel 4.5 or earlier](#Linux_kernel_4.5_or_earlier)
*   [9 Power management](#Power_management)
    *   [9.1 Fans](#Fans)
    *   [9.2 Undervolting](#Undervolting)
*   [10 Touchpad](#Touchpad)
    *   [10.1 Remove psmouse errors from dmesg](#Remove_psmouse_errors_from_dmesg)
    *   [10.2 Gestures](#Gestures)
*   [11 Keyboard](#Keyboard)
*   [12 Sound](#Sound)
    *   [12.1 Coil whine when using headphones](#Coil_whine_when_using_headphones)
    *   [12.2 High noise floor when using headphones](#High_noise_floor_when_using_headphones)
*   [13 Microphone](#Microphone)
    *   [13.1 No audio input through combo jack](#No_audio_input_through_combo_jack)
*   [14 TPM](#TPM)
    *   [14.1 TPM 2.0](#TPM_2.0)
*   [15 CPU slowdown after resume from suspend](#CPU_slowdown_after_resume_from_suspend)
*   [16 lspci and lsusb](#lspci_and_lsusb)
    *   [16.1 lspci](#lspci)
    *   [16.2 lsusb](#lsusb)
*   [17 See also](#See_also)

## Content adaptive brightness control

In the XPS 13 the display panels (both FHD and QHD+) come with adaptive brightness embedded in the panel firmware, this "content adaptive brightness control" (usually referred to as CABC or DBC) will adjust the screen brightness depending on the content displayed on the screen and will generally be found undesirable, especially for Linux users who are likely to be switching between dark and light screen content. Dell has issued a fix for this however it is only available to run in Windows and for the QHD+ model of the laptop so this precaution should be taken before installing Linux, the FHD model of the XPS 13 (9350) cannot be fixed. This is not a problem with the panel but rather a problem with the way the panels are configured for the XPS 13, as the same panel exists in the Dell's Latitude 13 7000 series (e7370) FHD model but with CABC disabled. The fix is available directly from [Dell](http://www.dell.com/support/home/uk/en/ukdhs1/Drivers/DriversDetails?driverId=PWD5K&fileId=3505631210&osCode=W764&productCode=xps-13-9350-laptop&languageCode=en&categoryId=AP).

## BIOS

The most convenient way to install Arch Linux is by disabling "Secure Boot" (Secure Boot > Disable). However it is possible to self-sign your kernel and boot with it enabled. For further information have a look at the [Secure Boot](/index.php/Secure_Boot "Secure Boot") article.

In case your `efivars` are not properly set it is most likely due to you not being booted into [UEFI](/index.php/UEFI "UEFI"). Should the problem persist be sure to consult the [UEFI#UEFI variables](/index.php/UEFI#UEFI_variables "UEFI") section.

### Updates

[BIOS update 1.10.1](https://www.dell.com/support/home/us/en/19/drivers/driversdetails?driverid=rdnw7) was released on 2019-03-18\. Store the update binary on your EFI partition (`/boot/EFI`) or on a USB flash drive (fat32), reboot, and choose BIOS Update in the F12 boot menu. This might also help if your machine will not resume after suspend.

### Firmware Updates

Dell provides firmware updates via Linux Vendor Firmware Service (LVFS). Refer to [Flashing BIOS from Linux#fwupd](/index.php/Flashing_BIOS_from_Linux#fwupd "Flashing BIOS from Linux") for additional information. A package is readily available at [fwupd](https://www.archlinux.org/packages/?name=fwupd).

## Thunderbolt 3 / USB 3.1

The USB-C port supports Thunderbolt 3, Displayport-over-USB-C and USB power delivery as well as USB 3.1.

In the event of devices not working correctly, ensure that you have updated to the latest BIOS (above) and Thunderbolt firmware (below).

Dell is working on a fwupd extension ([github repository](https://github.com/dell/thunderbolt-nvm-linux)) that allows updating Thunderbolt software from Linux.

Alternatively, the [Thunderbolt 3 Firmware Update 4.26.11.001, A08](https://downloads.dell.com/FOLDER04795516M/1/Intel_TBT3_FW_UPDATE_NVM26_FJJK7_A08_4.26.11.001.exe) was released on 2018-04-05\. Unlike the BIOS update and the Thunderbolt-nvm Linux update, this is a graphical application which must be run in a modern Windows environment (MS-DOS will not suffice) or you can attempt the procedure below (at your own risks).

Hotplug support for this port requires a [bug fix](https://bugzilla.kernel.org/show_bug.cgi?id=115121) which landed in kernel version 4.7\. It also requires the kernel to be built with <tt>CONFIG_PCI_HOTPLUG=y</tt>.

#### Doing Thunderbolt firmware updates without [fwupd](https://www.archlinux.org/packages/?name=fwupd) or Windows

The thunderbolt updates are a bit more complicated to do than the UEFI updates. The following was tested on kernel 4.16.13\. You need to download the Thunderbolt update executable then extract the files from it:

```
$ 7z x Intel_TBT3_FW_UPDATE_NVM26_FJJK7_A08_4.26.11.001.exe

```

If you don't have any thunderbolt device plugged in, you need to force the controller on

```
# echo 1 > /sys/devices/platform/PNP0C14:00/wmi_bus/wmi_bus-PNP0C14:00/*/force_power

```

Check the controller current firmware version:

```
# cat /sys/bus/thunderbolt/devices/0-0/nvm_version

```

Then copy the file to the controller's memory and authenticate

```
# dd if=Intel/0x0704_secure.bin of=/sys/bus/thunderbolt/devices/0-0/nvm_non_active0/nvmem
# echo 1 > /sys/bus/thunderbolt/devices/0-0/nvm_authenticate

```

The system may hang for a few seconds, and after a moment, if you read nvm_version again, it should show the new version number.

### External screen

External sceens are working well with newer BIOS and Thunderbolt firmware versions applied, e.g. fully functional with the external dock Dell WD15\.

Support for external screens either using an USB-C to HDMI or USB-C to Mini Display ports adapters may not be working properly in rare cases. Commonly the screen when plugged is reported to either:

*   display an image for a few milliseconds then switch to a black screen;
*   have no image at all;
*   being flickering after a few minutes to the extent this is basically unusable.

In some cases intermittent external monitor connection may be caused by WiFi interference with the 9350's USB-C port--particularly when the lid is closed. Reducing WiFi power via iw or iwconfig may allow a steady external monitor connection.

Refer to the [according Arch Forum entry](https://bbs.archlinux.org/viewtopic.php?id=205147) for an exhaustive discussion about working adapters and the [Dell forum entry](http://en.community.dell.com/techcenter/os-applications/f/4613/t/19988851).

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

The location of the `nvme` module for ["NVM Express"](https://en.wikipedia.org/wiki/NVM_Express "wikipedia:NVM Express") SSD has changed between [linux](https://www.archlinux.org/packages/?name=linux) kernel version 4.3 and 4.4\. If you experience "cannot find root device" on boot, it may be due to the [nvme module not being present in initramfs](https://bugs.archlinux.org/task/47761). In this case, the following may resolve your issue.

Edit your `/etc/mkinitcpio.conf` file:

```
   ...
   MODULES=(... "nvme")
   ...

```

Then update the [initial ramfs](/index.php/Arch_boot_process#initramfs "Arch boot process"), e.g. for the stock Linux kernel:

```
   # mkinitcpio -p linux

```

Replace `linux` with the image which is to be booted, e.g. `linux-hardened`, etc.

### Note on Mount Options

Using the `discard` mount option for your filesystem is not recommended, as mentioned in [this warning](/index.php/Solid_State_Drives#Continuous_TRIM "Solid State Drives") and [the forum](https://bbs.archlinux.org/viewtopic.php?pid=1593544#p1593544). See also [Solid State Drives/NVMe#Discards](/index.php/Solid_State_Drives/NVMe#Discards "Solid State Drives/NVMe") for further information.

## Wireless

For the non-developer edition, the built-in Broadcom BCM4350 is now supported in the current [linux](https://www.archlinux.org/packages/?name=linux) kernel (as of version 4.4.1-1). The wireless module `brcmfmac` also needs the firmware `brcmfmac4350-pcie.bin` from the related [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) package.

The Broadcom adapter does not report its regulatory country and so, by default, the global settings for channels and frequencies will be set. See [Wireless network configuration#Respecting the regulatory domain](/index.php/Wireless_network_configuration#Respecting_the_regulatory_domain "Wireless network configuration") for more information about how this can be changed.

## Bluetooth

### Intel WiFi

If your WiFi card supports Bluetooth, then the BT interface should be available out-of-the-box, as the required firmware is included in [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware).

### Broadcom Wifi

Bluetooth should work right away. Load the module `btusb` and `bluetooth` if it was not already and [start](/index.php/Start "Start")/[enable](/index.php/Enable "Enable") `bluetooth.service`. Refer to [Bluetooth](/index.php/Bluetooth "Bluetooth") for more information and configuration options.

**Note:** The Broadcom `brcmfmac` kernel module causes issues with Dell USB-C docks. Notably, the USB ports and ethernet connection will stop working when there are WiFi connection issues.

#### Wireless headset: strange bluetooth behavior

If your Bluetooth behaves unstable, such as connection loss, stuttering sound. being able to connect but not to listen through it, etc. you probably need the proprietary firmware.

The Broadcom Bluetooth firmware is not available in the kernel (the same as for the 2015 model [source](https://tech.sybreon.com/2015/03/15/xps13-9343-ubuntu-linux/)), therefore you will have to retrieve it from a Windows [.exe](https://downloads.dell.com/FOLDER03272920M/1/9350_Network_Driver_XMJK7_WN32_12.0.1.720_A00.EXE). You need to extract the `.exe` file with [p7zip](https://www.archlinux.org/packages/?name=p7zip) and then convert it to a `.hcd` file with *hex2hcd* from [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils):

```
$ 7z x 9350_Network_Driver_XMJK7_WN32_12.0.1.720_A00.EXE
$ cp Win32/BCM4350C5_003.006.007.0095.1703.hex ./
$ hex2hcd BCM4350C5_003.006.007.0095.1703.hex
# mv BCM4350C5_003.006.007.0095.1703.hcd /lib/firmware/brcm/BCM-0a5c-6412.hcd

```

Alternatively, you may simply install [bcm4350-firmware](https://aur.archlinux.org/packages/bcm4350-firmware/).

After a reboot, the firmware should be available for your Bluetooth interface.

## Video

The video should work with the `i915` driver of the current [linux](https://www.archlinux.org/packages/?name=linux) kernel. Consult [Intel graphics](/index.php/Intel_graphics "Intel graphics") for a detailed installation and configuration guide as well as for [Troubleshooting](/index.php/Intel_graphics#Troubleshooting "Intel graphics").

### Blank screen issue after booting

If using "late start" [KMS](/index.php/KMS "KMS") (the default) and the screen goes blank when loading modules, it may help to add `i915` and `intel_agp` to the initramfs or using a special [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"). Consult [Intel graphics#Blank screen during boot, when "Loading modules"](/index.php/Intel_graphics#Blank_screen_during_boot,_when_"Loading_modules" "Intel graphics") for more information about the kernel paramter way and have a look at [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting") for a guide on how to setup the modules for the initramfs.

### Linux kernel 4.8 or later power savings

**Warning:** The following options of the `i915` module taint the kernel, use at your own risks!

#### RC6

`i915.enable_rc6=1` seems to be stable, setting the value to a number higher than 1, will be ignored. The deeper GPU power states that this option enables (RC6p and RC6pp) do not exist on gen7+ hardware.[[1]](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/drivers/gpu/drm/i915/i915_drv.h#n2862)[[2]](https://lists.freedesktop.org/archives/intel-gfx/2012-June/018383.html).

#### Panel Self Refresh

`i915.enable_psr=1` allows for some really nice power savings by leaving the package longer in more efficient C-states. However, users experience freezes for a few seconds with this option fairly often, setting the value to [2 or 3](https://patchwork.kernel.org/patch/8182841/) may yield to similar power savings but without the freezes. `i915.disable_power_well=0` with `i915.enable_psr=1 i915.enable_rc6=1` also seems to be a stable configuration for PSR.

#### Frame Buffer Compression

`i915.enable_fbc=1` is stable but does not seem to yield significant power saving results.

#### GuC

[GuC](https://01.org/linuxgraphics/intel-linux-graphics-firmwares) loading with `i915.enable_guc_loading=1 i915.enable_guc_submission=1` seems stable too.

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

## Power management

### Fans

The fans may remain on even at low temperatures, draining the battery and producing an unpleasant noise that will only stop on reboot. This is due to the fans being controlled by the BIOS by default.

To prevent this behavior, configure i8k as described in [Fan speed control#Dell laptops](/index.php/Fan_speed_control#Dell_laptops "Fan speed control") and use [dell-bios-fan-control-git](https://aur.archlinux.org/packages/dell-bios-fan-control-git/) utility to disable BIOS control of fans which conflicts with i8k. You may also want to [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `dell-bios-fan-control.service` to ensure BIOS control of fans is disabled at boot.

If i8kutils is installed it will show fan speed and temperature sensors with:

```
$ watch sensors

```

### Undervolting

Undervolting CPU & GPU is possible. Use [intel-undervolt](https://aur.archlinux.org/packages/intel-undervolt/) utility. Change voltage settings by editing:

```
/etc/intel-undervolt.conf

```

For example, change *`undervolt 0 'CPU' 0.00`* to e.g. *`undervolt 0 'CPU' -25.00`* to decrease CPU setting by 25mV.

[Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `intel-undervolt.service`.

**Warning:** Be careful, do not undervolt with unstable values. It may lead to a system unable to boot.

Read undervolt settings:

```
# intel-undervolt -read

```

Apply undervolt settings from config file:

```
# intel-undervolt -apply

```

Measure power consumption:

```
# intel-undervolt -measure

```

Watch temperature sensors:

```
$ watch sensors

```

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
   FILES=("/etc/modprobe.d/modprobe.conf")
   ...

```

Rebuild your initial ramdisk image (see [Mkinitcpio#Image creation and activation](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio")).

### Gestures

Refer to [libinput#Gestures](/index.php/Libinput#Gestures "Libinput") for information about the current development state and available methods.

## Keyboard

By default, the keyboard backlight turns off after 10 seconds of inactivity. Some users might find this too short and annoying. Unfortunately this timeout cannot be adjusted by writing into `/sys/devices/platform/dell-laptop/leds/dell\:\:kbd_backlight/stop_timeout` like on other Dell XPS laptops. The delay can't even be increased (or decreased) by editing this file:

```
/sys/devices/platform/dell-laptop/leds/dell\:\:kbd_backlight/stop_timeout

```

[The BIOS is preventing](https://github.com/dell/libsmbios/issues/48) the user from changing the timeout on AC like on Dell XPS 9370 laptop models. A kernel workaround was added in 4.18 only for Dell XPS 9370 and not XPS 9350.

F-Keys to dim or disable/enable keyboard backlight does work.

## Sound

### Coil whine when using headphones

When using TLP and audio is not playing but headphones are plugged in you may experience extremely annoying whine when using the computer. This happens after the audio adapter power saving is enabled. By default TLP sets the timeout on battery to 1 second which will cause whining almost as soon as sound is paused. To remedy this you can edit `/etc/default/tlp` to set a higher timeout or disable it:

```
SOUND_POWER_SAVE_ON_AC=300
SOUND_POWER_SAVE_ON_BAT=300

```

### High noise floor when using headphones

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

## Microphone

**Note:** Not all hardware has the "Digital" channel

For ALSA, increase "Digital" channel for microphone to work.

### No audio input through combo jack

**Note:** This might only apply for the Developer Edition

The device is recognized when you plug in a headset, however there is no audio input when you speak into the microphone. To solve this issue you have to pass `model=auto` to the `snd-hda-intel` kernel module. You can do this with a drop-in file:

 `/etc/modprobe.d/fix-audio-input.conf`  `options snd-hda-intel model=auto` 

## TPM

As shipped the Trusted Platform Module (TPM) can be configured easily following the steps at [Trusted Platform Module](/index.php/Trusted_Platform_Module "Trusted Platform Module") and requires no otherwise special configuration. Handy packages to use with the TPM are [tpm-tools](https://aur.archlinux.org/packages/tpm-tools/) and [trousers](https://aur.archlinux.org/packages/trousers/).

### TPM 2.0

Originally the Dell XPS 13 (9350) shipped with TPM 1.2 - the TPM chip was configured to support the TPM Standard version 1.2\. However, Dell released a [firmware update](http://www.dell.com/support/home/uk/en/ukdhs1/drivers/driversdetails?driverId=RF87D) (internal version 1.3.2.8, A02) for the TPM chip that converts it to support the feature set of TPM Standard version 2.0\. Unfortunately, as of this moment the update cannot be applied through Linux or the BIOS direct flashing capabilities. The only way to install it seems to be to apply it through a running Windows OS. The easiest method is to run a temporary Windows installation on a USB drive, boot into it and run the update from there.
**Note:** It should be noted that this update is reversible once applied. To revert back to TPM 1.2 by using a [firmware update](http://www.dell.com/support/home/us/en/04/Drivers/DriversDetails?driverId=F3J3P) It also requires that the TPM memory and configuration is completely cleared.

**Note:** As for BIOS updates, please make sure the laptop is plugged in to a power source and that power source is stable.

To install the update one can follow the instructions on the above mentioned firmware update page to clear and reset the TPM chip and initiate the update. Users intending to later use the device in Linux, can skip the last steps 11 & 12 from section "Disable TPM Auto Provisioning in Windows". Another option is to just clear the TPM following [this guide](http://www.dell.com/support/article/uk/en/ukbsdt1/SLN155219/en) and just run the `.exe` file from Windows.

Once the update succeeds, the Linux kernel should automatically recognise the newly configured TPM device and enable it automatically on next boot. To make use of the now TPM 2.0 chip a couple of packages are worth installing - [tpm2-tss-git](https://aur.archlinux.org/packages/tpm2-tss-git/) and [tpm2-tools-git](https://aur.archlinux.org/packages/tpm2-tools-git/). To make the TSS resource manager work on boot, a handy systemd service is provided and its variants discussed [here](https://github.com/01org/TPM2.0-TSS/issues/321).

## CPU slowdown after resume from suspend

If you are experiencing a very slow computer after resume from suspend, you may be subject to a bug where your CPU frequency is capped to a very low value. Use `cpupower frequency-info` to check. If so, please read [this forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1558948#p1558948) for debug information, and a workaround.

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
*   [Service Manual for Dell XPS 13 (9350)](http://topics-cdn.dell.com/pdf/xps-13-9350-laptop_Service%20Manual_en-us.pdf)