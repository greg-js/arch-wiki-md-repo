Related articles

*   [Mac](/index.php/Mac "Mac")
*   <a class="mw-selflink selflink">MacBookPro7,1</a>
*   [MacBookPro8,1/8,2/8,3 (2011)](/index.php/MacBookPro8,1/8,2/8,3_(2011) "MacBookPro8,1/8,2/8,3 (2011)")
*   [MacBookPro9,2 (Mid-2012)](/index.php/MacBookPro9,2_(Mid-2012) "MacBookPro9,2 (Mid-2012)")

This page contains tips on installing Arch Linux on a Mid 2010 13" MacBook Pro alongside a pre-existing OSX operating system. For general help on the installation procedure see the [Installation guide](/index.php/Installation_guide "Installation guide").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Preparation](#Preparation)
    *   [1.1 Install Boot Manager](#Install_Boot_Manager)
    *   [1.2 Shrinking Macintosh HD](#Shrinking_Macintosh_HD)
    *   [1.3 EFI vs CSM mode](#EFI_vs_CSM_mode)
*   [2 Installation](#Installation)
    *   [2.1 Dual Boot](#Dual_Boot)
        *   [2.1.1 EFI-Mode](#EFI-Mode)
        *   [2.1.2 CSM-Mode](#CSM-Mode)
    *   [2.2 Bootloader](#Bootloader)
        *   [2.2.1 EFI-Mode](#EFI-Mode_2)
        *   [2.2.2 CSM-Mode or BIOS-compatibility](#CSM-Mode_or_BIOS-compatibility)
            *   [2.2.2.1 Can't find root device](#Can't_find_root_device)
*   [3 Network](#Network)
*   [4 Video](#Video)
    *   [4.1 Nouveau](#Nouveau)
    *   [4.2 Nvidia](#Nvidia)
*   [5 Fan Control](#Fan_Control)

## Preparation

### Install Boot Manager

**Optional.** The easiest way to begin is by [installing rEFInd](http://www.rodsbooks.com/refind/) on Mac OSX before moving on to Arch. This will place a boot menu on startup. The config will be in your OSX partition - if this is not desirable it is possible to install it later in Arch. Keep in mind that since Apple's OS X 10.11 (El Capitan), the feature System Integrity Protection (SIP) doesn't allow for rEFInd installation in the way described on the Installing rEFInd page. See [this site](https://www.rodsbooks.com/refind/sip.html) for more information and installation instructions.

### Shrinking Macintosh HD

Using Mac OSX's disk utility, create a new partition, calculate the amount of free space required for all new partitions and shrink Macintosh HD to accommodate for this amount. Leave the new partition as free space for now.

### EFI vs CSM mode

It's probably good to consider on forehand what the differences are and which will work best for you, especially considering the drawback EFI mode has on the NVIDIA driver.

## Installation

To install an x86_64 system, follow the [Mac](/index.php/Mac "Mac") EFI installation instructions. It is recommended to read the [UEFI](/index.php/UEFI "UEFI"), [GPT](/index.php/GPT "GPT") and [Arch boot process#Boot loader](/index.php/Arch_boot_process#Boot_loader "Arch boot process") pages before trying any of this on your machine. Also of note, [GIST](https://gist.github.com/Apsu/4108795).

See notes on **video support** before attempting installation!

*The following assumes that you have somehow managed to install archlinux to a single partition on your drive, and that you still have your osx installation on a different partition.*

### Dual Boot

If you want to dualboot osx and linux, the easiest way to do so is to use [rEFInd](/index.php/REFInd "REFInd"). rEFInd is a updated and maintained fork of [rEFIt](http://refit.sourceforge.net/) and should be used in its place.

I've found it easiest to install rEFInd from osx. Depending on your setup, you'll either install it to your osx partition, or to the ESP partition (install.sh --esp). See [here](http://www.rodsbooks.com/refind/installing.html#installsh) for instructions. Installing to the ESP partition can cause some **startup delay**, which can be overcome by simply renaming rEFInd's installation folder to "BOOT" and the executable to "bootx64.efi"[[1]](http://www.rodsbooks.com/refind/installing.html#sluggish)

Assuming that rEFInd was installed to the ESP, I've found it convenient to later mount the ESP as my "/boot" directory. That way, by setting

```
scan_all_linux_kernels

```

in your refind.conf, rEFInd will automatically pickup the kernel. All you need to add is a "refind_linux.conf" file to the root of the ESP, containing your boot args. I use:

```
"Boot with defaults"    "root=/dev/sda3 rootfstype=xfs ro add_efi_memmap"

```

Note that my root partion is sda3 and that I use the xfs filesystem on it, yours may differ! So my ESP partition looks like this when mounted under "/boot":

```
EFI/
 APPLE/
 BOOT/
  bootx64.efi
  drivers/
  icons/
  keys/
  refind.conf
initramfs-linux-fallback.img
initramfs-linux.img
refind_linux.conf
syslinux/ *** My bootloader of choice, see below ***
vmlinuz-linux

```

Note that the EFI/BOOT directory is normally named EFI/REFIND and that the bootx64.efi is normally named refind_x64.efi.

#### EFI-Mode

You should now be able to boot your mac in efi-mode via the kernel's efistub feature. rEFInd should present you with an option to do so. See [here](http://www.rodsbooks.com/refind/linux.html) for more general information on the topic. This however has some drawbacks, as mentioned in the **Video** section below.

#### CSM-Mode

Booting your mac in csm- or legacy-mode provides a solution. To do so, we need a **hybrid mbr**, with at least one 'active/bootable' partition. See [here](http://www.rodsbooks.com/gdisk/hybrid.html) for more general information on how to setup a hybrid mbr. Simply boot in **efi-mode**, then assuming you have three partitions, the ESP partition, an osx and a linux partition you'll need to use gdisk to set things up.

```
# gdisk /dev/sda

```

Press 'p' to print your partition table, which should look somewhat like mine:

```
Number  Start (sector)    End (sector)  Size       Code  Name
  1              40          409639   200.0 MiB   0700  EFI System Partition
  2          409640       393186215   187.3 GiB   AF00  OSX
  3       393186216       625142414   110.6 GiB   8300  Linux filesystem

```

Press 'r' to enter recovery and transformation mode.

Now press 'o' to print your mbr. It should only list a single partition covering the entire disk. Or depending on with which tools you used to partition your disk maybe some other entries.

Press 'h' to create a new hybrid mbr. You'll be prompted for some input:

```
Type from one to three GPT partition numbers, separated by spaces, to be
added to the hybrid MBR, in sequence:

```

I chose to mirror my gpt, so I entered '1 2 3', but it should be enough to just use one partition here. In my example, this would need to be the ESP partition, so '1', but in case you don't want to use the ESP to store your kernels, this could also be the linux partition, so '3'. You decide :)

Another and maybe more secure way to mirror the gpt is only to enter '1' for the first and only partition, the EFI or boot partition. This prevents the strange behaviour of MacOS. It can happen that MacOS or its bootsystem can't find his partition and will end up in a rather long loop. Then proceed as written below.

Make sure to say 'Yes' to the next promt:

```
Place EFI GPT (0xEE) partition first in MBR (good for GRUB)? (Y/N): y

```

Then set at least one partition as active/bootable:

```
Creating entry for GPT partition #1 (MBR partition #2)
Enter an MBR hex code (default 07): 
Set the bootable flag? (Y/N): y

```

Note the MBR hex code depends on the partition type, press 'l' in gdisk's main menu to list them.

Press 'o' (**make sure you're still in the recovery menu!!!**) again to see your new hybrid mbr, in my case:

```
Number  Boot  Start Sector   End Sector   Status      Code
  1                     1           39   primary     0xEE
  2      *             40       409639   primary     0x07
  3                409640    393186215   primary     0xAF
  4             393186216    625142414   primary     0x83

```

Or if you choose to only mirror the first one, it can also look like this:

```
Number  Boot  Start Sector   End Sector   Status      Code
  1                     1           39   primary     0xEE
  2      *             40       409639   primary     0xEF

```

Even if the mbr table looks like this (*note that in the second table only the last two lines are missing*), the bootloader will know what to boot. You can compare start and end sectors between the two tables if you wish.

Press 'w' to write the table to disk and reboot.

### Bootloader

The next important thing is the bootloader, which acts as the bridge from refind to your kernel. Based on the Mode you use to install arch, either **EFI** or **CSM**, you can choose a bootloader of your choice. But for now, We provide you with information about **Syslinux** and **Gummiboot**, because these are the two we tested successfully for now.

In both cases I assume that you managed to mount the EFI partition mentioned above to */boot/* already.

Grub is the one bootloader, which can handle both the EFI and the CSM mode. But because it's mighty, it also can be complex and the configuration are far-reaching. I recommending you, unless you want to configure the smallest detail in the bootloader for an **un**forgetting adventure during a booting, to use gummiboot (EFI-only) or syslinux (CSM-only), because both are really easy to setup.

#### EFI-Mode

If you do not need the power and its powersaving feature of the nvidia driver, then you should install [gummiboot](/index.php/Gummiboot "Gummiboot") or [GRUB](/index.php/GRUB "GRUB"), because these bootloaders are the one which actually works fine with EFI.

Here, let's do it with gummiboot:

```
# pacman -S gummiboot

```

After installing the package, it needs to be configured, so run the installer of gummiboot:

```
# gummiboot install

```

Then you need to create a config file for gummiboot and add an entry for the arch booting. The **sdaX** means that you have to replace it with your root partition, in this case it may be **/dev/sda3**.

 `# nano /boot/loader/entries/arch.conf` 
```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=**/dev/sdaX** rw
```

As usual, for more information on configuring and using gummiboot, see [gummiboot](/index.php/Gummiboot "Gummiboot").

#### CSM-Mode or BIOS-compatibility

Otherwise, if you don't want to miss out the advantages of the nvidia driver, I suggest you to install [syslinux](/index.php/Syslinux "Syslinux") or also [GRUB](/index.php/GRUB "GRUB") for the CSM-Mode. We'll use syslinux because it's the simplest to setup, but others should also work. Install it via pacman, and then just execute

```
# syslinux-install_update -i -a -m

```

It should detect your hybrid mbr and install itself automatically. Refer to [Syslinux](/index.php/Syslinux "Syslinux") for more details.

Make sure to configure the bootloader's menu entries correctly: (syslinux)

```
LABEL arch
MENU LABEL Arch Linux
LINUX ../vmlinuz-linux
APPEND root=/dev/sda3 ro vga=865
INITRD ../initramfs-linux.img

```

Note that 'sda3' refers to the **gpt mapping**, 'vga=865' means 1280x800 framebuffer resolution, nicer when using the nvidia driver.

##### Can't find root device

If booting fails, first try to use the initramfs-linux-fallback.img, as it includes more modules than your 'auto-detected' initramfs, and should allow the kernel to actually find your root partition. You'll then need to rebuild your regular initramfs. Rebuild it with

```
# mkinitcpio -p linux

```

If you're lucky, the whole booting process with the regular initramfs-linux will end up successfully, if not, then try to add the following configuration and rebuild the initramfs again. I needed to include modules in the initramfs file. In /etc/mkinitcpio.conf:

```
MODULES="ata_generic libata xfs"

```

Note, that you'll only need xfs if your root partition is actually formatted with it, exchange it with the appropriate module for the file-system you use.

Once you reboot, rEFInd should now present you with three options, two linux entries and one for osx. One linux entry will boot the kernel via efistub in **efi-mode**, the other will call syslinux(or your chosen bootloader) which then should boot the system in **csm-mode**. Do the latter from now on!

The easiest way to see if you were successful, is to install the [NVIDIA](/index.php/NVIDIA "NVIDIA") driver and start X.

## Network

[Wireless Setup](/index.php/Wireless_Setup "Wireless Setup") provides instructions on how to identify your card, but if your MacBook Pro 7,1 is like mine then you'll head to [Broadcom Wireless](/index.php/Broadcom_wireless "Broadcom wireless") and use this command.

```
# lspci -vnn -d 14e4:

```

If from this you discover that your full PCI-ID is `[14e4:432b]`, then the following advice applies to you: Don't waste time on the `b43` driver. I've been fiddling with it for weeks, and switching to `broadcom-wl` made all the problems go away. `broadcom-wl` might make your device names funky, but that's easily fixed with the udev rule documented on [Broadcom Wireless](/index.php/Broadcom_wireless "Broadcom wireless").

I also recommend `netctl`.

**Note:** Alternative solution for using b43:

As of kernel version 3.17.1-2, Broadcom Wireless driver most likely won't work (ERROR @wl_cfg80211_scan :WLC_SCAN error (-22)). The only option seems to be loading the b43 driver in [PIO](https://en.wikipedia.org/wiki/Programmed_input/output "wikipedia:Programmed input/output") mode. To enable PIO mode, install driver by following the guide at [wireless.kernel.org](http://wireless.kernel.org/en/users/Drivers/b43), then load the b43 kernel module with pio=1 and qos=0 parameters. To make this happen at boot, create `b43-firmware.conf` file in `/etc/modprobe.d/` and add the following lines:

 `b43-firmware.conf` 
```
options b43 pio=1 qos=0

blacklist wl
blacklist brcmsmac
blacklist brcmfmac
blacklist b43legacy
blacklist bcm43xx
blacklist brcm80211

```

~~Although using PIO should be much slower than using [DMA](https://en.wikipedia.org/wiki/Direct_memory_access "wikipedia:Direct memory access"), I haven't noticed any performance drop.~~ Further testing showed repetitive occurrences of noticable performance drops. Mostly expressed as rapid decrease of transfer speed, sometimes even dropped connections. It also seems that b43 driver has issues operating at 5Ghz.

Some later kernels are giving me more success (without PIO), but still some wifi drops have occurred.

## Video

According to the [Debian Wiki](http://wiki.debian.org/MacBookPro) the MacBook Pro 7,1 has an [NVIDIA GeForce GT 320M](http://www.geforce.com/hardware/desktop-gpus/geforce-GT-320-OEM) in it.

### Nouveau

Works out of the box, performance however is not that great and your system will get quite *hot* when running nouveau.

### Nvidia

The drivers work out of the box when booting the mac in csm- or legacy-mode. See [here](https://bbs.archlinux.org/viewtopic.php?id=162289) for some discussion on the topic.

Running the drivers in **efi-mode** requires setting some PCI registers before the kernel modules get loaded, preferably using a udev hook or GRUB script. Otherwise, the screen just remains black when X starts. Follow these [instructions](http://askubuntu.com/questions/264247/proprietary-nvidia-drivers-with-efi-on-mac-to-prevent-overheating/613573#613573) in order to find the appropriate PCI device IDs for which to set the registers. This approach has been confirmed to work and is still being actively discussed inside the above mentioned [thread](https://bbs.archlinux.org/viewtopic.php?pid=1522950#p1522950).

## Fan Control

For controlling the fans I recommend using mbpfan from the AUR ([mbpfan-git](https://aur.archlinux.org/packages/mbpfan-git/)), reasons being is that from my experience fan control isn't very great on Arch Linux by default and fans always run really loud without this package! Once you install that from the AUR add it to startup!

```
# systemctl mbpfan.service

```

**To be continued..**