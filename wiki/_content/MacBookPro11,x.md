# MacBookPro11,x

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Installation guide](/index.php/Installation_guide "Installation guide")
*   [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide")
*   [General Recommendations](/index.php/General_Recommendations "General Recommendations")
*   [MacBookPro10,x](/index.php/MacBookPro10,x "MacBookPro10,x")
*   [MacBook](/index.php/MacBook "MacBook")

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** This page flat-out ignores every possible [style](/index.php/Help:Style "Help:Style") rule (Discuss in [Talk:MacBookPro11,x#](https://wiki.archlinux.org/index.php/Talk:MacBookPro11,x))

This wiki page should help you in getting your MacBook Pro from Late 2013 or Mid 2014 to work with Arch Linux. (This includes models 1-3 in the 11,x series).

## Contents

*   [1 Preparing for the Installation](#Preparing_for_the_Installation)
    *   [1.1 Preparing the hard drive](#Preparing_the_hard_drive)
*   [2 Installation](#Installation)
    *   [2.1 Booting the live image](#Booting_the_live_image)
    *   [2.2 Console](#Console)
    *   [2.3 Internet](#Internet)
        *   [2.3.1 Wired](#Wired)
        *   [2.3.2 Wireless](#Wireless)
    *   [2.4 Bootloader](#Bootloader)
        *   [2.4.1 Using the MacBook's native EFI bootloader (recommended)](#Using_the_MacBook.27s_native_EFI_bootloader_.28recommended.29)
            *   [2.4.1.1 Method 1: creating an extra apple-format bootable partition with GRUB](#Method_1:_creating_an_extra_apple-format_bootable_partition_with_GRUB)
            *   [2.4.1.2 Method 2: Using the default EFI System Partition with Grub](#Method_2:_Using_the_default_EFI_System_Partition_with_Grub)
        *   [2.4.2 Direct EFI booting (rEFInd)](#Direct_EFI_booting_.28rEFInd.29)
        *   [2.4.3 Direct EFI booting (gummiboot)](#Direct_EFI_booting_.28gummiboot.29)
        *   [2.4.4 GRUB (with OS X)](#GRUB_.28with_OS_X.29)
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
*   [4 What does not work](#What_does_not_work)
    *   [4.1 General](#General)
    *   [4.2 Wi-Fi](#Wi-Fi)
    *   [4.3 Web cam](#Web_cam)
*   [5 Discussions](#Discussions)
*   [6 See also](#See_also)

## Preparing for the Installation

### Preparing the hard drive

Dual booting with OS X may be desirable if you wish to update firmware. If this is the case, in order to carry out the installation you will need to shrink the main OS X HFS+ partition from within OS X's Disk Utility program, this will also move the OS X Recovery partition to the end of the OS X partition.

**Note:** Please note you may need to disable Filevault encryption before you can resize the partition, feel free to reinitialize this after you perform the partition resize

## Installation

### Booting the live image

To begin your installation, download the current [Archboot](/index.php/Archboot "Archboot") ISO and write it to your USB drive according to the [USB flash installation media](/index.php/USB_flash_installation_media "USB flash installation media") instructions. Boot from the created USB drive by selecting it in the Apple boot manager which is accessible by holding `Alt` on power on.

rEFIt and [REFInd](/index.php/REFInd "REFInd") depending on how they are configured can also allow you to boot from the media.

If the install media you are using has a kernel version earlier than 3.13 you will need to edit the boot entry in the syslinux boot loader. This can be accomplished by pressing `Tab` to edit the entry and append `nomodeset` this will prevent visible screen corruption.

If the install media you are using has a kernel version later than 3.13 **do not** use `nomodeset` as it is not needed and will break [VA-API](/index.php/VA-API "VA-API").

### Console

As this model of notebook has a high DPI display, the console font displayed will be extremely small and depending on your preferences is likely to be uncomfortable to use. You may wish to change this for a more legible font, an example of which is;

```
$ setfont sun12x22

```

### Internet

#### Wired

Thunderbolt Ethernet adapters and USB-to-Ethernet adapters should be picked up automatically.

**Note:** You may have to power on the machine with the Thunderbolt Ethernet adapter plugged in for it to be picked up initially.

#### Wireless

As mentioned below, `broadcom-wl` is sufficient if you are using the Linux mainline kernel. For custom kernels, you need to use `broadcom-wl-dkms`. Both are available from the [AUR](/index.php/AUR "AUR"). The easiest way to get Wi-Fi connectivity during install is to build the package driver on a separate system. Note that it does have to be built against the exact same kernel version as used by the installer, and this may differ from the latest version. If built against the wrong kernel you may encounter an error _(ERROR: could not insert 'wl': Invalid argument)_ upon modprobe. Build the package as follows:

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

**Note:** You need to repeat this process when you have finished your installation and booting into the system for the first time. If kernel versions differ, you may want to ensure to install a number of essential packages while you have connectivity and before you boot into your system ,

these allow you to build the broadcom driver again and connect (provided you put the AUR tarball for the driver on USB drive too):

[dkms](https://www.archlinux.org/packages/?name=dkms),[wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant), [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) ([dialog](https://www.archlinux.org/packages/?name=dialog) and [netctl](https://www.archlinux.org/packages/?name=netctl) are needed if you want to use `wifi-menu` again after you boot)

### Bootloader

**Note:** Refer to the [MacBook](/index.php/MacBook "MacBook") page if you do not want to have a separate partition for GRUB but rather prefer to use [rEFInd](http://www.rodsbooks.com/refind/) (or [rEFIt](/index.php/MacBook#rEFIt "MacBook")).

**Tip:** If you want to use the native MacBook bootloader, you need an extra partition of at least 128 MiB.

#### Using the MacBook's native EFI bootloader (recommended)

##### Method 1: creating an extra apple-format bootable partition with GRUB

This method uses the MacBook's native EFI bootloader, i.e. the one the can be reached when holding the alt-key during boot. For additional info, see [GRUB EFI Examples#Apple Mac EFI systems](/index.php/GRUB_EFI_Examples#Apple_Mac_EFI_systems "GRUB EFI Examples").

**Note:** For this method you need an extra partition of at least 128 MiB. This partition will be used by the MacBook's native bootloader to launch Arch. It also assumes that you are dual-booting OS X and Arch.

**Note:** It is possible to avoid the HFS+ partition by using FAT32, this way you can do all the bootloader stuff right from the LiveCD.

At the end of the Arch Linux install process we would normally install GRUB (or a variation) to a partition on the drive. For this method we will place a `boot.efi` file on an extra partition used by the MacBook's native bootloader.

First, [install](/index.php/Install "Install") the [grub](https://www.archlinux.org/packages/?name=grub) package from the [official repositories](/index.php/Official_repositories "Official repositories"). Make sure to follow the steps for setting up grub on a partition using the `grub-install` and `grub-mkconfig` commands, like normal. We will use the config file that `grub-mkconfig` creates to generate a standalone `boot.efi` file using the `grub-mkstandalone` command, then we will wipe your just-created grub partition and set it up for Mac's native bootloader (or you can simply create a new partition and leave the grub partition alone, it is up to you).

When generating a grub config file, GRUB looks to `/etc/default/grub` for its configuration. Edit the parameter `GRUB_CMDLINE_LINUX_DEFAULT` to look something like this:

```
GRUB_CMDLINE_LINUX_DEFAULT="quiet rootflags=data=writeback libata.force=noncq"

```

The `libata.force=noncq` parameter will prevent SSD lockups and the `rootflags` option is used for SSD-performance.

**Note:** Do not use the `rootflags` option on Btrfs. It is not supported.

Now we generate the `boot.efi` file (in our current working directory):

```
# grub-mkconfig -o /boot/grub/grub.cfg
# grub-mkstandalone -o boot.efi -d /usr/lib/grub/x86_64-efi -O x86_64-efi /boot/grub/grub.cfg

```

Put this file on a USB (or other OS X accessible media) and reboot into OS X.

Launch `DiskUtility.app` and reformat the extra partition (or just make a new one) as HFS+ (in the "Erase" tab of Disk Utility), mount it, then create the following directory structure and file:

```
$ mount -t hfs /dev/diskXsY <Path to root of extra partition>
$ mkdir -p <Path to root of extra partition>/System/Library/CoreServices
$ touch <Path to root of extra partition>/mach_kernel

```

where `diskXsy` is the disk your partition is on (e.g. disk0s1). You can use `diskutil list` to list your disks and partitions.

Copy the `boot.efi` file to the `<Path to extra partition>/System/Library/CoreServices/` directory. Using your editor of choice, create a `SystemVersion.plist` file in the CoreServices directory, which is located here:

```
_<path to extra partition>_/System/Library/CoreServices/SystemVersion.plist

```

Edit that file to look like this:

```
<?xml version="1.0" encoding="utf-8"?>
<plist version="1.0">
<dict>
    <key>ProductBuildVersion</key>
    <string></string>
    <key>ProductName</key>
    <string>Linux</string>
    <key>ProductVersion</key>
    <string>Arch Linux</string>
</dict>
</plist>
```

**Note:** It is possible to do the above modifications to/on the extra partition from within Linux (if you have installed the proper HFS tools), but the following bless commands have to be executed from within OS X.

The last step is then to bless (make bootable) the extra partition (as root):

```
# bless --folder=<Path to root of extra partition> --file=<Path to root of extra partition>/System/Library/CoreServices/boot.efi --setBoot
# bless --mount=<Path to root of extra partition> --file=<Path to root of extra partition>/System/Library/CoreServices/boot.efi --setBoot

```

**Note:** It might not be necessary to execute both commands, but to be sure it worked it will not do any harm to execute both.

**Note:** In order to change grub settings both `grub.cfg` and `boot.efi` will have to be generated. This can be done from in Linux, without booting OS X.

Generate `grub.cfg` and `boot.efi` from Arch Linux:

```
# grub-mkconfig -o /boot/grub/grub.cfg
# mount -t hfsplus -o force,rw /dev/sdXY /mnt # mount the HFS+ partition
# grub-mkstandalone -o /mnt/System/Library/CoreServices/boot.efi -d /usr/lib/grub/x86_64-efi -O x86_64-efi /boot/grub/grub.cfg

```

##### Method 2: Using the default EFI System Partition with Grub

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** Coming this weekend... (Discuss in [Talk:MacBookPro11,x#](https://wiki.archlinux.org/index.php/Talk:MacBookPro11,x))

#### Direct EFI booting (rEFInd)

See: [UEFI_Bootloaders](/index.php/UEFI_Bootloaders "UEFI Bootloaders")

As of August 2013, refind can automatically detect the Arch kernel, removing the need for copying the kernel into the EFI partition. Simply install refind without the EFI file system drivers [[1]](http://forums.gentoo.org/viewtopic-t-967024-start-0.html) using the `--nodrivers` option [[2]](https://bbs.archlinux.org/viewtopic.php?pid=1348145#p1348145), and enable the `scan_all_linux_kernels` and `also_scan_dirs` options in `refind.conf` (see link above for instructions.).

An alternative way is to omit all the scans and put the following bootentry at the end of your "refind.conf":

```
menuentry "Arch" {
  icon EFI/refind/icons/os_arch.icns 
  volume <Volume label>
  ostype Linux
  loader /boot/vmlinuz-linux
  initrd /boot/initramfs-linux.img
  options "rw root=/dev/<arch partition> rootfstype=<filesystem type> libata.force=noncq"
}

```

Do not forget to replace the angle brackets with your data.

#### Direct EFI booting (gummiboot)

See [Beginners' guide#For_UEFI_motherboards](/index.php/Beginners%27_guide#For_UEFI_motherboards "Beginners' guide")

#### GRUB (with OS X)

Another solution is to install [GRUB](/index.php/GRUB "GRUB"). Edit `/tmp/install/boot/grub/grub.cfg` and edit the boot entry to load Linux mainline instead of the normal one.

**Note:** `libata.force=noncq` helps with hangs due to SSD speed.

Now cd into `/tmp/install/` and create the GRUB image by running:

```
grub-mkstandalone -o bootx64.efi -d usr/lib/grub/x86_64-efi -O x86_64-efi -C xz boot/grub/grub.cfg

```

This will create file called `boot64.efi` which contains GRUB and the configuration file incorporated inside. It is important to `cd` into the right directory to make it pick up the configuration file and put it into the right place within the image.

Copy this file to the MacBook's EFI partition. The downside of this method is that you need to repeat this step whenever you want to change the GRUB config. Reboot the machine and you should be able to select your installed Arch Linux by keeping the `Alt` button pressed. It should appear as `EFI boot`.

To generate a nicer config use: `grub-mkconfig`, remove `quiet` if you like the text, then to update your GRUB post-installation, do this to make the GRUB EFI file and put it in the EFI partition:

```
cd /
grub-mkstandalone -o bootx64.efi -d usr/lib/grub/x86_64-efi -O x86_64-efi -C xz boot/grub/grub.cfg
sudo mount /dev/sda1 /mnt
sudo cp bootx64.efi /mnt/EFI/boot/bootx64.efi

```

**Note:** You will need `hfsprogs` to run the above commands

## Post installation

### Console

Largest console font (although ugly) achieved by adding `FONT=sun12x22` to `/etc/vconsole.conf` It is still tiny but is at least readable.

### Graphics

###### MacBook Pro 11,1

*   Intel works on 3.12 with nomodeset
*   Intel works from 3.13.4-1-ARCH

###### MacBook Pro 11,2

*   Intel works from 3.13.4-1-ARCH

###### MacBook Pro 11,3

*   Nvidia works (both 319.60 and 331.17 drivers)
    *   Follow [http://cberner.com/2013/03/01/installing-ubuntu-13-04-on-macbook-pro-retina/](http://cberner.com/2013/03/01/installing-ubuntu-13-04-on-macbook-pro-retina/)
*   Intel works after patching grub, see below

###### MacBook Pro 11,5

*   The [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) package seems to be stable. Switching to VTs and back works fine from MATE and GNOME. SOmetimes Chromium causes a "kernele rejected pixbuf" error which freezes the desktop.
*   The [nvidia-dkms](https://aur.archlinux.org/packages/nvidia-dkms/)<sup><small>AUR</small></sup> driver has been crashing a lot.
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

By default the integrated card is powered off. To fix this we need a grub function called "apple_set_os". This function has not officially been merged yet, so we need to build grub ourselves. Download the [grub-git](https://aur.archlinux.org/packages/grub-git/)<sup><small>AUR</small></sup> package from the AUR. Using something like:

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

`sudo cat /sys/kernel/debug/vgaswitcheroo/switch`

NOTICE: gpu-switch has been tested only on a select few models, those being MacBookPro9,1, MacBookPro10,1, and MacBookPro11,3\. Use at your own risk.

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

Using this SuperUser receipt [[3]](http://superuser.com/questions/217615/how-to-right-click-using-the-keyboard-from-ubuntu-on-a-mac) I got Ctrl-click working as right-click. I had to increase the sleep time to 0.1 though.

#### input-mtrack

Another method is to use xf86-input-mtrack-git [[4]](https://aur.archlinux.org/packages/xf86-input-mtrack-git/). If you like to have a thumb resting on the touchpad, this driver is the right choice, because it has an option for IgnoreThumb.

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
*   Brightness in `/sys/class/backlight/gmux_backlight/brightness` can be modified comfortably via the [gmux_backlight](https://aur.archlinux.org/packages/gmux_backlight/)<sup><small>AUR</small></sup> utility without root privileges. Requires the `setpci` setting below.
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

## What does not work

Updated 2015-04-08

### General

### Wi-Fi

*   [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/)<sup><small>AUR</small></sup> or [broadcom-wl-dkms](https://aur.archlinux.org/packages/broadcom-wl-dkms/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR") works
    *   Stability is an issue for some, look at [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless") for possible fixes (e.g. downgrading kernel works if your card is BCM4360)

### Web cam

*   Listed on PCI bus as: Multimedia controller: Broadcom Corporation Device 1570.
    *   When the apple_set_os grub patch is used with a 11,3 machine lspci reports; 04:00.0 Multimedia controller: Broadcom Corporation 720p FaceTime HD Camera
*   In OS X, the camera is listed as FaceTime HD camera 1570.
*   No known Linux driver. [Kernel.org Bug](https://bugzilla.kernel.org/show_bug.cgi?id=71131)
*   Efforts to develop a reverse engineered driver: [https://github.com/patjak/bcwc_pcie/](https://github.com/patjak/bcwc_pcie/)

## Discussions

*   [https://bbs.archlinux.org/viewtopic.php?id=171883](https://bbs.archlinux.org/viewtopic.php?id=171883)

## See also

*   [MacBookPro10,x](/index.php/MacBookPro10,x "MacBookPro10,x")
*   [MacBook](/index.php/MacBook "MacBook")

Retrieved from "[https://wiki.archlinux.org/index.php?title=MacBookPro11,x&oldid=415743](https://wiki.archlinux.org/index.php?title=MacBookPro11,x&oldid=415743)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Apple](/index.php/Category:Apple "Category:Apple")

Hidden categories:

*   [Pages or sections flagged with Template:Style](/index.php/Category:Pages_or_sections_flagged_with_Template:Style "Category:Pages or sections flagged with Template:Style")
*   [Pages flagged with Template:Stub](/index.php/Category:Pages_flagged_with_Template:Stub "Category:Pages flagged with Template:Stub")