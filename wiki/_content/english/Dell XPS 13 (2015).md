**Note:** This page refers to the early 2015 model of XPS 13\. For the late 2015 model, see [Dell XPS 13 (2016)](/index.php/Dell_XPS_13_(2016) "Dell XPS 13 (2016)").

| **Device** | **Status** |
| Video | Working |
| Wireless | Working |
| Bluetooth | Works after installing firmware |
| Audio | Works, but [requires new kernel options](#I2S_mode) |
| Touchpad | Works after configuration |
| Webcam | Working |
| Card Reader | Working |
| Wireless switch | Works (Broadcom WiFi has some [issues](#rfkill_issues_with_Broadcom_wireless)) |

The [2015 Dell XPS 13 (9343)](http://www.dell.com/us/p/xps-13-9343-laptop/pd) is the second-generation model of Dell's XPS 13 line. Like its predecessor, it has official Linux support courtesy of Dell's Project Sputnik team. They target Ubuntu 14.04 LTS, but the improvements and support from the Sputnik team are generally applicable to all distros.

The installation process for Arch on the XPS 13 does not differ from any other PC. For installation help, please see the [Installation guide](/index.php/Installation_guide "Installation guide"), [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") and [UEFI](/index.php/UEFI "UEFI"). This page covers the current status of hardware support on Arch, as well as post-installation recommendations.

As of kernel 4.1.3, a patched kernel is no longer necessary. However, some manual configuration is still recommended to get the best experience.

## Contents

*   [1 Model differences](#Model_differences)
*   [2 Configuration](#Configuration)
    *   [2.1 BIOS updates](#BIOS_updates)
    *   [2.2 WiFi](#WiFi)
    *   [2.3 Bluetooth](#Bluetooth)
    *   [2.4 Audio](#Audio)
        *   [2.4.1 HDA mode](#HDA_mode)
        *   [2.4.2 I2S mode](#I2S_mode)
            *   [2.4.2.1 Enabling the microphone](#Enabling_the_microphone)
    *   [2.5 Touchpad](#Touchpad)
        *   [2.5.1 Synaptics driver](#Synaptics_driver)
        *   [2.5.2 Libinput driver](#Libinput_driver)
    *   [2.6 Powersaving](#Powersaving)
    *   [2.7 Calibrated ICC profile for QHD+ models](#Calibrated_ICC_profile_for_QHD.2B_models)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Pink & green artifacts in video or webcam output](#Pink_.26_green_artifacts_in_video_or_webcam_output)
    *   [3.2 Graphical artifacting/instability after S3 resume](#Graphical_artifacting.2Finstability_after_S3_resume)
    *   [3.3 Connection issues with Broadcom wireless](#Connection_issues_with_Broadcom_wireless)
    *   [3.4 rfkill issues with Broadcom wireless](#rfkill_issues_with_Broadcom_wireless)
    *   [3.5 EFISTUB does not boot](#EFISTUB_does_not_boot)
    *   [3.6 Random kernel hangs at boot](#Random_kernel_hangs_at_boot)
    *   [3.7 Sound doesn't work after upgrading to kernel 4.4+](#Sound_doesn.27t_work_after_upgrading_to_kernel_4.4.2B)
*   [4 See also](#See_also)

## Model differences

Although the XPS 13 is sold in a variety of configurations in most markets, those wanting to run Linux should pay special attention to display options (FHD/QHD+) and WiFi adapter differences (Dell DW1560 vs. Intel 7265). For users with the QHD+ model, you'll need to use a DE/WM that properly supports [HiDPI](/index.php/HiDPI "HiDPI"). Regarding the WiFi adapter choices, both cards do work in Arch, but the Dell DW1560 requires a proprietary kernel module that is not well-supported, whereas the Intel 7265 is supported by the mainline kernel.

There are no exclusive hardware differences between the Developer Edition and the Windows edition of this laptop; this guide is equally applicable to both models.

## Configuration

### BIOS updates

[BIOS update A07](http://www.dell.com/support/home/us/en/04/Drivers/DriversDetails?driverId=28M21) was released on 2015-11-26\. With A02 or newer, almost everything should work out of the box, and the kernel boot parameters that were used in conjunction with earlier BIOS versions are no longer necessary. Store the update binary on your EFI partition (`/boot/EFI`) or on a USB flash drive, reboot, and choose BIOS Update in the F12 boot menu.

### WiFi

Most configurations feature the Dell DW1560 802.11ac adapter (Broadcom BCM4352), which requires [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/) or [broadcom-wl-dkms](https://aur.archlinux.org/packages/broadcom-wl-dkms/) (in this case, remember to install `linux-headers` too; even if it is listed as an optional dependency) to be installed. See the [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless") page for more details and/or assistance.

Some higher-end models do not use the Dell-branded Broadcom adapter but instead use an Intel Wireless 7265, which is supported by the mainline kernel. This card is widely available as an aftermarket purchase for those wishing to replace the Broadcom adapter in their laptop. Compared to the Broadcom card, the Intel card has a 2-3 times wider reception range and a much higher throughput, making it an worthwhile upgrade should you decide to do so.

### Bluetooth

**Note:** **Intel WiFi users:** If your WiFi card supports Bluetooth, then the BT interface should be available out-of-the-box, as the required firmware is included in [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware).

The Broadcom Bluetooth firmware is not available in the kernel ([source](http://tech.sybreon.com/2015/03/15/xps13-9343-ubuntu-linux/)), so you will need to install [bt-dw1560-firmware](https://aur.archlinux.org/packages/bt-dw1560-firmware/) and reboot if you want to use bluetooth.

Alternatively, you can retrieve it from the [Windows driver](http://catalog.update.microsoft.com/v7/site/ScopedViewRedirect.aspx?updateid=87a7756f-1451-45da-ba8a-55f8aa29dfee) yourself. You need to extract the `.cab` file with [cabextract](https://www.archlinux.org/packages/?name=cabextract) and then convert it to a `.hcd` file with *hex2hcd* from [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils):

```
$ cabextract 20662520_6c535fbfa9dca0d07ab069e8918896086e2af0a7.cab
$ hex2hcd BCM20702A1_001.002.014.1443.1572.hex
# mv BCM20702A1_001.002.014.1443.1572.hcd /lib/firmware/brcm/BCM20702A1-0a5c-216f.hcd
# ln -rs /lib/firmware/brcm/BCM20702A1-0a5c-216f.hcd /lib/firmware/brcm/BCM20702A0-0a5c-216f.hcd

```

After reboot, the firmware should be available for your Bluetooth interface.

### Audio

**Note:** Proper audio support is dependent on having the latest BIOS update. If you have not yet updated to BIOS A02 or newer, please do that first.

The sound chipset in this laptop, a Realtek ALC3263, is described as "dual-mode", meaning it supports both the [HDA standard](https://en.wikipedia.org/wiki/Intel_High_Definition_Audio "wikipedia:Intel High Definition Audio") and the [I2S standard](https://en.wikipedia.org/wiki/I%C2%B2S "wikipedia:I²S"). The embedded controller in the XPS 13 uses the [ACPI](https://en.wikipedia.org/wiki/Advanced_Configuration_and_Power_Interface "wikipedia:Advanced Configuration and Power Interface") _REV value provided by the OS you use to determine which mode the sound chipset should be initialized in at boot.

#### HDA mode

With BIOS A02+ and Arch kernel **4.3 or older**, the sound card will be initialized in HDA mode.

By default, ALSA doesn't output sound to the PCH card but to the HDMI card. This can be changed by following [ALSA#Set the default sound card](/index.php/ALSA#Set_the_default_sound_card "ALSA"). In the current case, both cards use the `snd_hda_intel` module. To set the proper order, create the following `.conf` file in `/etc/modprobe.d/` [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1446773#p1446773):

 `/etc/modprobe.d/alsa-base.conf`  `options snd_hda_intel index=1,0` 

Note that if you are dual-booting with Windows, you will have to do a cold boot twice before HDA sound will work in Linux and vice-versa. This is not necessary in I2S mode.

#### I2S mode

With BIOS A02+ and Arch kernel **4.4 or newer**, the sound card will be initialized in I2S mode. I2S support requires [alsa-lib](https://www.archlinux.org/packages/?name=alsa-lib) 1.1.0 or newer.[[2]](http://www.spinics.net/lists/linux-acpi/msg57457.html)

**Note:** Kernel 4.5+ requires the options `CONFIG_DW_DMAC=y` and `SND_SOC_INTEL_BROADWELL_MACH=m` to be statically compiled[[3]](https://bugzilla.redhat.com/show_bug.cgi?id=1308792#c21); otherwise, the sound card will not be recognized. This has been resolved in Arch kernel 4.5.2, which is now in testing.[[4]](https://bugs.archlinux.org/task/48936) In the meantime, users may stay on kernel 4.4 or use the [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) kernel.

##### Enabling the microphone

The built-in microphone is muted by default. To enable it, open `alsamixer`, then press F6 and select the `broadwell-rt286` sound card. Then, press F4 to switch to the Capture view and ensure that ADC0 has the CAPTURE label. If it doesn't, toggle over to it with your arrow keys and press the spacebar to turn on CAPTURE. Finally, toggle over to the Mic item and raise the volume to 100.

### Touchpad

With the latest BIOS, the touchpad should work out-of-the-box with either the synaptics or libinput drivers.

#### Synaptics driver

For more advanced settings with the Synaptics driver, see [Touchpad Synaptics](/index.php/Touchpad_Synaptics#Buttonless_touchpads_.28aka_ClickPads.29 "Touchpad Synaptics").

If the touchpad freezes when you use more than one finger, try enabling Clickpad mode with `synclient Clickpad=1`.

#### Libinput driver

For better multi-touch support, you can use [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput). The libinput driver supports nearly all button layouts out of the box with few additional settings.

 `/etc/X11/xorg.conf.d/50-libinput.conf` 
```
Section "InputClass"
	Identifier "touchpad"
	MatchProduct "DLL0665:01 06CB:76AD Touchpad"
	Driver "libinput"
	Option	"Tapping"	"on"
	Option	"AccelSpeed"	"1"
EndSection

```

### Powersaving

With kernel 4.1 and [tlp](https://www.archlinux.org/packages/?name=tlp), the idle power usage is reduced to ~3.5 W with the following [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"):

```
pcie_aspm=force i915.enable_fbc=1 i915.enable_rc6=7

```

At least since kernel 4.3.3 the flickering caused by `i915.enable_fbc=1` seems to have been fixed, and freezes happen significantly less often. However, heavy flickering may still occur with external monitors.

Additionally, [powertop](/index.php/Powertop "Powertop") may also be employed to tweak the performance and monitor power consumption.

**Note:**

*   Enabling PSR support, via `i915.enable_psr=1`, will further reduce idle power usage to ~2.6 W. As of kernel version 4.3.3 it still causes occasional flickering but no longer so much as to be unusable.
*   `i915.lvds_downclock=1` for lvds_downclock is no longer needed. From the MacBook page: "there's a new auto-downclock for eDP panels in recent kernels and it's enabled by default if available, so don't use - recommendation from irc #intel-gfx").

### Calibrated ICC profile for QHD+ models

**Warning:** This profile is only for QHD+ models. Do not use it if you have the FHD model of the XPS 13.

An [ICC profile](/index.php/ICC_profiles "ICC profiles") is a binary file which contains precise data regarding the color attributes of the monitor. It allows you to produce consistent and repeatable results for graphic and document editing and publishing. The following ICC profiles are made with DispcalGUI, ArgyllCMS and a spectrophotometer for absolute color accuracy. It is possible to achieve better results by calibrating your own monitor, but generally this profile will be an improvement over the stock profile.

This profile has been made with the spectrophotometer's high resolution spectral mode, with white and black level drift compensation, the high quality ArgyllCMS switch and 3440 patches. Dynamic Brightness Control has been disabled and the monitor has been turned on at least 30 minutes before commencing the calibration.

*   [QHD+, D65, Gamma 2.2, max luminance](https://mega.nz/#!nkNVQDCI!YYcS32HLWk1Aqry30dmOrt0wrfH9W_VczNesHQEpG_U).

## Troubleshooting

### Pink & green artifacts in video or webcam output

Update [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) if you haven't already; this should fix the issue.

### Graphical artifacting/instability after S3 resume

If you encounter some artifacts and/or an unusable graphical environment after resuming from a suspend, you may want to [switch your Intel graphics acceleration from SNA to UXA](/index.php/Intel_graphics#SNA_issues "Intel graphics"). Switching to UXA, however, will result in decreased performance. Switching to xf86-video-modesetting (glamor acceleration) should not decrease performance much, however it is still not known if will fix resume.

### Connection issues with Broadcom wireless

If `wifi-menu` and `iwlist scan` fail after driver installation and reboot, try disabling "Wireless Switch" control in the BIOS.

### rfkill issues with Broadcom wireless

With kernel 4.4 and Broadcom WiFi card, the wireless switch has no effect except freezing the pointer in the KDE desktop. To unfreeze it, switch to another virtual console and back.

With lower kernel versions, it switches the wireless card on/off at the hardware level, but the Broadcom driver does not not react to it properly: it does not realise the card is off, and only sees a lost connection. It then fails to recover when the card is switched back on. You can work-around this issue by switching WiFi off and on again in the NetworkManager applet or by setting `/sys/class/rfkill/rfkill0/state` to 0 and then 1\. Alternatively, you can disable the "Wireless Switch" control in the firmware setup.

### EFISTUB does not boot

As of version A07, the BIOS does not pass any boot parameters to the kernel. Use a [UEFI boot loader](/index.php/Boot_loaders#UEFI-only_boot_loaders "Boot loaders") instead. [systemd-boot](/index.php/Systemd-boot "Systemd-boot") works with current kernels.

### Random kernel hangs at boot

See [here](https://bugzilla.kernel.org/show_bug.cgi?id=105251). This issue seems to only affect those with touchscreens. The fix consists in removing "keyboard" from the HOOKS in /etc/mkinitcpio.conf and instead using MODULES="atkbd.ko usbhid hid-generic" (if you need the keyboard hook). Obviously you will have to run:

```
# mkinitcpio -p linux

```

### Sound doesn't work after upgrading to kernel 4.4+

You need to do two cold boots (*don't* reboot; shutdown and turn back on again) to make sound work again. This is necessary because I2S support was enabled in the Arch 4.4 stock kernel, and the XPS 13's embedded controller requires two cold boots to recognize changes in the sound chipset mode.

Refer to the Audio section above for more info, as well as the [BBS thread](https://bbs.archlinux.org/viewtopic.php?id=208674) and [Arch bug report](https://bugs.archlinux.org/task/47989).

## See also

General:

*   [Collection of links and different configurations](https://github.com/mpalourdio/xps13)

Project Sputnik:

*   [Recent Fixes for XPS 13 developer edition](http://bartongeorge.net/2015/08/28/recent-fixes-for-xps-13-developer-edition/)
*   [Update 2: Dell XPS 13 laptop, developer edition – Sputnik Gen 4](http://bartongeorge.net/2015/02/23/update-2-dell-xps-13-laptop-developer-edition-sputnik-gen-4/)
*   [Update: Dell XPS 13 laptop, developer edition – Sputnik Gen 4](http://bartongeorge.net/2015/02/05/update-dell-xps-13-laptop-developer-edition-sputnik-gen-4/)
*   [4th gen Dell XPS 13 developer edition available!](http://bartongeorge.net/2015/04/09/4th-gen-dell-xps-13-developer-edition-available/)