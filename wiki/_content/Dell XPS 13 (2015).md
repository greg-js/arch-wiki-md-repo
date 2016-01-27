# Dell XPS 13 (2015)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**Note:** This page refers to the early 2015 model of XPS 13\. For the late 2015 model, see [Dell XPS 13 (2016)](/index.php/Dell_XPS_13_(2016) "Dell XPS 13 (2016)").

<table class="wikitable" style="float: right;">

<tbody>

<tr>

<td>**Device**</td>

<td>**Status**</td>

<td>**Modules**</td>

</tr>

<tr>

<td>Video</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>i915</td>

</tr>

<tr>

<td>Wireless</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>wl _or_ iwlwifi</td>

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

<td>hid_multitouch</td>

</tr>

<tr>

<td>Webcam</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>linux-uvc</td>

</tr>

<tr>

<td>Card Reader</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>rtsx_usb</td>

</tr>

<tr>

<td>Wireless switch</td>

<td style="background: #ffa; color: inherit; vertical-align: middle; text-align: center;">Works, but is [problematic](#rfkill_issues_with_Broadcom_wireless) with Broadcom WiFi</td>

<td>rfkill</td>

</tr>

</tbody>

</table>

The [2015 Dell XPS 13 (9343)](http://www.dell.com/us/p/xps-13-9343-laptop/pd) is the second-generation model of the XPS 13 line, and like its predecessor, it has official Linux support courtesy of Dell's Project Sputnik team. They target Ubuntu 14.04 LTS, but the improvements and support from the Sputnik team are generally applicable to all distros.

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
        *   [2.4.3 ALSA configuration](#ALSA_configuration)
    *   [2.5 High quality ICC monitor profiles](#High_quality_ICC_monitor_profiles)
    *   [2.6 Touchpad](#Touchpad)
    *   [2.7 Powersaving](#Powersaving)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Pink & green artifacts in video or webcam output](#Pink_.26_green_artifacts_in_video_or_webcam_output)
    *   [3.2 Graphical artifacting/instability after S3 resume](#Graphical_artifacting.2Finstability_after_S3_resume)
    *   [3.3 Connection issues with Broadcom wireless](#Connection_issues_with_Broadcom_wireless)
    *   [3.4 rfkill issues with Broadcom wireless](#rfkill_issues_with_Broadcom_wireless)
    *   [3.5 EFISTUB does not boot](#EFISTUB_does_not_boot)
    *   [3.6 Repeating keys issue](#Repeating_keys_issue)
    *   [3.7 Random kernel hangs at boot](#Random_kernel_hangs_at_boot)
*   [4 See also](#See_also)

## Model differences

Although the XPS 13 is sold in a variety of configurations in most markets, those wanting to run Linux should pay special attention to display options (FHD/QHD+) and WiFi adapter differences (Dell DW1560 vs. Intel 7265). For users with the QHD+ model, you'll need to use a DE/WM that properly supports [HiDPI](/index.php/HiDPI "HiDPI"). Regarding the WiFi adapter choices, both cards do work in Arch, but the Dell DW1560 requires a proprietary kernel module that is not well-supported, whereas the Intel 7265 is supported by the mainline kernel.

There are no exclusive hardware differences between the Developer Edition and the Windows edition of this laptop; this guide is equally applicable to both models.

## Configuration

### BIOS updates

[BIOS update A07](http://www.dell.com/support/home/us/en/04/Drivers/DriversDetails?driverId=28M21) was released on 2015-11-26\. With A02 or newer, almost everything should work out of the box, and the kernel boot parameters that were used in conjunction with earlier BIOS versions are no longer necessary. Store the update binary on your EFI partition (`/boot/efi`) or on a USB flash drive, reboot, and choose BIOS Update in the F12 boot menu.

### WiFi

Most configurations feature the Dell DW1560 802.11ac adapter (Broadcom BCM4352), which requires [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/)<sup><small>AUR</small></sup> or [broadcom-wl-dkms](https://aur.archlinux.org/packages/broadcom-wl-dkms/)<sup><small>AUR</small></sup> to be installed. See the [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless") page for more details and/or assistance.

Some higher-end models do not use the Dell-branded adapter but instead use an Intel Wireless 7265, which is supported by the mainline kernel. This card is generally available as an aftermarket purchase for those wishing to replace the Broadcom wireless in their laptop. Compared to the Broadcom card, the Intel card has a 2-3 times wider reception range and way higher throughput, making it an worthwhile upgrade should you decide to do so. Note that the Intel 7265 card exists as both a WLAN standalone and WLAN/Bluetooth combo card; both work, so it's your decision if you are willing to pay extra to get Bluetooth support or not.

**Tip:** **Intel users:** Intel Linux driver maintainer Emmanuel Grumbach maintains a [fork of the linux-firmware repository](https://git.kernel.org/cgit/linux/kernel/git/iwlwifi/linux-firmware.git) which contains bleeding edge firmware that provides improved throughput and connection stability for the Intel 7265 card, see [linux-firmware-git-iwlwifi](https://aur.archlinux.org/packages/linux-firmware-git-iwlwifi/)<sup><small>AUR</small></sup>.

### Bluetooth

**Note:** **Intel WiFi users:** If your WiFi card supports Bluetooth, then the BT interface should be available out-of-the-box, as the required firmware is included in [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware).

The Broadcom Bluetooth firmware is not available in the kernel ([source](http://tech.sybreon.com/2015/03/15/xps13-9343-ubuntu-linux/)), so you will have to retrieve it from the [Windows driver](http://catalog.update.microsoft.com/v7/site/ScopedViewRedirect.aspx?updateid=87a7756f-1451-45da-ba8a-55f8aa29dfee). You need to extract the `.cab` file with [cabextract](https://www.archlinux.org/packages/?name=cabextract) and then convert it to a `.hcd` file with _hex2hcd_ from [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils):

```
$ cabextract 20662520_6c535fbfa9dca0d07ab069e8918896086e2af0a7.cab
$ hex2hcd BCM20702A1_001.002.014.1443.1572.hex
# mv BCM20702A1_001.002.014.1443.1572.hcd /lib/firmware/brcm/BCM20702A1-0a5c-216f.hcd
# ln -rs /lib/firmware/brcm/BCM20702A1-0a5c-216f.hcd /lib/firmware/brcm/BCM20702A0-0a5c-216f.hcd

```

After reboot, the firmware should be available for your Bluetooth interface.

### Audio

**Note:** Proper audio support is dependent on having the latest BIOS update. If you have not yet updated to BIOS A02 or newer, please do that first.

The sound chipset in this laptop, a Realtek ALC3263, is described as "dual-mode", meaning it supports both the [HDA standard](https://en.wikipedia.org/wiki/Intel_High_Definition_Audio) and the [I2S standard](https://en.wikipedia.org/wiki/I%C2%B2S). The embedded controller in the XPS 13 uses the [ACPI](https://en.wikipedia.org/wiki/Advanced_Configuration_and_Power_Interface) _REV value provided by the OS you use to determine which mode the sound chipset should be initialized in at boot.

#### HDA mode

With BIOS A02+, the kernel will automatically use the sound card in HDA mode.

Microphone support was finally fixed in the mainline kernel in 4.1.3\. All older kernel versions require patches to fix it. To fix it on kernels 4.1.0-4.1.2, apply the patch [available here](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=831bfdf9520e389357cfeee42a6174a73ce7bdb7). To fix it on kernels older than 4.1, apply this patchset: [1](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit?id=e1e62b98ebddc3234f3259019d3236f66fc667f8), [2](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit?id=f3b703326541d0c1ce85f5e570f6d2b6bd4296ec).

Note that if you are dual-booting with Windows, you will have to do a cold boot twice before HDA sound will work in Linux and vice-versa.

#### I2S mode

I2S support in Linux is still quite nascent, and some important features, notably jack detection, are not due to land until kernel 4.2 or later. [[1]](http://www.spinics.net/lists/linux-acpi/msg57126.html) As a result, I2S support is currently disabled in favor of HDA mode. An ACPI REV quirk mode was merged in for 4.2 that will force HDA mode on until I2S support is ready. [[2]](http://thread.gmane.org/gmane.linux.acpi.devel/75464/focus=75466)[[3]](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=18d78b64fddc11eb336f01e46ad3303a3f55d039)

In I2S mode, the dual-boot workaround is not necessary.

#### ALSA configuration

By default, ALSA doesn't output sound to the PCH card but to the HDMI card. This can be changed by following [ALSA#Set the default sound card](/index.php/ALSA#Set_the_default_sound_card "ALSA"). In the current case, both cards use the `snd_hda_intel` module. To set the proper order, create the following `.conf` file in `/etc/modprobe.d/` [[4]](https://bbs.archlinux.org/viewtopic.php?pid=1446773#p1446773):

 `/etc/modprobe.d/alsa-base.conf`  `options snd_hda_intel index=1,0` 

### High quality ICC monitor profiles

An ICC profile is a binary file which contains precise data regarding the color attributes of the monitor. It allows you to produce consistent and repeatable results for graphic and document editing and publishing. The following ICC profiles are made with DispcalGUI, ArgyllCMS and a spectrophotometer for absolute color accuracy. Since every monitor is different it is possible to achieve better results calibrating your own monitor, but if you don't have a colorimeter or a spectrophotometer you will get far better results with the following XYZ LUT + MATRIX profiles made with a ~3500 patches testchart instead of the canned ones. If you previously didn't install a canned profile you will notice a night and day difference in color accuracy. Do not use a profile made for the QHD+ version with the FHD one and vice versa. The profiles has been made with the spectrophotometer's high resolution spectral mode, with white and black level drift compensation, the high quality ArgyllCMS switch and 3440 patches. The monitor has been turned on for at least 30 minutes before commencing the calibration.

*   QHD+, D65, Gamma 2.2, max luminance: [https://mega.nz/#!LpMGUJCD!cqGOyY-BCHL3znTZI-kwwagLWD0gnaarKTurdzRH1Qo](https://mega.nz/#!LpMGUJCD!cqGOyY-BCHL3znTZI-kwwagLWD0gnaarKTurdzRH1Qo)

**Note:** You should disbale Dynamic Brightness Control to accurately calibrate the QHD+ display: [https://github.com/advancingu/XPS13Linux/issues/2](https://github.com/advancingu/XPS13Linux/issues/2)

**Note:** This profile has been made with DBC on, so I will upload another profile with DBC off

*   FHD, D65, Gamma 2.2, max luminance: coming soon (I will get my hands on the FHD monitor in February)

**Note:** It may not be possible to accurately calibrate the FHD display due to the dynamic contrast behaviour of the panel which cannot be disabled

### Touchpad

With the latest BIOS patch, most of the touchpad functions should work, although [palm detection](/index.php/Touchpad_Synaptics#Using_the_driver.27s_automatic_palm_detection "Touchpad Synaptics") does not work in i2c mode yet. For advanced settings with [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics), the _psmouse_ kernel module must be [blacklisted](/index.php/Kernel_modules#Blacklisting "Kernel modules") first.

The touchpad may freeze if two fingers are detected on the pad. This can be fixed by setting `synclient Clickpad=1`

If your desktop does not provide useful default settings for the clickpad (no right or middle button emulation, for example) or you want more control than your desktop environments settings provide, see [Touchpad Synaptics](/index.php/Touchpad_Synaptics#Buttonless_touchpads_.28aka_ClickPads.29 "Touchpad Synaptics")

If you need working palm detection, you can use [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput). The libinput driver supports nearly all button layouts out of the box with few additional settings.

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 

```
Section "InputClass"
	Identifier "touchpad"
	MatchProduct "DLL0665:01 06CB:76AD UNKNOWN"
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

*   Enabling PSR support, via `i915.enable_psr=1`, will further reduce idle power usage to ~2.6 W. As of kernel version 4.3.3 it still causes occasional flickering but no longer so mch as to be unusable.
*   `i915.lvds_downclock=1` for lvds_downclock is no longer needed. From the MacBook page: "there's a new auto-downclock for eDP panels in recent kernels and it's enabled by default if available, so don't use - recommendation from irc #intel-gfx").

## Troubleshooting

### Pink & green artifacts in video or webcam output

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** kept for users of other distros until the fix is released upstream. (Discuss in [Talk:Dell XPS 13 (2015)#](https://wiki.archlinux.org/index.php/Talk:Dell_XPS_13_(2015)))

Update [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) if you haven't already; this should fix the issue.

### Graphical artifacting/instability after S3 resume

If you encounter some artifacts and/or an unusable graphical environment after resuming from a suspend, you may want to [switch your Intel graphics acceleration from SNA to UXA](/index.php/Intel_graphics#SNA_issues "Intel graphics"). Switching to UXA, however, will result in decreased performance.

### Connection issues with Broadcom wireless

If `wifi-menu` and `iwlist scan` fail after driver installation and reboot, try disabling "Wireless Switch" control in the BIOS.

### rfkill issues with Broadcom wireless

The wireless switch key (to the right of the "Brightness up" key) switches the wireless card on/off at the hardware level, but the Broadcom driver does not react to it properly: it does not realise the card is off, and only sees a lost connection. It then fails to recover when the card is switched back on. You can work-around this issue by switching WiFi off and on again in the NetworkManager applet or by setting `/sys/class/rfkill/rfkill0/state` to 0 and then 1\. Alternatively, you can disable the "Wireless Switch" control in the firmware setup.

### EFISTUB does not boot

As of version A05, the BIOS does not pass any boot parameters to the kernel. Use a [UEFI boot loader](/index.php/Boot_loaders#UEFI-only_boot_loaders "Boot loaders") instead. [systemd-boot](/index.php/Systemd-boot "Systemd-boot") works with current kernels.

### Repeating keys issue

BIOS A07 should fix this.

### Random kernel hangs at boot

See [here](https://bugzilla.kernel.org/show_bug.cgi?id=105251). This issue seems to only affect those with touchscreens. The fix consists in removing "keyboard" from the HOOKS in /etc/mkinitcpio.conf and instead using MODULES="atkbd.ko usbhid hid-generic" (if you need the keyboard hook). Obviously you will have to run:

```
# mkinitcpio -p linux

```

## See also

General:

*   [Collection of links and different configurations](https://github.com/mpalourdio/xps13)

Project Sputnik:

*   [Recent Fixes for XPS 13 developer edition](http://bartongeorge.net/2015/08/28/recent-fixes-for-xps-13-developer-edition/)
*   [Update 2: Dell XPS 13 laptop, developer edition – Sputnik Gen 4](http://bartongeorge.net/2015/02/23/update-2-dell-xps-13-laptop-developer-edition-sputnik-gen-4/)
*   [Update: Dell XPS 13 laptop, developer edition – Sputnik Gen 4](http://bartongeorge.net/2015/02/05/update-dell-xps-13-laptop-developer-edition-sputnik-gen-4/)
*   [4th gen Dell XPS 13 developer edition available!](http://bartongeorge.net/2015/04/09/4th-gen-dell-xps-13-developer-edition-available/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dell_XPS_13_(2015)&oldid=417101](https://wiki.archlinux.org/index.php?title=Dell_XPS_13_(2015)&oldid=417101)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Dell](/index.php/Category:Dell "Category:Dell")

Hidden category:

*   [Pages or sections flagged with Template:Out of date](/index.php/Category:Pages_or_sections_flagged_with_Template:Out_of_date "Category:Pages or sections flagged with Template:Out of date")