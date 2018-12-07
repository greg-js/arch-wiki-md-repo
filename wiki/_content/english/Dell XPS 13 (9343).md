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

Related articles

*   [Dell XPS 13 (9333)](/index.php/Dell_XPS_13_(9333) "Dell XPS 13 (9333)")
*   [Dell XPS 13 (9350)](/index.php/Dell_XPS_13_(9350) "Dell XPS 13 (9350)")
*   [Dell XPS 13 (9360)](/index.php/Dell_XPS_13_(9360) "Dell XPS 13 (9360)")
*   [Dell XPS 13 (9370)](/index.php/Dell_XPS_13_(9370) "Dell XPS 13 (9370)")
*   [Dell XPS 13 2-in-1 (9365)](/index.php/Dell_XPS_13_2-in-1_(9365) "Dell XPS 13 2-in-1 (9365)")

The [2015 Dell XPS 13 (9343)](http://www.dell.com/us/p/xps-13-9343-laptop/pd) is the second-generation model of Dell's XPS 13 line. Like its predecessor, it has official Linux support courtesy of Dell's Project Sputnik team[[1]](https://bartongeorge.io/2015/04/09/4th-gen-dell-xps-13-developer-edition-available/). They target Ubuntu 14.04 LTS, but the improvements and support from the Sputnik team are generally applicable to all distros.

The installation process for Arch Linux on the XPS 13 does not differ from any other PC. For installation help, please see the [Installation guide](/index.php/Installation_guide "Installation guide") and [UEFI](/index.php/UEFI "UEFI") pages. This page covers the current status of hardware support on Arch, as well as post-installation recommendations.

As of kernel 4.1.3 (released July 2015), a patched kernel is no longer necessary. However, some manual configuration is still recommended to get the best experience.

## Contents

*   [1 Model differences](#Model_differences)
*   [2 Configuration](#Configuration)
    *   [2.1 BIOS updates](#BIOS_updates)
    *   [2.2 Screen and Keyboard Backlight](#Screen_and_Keyboard_Backlight)
        *   [2.2.1 Dynamic Backlight/Brightness Control (DBC)](#Dynamic_Backlight/Brightness_Control_(DBC))
    *   [2.3 SSD](#SSD)
    *   [2.4 Wi-Fi](#Wi-Fi)
    *   [2.5 Bluetooth](#Bluetooth)
    *   [2.6 Audio](#Audio)
        *   [2.6.1 HDA mode](#HDA_mode)
            *   [2.6.1.1 Setting the default sound card](#Setting_the_default_sound_card)
        *   [2.6.2 I2S mode](#I2S_mode)
            *   [2.6.2.1 Enabling the microphone](#Enabling_the_microphone)
            *   [2.6.2.2 Using Jack](#Using_Jack)
    *   [2.7 Touchpad](#Touchpad)
        *   [2.7.1 Synaptics driver](#Synaptics_driver)
        *   [2.7.2 Libinput driver](#Libinput_driver)
    *   [2.8 Powersaving](#Powersaving)
    *   [2.9 Calibrated ICC profile](#Calibrated_ICC_profile)
        *   [2.9.1 QHD+ model](#QHD+_model)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Sometimes the system fails to resume from suspend after closing and reopening the LID](#Sometimes_the_system_fails_to_resume_from_suspend_after_closing_and_reopening_the_LID)
    *   [3.2 DE can't connect Bluetooth devices](#DE_can't_connect_Bluetooth_devices)
    *   [3.3 Pink & green artifacts in video or webcam output](#Pink_&_green_artifacts_in_video_or_webcam_output)
    *   [3.4 Graphical artifacting/instability after S3 resume](#Graphical_artifacting/instability_after_S3_resume)
    *   [3.5 Connection issues with Broadcom wireless](#Connection_issues_with_Broadcom_wireless)
    *   [3.6 rfkill issues with KDE](#rfkill_issues_with_KDE)
    *   [3.7 EFISTUB does not boot](#EFISTUB_does_not_boot)
    *   [3.8 Random kernel hangs at boot](#Random_kernel_hangs_at_boot)
    *   [3.9 Sound doesn't work after upgrading to kernel 4.4+](#Sound_doesn't_work_after_upgrading_to_kernel_4.4+)
    *   [3.10 Loud cracks/noise during boot or audio playback](#Loud_cracks/noise_during_boot_or_audio_playback)
*   [4 See also](#See_also)

## Model differences

Although the XPS 13 is sold in a variety of configurations in most markets, those wanting to run Linux should pay special attention to **display** options (FHD or QHD+) and **Wi-Fi adapter** differences (Dell DW1560 or Intel 7265).

Users with QHD+ displays should use a DE/WM that properly supports [HiDPI](/index.php/HiDPI "HiDPI").

Regarding the Wi-Fi adapter, both cards work in Arch Linux. If the Intel one works out-of-the-box thanks to mainline kernel support, the Dell DW1560 instead requires a proprietary kernel module that is not well-supported; further details are reported in the proper below section.

There are no exclusive hardware differences between the *Developer Edition* and the standard Windows edition, so this guide is equally applicable to both models.

## Configuration

### BIOS updates

The latest BIOS update is [A18](https://www.dell.com/support/Home/us/en/19/Drivers/DriversDetails?driverId=RR83R) and it was released on 23th November 2018\. With version A02 or newer, almost everything should work out-of-the-box and the kernel boot parameters that were used in conjunction with earlier BIOS versions are no longer necessary.

BIOS upgrade is easy, thanks to the EFI implementation: place the update binary in the EFI partition (`/boot/EFI`) or on a USB flash drive, reboot, press `F12` key in order to enter in the Boot Menu and then choose *BIOS Update*.

### Screen and Keyboard Backlight

Backlight and its control work out-of-the-box:

*   The [systemd-backlight.service](/index.php/Backlight#systemd-backlight_service "Backlight") takes care of both *eDP panel* and *keyboard* backlight (and any other external device) status, saving at shutdown and restoring their values at boot.
*   Hardware Function keys (`Fn-F11` and `Fn-F12` for screen backlight and `Fn-F10` for keyboard backlight) work without any operation, as well.

**Note:** By default, the keyboard backlight automatically turns off after 60 seconds of inactivity. You can change the default behaviour by editing the related *sysfs* entry `/sys/devices/platform/dell-laptop/leds/dell\:\:kbd_backlight/stop_timeout`.

#### Dynamic Backlight/Brightness Control (DBC)

You may notice that the screen looks dimmer than you expect or the screen overall brightness changes constantly. This behaviour is not a symptom of any monitor issue but a technology called **Dynamic Backlight/Brightness Control (DBC)**, designed to save energy according to the content displayed on the screen.

**Tip:** You can check this feature on this [website](https://tylerwatt12.com/dc/).

**Warning:** This feature is *automatic* and *not-controllable*. According to official Dell [source](http://www.dell.com/support/article/us/en/19/sln304876/xps-9343-9350-9360-and-9365-2-in-1-lcd-brightness-issues), only the **QHD+ models** have a chance to disable it via a firmware update.

### SSD

This laptop series comes with a SSD as storage device, connected via SATA. This technology needs some configuration in order to achieve the best operative conditions. See [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives") for further information.

### Wi-Fi

Most configurations sport the Dell DW1560 802.11ac adapter (based on the Broadcom BCM4352 chip) which requires [broadcom-wl](https://www.archlinux.org/packages/?name=broadcom-wl) or [broadcom-wl-dkms](https://www.archlinux.org/packages/?name=broadcom-wl-dkms) (in this case, remember to install `linux-headers` too, even if it is listed as an optional dependency) to be installed. See the [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless") page for more details and/or assistance.

Some higher-end models do not use the Dell-branded Broadcom adapter, instead they use an Intel Wireless 7265 card which is supported by the mainline kernel.

**Note:** This card is widely available as an after-market purchase for those wishing to replace the Broadcom adapter in their laptop. This wireless adapter, other than an enviable driver support for both Wi-Fi and Bluetooth that makes installation easier, compared to the Broadcom card, it has a 2-3 times wider reception range and a much higher throughput, making it an worthwhile upgrade. Other cards are also available. The Intel Wireless 8265 is known to work

### Bluetooth

**Note:** For users with Intel wireless adapter with both Wi-Fi and Bluetooth, the Bluetooth interface should be available out-of-the-box, as the required firmware is included in [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware).

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

**Note:** Proper audio support is dependent on having the latest BIOS update. If you have not yet updated to BIOS A02 or newer, please perform [#BIOS updates](#BIOS_updates) first.

The sound chipset in this laptop, a Realtek ALC3263, is described as "dual-mode", meaning it supports both the [HDA standard](https://en.wikipedia.org/wiki/Intel_High_Definition_Audio "wikipedia:Intel High Definition Audio") and the [I2S standard](https://en.wikipedia.org/wiki/I%C2%B2S "wikipedia:I²S"). The embedded controller in the XPS 13 uses the [ACPI](https://en.wikipedia.org/wiki/Advanced_Configuration_and_Power_Interface "wikipedia:Advanced Configuration and Power Interface") _REV value provided by the OS itself to determine in which mode the sound chipset should be initialized in at boot.

#### HDA mode

With BIOS A02+ and official Arch Linux kernels **older than 4.4** and again starting **from version 4.11.5**, the sound card will be initialized in HDA mode.

**Note:** To use HDA mode on excluded kernels, re-compile them with the option `CONFIG_ACPI_REV_OVERRIDE_POSSIBLE=y`. This will force HDA mode on.

##### Setting the default sound card

By default, ALSA does not output sound to the PCH card but to the HDMI card. This can be changed by following [ALSA#Set the default sound card](/index.php/ALSA#Set_the_default_sound_card "ALSA"). To set the proper order, create the following `.conf` file in `/etc/modprobe.d/` [[2]](https://bbs.archlinux.org/viewtopic.php?pid=1446773#p1446773):

 `/etc/modprobe.d/alsa-base.conf`  `options snd_hda_intel index=1,0` 
**Note:** If you are dual-booting with Windows, you will have to do a cold boot twice before to have sound working in Linux and vice-versa.

**Note:** This is not necessary in I2S mode.

#### I2S mode

With BIOS A02+ and official Arch Linux kernels **from 4.4 to 4.11.4**, the sound card will be initialized in I2S mode. I2S support requires [alsa-lib](https://www.archlinux.org/packages/?name=alsa-lib) 1.1.0[[3]](http://www.spinics.net/lists/linux-acpi/msg57457.html) or newer. (I2S support was broken in mainline kernel 4.5, and fixed in Arch kernel 4.5.2 and mainline 4.8[[4]](https://bugs.archlinux.org/task/48936)[[5]](https://git.kernel.org/cgit/linux/kernel/git/broonie/sound.git/commit/?h=topic/intel&id=a395bdd6b24b692adbce0df6510ec9f2af57573e)).

##### Enabling the microphone

**Note:** The microphone appears to be enabled by default as of official Arch Linux kernel 4.5.3, so these instructions may be unnecessary [[6]](https://bugs.archlinux.org/task/47989#comment146876).

In I2S mode, the built-in microphone is muted by default. To enable it you have to unmute the `Mic` item. Follow the instructions below in order to achieve the goal:

*   open `alsamixer` (an utility included in the [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) package)
*   press `F6` and select the ***broadwell-rt286*** sound card
*   press `F4` to switch to the *Capture view* and ensure that **ADC0** has the *CAPTURE* label. If it doesn't, toggle over to it with your arrow keys and press the spacebar to turn it on *CAPTURE*
*   finally, toggle over to the **Mic** item and raise the volume to 100.

**Note:** Cycling the **Port** (from *Main Microphone* to *Headset Microphone (unplugged)*, and back) of the **Input Devices** tab in the `pavucontrol` application, has the same effect of the above instructions.

##### Using Jack

By default Jack recognises four capture ports and is unusable because the transport is broken into short fragments with breaks between them. Limit input to two channels with `-i2` on the command line or the corresponding option in [qjackctl](https://www.archlinux.org/packages/?name=qjackctl)'s advanced settings.

### Touchpad

With the latest BIOS, the touchpad should work out-of-the-box with either the synaptics or libinput drivers. The second is recommended over the former.

#### Synaptics driver

For more advanced settings with the Synaptics driver, see [Touchpad Synaptics](/index.php/Touchpad_Synaptics#Buttonless_touchpads_(aka_ClickPads) "Touchpad Synaptics").

If the touchpad freezes when you use more than one finger, try enabling Clickpad mode with `synclient Clickpad=1`.

#### Libinput driver

For better multi-touch support, you can use [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput). The libinput driver supports nearly all button layouts out-of-the-box with few additional settings.

Refer to the specific [libinput](/index.php/Libinput "Libinput") page for more details.

For further configurable options (e.g. NaturalScrolling, MiddleEmulation), see [libinput(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libinput.1).

### Powersaving

With kernel 4.6.5 and [tlp](https://www.archlinux.org/packages/?name=tlp), the idle power usage can reach ~2.3 W with the [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `pcie_aspm=force` enabled.

You may use [powertop](https://www.archlinux.org/packages/?name=powertop) or [powerstat-git](https://aur.archlinux.org/packages/powerstat-git/) to reproduce and check this behaviour by yourself.

**Note:**  

*   With kernel 4.6+, frame-buffer compression (**FBC**) is enabled by default, so `i915.enable_fbc` is no longer needed.
*   Panel self refresh (**PSR**) causes the display to flicker, so it has been disabled by default as of kernel 4.9 [[7]](https://bugs.freedesktop.org/show_bug.cgi?id=95176).
*   `i915.lvds_downclock=1` for **LVDS downclock** is no longer needed. According to IRC #intel-gfx, *"[...] there is a new auto-downclock for eDP panels in recent kernels and it is enabled by default if available, [...]"*.
*   `i915.enable_rc6=7` is useless on Broadwell (**Gen8**) systems because the deeper GPU power states that this option enables (RC6p and RC6pp) do not exist on **Gen7+** hardware [[8]](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/drivers/gpu/drm/i915/i915_drv.h#n2862)[[9]](https://lists.freedesktop.org/archives/intel-gfx/2012-June/018383.html).

### Calibrated ICC profile

#### QHD+ model

**Warning:** This profile is only for QHD+ model. Do not use it if you have the FHD one.

An [ICC profile](/index.php/ICC_profiles "ICC profiles") is a binary file which contains precise data regarding the colour attributes of the monitor. It allows you to produce consistent and repeatable results for graphic and document. The following ICC profile is made with dispcalGUI ( [displaycal](https://www.archlinux.org/packages/?name=displaycal)) ArgyllCMS ( [argyllcms](https://www.archlinux.org/packages/?name=argyllcms)) and a spectrophotometer for absolute colour accuracy; even if it is possible to achieve better results by calibrating your own monitor by yourself, in general this profile is definitively an improvement over the stock profile.

This profile has been made with the spectrophotometer's high resolution spectral mode, with white and black level drift compensation, the high quality ArgyllCMS switch and 3440 patches. Dynamic Brightness Control has been disabled and the monitor has been turned on for at least 30 minutes prior to start the calibration.

*   [QHD+, D65, Gamma 2.2, max luminance](https://mega.nz/#!nkNVQDCI!YYcS32HLWk1Aqry30dmOrt0wrfH9W_VczNesHQEpG_U).

## Troubleshooting

### Sometimes the system fails to resume from suspend after closing and reopening the LID

According to [this kernel.org bug report](https://bugzilla.kernel.org/show_bug.cgi?id=86241) this is supposed to be fixed since a long time, yet it still happens with kernels up to 4.18.6 (at least on the QHD+ model). You can work it around with the following command:

```
sudo cat << EOF > /etc/modprobe.d/blacklist.suspend-bug.conf

blacklist mei
blacklist mei_me
EOF

```

### DE can't connect Bluetooth devices

If the Bluetooth GUI can't connect the device, try to use `bluetoothctl` to connect manually.

### Pink & green artifacts in video or webcam output

Update [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) to latest version. This should fix the issue.

### Graphical artifacting/instability after S3 resume

If you encounter some artifacts and/or an unusable graphical environment after resuming from a suspend, you may want to [switch your Intel graphics acceleration from SNA to UXA](/index.php/Intel_graphics#SNA_issues "Intel graphics"). Switching to UXA, however, will result in worse performance. Switching to xf86-video-modesetting (Glamor acceleration) should not decrease performance considerably,however it is still not known if will fix the resume issue.

### Connection issues with Broadcom wireless

If `wifi-menu` and `iwlist scan` fail after driver installation and reboot, try disabling "Wireless Switch" control in the BIOS.

### rfkill issues with KDE

As from kernel version 4.4 the rfkill switch works. The KDE plasma-nm (NetworkManager) widget does not indicate that wlan is active after it has been reactivated, but still connects correctly. The KDE system tray bluetooth widget usually disappears if the switch disables bluetooth, and fails to reappear when it is reactivated. You can work around this by setting the switch not to switch bluetooth in the BIOS setup. With kernel version < 4.13.11 and/or plasma-desktop < 5.11 the mouse pointer may freeze first time that the rfkill switch is used. To unfreeze it, switch to another virtual console and back.

### EFISTUB does not boot

As of version A07, the BIOS does not pass any boot parameters to the kernel. Use a UEFI [boot loader](/index.php/Boot_loader "Boot loader") instead. [systemd-boot](/index.php/Systemd-boot "Systemd-boot") will work with current kernels.

### Random kernel hangs at boot

See [here](https://bugzilla.kernel.org/show_bug.cgi?id=105251). This issue seems to affect only touchscreen model owners. The fix consists in removing "keyboard" from the HOOKS array in /etc/mkinitcpio.conf. If you need the keyboard at boot, edit the MODULES array as follow MODULES="atkbd usbhid hid-generic". You will have to run `mkinitcpio -p linux` as root afterwards.

### Sound doesn't work after upgrading to kernel 4.4+

You need to do two cold boots (**NOT** a simple reboot, shut it down and turn it back on again) to make sound working again.

Refer to the [#HDA mode](#HDA_mode) above for more info, as well as the [BBS thread](https://bbs.archlinux.org/viewtopic.php?id=208674) and [Arch Linux bug report](https://bugs.archlinux.org/task/47989).

### Loud cracks/noise during boot or audio playback

Some users have reported the above sound problems, as described [here](https://bbs.archlinux.org/viewtopic.php?id=208496) for example.

[Disabling audio powersafe](/index.php/Advanced_Linux_Sound_Architecture/Troubleshooting#Pops_when_starting_and_stopping_playback "Advanced Linux Sound Architecture/Troubleshooting") may work for people using the **HDA** audio mode.

However, it is still unknown how to solve this issue for the **I2S** audio mode.

For further reference, see the corresponding [kernel bug entry](https://bugzilla.kernel.org/show_bug.cgi?id=112611).

## See also

General:

*   [Collection of links and different configurations](https://github.com/mpalourdio/xps13)
*   [Service Manual for Dell XPS 13 (9343)](http://downloads.dell.com/Manuals/all-products/esuprt_laptop/esuprt_xps_laptop//xps-13-9343-laptop_Service%20Manual_en-us.pdf)

Project Sputnik:

*   [Recent Fixes for XPS 13 developer edition](http://bartongeorge.net/2015/08/28/recent-fixes-for-xps-13-developer-edition/)
*   [Update 2: Dell XPS 13 laptop, developer edition – Sputnik Gen 4](http://bartongeorge.net/2015/02/23/update-2-dell-xps-13-laptop-developer-edition-sputnik-gen-4/)
*   [Update: Dell XPS 13 laptop, developer edition – Sputnik Gen 4](http://bartongeorge.net/2015/02/05/update-dell-xps-13-laptop-developer-edition-sputnik-gen-4/)
*   [4th gen Dell XPS 13 developer edition available!](http://bartongeorge.net/2015/04/09/4th-gen-dell-xps-13-developer-edition-available/)