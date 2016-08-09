**Note:** This page refers to the early 2015 model of XPS 13\. For the late 2015 model, see [Dell XPS 13 (2016)](/index.php/Dell_XPS_13_(2016) "Dell XPS 13 (2016)").

| **Device** | **Status** |
| Video | Working |
| Backlight control | Working |
| Wireless | Working |
| Bluetooth | Works after installing firmware |
| Audio | Working |
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
    *   [2.2 Backlight](#Backlight)
    *   [2.3 SSD](#SSD)
    *   [2.4 WiFi](#WiFi)
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
    *   [2.9 Calibrated ICC profile for QHD+ models](#Calibrated_ICC_profile_for_QHD.2B_models)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Random hangs after login with external monitor](#Random_hangs_after_login_with_external_monitor)
    *   [3.2 Pink & green artifacts in video or webcam output](#Pink_.26_green_artifacts_in_video_or_webcam_output)
    *   [3.3 Graphical artifacting/instability after S3 resume](#Graphical_artifacting.2Finstability_after_S3_resume)
    *   [3.4 Connection issues with Broadcom wireless](#Connection_issues_with_Broadcom_wireless)
    *   [3.5 rfkill issues with Broadcom wireless](#rfkill_issues_with_Broadcom_wireless)
    *   [3.6 EFISTUB does not boot](#EFISTUB_does_not_boot)
    *   [3.7 Random kernel hangs at boot](#Random_kernel_hangs_at_boot)
    *   [3.8 Sound doesn't work after upgrading to kernel 4.4+](#Sound_doesn.27t_work_after_upgrading_to_kernel_4.4.2B)
*   [4 See also](#See_also)

## Model differences

Although the XPS 13 is sold in a variety of configurations in most markets, those wanting to run Linux should pay special attention to display options (FHD/QHD+) and WiFi adapter differences (Dell DW1560 vs. Intel 7265). For users with the QHD+ model, you'll need to use a DE/WM that properly supports [HiDPI](/index.php/HiDPI "HiDPI"). Regarding the WiFi adapter choices, both cards do work in Arch, but the Dell DW1560 requires a proprietary kernel module that is not well-supported, whereas the Intel 7265 is supported by the mainline kernel.

There are no exclusive hardware differences between the Developer Edition and the Windows edition of this laptop; this guide is equally applicable to both models.

## Configuration

### BIOS updates

[BIOS update A07](http://www.dell.com/support/home/us/en/04/Drivers/DriversDetails?driverId=28M21) was released on 2015-11-26\. With A02 or newer, almost everything should work out of the box, and the kernel boot parameters that were used in conjunction with earlier BIOS versions are no longer necessary. Store the update binary on your EFI partition (`/boot/EFI`) or on a USB flash drive, reboot, and choose BIOS Update in the F12 boot menu.

### Backlight

Works out-of-the-box:

*   The [systemd-backlight.service](/index.php/Backlight#systemd-backlight_service "Backlight") takes care of both eDP panel and keyboard backlight (and any other external device) status, saving at shutdown and restoring their values at boot.
*   hardware keys (`Fn-F10` to `Fn-F12`) works without any operation, as well.

### SSD

This laptop series comes with a SSD as storage device; this section aims to remind you that this technology needs some configuration in order to achieve the best operative conditions. See [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives") for information.

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

To use HDA mode on newer kernels, compile your kernel with the option `CONFIG_ACPI_REV_OVERRIDE_POSSIBLE=y`. This will force HDA mode on; you will not be able to use I2S mode.

##### Setting the default sound card

By default, ALSA doesn't output sound to the PCH card but to the HDMI card. This can be changed by following [ALSA#Set the default sound card](/index.php/ALSA#Set_the_default_sound_card "ALSA"). To set the proper order, create the following `.conf` file in `/etc/modprobe.d/` [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1446773#p1446773):

 `/etc/modprobe.d/alsa-base.conf`  `options snd_hda_intel index=1,0` 

Note that if you are dual-booting with Windows, you will have to do a cold boot twice before HDA sound will work in Linux and vice-versa. This is not necessary in I2S mode.

#### I2S mode

With BIOS A02+ and Arch kernel **4.4 or newer**, the sound card will be initialized in I2S mode. I2S support requires [alsa-lib](https://www.archlinux.org/packages/?name=alsa-lib) 1.1.0 or newer.[[2]](http://www.spinics.net/lists/linux-acpi/msg57457.html)

**Note:** Kernels 4.5-4.7 require the options `CONFIG_DW_DMAC=y` and `SND_SOC_INTEL_BROADWELL_MACH=m` to be statically compiled[[3]](https://bugzilla.redhat.com/show_bug.cgi?id=1308792#c21); otherwise, the sound card will not be recognized. This has been resolved in Arch kernel 4.5.2+[[4]](https://bugs.archlinux.org/task/48936); meanwhile, a better fix is forthcoming in kernel 4.8.[[5]](https://git.kernel.org/cgit/linux/kernel/git/broonie/sound.git/commit/?h=topic/intel&id=a395bdd6b24b692adbce0df6510ec9f2af57573e)

##### Enabling the microphone

**Note:** The microphone appears to be enabled by default as of Arch kernel 4.5.3, so these instructions may be unnecessary.[[6]](https://bugs.archlinux.org/task/47989#comment146876)

In I2S mode, the built-in microphone is muted by default. To enable it you have to unmute `Mic` item; follow the instructions below in order to achieve the goal:

*   open `alsamixer` (an utility included into the [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) package)
*   press `F6` and select the ***broadwell-rt286*** sound card
*   press `F4` to switch to the *Capture view* and ensure that **ADC0** has the *CAPTURE* label. If it doesn't, toggle over to it with your arrow keys and press the spacebar to turn it on *CAPTURE*
*   finally, toggle over to the **Mic** item and raise the volume to 100.

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

Additionally, [powertop](/index.php/Powertop "Powertop") may also be employed to tweak performance and monitor power consumption.

**Note:**  

*   With kernel 4.6+, frame-buffer compression (FBC) and panel self-refresh (PSR) are enabled by default, so `i915.enable_fbc` and `i915.enable_psr` are no longer needed. Kernel 4.6.2+ is recommended as older kernels may cause the display to flicker.
*   `i915.lvds_downclock=1` for LVDS downclock is no longer needed. According to irc #intel-gfx, "there's a new auto-downclock for eDP panels in recent kernels and it's enabled by default if available, so don't use."
*   `i915.enable_rc6=7` is useless on Broadwell/gen8 systems. The deeper GPU power states that this option enables (RC6p and RC6pp) do not exist on gen7+ hardware.[[7]](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/drivers/gpu/drm/i915/i915_drv.h#n2862)[[8]](https://lists.freedesktop.org/archives/intel-gfx/2012-June/018383.html)

### Calibrated ICC profile for QHD+ models

**Warning:** This profile is only for QHD+ models. Do not use it if you have the FHD model of the XPS 13.

An [ICC profile](/index.php/ICC_profiles "ICC profiles") is a binary file which contains precise data regarding the color attributes of the monitor. It allows you to produce consistent and repeatable results for graphic and document editing and publishing. The following ICC profiles are made with DispcalGUI, ArgyllCMS and a spectrophotometer for absolute color accuracy. It is possible to achieve better results by calibrating your own monitor, but generally this profile will be an improvement over the stock profile.

This profile has been made with the spectrophotometer's high resolution spectral mode, with white and black level drift compensation, the high quality ArgyllCMS switch and 3440 patches. Dynamic Brightness Control has been disabled and the monitor has been turned on at least 30 minutes before commencing the calibration.

*   [QHD+, D65, Gamma 2.2, max luminance](https://mega.nz/#!nkNVQDCI!YYcS32HLWk1Aqry30dmOrt0wrfH9W_VczNesHQEpG_U).

## Troubleshooting

### Random hangs after login with external monitor

Very often, three-quarters of times, if I boot up the machine with an external monitor connected (I use a miniDP to HDMI cable), the computer hangs after I login in through graphical display manager. i.e. in my case, using GDM to login in into gnome desktop, after I enter the password, cursor disappears and system becomes totally unresponsive; the only way to "continue" is to force a reboot by pressing the power button. I don't know if it was only a problem of mine due to a strange hardware/software combination but, anyway and fortunately, it seems fixed *starting from May 2016*, likely thanks to a kernel bug fix. This mean `kernel-lts` users may still suffer of this issue.

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

As of version A07, the BIOS does not pass any boot parameters to the kernel. Use a UEFI [boot loader](/index.php/Boot_loader "Boot loader") instead. [systemd-boot](/index.php/Systemd-boot "Systemd-boot") will work with current kernels.

### Random kernel hangs at boot

See [here](https://bugzilla.kernel.org/show_bug.cgi?id=105251). This issue seems to only affect those with touchscreens. The fix consists in removing "keyboard" from the HOOKS in /etc/mkinitcpio.conf and instead using MODULES="atkbd.ko usbhid hid-generic" (if you need the keyboard hook). You will have to run `mkinitcpio -p linux` as root afterwards.

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