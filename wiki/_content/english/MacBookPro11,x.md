Related articles

*   [Installation guide](/index.php/Installation_guide "Installation guide")
*   [General recommendations](/index.php/General_recommendations "General recommendations")
*   [MacBookPro10,x](/index.php/MacBookPro10,x "MacBookPro10,x")
*   [Mac](/index.php/Mac "Mac")

The MacBook Pro 11,x consists of models with Retina display shipped by Apple In Late 2013 and Mid 2014\. Like its predecessors, it is based on Intel chipset, although some manual configuration might be required in specific cases in order to deal with Apple-related features.

Like previous MacBook models, the MacBook Pro 11,x supports UEFI. This page will cover the current status of hardware support on Arch Linux, as well as post-installation recommendations.

## Contents

*   [1 Overview](#Overview)
*   [2 Firmware updates](#Firmware_updates)
*   [3 Partitioning](#Partitioning)
*   [4 Installation](#Installation)
    *   [4.1 Internet](#Internet)
*   [5 Setup bootloader](#Setup_bootloader)
*   [6 Post installation](#Post_installation)
    *   [6.1 Kernel parameters](#Kernel_parameters)
    *   [6.2 Fan control](#Fan_control)
    *   [6.3 Console](#Console)
    *   [6.4 Graphics](#Graphics)
        *   [6.4.1 Getting the integrated intel card to work on 11,3](#Getting_the_integrated_intel_card_to_work_on_11,3)
        *   [6.4.2 Alternative method to disable NVIDIA card](#Alternative_method_to_disable_NVIDIA_card)
    *   [6.5 Microcode](#Microcode)
    *   [6.6 HiDPI](#HiDPI)
    *   [6.7 Sound](#Sound)
    *   [6.8 Touchpad](#Touchpad)
        *   [6.8.1 Ctrl-Click as Right-Click](#Ctrl-Click_as_Right-Click)
        *   [6.8.2 input-mtrack](#input-mtrack)
    *   [6.9 Keyboard backlight](#Keyboard_backlight)
    *   [6.10 Screen backlight](#Screen_backlight)
    *   [6.11 Suspend](#Suspend)
    *   [6.12 Powersave](#Powersave)
    *   [6.13 SD Card Reader](#SD_Card_Reader)
    *   [6.14 Repurpose the power key](#Repurpose_the_power_key)
    *   [6.15 Web cam](#Web_cam)
*   [7 What does not work](#What_does_not_work)
    *   [7.1 General](#General)
    *   [7.2 Wi-Fi](#Wi-Fi)
    *   [7.3 Backlight keys / Suspend support](#Backlight_keys_/_Suspend_support)
*   [8 Discussions](#Discussions)
*   [9 See also](#See_also)

## Overview

Specifically, the procedure for installing Arch Linux on a MacBook is:

1.  [#Firmware updates](#Firmware_updates): It always helps to start from a clean, backed up, and up-to-date install of OS X.
2.  [#Partitioning](#Partitioning): Resizing or deleting the OS X partition to create partitions for Arch Linux.
3.  [#Setup bootloader](#Setup_bootloader): Making sure that the new partition is bootable.
4.  [#Installation](#Installation): Actually installing Arch Linux.
5.  [#Post installation](#Post_installation): MacBook-specific configuration.

## Firmware updates

Before proceeding with the installation of Arch Linux, it is important to ensure that the latest firmware updates for you MacBook are installed. This procedure requires OS X. In OS X, open the App Store and check for updates. If your Mac finds and installs any updates, make sure to **reboot** your computer, and then check again for updates to make sure that you installed everything.

**Note:** If you uninstalled OS X or want to reinstall it, [Apple](https://support.apple.com/en-us/HT204904) has great instructions.

It is advisable to keep OS X installed, because MacBook firmware updates can only be installed using OS X. However, if you plan to remove OS X completely, make backups of these files, which you will need in Linux for adjusting the color profile:

```
/Library/ColorSync/Profiles/Displays/*

```

## Partitioning

By default, the MacBook's drive is formatted using GPT and contains at least 3 partitions:

*   **EFI**: the ~200 MB [EFI system partition](/index.php/EFI_system_partition "EFI system partition").
*   **OS X**: the main partition containing your OS X installation. It is formatted using [HFS+](/index.php/File_systems "File systems").
*   **Recovery**: A recovery partition used for special purposes.

As a general rule, partitioning is no different from any other hardware that Arch Linux can be installed on. If you plan on keeping OS X for the purpose of dual booting, you need to manually shrink the main OS X HFS+ partition from within OS X's Disk Utility program.

**Note:** The OS X **Recovery partition** is not visible inside OS X `Disk Utility`. However, the partition will be automatically moved after the OS X partition if you resize it.

**Warning:** If your OS X partition is encrypted with FileVault 2, you **must** disable the disk encryption before proceeding. After the OS X partition has been resized, FileVault 2 can be re-enabled.

**Note:** If you plan to remove OS X, it is advisable to **disable** the MacBook startup sound before proceeding with partitioning. Just boot in OS X, mute your system sound and reboot again to the Arch Linux Installation media. Please keep in mind that the volume of the startup sound can only be modified reliably in OS X.

## Installation

Installation is similar to any other standard laptop. Please refer to the official [Installation guide](/index.php/Installation_guide "Installation guide"). The Apple boot manager is accessible by holding the `Alt` button during power on. As any other computer that does not have a CDROM drive, you need to use an [USB flash installation media](/index.php/USB_flash_installation_media "USB flash installation media").

As this model of notebook has a high DPI display, the console font displayed will be extremely small and depending on your preferences is likely to be uncomfortable to use. You may wish to change this for a more legible font, an example of which is;

```
$ setfont sun12x22

```

### Internet

Thunderbolt Ethernet adapters and USB-to-Ethernet adapters are usually picked up automatically. In case you use a Thunderbolt ethernet adapter, you may have to power on the machine with the adapter plugged in for it to be picked up by the system.

Another easy option is to use USB tethering with an Android device. For more information, see [Android tethering](/index.php/Android_tethering "Android tethering").

If you have neither, the only option is to use the onboard wireless adapter. Depending on your model, you may have the Broadcom BCM43602, which is supported by the open source brcmfac which is included by default in the kernel (see [here](/index.php/Broadcom_wireless#brcm80211 "Broadcom wireless")). If this is the case, you should have wireless available from the installer.

Unfortunately, other BCM43xx chipsets may only be supported by a [proprietary driver](/index.php/Broadcom_wireless "Broadcom wireless") which is unavailable in the installation environment. It is possible to build the package driver [broadcom-wl](https://www.archlinux.org/packages/?name=broadcom-wl) on a separate system, but it **must** be built against the exact same kernel version used by the installer. Build the package in a separate machine as follows:

```
$ curl -O [https://aur.archlinux.org/cgit/aur.git/snapshot/broadcom-wl.tar.gz](https://aur.archlinux.org/cgit/aur.git/snapshot/broadcom-wl.tar.gz)
$ tar -zxvf broadcom-wl.tar.gz
$ cd broadcom-wl
$ makepkg -s

```

**Note:** For older MacBooks the linked chipset will not work. Instead, use [b43-firmware](https://aur.archlinux.org/packages/b43-firmware/) by cloning the repository and then following the instructions above. You will then also need to use `modprobe b43` instead of `modprobe wl` in the steps below.

This will give you a package (`broadcom-wl-*.pkg.tar.xz`) which can be installed using [pacman](/index.php/Pacman "Pacman"). Put this package on a USB drive, mount it, and install the package using:

```
# pacman -U broadcom-wl-*.pkg.tar.xz
# rmmod b43
# rmmod ssb
# modprobe wl

```

You may now use `wifi-menu` to connect to your network of choice.

**Note:** The driver will need to be reinstalled after booting into the system for the first time. For more information, please see [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless"))

## Setup bootloader

MacBooks can be easily configured to use [systemd-boot](/index.php/Systemd-boot "Systemd-boot") or [GRUB](/index.php/GRUB "GRUB") directly from the Apple bootloader, without the need for third-party tools such as [rEFInd](/index.php/REFInd "REFInd"). Systemd-boot is the recommended way for systems that support UEFI.

*   First, make sure you mounted the EFI System Partition at `/boot` (that is within the chroot, so mount it as `/mnt/boot` with `mount /dev/sdXY /mnt/boot`)
*   Proceed with [Installation guide](/index.php/Installation_guide "Installation guide") normally
*   Once inside the chrooted enviroment, type the following command to install *systemd-boot*:

 `# bootctl --path=/boot install` 

The above command will copy the *systemd-boot* binary to `/boot/EFI/Boot/BOOTX64.EFI` and add *systemd-boot* itself as the default EFI application (default boot entry) loaded by the EFI Boot Manager.

*   Proceed to [systemd-boot#Configuration](/index.php/Systemd-boot#Configuration "Systemd-boot") in order to correctly set up the bootloader

At the next reboot, the Apple Boot Manager, shown when holding down the option key when booting the MacBook, should display Arch Linux (it will be displayed as `EFI Boot` as a possible boot option).

**Note:** If you wish to use GRUB, have a look at [Mac#Using the native Apple bootloader with GRUB](/index.php/Mac#Using_the_native_Apple_bootloader_with_GRUB "Mac").

**Tip:** After the installation, it is optionally possible to set a custom icon that will be displayed in the MacBook boot loader. In order to do that, you need to install the [wget](https://www.archlinux.org/packages/?name=wget), [librsvg](https://www.archlinux.org/packages/?name=librsvg) and [libicns](https://www.archlinux.org/packages/?name=libicns) packages. After that, just follow the following commands:
```
 $ wget -O /tmp/archlinux.svg [https://www.archlinux.org/logos/archlinux-icon-crystal-64.svg](https://www.archlinux.org/logos/archlinux-icon-crystal-64.svg)
 $ rsvg-convert -w 128 -h 128 -o /tmp/archlogo.png /tmp/archlinux.svg
 # png2icns /boot/.VolumeIcon.icns /tmp/archlogo.png
 $ rm /tmp/archlogo.png
 $ rm /tmp/archlinux.svg

```

Obviously, you can replace the Arch logo with any other icon you like.

**Tip:** If you installed Arch Linux alongside OS X, you will be able to change the default boot location from system Settings inside OS X. If Arch Linux does not show up as a possible boot option, you will have to mount the EFI System Partition inside OS X before selecting your boot option: `$ diskutil mount disk0s1` 

Keep in mind, however, it is also possible to load OS X from [systemd-boot](/index.php/Systemd-boot "Systemd-boot").

## Post installation

See [General recommendations](/index.php/General_recommendations "General recommendations") for system management directions and post-installation tutorials.

Additionally, you might want to have a look at the [Power management](/index.php/Power_management "Power management") page for useful tips in power management and battery-saving software.

### Kernel parameters

**Warning:** Since Kernel version 4.17.2-1 adding `acpi_osi` parameter with an empty value causes battery to be undetectable. See this [forum thread](https://bbs.archlinux.org/viewtopic.php?id=238194) for more information. It's required to specify `acpi_osi=Darwin` as a kernel boot parameter in order to let suspension/hibernation work properly.

Due to [this bug](https://bugzilla.kernel.org/show_bug.cgi?id=177151), it might be required to add `acpi_osi=` as a kernel boot parameter in order to improve battery life.

Due to [this bug](https://bugzilla.kernel.org/show_bug.cgi?id=117481), it may be necessary to disable GPE06 by adding `acpi_mask_gpe=0x06` as a kernel boot parameter. To verify that this is required, check `cat /sys/firmware/acpi/interrupts/gpe06`. There should be a rapidly increasing number of interrupts registered, and one of your cores should be pegged at 100%.

### Fan control

Install [mbpfan-git](https://aur.archlinux.org/packages/mbpfan-git/) or [macfanctld](https://aur.archlinux.org/packages/macfanctld/) and [enable](/index.php/Enable "Enable") the mbpfan.service in order to prevent laptop overheating.

### Console

Largest console font can be achieved by adding `FONT=sun12x22` to `/etc/vconsole.conf`:

 `# nano /etc/vconsole.conf` 
```
...
FONT=sun12x22
```

### Graphics

MacBook Pro with integrated Intel graphics and no discrete GPU are supported out of the box. See [Intel graphics](/index.php/Intel_graphics "Intel graphics") for additional details and configuration options.

Versions which include a discrete Nvidia GPU should need additional configuration:

*   MacBook Pro 11,3:
    *   nvidia drivers work, see [NVIDIA](/index.php/NVIDIA "NVIDIA") or [Nouveau](/index.php/Nouveau "Nouveau"). In case you use the proprietary driver, see the following link [[1]](http://cberner.com/2013/03/01/installing-ubuntu-13-04-on-macbook-pro-retina/) for additional details.
    *   It is possible to configure the integrated intel GPU, provided you are using [GRUB](/index.php/GRUB "GRUB") as your bootloader of choice. See below for details
*   MacBook Pro 11,5
    *   The [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) package seems to be stable. Switching to VTs and back works fine from MATE and GNOME. SOmetimes Chromium causes a "kernele rejected pixbuf" error which freezes the desktop.
    *   The [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms) driver has been crashing a lot.
    *   The [nvidia](https://www.archlinux.org/packages/?name=nvidia) driver seems to be super stable, but GNOME desktop won't like to start, showing you a "Oh no! Something has gone wrong" message. Cinnamon Desktop is buttery smooth with the nvidia driver, and if you want your GNOME desktop, you can run `gnome-shell --relace &` while in cinnamon desktop to switch to Gnome Shell as a workaround.

Note that the video output ports (HDMI and DisplayPort) are hardwired to the Nvidia GPU, so they will not work if you use the Intel GPU and power off the Nvidia GPU. Switching GPUs requires a reboot, so if you primarily keep the laptop docked at a desk, configuring switchable graphics may not be worth the hassle of setting it up and then rebooting every time you need to switch. However, the Nvidia GPU does use significantly more power than the Intel one, so you will take a significant hit to battery life.

#### Getting the integrated intel card to work on 11,3

By default the integrated card is powered off. To fix this we need a grub function called "apple_set_os". This function has not officially been merged yet, so we need to build grub ourselves. Download the [grub-git](https://aur.archlinux.org/packages/grub-git/) package from the AUR. Using something like:

```
$ packer -G grub-git
$ cd grub-git

```

Get the patch from [[2]](http://lists.gnu.org/archive/html/grub-devel/2013-12/msg00442.html).

Put the patch contents into a file labeled something like "apple.patch"

Add this patch to your PKGBUILD and run:

```
$ makepkg -si

```

Reboot into OS X and download gfxCardStatus v2.2.1 (newer versions do not work properly) run the app and specify the integrated card.

Reboot and at the grub prompt type 'c' to get into console, followed by "apple_set_os" at the prompt.

You should now be able to install [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) and get your card running.

Note that the HDMI port and MiniDP are soldered to the nvidia card meaning that to run external displays you need to use the dedicated card.

#### Alternative method to disable NVIDIA card

While the above method for switching graphics works, there is a more effective method that does not require the use of gfxCardStatus or a patched GRUB installation (but it can be used if desired).

First, the Intel GPU will not function without a patch called apple_set_os. You can either use a patched GRUB (as seen above) or use the apple_set_os.efi patch via rEFInd or chainload it via GRUB, the EFI patch can be download here, [https://github.com/0xbb/apple_set_os.efi](https://github.com/0xbb/apple_set_os.efi), this tricks the machine into thinking that it is booting a Mac OS X installation, making the hardware behave as such, allowing the Intel GPU to be used. rEFInd should automatically detect the patch as described on the application page. This will need to be loaded before each boot of Arch or else the Intel GPU will not function, to load it automatically it can be chainloaded via GRUB. Also, download and install the Intel drivers as described above.

Then you will need to download an application called gpu-switch for switching the GPU on dual MacBook Pros, it is fairly easy to use as well. It can be downloaded from here, [https://github.com/0xbb/gpu-switch](https://github.com/0xbb/gpu-switch).

Secondly, once you have downloaded gpu-switch, extract the application to your home directory and open up a terminal emulator and cd to that directory. To switch to the Intel graphics, run `gpu-switch -i` as sudo, and the card will be active on reboot. Conversely, to enable the dedicated card instead, run `gpu-switch -d` as sudo. You must have booted with the aforementioned patch for this to work.

Next, gpu-switch will not completely power down the dedicated card. To do that, you will have to create a custom grub menuentry and compile a program that will power off the dedicated card.

To do that, please refer to the following article, [MacBookPro10,x#Graphics_2](/index.php/MacBookPro10,x#Graphics_2 "MacBookPro10,x").

You should now have working integrated graphics and the dedicated GPU should now power down. If you get a blank screen after doing this, wait and see what happens, if it stays blank for a prolonged period of time, try resetting the SMC, and then booting back into Arch.

I noticed that afterwards VGA switcheroo disabled the nouveau driver, if this workaround still does not work, try installing a cronjob package, and adding the following:

`@reboot echo OFF > /sys/kernel/debug/vgaswitcheroo/switch` `@reboot echo IGD > /sys/kernel/debug/vgaswitcheroo/switch`

I'm not sure if the vgaswitcheroo commands actually do anything, I need somebody to test this workaround and let me know how it works for them.

To see if you dedicated GPU is actually disabled, run:

```
# cat /sys/kernel/debug/vgaswitcheroo/switch

```

**Note:** gpu-switch has been tested only on a select few models, those being MacBookPro9,1, MacBookPro10,1, and MacBookPro11,3\. Use at your own risk.

### Microcode

You may need to install [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode), especially if you have Nvidia drivers. Read the wiki page to learn more about [Microcode](/index.php/Microcode "Microcode").

### HiDPI

See [HiDPI](/index.php/HiDPI "HiDPI") for information on how to tweak the system for a Retina screen.

### Sound

*   Headphones work
*   Speakers work (tested with kernel 4.8)

If you do not want to hear the annoying sound at system start-up, one way to get rid of it is to turn sound off while under Mac OS.

Volume keys can be made to work with `xfce4-volumed` (if you are using Xfce).

Also, if you are using PulseAudio, sometimes it thinks HDMI is the default sound card; to solve this problem, install [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) and set Analog Stereo as the fallback device.

### Touchpad

One method is to install [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) and configure to your liking in `/etc/X11/xorg.conf.d/50-synaptics.conf`:

```
Section "InputClass"
    MatchIsTouchpad "on"
    Identifier      "touchpad catchall"
    Driver          "synaptics"
    # 1 = left, 2 = right, 3 = middle
    Option          "TapButton1" "1"  
    Option          "TapButton2" "3"
    Option          "TapButton3" "2"
    # Palm detection
    Option          "PalmDetect" "1"
    # Horizontal scrolling
    Option "HorizTwoFingerScroll" "1"
    # Natural Scrolling (and speed)
    Option "VertScrollDelta" "-100"
    Option "HorizScrollDelta" "-100"
EndSection

```

#### Ctrl-Click as Right-Click

Using this SuperUser receipt [[3]](http://superuser.com/questions/217615/how-to-right-click-using-the-keyboard-from-ubuntu-on-a-mac) I got Ctrl-click working as right-click. I had to increase the sleep time to 0.1 though.

#### input-mtrack

Another method is to use [xf86-input-mtrack-git](https://aur.archlinux.org/packages/xf86-input-mtrack-git/). If you like to have a thumb resting on the touchpad, this driver is the right choice, because it has an option for IgnoreThumb.

With this config the touchpad behavior becomes more osx-like.

```
/etc/X11/xorg.conf.d/00-touchpad.conf

```

```
Section "InputClass"
    MatchIsTouchpad "on"
    Identifier      "Touchpads"
    Driver          "mtrack"
    Option          "Sensitivity" "0.64"
    Option          "FingerHigh" "5"
    Option          "FingerLow" "1"
    Option          "IgnoreThumb" "true"
    Option          "IgnorePalm" "true"
    Option          "DisableOnPalm" "true"
    Option          "TapButton1" "1"
    Option          "TapButton2" "3"
    Option          "TapButton3" "2"
    Option          "TapButton4" "0"
    Option          "ClickFinger1" "1"
    Option          "ClickFinger2" "2"
    Option          "ClickFinger3" "3"
    Option          "ButtonMoveEmulate" "false"
    Option          "ButtonIntegrated" "true"
    Option          "ClickTime" "25"
    Option          "BottomEdge" "30"
    Option          "SwipeLeftButton" "8"
    Option          "SwipeRightButton" "9"
    Option          "SwipeUpButton" "0"
    Option          "SwipeDownButton" "0"
    Option          "ScrollDistance" "75"
    Option          "VertScrollDelta" "-111"
    Option          "HorizScrollDelta" "-111"
EndSection

```

### Keyboard backlight

*   Works, see [Mac#Keyboard Backlight](/index.php/Mac#Keyboard_Backlight "Mac")
*   On KDE controlling the backlight with the increase or decrease brightness keys work fine, but they need upower to start before the desktop. To do this create the file `/etc/systemd/system/kdm.service.d/kbd_backlight.conf` with this content (you might need to create the directory as well)

```
[Unit]
Requires=upower.service
After=upower.service

```

### Screen backlight

*   Intel, works on Linux 3.13
*   Framebuffer, works for MacBook Pro 11,1 and 11,3 via `/sys/class/backlight/gmux_backlight/brightness`.
*   Brightness in `/sys/class/backlight/gmux_backlight/brightness` can be modified comfortably via the [gmux_backlight](https://aur.archlinux.org/packages/gmux_backlight/) utility without root privileges. Requires the `setpci` setting below.
*   Nvidia, does not work using default settings. Try executing as root `setpci -v -H1 -s 00:01.00 BRIDGE_CONTROL=0`. It may be worthwhile to create a systemd unit to execute this on boot.
*   AMD models may require a patched kernel for the backlight to be adjusted. The [linux-macbook](https://aur.archlinux.org/packages/linux-macbook/) kernel fixes this.

**Note:** If the screen does not show the prompt or the login manager (i.e. a black screen), append `i915.invert_brightness=1` to the kernel.

### Suspend

*   Works from Linux 3.13
    *   It may be necessary to disable USB's wakeup ability by by echoing 'XHC1' to '/proc/acpi/wakeup' in order to prevent immediate wakeup on suspend.
*   No backlight after suspend with Linux 3.12
    *   Use hibernate instead

### Powersave

Disabling the internal cardreader and bluetooth controller may save battery life. When not using them, create the following [udev](/index.php/Udev "Udev") rules:

 `/etc/udev/rules.d/99-apple_cardreader.rules`  `SUBSYSTEMS=="usb", ATTRS{idVendor}=="05ac", ATTRS{idProduct}=="8406", RUN+="/usr/local/sbin/remove_ignore_usb-device.sh 05ac 8406"`  `/etc/udev/rules.d/99-apple_broadcom_bcm2046_bluetooth.rules` 
```
SUBSYSTEMS=="usb", ATTRS{idVendor}=="05ac", ATTRS{idProduct}=="8289", RUN+="/usr/local/sbin/remove_ignore_usb-device.sh 05ac 8289"
SUBSYSTEMS=="usb", ATTRS{idVendor}=="0a5c", ATTRS{idProduct}=="4500", RUN+="/usr/local/sbin/remove_ignore_usb-device.sh 0a5c 4500"
```

As udev's `OPTIONS=="ignore_device"` may not work reliably, the above rules use [a script](https://gist.github.com/anonymous/9c9d45c4818e3086ceca) to manually remove the usb device from `/sys/bus/usb/devices/`.

If battery life is not satisfactory, it may help to use power saving utilities, such as [tlp](https://www.archlinux.org/packages/?name=tlp), and/or [powertop](https://www.archlinux.org/packages/?name=powertop) from the official repositories. To better optimize battery life, TLP also has a configuration file located at `/etc/default/tlp` that you can edit to suit your machine. For more information, visit the wiki pages for these tools, [TLP](/index.php/TLP "TLP") and [Powertop](/index.php/Powertop "Powertop"), respectively.

### SD Card Reader

*   Disappears sporadically after suspend as of Linux 3.18\. Workaround is to create `/etc/modprobe.d/xhci-reset-on-suspend.conf` with:

```
  # Reset XHCI USB devices on suspend/resume, fixes SD Card reader vanishing after suspend 
  options xhci_hcd quirks=0x80

```

Note: As of Linux 3.18.6-1 (and possibly earlier versions post-3.18), this fix **may** not be needed and might cause issues ranging from failed suspend to the SD card not being recognized at all. Test with and without the fix to determine which works best for you.

### Repurpose the power key

By default systemd handles the rMBPs power key as defined in /etc/systemd/logind.conf. By setting

```
   HandlePowerKey=ignore

```

systemd ignores power key events.

Now the power key can be repurposed as keycode 124\. For example in i3 conf:

```
   bindcode 124 ...

```

### Web cam

A reverse engineered driver is being developed here: [https://github.com/patjak/bcwc_pcie/](https://github.com/patjak/bcwc_pcie/) . It is marked experimental, but basic functionality seems to be working. Install [bcwc-pcie-dkms](https://aur.archlinux.org/packages/bcwc-pcie-dkms/) or [bcwc-pcie-git](https://aur.archlinux.org/packages/bcwc-pcie-git/).

## What does not work

Updated 2016-07-21

### General

### Wi-Fi

*   [broadcom-wl](https://www.archlinux.org/packages/?name=broadcom-wl) or [broadcom-wl-dkms](https://www.archlinux.org/packages/?name=broadcom-wl-dkms) from the [AUR](/index.php/AUR "AUR") works
    *   Stability is an issue for some, look at [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless") for possible fixes (e.g. downgrading kernel works if your card is BCM4360)
    *   If stability is still an issue after the above, a possible alternative is to connect on a 802.11g network. More recent standards can cause the BCM4360 to disconnect randomly.

### Backlight keys / Suspend support

[linux-macbook](https://aur.archlinux.org/packages/linux-macbook/) is an AUR package created specifically for MacBook laptops that includes patches for these issues, as well fixing powering off correctly and CPU frequency scaling with the intel_pstate driver.

## Discussions

*   [https://bbs.archlinux.org/viewtopic.php?id=171883](https://bbs.archlinux.org/viewtopic.php?id=171883)

## See also

*   [MacBookPro10,x](/index.php/MacBookPro10,x "MacBookPro10,x")
*   [Mac](/index.php/Mac "Mac")