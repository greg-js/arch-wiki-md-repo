**Note:** This page refers to the *early* 2015 model of XPS 13\. For the *late* 2015 model, see [Dell XPS 13 (9350)](/index.php/Dell_XPS_13_(9350) "Dell XPS 13 (9350)").

| **Device** | **Status** |
| Video | Working |
| Backlight control | Working |
| Wi-Fi | Working |
| Bluetooth | Working |
| Audio | Working |
| Touchpad | Working |
| Webcam | Working |
| Card Reader | Working |
| Wireless switch | Working ([Some issues with kde](#rfkill_issues_with_KDE)) |

The [2015 Dell XPS 13 (9343)](http://www.dell.com/us/p/xps-13-9343-laptop/pd) is the second-generation model of Dell's XPS 13 line. Like its predecessor, it has official Linux support courtesy of Dell's Project Sputnik team[[1]](https://bartongeorge.io/2015/04/09/4th-gen-dell-xps-13-developer-edition-available/). They target Ubuntu 14.04 LTS, but the improvements and support from the Sputnik team are generally applicable to all distros.

The installation process for Arch Linux on the XPS 13 does not differ from any other PC. For installation help, please see the [Installation guide](/index.php/Installation_guide "Installation guide") and [UEFI](/index.php/UEFI "UEFI"). This page covers the current status of hardware support on Arch, as well as post-installation recommendations.

As of kernel 4.1.3, a patched kernel is no longer necessary and this means Installation Media newer than 2015.08.01 (release date: 2015-08-01) should all be able to boot this machine without problems.

However, some manual configuration is still recommended to get the best experience.

## Contents

*   [1 Model differences](#Model_differences)
*   [2 Configuration](#Configuration)
    *   [2.1 BIOS updates](#BIOS_updates)
    *   [2.2 Backlight](#Backlight)
    *   [2.3 SSD](#SSD)
    *   [2.4 Wi-Fi](#Wi-Fi)
    *   [2.5 Bluetooth](#Bluetooth)
    *   [2.6 Audio](#Audio)
        *   [2.6.1 HDA mode](#HDA_mode)
            *   [2.6.1.1 Setting the default sound card](#Setting_the_default_sound_card)
        *   [2.6.2 I2S mode](#I2S_mode)
            *   [2.6.2.1 Enabling the microphone](#Enabling_the_microphone)
    *   [2.7 Touchpad](#Touchpad)
        *   [2.7.1 Synaptics driver](#Synaptics_driver)
        *   [2.7.2 Libinput driver](#Libinput_driver)
    *   [2.8 Powersaving](#Powersaving)
    *   [2.9 Calibrated ICC profile](#Calibrated_ICC_profile)
        *   [2.9.1 QHD+ model](#QHD.2B_model)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Pink & green artifacts in video or webcam output](#Pink_.26_green_artifacts_in_video_or_webcam_output)
    *   [3.2 Graphical artifacting/instability after S3 resume](#Graphical_artifacting.2Finstability_after_S3_resume)
    *   [3.3 Connection issues with Broadcom wireless](#Connection_issues_with_Broadcom_wireless)
    *   [3.4 rfkill issues with KDE](#rfkill_issues_with_KDE)
    *   [3.5 EFISTUB does not boot](#EFISTUB_does_not_boot)
    *   [3.6 Random kernel hangs at boot](#Random_kernel_hangs_at_boot)
    *   [3.7 Sound doesn't work after upgrading to kernel 4.4+](#Sound_doesn.27t_work_after_upgrading_to_kernel_4.4.2B)
    *   [3.8 Loud cracks/noise during boot or audio playback](#Loud_cracks.2Fnoise_during_boot_or_audio_playback)
    *   [3.9 Display freezes while manipulating external displays with Xrandr / random blanking](#Display_freezes_while_manipulating_external_displays_with_Xrandr_.2F_random_blanking)
*   [4 See also](#See_also)

## Model differences

Although the XPS 13 is sold in a variety of configurations in most markets, those wanting to run Linux should pay special attention to **display** options (FHD or QHD+) and **Wi-Fi adapter** differences (Dell DW1560 or Intel 7265).

For users with QHD+ display, they need to use a DE/WM that properly supports [HiDPI](/index.php/HiDPI "HiDPI"). Regarding the Wi-Fi adapter, both cards work in Arch Linux; while the Intel 7265 has mainline kernel support, hence it will work out-of-the-box, the Dell DW1560 instead requires a proprietary kernel module that is not well-supported; further details are in the proper below section.

There are no exclusive hardware differences between the *Developer Edition* and the *classical edition* (the one with Windows) of this laptop that means this guide is equally applicable to both models.

## Configuration

### BIOS updates

Best practice is to install and use software on the latest BIOS version and this laptop makes no difference.

The latest BIOS update is [A11](http://www.dell.com/support/home/us/en/04/Drivers/DriversDetails?driverId=MYXCY&fileId=3598184217) and was released on 2017-02-02\. With A02 or newer, almost everything should work out-of-the-box, and the kernel boot parameters that were used in conjunction with earlier BIOS versions are no longer necessary.

BIOS upgrade is easy, thanks to the EFI implementation: store the update binary on the EFI partition (`/boot/EFI`) or on a USB flash drive, reboot, press `F12` key in order to enter in the Boot Menu and then choose *BIOS Update*.

### Backlight

Works out-of-the-box:

*   The [systemd-backlight.service](/index.php/Backlight#systemd-backlight_service "Backlight") takes care of both eDP panel and keyboard backlight (and any other external device) status, saving at shutdown and restoring their values at boot.
*   Hardware Function keys (`Fn-F10` to `Fn-F12`) works without any operation, as well.

### SSD

This laptop series comes with a SSD as storage device; this section aims to remind you that this technology needs some configuration in order to achieve the best operative conditions. See [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives") for information.

### Wi-Fi

Most configurations feature the Dell DW1560 802.11ac adapter (based on the Broadcom BCM4352 chip) which requires [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/) or [broadcom-wl-dkms](https://aur.archlinux.org/packages/broadcom-wl-dkms/) (in this case, remember to install `linux-headers` too, even if it is listed as an optional dependency) to be installed. See the [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless") page for more details and/or assistance.

Some higher-end models do not use the Dell-branded Broadcom adapter but instead they use an Intel Wireless 7265 card, which is supported by the mainline kernel. This card is widely available as an after-market purchase for those wishing to replace the Broadcom adapter in their laptop. This wireless adapter, other than an enviable driver support, for both Wi-Fi and Bluetooth, that makes installation easier, compared to the Broadcom card, it has a 2-3 times wider reception range and a much higher throughput [citation needed], making it an worthwhile upgrade should you decide to do so.

### Bluetooth

**Note:** users with Intel wireless adapter with both Wi-Fi and Bluetooth, the Bluetooth interface should be available out-of-the-box, as the required firmware is included in [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware).

The Broadcom Bluetooth firmware is not available in the kernel ([source](http://tech.sybreon.com/2015/03/15/xps13-9343-ubuntu-linux/)), so you need to install [bcm20702a1-firmware](https://aur.archlinux.org/packages/bcm20702a1-firmware/) and reboot if you want to use Bluetooth.

Alternatively, you can retrieve the firmware directly from the [Windows driver](http://catalog.update.microsoft.com/v7/site/ScopedViewRedirect.aspx?updateid=87a7756f-1451-45da-ba8a-55f8aa29dfee) by yourself. You need to extract the `.cab` file with [cabextract](https://www.archlinux.org/packages/?name=cabextract) and then convert it to a `.hcd` file with *hex2hcd* from [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils):

```
$ cabextract 20662520_6c535fbfa9dca0d07ab069e8918896086e2af0a7.cab
$ hex2hcd BCM20702A1_001.002.014.1443.1572.hex
# mv BCM20702A1_001.002.014.1443.1572.hcd /lib/firmware/brcm/BCM20702A1-0a5c-216f.hcd
# ln -rs /lib/firmware/brcm/BCM20702A1-0a5c-216f.hcd /lib/firmware/brcm/BCM20702A0-0a5c-216f.hcd

```

After reboot, the firmware is available for your Bluetooth interface.

### Audio

**Note:** Proper audio support is dependent on having the latest BIOS update. If you have not yet updated to BIOS A02 or newer, please do that first.

The sound chipset in this laptop, a Realtek ALC3263, is described as "dual-mode", meaning it supports both the [HDA standard](https://en.wikipedia.org/wiki/Intel_High_Definition_Audio "wikipedia:Intel High Definition Audio") and the [I2S standard](https://en.wikipedia.org/wiki/I%C2%B2S "wikipedia:I²S"). The embedded controller in the XPS 13 uses the [ACPI](https://en.wikipedia.org/wiki/Advanced_Configuration_and_Power_Interface "wikipedia:Advanced Configuration and Power Interface") _REV value provided by the OS you use to determine which mode the sound chipset should be initialized in at boot.

#### HDA mode

With BIOS A02+ and official Arch Linux kernel **4.3 or older**, the sound card will be initialized in HDA mode.

To use HDA mode on newer kernels, compile your kernel with the option `CONFIG_ACPI_REV_OVERRIDE_POSSIBLE=y`. This will force HDA mode on; you will not be able to use I2S mode by using that kernel.

##### Setting the default sound card

By default, ALSA doesn't output sound to the PCH card but to the HDMI card. This can be changed by following [ALSA#Set the default sound card](/index.php/ALSA#Set_the_default_sound_card "ALSA"). To set the proper order, create the following `.conf` file in `/etc/modprobe.d/` [[2]](https://bbs.archlinux.org/viewtopic.php?pid=1446773#p1446773):

 `/etc/modprobe.d/alsa-base.conf`  `options snd_hda_intel index=1,0` 

Note that if you are dual-booting with Windows, you will have to do a cold boot twice before HDA sound will work in Linux and vice-versa. This is not necessary in I2S mode.

#### I2S mode

With BIOS A02+ and official Arch Linux kernel **4.4 or newer**, the sound card will be initialized in I2S mode. I2S support requires [alsa-lib](https://www.archlinux.org/packages/?name=alsa-lib) 1.1.0[[3]](http://www.spinics.net/lists/linux-acpi/msg57457.html) or newer.

**Note:** Kernels 4.5-4.7 require the options `CONFIG_DW_DMAC=y` and `SND_SOC_INTEL_BROADWELL_MACH=m` to be statically compiled[[4]](https://bugzilla.redhat.com/show_bug.cgi?id=1308792#c21) otherwise the sound card will not be recognized. This has been resolved in official Arch Linux kernel 4.5.2+[[5]](https://bugs.archlinux.org/task/48936); anyhow, a better fix[[6]](https://git.kernel.org/cgit/linux/kernel/git/broonie/sound.git/commit/?h=topic/intel&id=a395bdd6b24b692adbce0df6510ec9f2af57573e) is included in kernel 4.8.

##### Enabling the microphone

**Note:** The microphone appears to be enabled by default as of official Arch Linux kernel 4.5.3, so these instructions may be unnecessary.[[7]](https://bugs.archlinux.org/task/47989#comment146876)

In I2S mode, the built-in microphone is muted by default. To enable it you have to unmute `Mic` item; follow the instructions below in order to achieve the goal:

*   open `alsamixer` (an utility included into the [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) package)
*   press `F6` and select the ***broadwell-rt286*** sound card
*   press `F4` to switch to the *Capture view* and ensure that **ADC0** has the *CAPTURE* label. If it doesn't, toggle over to it with your arrow keys and press the spacebar to turn it on *CAPTURE*
*   finally, toggle over to the **Mic** item and raise the volume to 100.

**Note:** Cycling the **Port** (from *Main Microphone* to *Headset Microphone (unplugged)*, and back) of the **Input Devices** tab in the `pavucontrol` application, has the same effect of the above instructions.

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

Refer to `man libinput` for more configurable options (e.g. NaturalScrolling, MiddleEmulation.)

### Powersaving

With kernel 4.6.5 and [tlp](https://www.archlinux.org/packages/?name=tlp), the idle power usage can reach ~2.3 W with the [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `pcie_aspm=force` enabled.

You may use [powertop](https://www.archlinux.org/packages/?name=powertop) or [powerstat-git](https://aur.archlinux.org/packages/powerstat-git/) to reproduce and check this behaviour by yourself.

**Note:**  

*   With kernel 4.6+, frame-buffer compression (FBC) and panel self-refresh (PSR) are enabled by default, so `i915.enable_fbc` and `i915.enable_psr` parameters are no longer needed. Kernel 4.6.2+ is recommended as older kernels may cause the display to flicker.
*   Soon panel self-refresh (PSR) will be disabled again. [[8]](https://patchwork.freedesktop.org/patch/127188/) Commit 2ee7dc497e348eecbb82adbb1ea9e9a7e29fe921 (drm/i915: disable PSR by default on HSW/BDW) landed on 2016-12-14 and is marked for inclusion in the stable kernel. Kernel 4.9 is already *affected*. This is the reference bug [[9]](https://bugs.freedesktop.org/show_bug.cgi?id=95176).
*   `i915.lvds_downclock=1` for LVDS downclock is no longer needed. According to IRC #intel-gfx, "there is a new auto-downclock for eDP panels in recent kernels and it is enabled by default if available, so do not use."
*   `i915.enable_rc6=7` is useless on Broadwell (Gen8) systems. The deeper GPU power states that this option enables (RC6p and RC6pp) do not exist on Gen7+ hardwares.[[10]](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/drivers/gpu/drm/i915/i915_drv.h#n2862)[[11]](https://lists.freedesktop.org/archives/intel-gfx/2012-June/018383.html)

### Calibrated ICC profile

#### QHD+ model

**Warning:** This profile is only for QHD+ model. Do not use it if you have the FHD one.

An [ICC profile](/index.php/ICC_profiles "ICC profiles") is a binary file which contains precise data regarding the colour attributes of the monitor. It allows you to produce consistent and repeatable results for graphic and document. The following ICC profile is made with dispcalGUI ( [displaycal](https://www.archlinux.org/packages/?name=displaycal)), ArgyllCMS ( [argyllcms](https://www.archlinux.org/packages/?name=argyllcms)) and a spectrophotometer for absolute colour accuracy; even if it is possible to achieve better results by calibrating your own monitor by yourself, in general this profile is definitively an improvement over the stock profile.

This profile has been made with the spectrophotometer's high resolution spectral mode, with white and black level drift compensation, the high quality ArgyllCMS switch and 3440 patches. Dynamic Brightness Control has been disabled and the monitor has been turned on for at least 30 minutes prior to start the calibration.

*   [QHD+, D65, Gamma 2.2, max luminance](https://mega.nz/#!nkNVQDCI!YYcS32HLWk1Aqry30dmOrt0wrfH9W_VczNesHQEpG_U).

## Troubleshooting

### Pink & green artifacts in video or webcam output

Update [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) if you haven't already; this should fix the issue.

### Graphical artifacting/instability after S3 resume

If you encounter some artifacts and/or an unusable graphical environment after resuming from a suspend, you may want to [switch your Intel graphics acceleration from SNA to UXA](/index.php/Intel_graphics#SNA_issues "Intel graphics"). Switching to UXA, however, will result in decreased performance. Switching to xf86-video-modesetting (glamor acceleration) should not decrease performance much, however it is still not known if will fix resume.

### Connection issues with Broadcom wireless

If `wifi-menu` and `iwlist scan` fail after driver installation and reboot, try disabling "Wireless Switch" control in the BIOS.

### rfkill issues with KDE

With recent kernel versions (as from 4.4) the rfkill switch works. Under the KDE desktop, the first time that the rfkill switch is used, the mouse pointer freezes. To unfreeze it, switch to another virtual console and back.

### EFISTUB does not boot

As of version A07, the BIOS does not pass any boot parameters to the kernel. Use a UEFI [boot loader](/index.php/Boot_loader "Boot loader") instead. [systemd-boot](/index.php/Systemd-boot "Systemd-boot") will work with current kernels.

### Random kernel hangs at boot

See [here](https://bugzilla.kernel.org/show_bug.cgi?id=105251). This issue seems to only affect those with touchscreens. The fix consists in removing "keyboard" from the HOOKS in /etc/mkinitcpio.conf and instead using MODULES="atkbd usbhid hid-generic" (if you need the keyboard hook). You will have to run `mkinitcpio -p linux` as root afterwards.

### Sound doesn't work after upgrading to kernel 4.4+

You need to do two cold boots (*don't* reboot; shutdown and turn back on again) to make sound work again. This is necessary because I2S support was enabled in the stock Linux 4.4 kernel, and the XPS 13's embedded controller requires two cold boots to recognize changes in the sound chipset mode.

Refer to the Audio section above for more info, as well as the [BBS thread](https://bbs.archlinux.org/viewtopic.php?id=208674) and [Arch Linux bug report](https://bugs.archlinux.org/task/47989).

### Loud cracks/noise during boot or audio playback

Some users have reported above sound outputs, as described e.g. in [this BBS thread](https://bbs.archlinux.org/viewtopic.php?id=208496). [Disabling audio powersafe](https://wiki.archlinux.org/index.php/Advanced_Linux_Sound_Architecture/Troubleshooting#Pops_when_starting_and_stopping_playback) may work for people using the **HDA** audio mode. However, it is still unknown how to solve this issue for the **I2S** audio mode. For further reference, see the corresponding [kernel bug record](https://bugzilla.kernel.org/show_bug.cgi?id=112611).

### Display freezes while manipulating external displays with Xrandr / random blanking

`xrandr` commands (for eg. [HiDPI#Multiple_displays](/index.php/HiDPI#Multiple_displays "HiDPI")) can result in display freezes with no clear journalctl or Xorg error logs. Reported to occur for QHD models running kernel version 4.3.x and up [[12]](https://wiki.gentoo.org/wiki/Dell_XPS_13_9343#GPU_hang.2Ffreeze4_with_external_display) [[13]](https://wiki.archlinux.org/index.php/Intel_graphics#Skylake_support). Setting [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `i915.preliminary_hw_support=0` can reduce or remove this issue.

If you are experiencing freezes in GNOME on Login and/or after, be sure you have latest BIOS installed and disabled the C state feature.

## See also

General:

*   [Collection of links and different configurations](https://github.com/mpalourdio/xps13)

Project Sputnik:

*   [Recent Fixes for XPS 13 developer edition](http://bartongeorge.net/2015/08/28/recent-fixes-for-xps-13-developer-edition/)
*   [Update 2: Dell XPS 13 laptop, developer edition – Sputnik Gen 4](http://bartongeorge.net/2015/02/23/update-2-dell-xps-13-laptop-developer-edition-sputnik-gen-4/)
*   [Update: Dell XPS 13 laptop, developer edition – Sputnik Gen 4](http://bartongeorge.net/2015/02/05/update-dell-xps-13-laptop-developer-edition-sputnik-gen-4/)
*   [4th gen Dell XPS 13 developer edition available!](http://bartongeorge.net/2015/04/09/4th-gen-dell-xps-13-developer-edition-available/)