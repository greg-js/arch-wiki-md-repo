[GPD Win](https://www.indiegogo.com/projects/gpd-win-intel-z8700-win-10-os-game-console-laptop#/) is a small (5.5 inch screen) handheld device.

## Contents

*   [1 Fixes](#Fixes)
    *   [1.1 Built-in Wi-Fi](#Built-in_Wi-Fi)
    *   [1.2 Battery monitoring](#Battery_monitoring)
    *   [1.3 Rotating X Session](#Rotating_X_Session)
    *   [1.4 Rotating touch screen](#Rotating_touch_screen)
    *   [1.5 Fixing occasional crash when using all cores](#Fixing_occasional_crash_when_using_all_cores)
    *   [1.6 Sound](#Sound)
    *   [1.7 Memory card reader](#Memory_card_reader)
    *   [1.8 Physical power and volume buttons](#Physical_power_and_volume_buttons)
    *   [1.9 Adjusting screen brightness](#Adjusting_screen_brightness)
    *   [1.10 Suspend/resume/waking up when opening the lid](#Suspend.2Fresume.2Fwaking_up_when_opening_the_lid)
*   [2 Installation guide](#Installation_guide)
    *   [2.1 Boot the installer](#Boot_the_installer)
    *   [2.2 Formating and mounting partitions for dual booting with Windows 10](#Formating_and_mounting_partitions_for_dual_booting_with_Windows_10)
    *   [2.3 Install Arch Linux](#Install_Arch_Linux)
    *   [2.4 Install bootloader](#Install_bootloader)

## Fixes

**Things not mentioned below should work out-of-the-box.**

#### Built-in Wi-Fi

Before [Linux Bug 185661](https://bugzilla.kernel.org/show_bug.cgi?id=185661) is resolved, a fix is needed to get built-in Wi-Fi working. Current solution is to grab **brcmfmac4356-pcie.txt** from [here](https://chromium.googlesource.com/chromiumos/third_party/linux-firmware/+/f151f016b4fe656399f199e28cabf8d658bcb52b/brcm/brcmfmac4356-pcie.txt) and drop it into **/lib/firmware/brcm** and reload the **brcmfmac** module.

**Note:** The "txt" button at the bottom right corner of the web page does not download the correct file. You need to manually copy and paste the content to brcmfmac4356-pcie.txt.

Easiest way to get built-in Wi-Fi working on the Arch Linux installer is, from Windows 10, download the file above to C:\. Then from the installer do the following:

Make a directory and mount the Windows 10 partition (**Replace mmcblk0p2 with your Windows 10 partition found by running lsblk**)

```
mkdir windows
mount /dev/mmcblk0p2 windows

```

Copy the file

```
cp windows/brcmfmac4356-pcie.txt /lib/firmware/brcm

```

Reload the module

```
modprobe -r brcmfmac
modprobe brcmfmac

```

Connect to Wi-Fi

```
wifi-menu

```

#### Battery monitoring

Works out of the box since kernel 4.12. Earlier kernels require [Hans de Goede's patched kernel](http://hansdegoede.livejournal.com/17445.html). His kernel will also fix "Not charging when the power cable gets plugged in after boot" and "Only drawing max 0.5A from the charger, charging slowly if at all".

#### Rotating X Session

Because the device uses a phone screen, the display has to be rotated to function properly. Since kernel 4.9.2, rotating X session (manually with [xrandr](/index.php/Xrandr "Xrandr") or within settings of a desktop environment) works out-of-the-box. (NB: before investing too much time (or buying the device) it is worth noting there may be idiosyncrasies in the gpdwin batches. Running 4.9.11-1 (March 7, 2017) did not fix the screen rotation issue on my gpdwin.).

If you are using Gnome and finding that everything is upscaled, you can restore scaling by running:

```
$ gsettings set org.gnome.desktop.interface scaling-factor 1

```

#### Rotating touch screen

Since kernel 4.9.2, rotating X session will automatically rotate touch screen (so far, only tested with gnome-control-center). If not able to rotate, running the following command might work for you, but results seems to differ for people.

```
xinput set-prop 'Goodix Capacitive TouchScreen' 'Coordinate Transformation Matrix' -1 0 1 0 -1 1 0 0 1

```

#### Fixing occasional crash when using all cores

Turbo Boost on this CPU is software-controlled and the Linux kernel (4.4) is not throttling down the CPU enough, running at or close to 2.4Ghz the whole time even with 4 cores active which crashes the CPU eventually. Disabling the Turbo Boost feature ("Turbo Mode" in the BIOS) fixed those crashes. More info [here](https://www.reddit.com/r/gpdwin/comments/5o2m1v/solved_linux_44_crashing_when_using_all_4_cores/).

#### Sound

Works out of the box with latest and [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) kernel. Headphone jack works but currently requires [Hans de Goede's patched kernel](http://hansdegoede.livejournal.com/17445.html).

#### Memory card reader

Works out of the box with latest and [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) kernel.

#### Physical power and volume buttons

Works but currently requires [Hans de Goede's patched kernel](http://hansdegoede.livejournal.com/17445.html).

#### Adjusting screen brightness

Works but currently requires [Hans de Goede's patched kernel](http://hansdegoede.livejournal.com/17445.html).

#### Suspend/resume/waking up when opening the lid

Works but currently requires [Hans de Goede's patched kernel](http://hansdegoede.livejournal.com/17445.html).

## Installation guide

#### Boot the installer

Reboot holding either **"Del"** or **"Esc"** to enter BIOS. From the BIOS screen, either change the boot options to prioritize your usb drive or boot from it once.

On the Arch Linux boot option screen, with the first option highlighted, click **"e"** to edit boot options and add **"i915.fastboot=1"** to avoid black screen on boot and **"fbcon=rotate:1"** for screen to be rotated correctly.

#### Formating and mounting partitions for dual booting with Windows 10

Use "Disk Management" in Windows or similar tools to shrink the Windows 10 partition and use the space to create a new partition for Arch Linux.

Run lsblk to list partitions and note the numbers for the following partitions:

*   (**X**) Windows Boot Loader, a 100MB partition
*   (**Y**) Windows 10 partition
*   (**Z**) New Linux partition

Format the new Linux partition and mount it

```
mkfs.ext4 /dev/mmcblk0p**Z**
mount /dev/mmcblk0p**Z** /mnt

```

Create boot directory and mount Windows Boot Loader

```
mkdir /mnt/boot
mount /dev/mmcblk0p**X** /mnt/boot

```

#### Install Arch Linux

Install base system

```
pacstrap -i /mnt base base-devel

```

Copy the file from the Wi-Fi fix to the new installation

```
cp /lib/firmware/brcm/brcmfmac4356-pcie.txt /mnt/lib/firmware/brcm

```

Continue by following [the regular install guide](/index.php/Installation_guide#Configure_the_system "Installation guide") until bootloader step, then continue below.

#### Install bootloader

Install bootloader

```
bootctl install

```

Create and fill **/boot/loader/entries/arch.conf**

**Note:** If you use [linux-lts](https://www.archlinux.org/packages/?name=linux-lts), replace **/vmlinuz-linux** with **/vmlinuz-linux-lts** and **/initramfs-linux.img** with **/initramfs-linux-lts.img**

```
title   Arch Linux
linux   /vmlinuz-linux
initrd  /initramfs-linux.img
options i915.fastboot=1 fbcon=rotate:1 root=/dev/mmcblk0p**Z** rw

```

**You have now installed Arch Linux on your GPD Win!**