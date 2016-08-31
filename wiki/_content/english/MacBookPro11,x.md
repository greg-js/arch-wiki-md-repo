The MacBook Pro 11,x consists of models with Retina display shipped by Apple In Late 2013 and Mid 2014\. Like its predecessors, it is based on Intel chipset, although some manual configuration might be required in specific cases in order to deal with Apple-related features.

Like previous MacBook models, the MacBook Pro 11,x supports UEFI. This page will cover the current status of hardware support on Arch Linux, as well as post-installation recommendations.

## Contents

*   [1 Preparing for the Installation](#Preparing_for_the_Installation)
    *   [1.1 Firmware updates](#Firmware_updates)
    *   [1.2 Partitioning](#Partitioning)
*   [2 Installation](#Installation)
    *   [2.1 Booting the live image](#Booting_the_live_image)
    *   [2.2 Console](#Console)
    *   [2.3 Internet](#Internet)
        *   [2.3.1 Wired](#Wired)
        *   [2.3.2 Wireless](#Wireless)
    *   [2.4 Bootloader](#Bootloader)
*   [3 Post installation](#Post_installation)
    *   [3.1 Console](#Console_2)
    *   [3.2 Graphics](#Graphics)
        *   [3.2.1 MacBook Pro 11,1](#MacBook_Pro_11.2C1)
        *   [3.2.2 MacBook Pro 11,2](#MacBook_Pro_11.2C2)
        *   [3.2.3 MacBook Pro 11,3](#MacBook_Pro_11.2C3)
        *   [3.2.4 MacBook Pro 11,5](#MacBook_Pro_11.2C5)
        *   [3.2.5 Microcode](#Microcode)
        *   [3.2.6 HiDPI](#HiDPI)
        *   [3.2.7 Xfce](#Xfce)
        *   [3.2.8 lightdm](#lightdm)
        *   [3.2.9 MATE](#MATE)
        *   [3.2.10 GNOME](#GNOME)
        *   [3.2.11 Getting the integrated intel card to work on 11,3](#Getting_the_integrated_intel_card_to_work_on_11.2C3)
        *   [3.2.12 Alternative method to disable NVIDIA card](#Alternative_method_to_disable_NVIDIA_card)
    *   [3.3 Sound](#Sound)
    *   [3.4 Touchpad](#Touchpad)
        *   [3.4.1 Ctrl-Click as Right-Click](#Ctrl-Click_as_Right-Click)
        *   [3.4.2 input-mtrack](#input-mtrack)
    *   [3.5 Keyboard backlight](#Keyboard_backlight)
    *   [3.6 Screen backlight](#Screen_backlight)
    *   [3.7 Suspend](#Suspend)
    *   [3.8 Powersave](#Powersave)
    *   [3.9 SD Card Reader](#SD_Card_Reader)
    *   [3.10 Repurpose the power key](#Repurpose_the_power_key)
    *   [3.11 Web cam](#Web_cam)
*   [4 What does not work](#What_does_not_work)
    *   [4.1 General](#General)
    *   [4.2 Wi-Fi](#Wi-Fi)
    *   [4.3 Backlight keys / Suspend support](#Backlight_keys_.2F_Suspend_support)
*   [5 Discussions](#Discussions)
*   [6 See also](#See_also)

## Preparing for the Installation

### Firmware updates

Before proceeding with the installation of Arch Linux, it is important to ensure that the latest firmware updates for you MacBook are installed. This procedure requires OS X. In OS X, open the App Store and check for updates. If your mac finds and installs any updates, make sure to **reboot** your computer, and then check again for updates to make sure that you installed everything.

**Note:** If you uninstalled OS X or want to reinstall it, [Apple](https://support.apple.com/en-us/HT204904) has great instructions.

It is advisable to keep OS X installed, because MacBook firmware updates can only be installed using OS X. However, if you plan to remove OS X completely, make backups of these files, which you will need in Linux for adjusting the [color profile](#Color_Profile):

```
/Library/ColorSync/Profiles/Displays/*

```

### Partitioning

By default, the MacBook's drive is formatted using GPT and contains at least 3 partitions:

*   **EFI**: the ~200 MB [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition").
*   **OS X**: the main partition containing your OS X installation. It is formatted using [HFS+](/index.php/File_systems "File systems").
*   **Recovery**: A recovery partition used for special purposes.

As a general rule, partitioning is no different from any other hardware that Arch Linux can be installed on. If you plan on keeping OS X for the purpose of dual booting, you need to manually shrink the main OS X HFS+ partition from within OS X's Disk Utility program.

**Note:** The OS X **Recovery partition** is not visible inside OS X `Disk Utility`. However, the partition will be automatically moved after the OS X partition if you resize it.

**Warning:** If you OS X partition is encrypted with FileVault 2, you **must** disable the disk encryption before proceeding. After the OS X partition has been resized, FileVault 2 can be re-enabled.

**Note:** If you plan to remove OS X, it is advisable to **disable** the MacBook startup sound before proceeding with partitioning. Just boot in OS X, mute your system sound and reboot again to the Arch Linux Installation media. Please keep in mind that the volume of the startup sound can only be modified reliably in OS X.

## Installation

### Booting the live image

The Apple boot manager is accessible by holding the `Alt` button during power on. As any other computer that does not have a CDROM drive, you need to use an [USB flash installation media](/index.php/USB_flash_installation_media "USB flash installation media"). After booting, please refer to the official [Installation guide](/index.php/Installation_guide "Installation guide").

### Console

As this model of notebook has a high DPI display, the console font displayed will be extremely small and depending on your preferences is likely to be uncomfortable to use. You may wish to change this for a more legible font, an example of which is;

```
$ setfont sun12x22

```

If you want to make this change permanent, add the following line to `/etc/vconsole.conf`

```
 FONT=sun12x22

```

### Internet

#### Wired

Thunderbolt Ethernet adapters and USB-to-Ethernet adapters should be picked up automatically.

**Note:** You may have to power on the machine with the Thunderbolt Ethernet adapter plugged in for it to be picked up initially.

#### Wireless

As mentioned below, `broadcom-wl` is sufficient if you are using the Linux mainline kernel. For custom kernels, you need to use `broadcom-wl-dkms`. Both are available from the [AUR](/index.php/AUR "AUR"). The easiest way to get Wi-Fi connectivity during install is to build the package driver on a separate system. Note that it does have to be built against the exact same kernel version as used by the installer, and this may differ from the latest version. If built against the wrong kernel you may encounter an error *(ERROR: could not insert 'wl': Invalid argument)* upon modprobe. Build the package as follows:

```
$ curl -O [https://aur.archlinux.org/cgit/aur.git/snapshot/broadcom-wl-dkms.tar.gz](https://aur.archlinux.org/cgit/aur.git/snapshot/broadcom-wl-dkms.tar.gz)
$ tar -zxvf broadcom-wl-dkms.tar.gz
$ cd broadcom-wl-dkms
$ makepkg -s

```

This will give you a package (`broadcom-wl-*.pkg.tar.xz`) which can be installed using [pacman](/index.php/Pacman "Pacman"). Put this package on a USB drive, mount it, and install the package using:

```
# pacman -U broadcom-wl-*.pkg.tar.xz
# modprobe wl

```

You may now use `wifi-menu` to connect to your network of choice.

**Note:** You need to repeat this process when you have finished your installation and booting into the system for the first time. If kernel versions differ, you may want to ensure to install a number of essential packages while you have connectivity and before you boot into your system, these allow you to build the broadcom driver again and connect (provided you put the AUR tarball for the driver on USB drive too): [dkms](https://www.archlinux.org/packages/?name=dkms),[wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant), [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) ([dialog](https://www.archlinux.org/packages/?name=dialog) and [netctl](https://www.archlinux.org/packages/?name=netctl) are needed if you want to use `wifi-menu` again after you boot)

### Bootloader

MacBooks can be easily configured to use [systemd-boot](/index.php/Systemd-boot "Systemd-boot") or [GRUB](/index.php/GRUB "GRUB") directly from the Apple bootloader, without the need for third-party tools such as [rEFInd](/index.php/REFInd "REFInd"). Systemd-boot is the recommended way for systems that support UEFI.

*   First, make sure you mounted the EFI System Partition at `/boot`
*   Proceed with [Installation](/index.php/Installation_guide "Installation guide") normally
*   Once inside the chrooted enviroment, type the following command to install *systemd-boot*:

 `# bootctl --path=/boot install` 

The above command will copy the *systemd-boot* binary to `/boot/EFI/Boot/BOOTX64.EFI` and add *systemd-boot* itself as the default EFI application (default boot entry) loaded by the EFI Boot Manager.

*   Proceed to [systemd-boot#Configuration](/index.php/Systemd-boot#Configuration "Systemd-boot") in order to correctly set up the bootloader

At the next reboot, the Apple Boot Manager, shown when holding down the option key when booting the MacBook, should display Arch Linux (it will be displayed as `EFI Boot` as a possible boot option).

**Note:** If you wish to use GRUB, have a look at the [MacBook](/index.php/MacBook#Using_the_native_Apple_bootloader_with_GRUB "MacBook") page.

**Tip:** If you installed Arch Linux alongside OS X, you will be able to change the default boot location from system Settings inside OS X. If Arch Linux does not show up as a possible boot option, you will have to mount the EFI System Partition inside OS X before selecting your boot option: `$ diskutil mount disk0s1` 

Keep in mind, however, it is also possible to load OS X from [systemd-boot](/index.php/Systemd-boot "Systemd-boot").

## Post installation

### Console

Largest console font can be achieved by adding `FONT=sun12x22` to `/etc/vconsole.conf`:

 `# nano /etc/vconsole.conf` 
```
...
FONT=sun12x22
```

### Graphics

###### MacBook Pro 11,1

*   Works, see [Intel graphics](/index.php/Intel_graphics "Intel graphics")

###### MacBook Pro 11,2

*   Intel works from 3.13.4-1-ARCH

###### MacBook Pro 11,3

*   Nvidia works (both 319.60 and 331.17 drivers)
    *   Follow [http://cberner.com/2013/03/01/installing-ubuntu-13-04-on-macbook-pro-retina/](http://cberner.com/2013/03/01/installing-ubuntu-13-04-on-macbook-pro-retina/)
*   Intel works after patching grub, see below

###### MacBook Pro 11,5

*   The [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) package seems to be stable. Switching to VTs and back works fine from MATE and GNOME. SOmetimes Chromium causes a "kernele rejected pixbuf" error which freezes the desktop.
*   The [nvidia-dkms](https://aur.archlinux.org/packages/nvidia-dkms/) driver has been crashing a lot.
*   The [nvidia](https://www.archlinux.org/packages/?name=nvidia) driver seems to be super stable, but GNOME desktop won't like to start, showing you a "Oh no! Something has gone wrong" message. Cinnamon Desktop is buttery smooth with the nvidia driver, and if you want your GNOME desktop, you can run `gnome-shell --relace &` while in cinnamon desktop to switch to Gnome Shell as a workaround.

###### Microcode

You may need to install [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode), especially if you have Nvidia drivers. Read the wiki page to learn more about [Microcode](/index.php/Microcode "Microcode").

###### HiDPI

See [HiDPI](/index.php/HiDPI "HiDPI") for information on how to tweak the system for a Retina screen.

###### Xfce

If you are using [Xfce](/index.php/Xfce "Xfce"), you will probably experience tearing in Firefox, VLC, etc. Until newer versions of xfwm support OpenGL rendering, use another compositing window manager like [compton](/index.php/Compton "Compton") with `backend = "glx"`.

###### lightdm

If you are using lightdm on HiDPI/Retina screens you may experience a small login box , to use the native resolution of 2560x1600 on the login screen create a script

```
  #!/bin/sh
  xrandr --output eDP1 --primary --mode 2560x1600

```

and set it as display-setup-script in /etc/lightdm/lightdm.conf

###### MATE

MATE's Marco seems to have problems. Replace it with GNOME's Mutter for nice animated effects. This works best with the nouveau driver.

```
# mutter --replace &&

```

Or configure MATE to use Mutter in dconf...

###### GNOME

It all works great out of the box with the nouveau driver.

#### Getting the integrated intel card to work on 11,3

By default the integrated card is powered off. To fix this we need a grub function called "apple_set_os". This function has not officially been merged yet, so we need to build grub ourselves. Download the [grub-git](https://aur.archlinux.org/packages/grub-git/) package from the AUR. Using something like:

```
$ packer -G grub-git
$ cd grub-git

```

Get the patch from here: [http://lists.gnu.org/archive/html/grub-devel/2013-12/msg00442.html](http://lists.gnu.org/archive/html/grub-devel/2013-12/msg00442.html)

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

### Sound

*   Headphones work
*   Speakers work from kernel 3.13 and 3.12.2\. 3.12.1 only with patch
    *   Patch: [https://bugzilla.kernel.org/attachment.cgi?id=114081](https://bugzilla.kernel.org/attachment.cgi?id=114081).
    *   See discussion here: [https://bugzilla.kernel.org/show_bug.cgi?id=64401](https://bugzilla.kernel.org/show_bug.cgi?id=64401)
*   Optical audio can be turned off and on with above sound patch.

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

Using this SuperUser receipt [[1]](http://superuser.com/questions/217615/how-to-right-click-using-the-keyboard-from-ubuntu-on-a-mac) I got Ctrl-click working as right-click. I had to increase the sleep time to 0.1 though.

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

*   Works, see [MacBook#Keyboard_Backlight](/index.php/MacBook#Keyboard_Backlight "MacBook")
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
*   Nvidia, does not work using default settings. Try adding `setpci -v -H1 -s 00:01.00 BRIDGE_CONTROL=0` to `/etc/rc.local`.

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

*   [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/) or [broadcom-wl-dkms](https://aur.archlinux.org/packages/broadcom-wl-dkms/) from the [AUR](/index.php/AUR "AUR") works
    *   Stability is an issue for some, look at [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless") for possible fixes (e.g. downgrading kernel works if your card is BCM4360)

### Backlight keys / Suspend support

[linux-macbook](https://aur.archlinux.org/packages/linux-macbook/) is an AUR package created specifically for MacBook laptops that includes patches for these issues, as well fixing powering off correctly and CPU frequency scaling with the intel_pstate driver.

## Discussions

*   [https://bbs.archlinux.org/viewtopic.php?id=171883](https://bbs.archlinux.org/viewtopic.php?id=171883)

## See also

*   [MacBookPro10,x](/index.php/MacBookPro10,x "MacBookPro10,x")
*   [MacBook](/index.php/MacBook "MacBook")