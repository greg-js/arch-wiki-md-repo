This guide outlines special information on installing and configuring Arch on the more recent Macbook 9,x (Mid-2012) hardware alongside a pre-existing OSX operating system. This requires adequate free disk space, install media (such as a USB or CD), and a wired connection for the initial steps of the install procedure.

This article is written with a dual-boot setup in mind, and does _not_ cover how to replace OSX with Arch.

For general help on the install preocedure see the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide")

**Note:** Remember to back up your pre-existing OSX installation before proceeding!

## Contents

*   [1 Preparation](#Preparation)
    *   [1.1 Recording UIDs](#Recording_UIDs)
    *   [1.2 Install Boot Manager](#Install_Boot_Manager)
    *   [1.3 Shrinking Macintosh HD](#Shrinking_Macintosh_HD)
*   [2 Installation](#Installation)
    *   [2.1 Preparing Installation Media](#Preparing_Installation_Media)
    *   [2.2 Running the Arch Installation](#Running_the_Arch_Installation)
        *   [2.2.1 Sample partition layout](#Sample_partition_layout)
        *   [2.2.2 Install Bootloader](#Install_Bootloader)
        *   [2.2.3 Note about Macbook Pro 9,1 and 9,2](#Note_about_Macbook_Pro_9.2C1_and_9.2C2)
*   [3 Post Installation](#Post_Installation)
    *   [3.1 Users](#Users)
    *   [3.2 Wireless](#Wireless)
        *   [3.2.1 b43](#b43)
        *   [3.2.2 wl](#wl)
    *   [3.3 Xorg](#Xorg)
*   [4 Bells & Whistles](#Bells_.26_Whistles)
    *   [4.1 Emulating OSX Touchpad Gestures](#Emulating_OSX_Touchpad_Gestures)
        *   [4.1.1 Using synclient](#Using_synclient)
        *   [4.1.2 Using Touchegg](#Using_Touchegg)

## Preparation

### Recording UIDs

If you want to access your OSX user directories from Linux, write down the UID and GID for the users.

**Note:** OSX begins with the first user's UID at 501 while Arch defaults to 1000.

**Warning:** Never, _ever_ change any file permissions in your OSX partition from Linux. Doing so can and will lead to serious repercussions.

### Install Boot Manager

**Optional.** The easiest way to begin is by [installing rEFInd](http://www.rodsbooks.com/refind/) on Mac OSX before moving on to Arch. This will place a boot menu on startup. The config will be in your OSX partition - if this is not desirable it is possible to install it later in Arch. For more information consult [UEFI](/index.php/UEFI "UEFI").

### Shrinking Macintosh HD

Although nowadays Boot Camp requires a Windows installation disc before altering partitions, it is possible to do this using Mac OSX's disk utility. Create a new partition, calculate the amount of free space required for all new partitions and shrink Macintosh HD to accommodate for this amount. Leave the new partition as free space for now.

## Installation

### Preparing Installation Media

[Download Arch](https://archlinux.org/download/) and burn it to a USB, CD or DVD, and boot into the Arch install.

### Running the Arch Installation

Proceed from the Installation section in either [Beginners' guide/Installation](/index.php/Beginners%27_guide/Installation "Beginners' guide/Installation") or [Installation guide#Installation](/index.php/Installation_guide#Installation "Installation guide"). Note that you'll need a wired connection to continue for now.

The following differences will apply to MacBooks:

#### Sample partition layout

**Note:** Apple prefers having 128MB of unallocated space between partitions. Whether or not this is completely necessary is uncertain, but if it seems like there is more than enough space available, then creating this buffer of free space may be a good idea.

```
partition  mountpoint  size       type  label
/dev/sda1  /boot/efi   200MiB     vfat  EFI
/dev/sda2  -           ?          hfs+  Mac OS X
/dev/sda3  -           ?          hfs+  Recovery
/dev/sda4  /boot       100MiB     boot  boot
/dev/sda5  /           10GiB      ext4  root
/dev/sda6  /home       remaining  ext4  home (optional)
/dev/sda7  ?           ?          ?     shared (optional)

```

For sharing files between OSX and Linux, a number of filesystem options exist. FAT32 is natively supported on all systems - however, it lacks support for filesystems larger than 2TB or files larger than 4GB. Journaled HFS+ partitions, such as the Macintosh HD partition, will only mount read-only in Linux. Full read-write support is available for unjournaled HFS+ filesystems. ExFAT support can be made available by installing [fuse-exfat](https://www.archlinux.org/packages/?name=fuse-exfat) and [exfat-utils](https://www.archlinux.org/packages/?name=exfat-utils).

#### Install Bootloader

Use [GRUB2#UEFI systems](/index.php/GRUB2#UEFI_systems "GRUB2") for more information.

After setting up the base system, do the following in your chrooted environment:

```
# pacman -S grub-efi-x86_64
# pacman -S efibootmgr

# mkdir -p /boot/efi
# mount -t vfat /dev/sda1 /boot/efi

# modprobe dm-mod
# grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=arch_grub --recheck --debug
# mkdir -p /boot/grub/locale (this may already exist)
# cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo

```

#### Note about Macbook Pro 9,1 and 9,2

For Macbook Pro 9,1 users, the process is similar.

```
# pacman -S grub-efi-x86_64 efibootmgr

# mkdir -p /boot/efi
# mount -t vfat /dev/sda1 /boot/efi

# modprobe dm-mod
# grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=arch_grub --recheck --debug
# grub-mkconfig -o /boot/grub/grub.cfg (may not be necessary for 9,2)
# mkdir -p /boot/grub/locale
# cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo

```

The only difference is installing efibootmgr (required for 9,2) and running grub-mkconfig (may not be required for 9,2)

## Post Installation

Continue with [Beginners' guide/Post-installation](/index.php/Beginners%27_guide/Post-installation "Beginners' guide/Post-installation") or [Installation guide#Post-installation](/index.php/Installation_guide#Post-installation "Installation guide"), noting the following modifications:

### Users

If you wrote down your OSX uid's and gid's eariler, new users can be created by running:

```
# useradd -m -u [uid] -g [gid] -G [additional_groups] -s [login_shell] [username]

```

In order to be able to access a OSX user's directory, only the uid and gid need to match. (usernames can differ)

### Wireless

Macbooks 8,1 to 9,2 (and possibly newer) use BCM4331 for Wifi. As of June 2013 two options are available, the open source b43 driver and Broadcom's proprietary wl driver.

#### b43

**Warning:** compat-drivers is outdated and was renamed to [backports](http://wireless.kernel.org/en/users/Download/stable/).

```
$ curl -O [https://www.kernel.org/pub/linux/kernel/projects/backports/2013/03/28/compat-drivers-2013-03-28-5.tar.bz2](https://www.kernel.org/pub/linux/kernel/projects/backports/2013/03/28/compat-drivers-2013-03-28-5.tar.bz2)
$ tar xjf compat-drivers-2013-03-28-5.tar.bz2
$ cd compat-drivers-2013-03-28-5

$ scripts/driver-select b43
$ make
$ sudo make install

```

Create `/etc/modules-load.d/b43.conf` and write `b43` to load wireless at startup.

Install [b43-firmware](https://aur.archlinux.org/packages/b43-firmware/) from [AUR](/index.php/AUR "AUR") and reboot. From here on in, wifi configuration should proceed normally - once it's working the wired connection may be disconnected.

#### wl

_more to come._

Download, extract, and install [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/) from [AUR](/index.php/AUR "AUR") and reboot.

### Xorg

Main Page: [Xorg](/index.php/Xorg "Xorg")

Install [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) and setup Xorg as you normally would.

The built-in keyboard and most usb input devices will work out-of-the-box, but [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) is needed in order to use the built-in touchpad.

## Bells & Whistles

### Emulating OSX Touchpad Gestures

With a little bit of work it's possible to tweak the multitouch options on the trackpad. This can be achieved with a combination of X11 driver settings and open source software.

#### Using synclient

`synclient` is included with the [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) driver. It is useful for experimenting with settings as they take effect immediately and expire at the end of an X session. Many OSX options can be emulated without any additional software.

Run `synclient -l` to have a look at all the available options. Here are some suggestions which resemble the options found in OSX's System Preferences:

*   By default synaptics is configured to use a double-tap drag gesture found on older touchpads - one may argue that this is not necessary on a clickpad. `synclient TapAndDragGesture=0` will turn this off.
*   TapButtonX and ClickFingerX sets the mouse button triggered by tapping or clicking with X fingers. set `TapButton2=3` and `ClickFinger2=3` to assign two-finger click to the right mouse button.
*   Setting the bottom-right corner click to right mouse button can be done by subtracting about 500 from `RightEdge` and `BottomEdge` and plugging the new values into `RightButtonAreaLeft` and `RightButtonAreaTop`. If the last two options are not visible, set `Clickpad=1`.

To make settings permanent, just modify `/etc/X11/xorg.conf.d/10-synaptics.conf`.

**Note:** Right/Middle ButtonArea options are only recognized once the X fully loads the driver. To work around this, create a script file `/usr/local/bin/synarea.sh` with the required synclient commands, and add the script to the X startup sequence.

#### Using Touchegg

[touchegg](https://aur.archlinux.org/packages/touchegg/) from the [AUR](/index.php/AUR "AUR") is an application which can recognize additional gestures. To use this you'll need to replace the synaptics driver with [xf86-input-synaptics-mtpatch](https://aur.archlinux.org/packages/xf86-input-synaptics-mtpatch/). See however [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1502743#p1502743).

 `$(HOME)/.config/touchegg/touchegg.conf` 

```
...
<application name="All">
        ...
        <gesture type="DRAG" fingers="3" direction="ALL">
                <action type="DRAG_AND_DROP"></action>
        </gesture>
        ...
</application>
...
```