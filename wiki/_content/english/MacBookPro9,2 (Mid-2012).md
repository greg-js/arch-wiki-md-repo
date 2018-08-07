Related articles

*   [Mac](/index.php/Mac "Mac")
*   [MacBookPro7,1](/index.php/MacBookPro7,1 "MacBookPro7,1")
*   [MacBookPro8,1/8,2/8,3 (2011)](/index.php/MacBookPro8,1/8,2/8,3_(2011) "MacBookPro8,1/8,2/8,3 (2011)")
*   <a class="mw-selflink selflink">MacBookPro9,2 (Mid-2012)</a>

This guide outlines special information on installing and configuring Arch on the more recent Macbook 9,x (Mid-2012) hardware alongside a pre-existing OSX operating system. This requires adequate free disk space, install media (such as a USB or CD), and a wired connection for the initial steps of the install procedure.

This article is written with a dual-boot setup in mind, and does *not* cover how to replace OSX with Arch.

For general help on the install preocedure see the [Installation guide](/index.php/Installation_guide "Installation guide")

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
        *   [2.2.4 rEFInd](#rEFInd)
*   [3 Post Installation](#Post_Installation)
    *   [3.1 SD Card Reader](#SD_Card_Reader)
    *   [3.2 Users](#Users)
    *   [3.3 Wireless](#Wireless)
    *   [3.4 Inverting FN keys](#Inverting_FN_keys)
        *   [3.4.1 Wireless Flakiness](#Wireless_Flakiness)
        *   [3.4.2 Keyboard Backlight](#Keyboard_Backlight)
    *   [3.5 Xorg](#Xorg)
*   [4 Bells & Whistles](#Bells_.26_Whistles)
    *   [4.1 Emulating OSX Touchpad Gestures](#Emulating_OSX_Touchpad_Gestures)
        *   [4.1.1 Using synclient](#Using_synclient)
        *   [4.1.2 Using Touchegg](#Using_Touchegg)

## Preparation

### Recording UIDs

If you want to access your OSX user directories from Linux, write down the UID and GID for the users.

**Note:** OSX begins with the first user's UID at 501 while Arch defaults to 1000.

**Warning:** Never, *ever* change any file permissions in your OSX partition from Linux. Doing so can and will lead to serious repercussions.

### Install Boot Manager

**Optional.** The easiest way to begin is by [installing rEFInd](http://www.rodsbooks.com/refind/) on Mac OSX before moving on to Arch. This will place a boot menu on startup. The config will be in your OSX partition - if this is not desirable it is possible to install it later in Arch. For more information consult [UEFI](/index.php/UEFI "UEFI").

### Shrinking Macintosh HD

Although nowadays Boot Camp requires a Windows installation disc before altering partitions, it is possible to do this using Mac OSX's disk utility. Create a new partition, calculate the amount of free space required for all new partitions and shrink Macintosh HD to accommodate for this amount. Leave the new partition as free space for now.

## Installation

### Preparing Installation Media

[Download Arch](https://archlinux.org/download/) and burn it to a USB, CD or DVD, and boot into the Arch install.

### Running the Arch Installation

Proceed from the Installation section in [Installation guide#Installation](/index.php/Installation_guide#Installation "Installation guide"). Note that you'll need a wired connection to continue for now.

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

For sharing files between OSX and Linux, a number of filesystem options exist. FAT32 is natively supported on all systems - however, it lacks support for filesystems larger than 2TB or files larger than 4GB. Journaled HFS+ partitions, such as the Macintosh HD partition, will only mount read-only in Linux. Full read-write support is available for unjournaled HFS+ filesystems. ExFAT support can be made available by installing [exfat-utils](https://www.archlinux.org/packages/?name=exfat-utils).

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

#### rEFInd

Alternatively you can use rEFInd as your boot manager. Very simple installation as the refind-install script does everything for you.

```
# pacman -S refind-efi
# refind-install

```

Configure /boot/EFI/refind/refind.conf and uncomment the scan line and edit to reflect the below values for mac.

```
scanfor internal,hdbios,external,biosexternal,optical,cd,manual

```

If you are seeing a slow bootup (30s) move rEFInd to the fallback efi boot path.

```
# mv /boot/EFI/refind /boot/EFI/BOOT
# mv /boot/EFI/BOOT/refind_x64.efi /boot/EFI/BOOT/bootx64.efi

```

If you are having problems check the efi boot order with efibootmgr.

```
# efibootmgr -v

```

## Post Installation

Continue with [General recommendations](/index.php/General_recommendations "General recommendations"), noting the following modifications:

### SD Card Reader

The sdcard reader does not work properly with the highest speeds currently and may never work properly. To get it working you will have to sacrifice the ultra fast modes and use a quirk in your boot parameters.

```
sdhci.debug_quirks2=4

```

### Users

If you wrote down your OSX uid's and gid's eariler, new users can be created by running:

```
# useradd -m -u [uid] -g [gid] -G [additional_groups] -s [login_shell] [username]

```

In order to be able to access a OSX user's directory, only the uid and gid need to match. (usernames can differ)

### Wireless

Macbooks 8,1 to 9,2 (and possibly newer) use BCM4331 for Wifi. See [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless") for details.

### Inverting FN keys

To make the FN keys function as normal FN keys, follow [Apple Keyboard#Function keys do not work](/index.php/Apple_Keyboard#Function_keys_do_not_work "Apple Keyboard").

#### Wireless Flakiness

The only connection manager combination with BCM4331 that doesn't result in flakiness seems to be connman + disabled background scanning.

 `/etc/connman/main.conf` 
```
[General]
BackgroundScanning = false
```

#### Keyboard Backlight

A "just works" solution is the [acpibacklight](https://aur.archlinux.org/packages/acpibacklight/) package. It provides the just work case when controlling it with the keyboard shortcuts.

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