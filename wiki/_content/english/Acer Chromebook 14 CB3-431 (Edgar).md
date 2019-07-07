**Warning:** This article assumes the reader is willing to replace ChromeOS with Arch Linux.

The following article briefly explains all necessary procedures to install a fully-functional Arch Linux configuration on the Acer Chromebook 14 cb3-431 (Edgar).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Write Protection](#Write_Protection)
*   [2 Developer Mode](#Developer_Mode)
*   [3 Flashing a custom SeaBios](#Flashing_a_custom_SeaBios)
*   [4 Installation](#Installation)
    *   [4.1 Booting the Installation Media](#Booting_the_Installation_Media)
    *   [4.2 Post installation](#Post_installation)
*   [5 Fixes](#Fixes)
    *   [5.1 Sound](#Sound)
    *   [5.2 Internal Keyboard](#Internal_Keyboard)
    *   [5.3 Trackpad](#Trackpad)

## Write Protection

Write Protection does not have to be voided to follow this guideline.

## Developer Mode

Prior to the installation, certain actions must be taken to grant bios reading permission on unsigned installation mediums. This includes enabling [Developer Mode](http://www.chromium.org/chromium-os/developer-information-for-chrome-os-devices/acer-c720-chromebook#TOC-Developer-Mode), and flashing a custom SeaBios.

**Warning:** Enabling Developer Mode will wipe all of your data.

Enabling Developer Mode:

1.  Enter recovery mode by pressing the power button while holding down `Esc+F3` (Refresh).
2.  Once greeted in recovery mode (large yellow exclamation mark) press `Ctrl+d`.
3.  You will be prompted for confirmation, press enter to confirm developer mode.
4.  The device will reset and greet the user with a warning screen on every boot, that can be skipped by pressing `Ctrl+d`.

## Flashing a custom SeaBios

A custom SeaBios is required to load unsigned or self-signed installation mediums, in our case, being the Arch Linux Installation Media.

In ChromeOS, estasblish internet connection and enter the superuser shell with `Ctrl+Alt+F2` using the `chronos` username. Then obtain MrChromeBox's SeaBios utility:

```
# curl -L -O https://mrchromebox.tech/firmware-util.sh

```

Execute the firmware utility:

```
# bash firmware-util.sh

```

Select option 1 to Install RW_LEGACY, permitting booting from an external installation media from SeaBios.

Before selecting the reboot option and proceeding to the next part, ensure an Arch Linux Installation Media is inserted.

## Installation

### Booting the Installation Media

During the white "OS verification disabled" screen, toggle `Ctrl+l` to enter SeaBios. Then press the `Esc` key to load the boot menu, and select your external installation media.

Unless the installation media runs on a Linux version 4.8.14 or prior, the internal keyboard, sound, and trackpad will not function during the installation. From this point on, proceed with the official [Arch Linux Installation Guide](/index.php/Installation_guide "Installation guide").

**Note:** If SeaBios has immediately attempted to load from the internal disk, or simply ignored the `Esc` key boot menu request, the device has been fully shut down prior to the SeaBios load. SeaBios must be entered on reboot from ChromeOS to enter the Boot Menu

### Post installation

Unless RW protection has been voided and SeaBios has been set to boot as default, booting into grub is only possible by toggling `Ctrl+l` during the white "OS verification disabled" screen on boot.

## Fixes

Due to the unpopularity of the Intel Braswell Chipset, a number of issues may be encountered which require manual fixes.

As of [linux](https://www.archlinux.org/packages/?name=linux) 4.12.4 the internal keyboard and trackpad now work out of the box without the need for any additional kernel patches. The following features are not expected to work out of the box:

*   Sound/Audio

### Sound

To fix audio/sound output, install the Braswell config files from [GalliumOS](https://github.com/GalliumOS/galliumos-braswell). Installing the [galliumos-braswell-config](https://aur.archlinux.org/packages/galliumos-braswell-config/) package using the `pacman --force` parameter automates this process.

Currently, the internal microphone does not function and there is no known workaround.

### Internal Keyboard

The internal keyboard should be fully functional when using the latest kernel, with the exception of the top row hotkeys which are mapped to the function keys by default. See [Chrome OS devices#Hotkeys](/index.php/Chrome_OS_devices#Hotkeys "Chrome OS devices") for methods to implement the Chrome OS keyboard hotkeys.

### Trackpad

To fix trackpad pressure sensitivity issues for the [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) driver, add the following configuration file under `/etc/X11/xorg.conf.d/10-synaptics.conf`

 `/etc/X11/xorg.conf.d/10-synaptics.conf` 
```
Section "InputClass"
	Identifier "touchpad catchall"
	Driver "synaptics"
	MatchIsTouchpad "on"
	MatchDevicePath "/dev/input/event*"
	Option "FingerLow" "1"
	Option "FingerHigh" "5"
EndSection

```

To fix trackpad sensitivity issues when using the [libinput](https://www.archlinux.org/packages/?name=libinput) driver, add the following local device quirk under `/etc/libinput/local-overrides.quirks`

 `/etc/libinput/local-overrides.quirks` 
```
[Touchpad pressure override]
MatchUdevType=touchpad
MatchName=*Elan Touchpad
MatchDMIModalias=dmi:*svnGOOGLE:*pnEdgar*
AttrPressureRange=4:3

```

After the XServer has been restarted, the changes will take place.

When using hibernation ([Suspend and hibernate#Hibernation](/index.php/Suspend_and_hibernate#Hibernation "Suspend and hibernate")) an issue may be encountered where the module required for the touchpad `elan_i2c` is not loaded on resuming, meaning that the touchpad won't be operable. A workaround for this is to enable the required module during the [initramfs stage](/index.php/Arch_boot_process#initramfs "Arch boot process").

 `/etc/mkinitcpio.conf` 
```
MODULES=(... elan_i2c ...)

```

After the recreating the initramfs image and rebooting the touchpad should now be working on resuming from hibernation.