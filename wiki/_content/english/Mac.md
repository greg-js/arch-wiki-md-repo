Related articles

*   [Installation guide](/index.php/Installation_guide "Installation guide")
*   [General recommendations](/index.php/General_recommendations "General recommendations")
*   [MacBook5,2 (early-mid 2009)](/index.php/MacBook5,2_(early-mid_2009) "MacBook5,2 (early-mid 2009)")
*   [MacBookPro7,1](/index.php/MacBookPro7,1 "MacBookPro7,1")
*   [MacBookPro8,1/8,2/8,3 (2011)](/index.php/MacBookPro8,1/8,2/8,3_(2011) "MacBookPro8,1/8,2/8,3 (2011)")
*   [MacBookPro9,2 (Mid-2012)](/index.php/MacBookPro9,2_(Mid-2012) "MacBookPro9,2 (Mid-2012)")
*   [MacBookPro10,x](/index.php/MacBookPro10,x "MacBookPro10,x")
*   [MacBookPro11,x](/index.php/MacBookPro11,x "MacBookPro11,x")
*   [iMac Aluminum](/index.php/IMac_Aluminum "IMac Aluminum")
*   [Apple Fusion Drive](/index.php/Apple_Fusion_Drive "Apple Fusion Drive")

Installing Arch Linux on a MacBook (12"/Air/Pro) or an iMac is quite similar to installing it on any other computer. However, due to the specific hardware configuration of a Mac, there are a few deviations and special considerations which warrant a separate guide. For more background information, please see the [Installation guide](/index.php/Installation_guide "Installation guide") and [UEFI](/index.php/UEFI "UEFI"). This guide contains installation-instructions that can be used on any Apple computer whose hardware is supported by the Linux kernel. Please see 'related' pages (on the top right of this page) for model-specific tips and troubleshooting.

## Contents

*   [1 Overview](#Overview)
*   [2 Firmware updates](#Firmware_updates)
*   [3 Partitions](#Partitions)
    *   [3.1 Arch Linux only](#Arch_Linux_only)
    *   [3.2 Arch Linux with OS X or other operating systems](#Arch_Linux_with_OS_X_or_other_operating_systems)
        *   [3.2.1 Option 1: EFI](#Option_1:_EFI)
        *   [3.2.2 Option 2: BIOS-compatibility](#Option_2:_BIOS-compatibility)
    *   [3.3 OS X, Windows XP, and Arch Linux triple boot](#OS_X.2C_Windows_XP.2C_and_Arch_Linux_triple_boot)
*   [4 Setup bootloader](#Setup_bootloader)
    *   [4.1 Using the native Apple bootloader with systemd-boot (Recommended)](#Using_the_native_Apple_bootloader_with_systemd-boot_.28Recommended.29)
    *   [4.2 Using the native Apple bootloader with GRUB](#Using_the_native_Apple_bootloader_with_GRUB)
    *   [4.3 Other methods](#Other_methods)
    *   [4.4 Installing GRUB to EFI partition directly](#Installing_GRUB_to_EFI_partition_directly)
    *   [4.5 Using blessing](#Using_blessing)
    *   [4.6 Compilation](#Compilation)
*   [5 Installation](#Installation)
*   [6 Post-installation](#Post-installation)
    *   [6.1 Video](#Video)
        *   [6.1.1 NVIDIA note](#NVIDIA_note)
    *   [6.2 Touchpad](#Touchpad)
    *   [6.3 Keyboard](#Keyboard)
        *   [6.3.1 Keyboard Backlight](#Keyboard_Backlight)
            *   [6.3.1.1 NVIDIA note](#NVIDIA_note_2)
    *   [6.4 Wi-Fi](#Wi-Fi)
    *   [6.5 Power management](#Power_management)
        *   [6.5.1 Suspend and Hibernate](#Suspend_and_Hibernate)
    *   [6.6 Light sensor](#Light_sensor)
    *   [6.7 Sound](#Sound)
    *   [6.8 Bluetooth](#Bluetooth)
    *   [6.9 Magic Mouse](#Magic_Mouse)
    *   [6.10 Webcam](#Webcam)
        *   [6.10.1 iSight](#iSight)
        *   [6.10.2 Facetime HD](#Facetime_HD)
    *   [6.11 Temperature Sensors](#Temperature_Sensors)
    *   [6.12 Color Profile](#Color_Profile)
    *   [6.13 Apple Remote](#Apple_Remote)
    *   [6.14 HFS partition sharing](#HFS_partition_sharing)
    *   [6.15 HFS+ Partitions](#HFS.2B_Partitions)
        *   [6.15.1 Journaling](#Journaling)
        *   [6.15.2 Yosemite and later](#Yosemite_and_later)
    *   [6.16 Home Sharing](#Home_Sharing)
        *   [6.16.1 In OS X](#In_OS_X)
            *   [6.16.1.1 Step 1: change UID and GID(s)](#Step_1:_change_UID_and_GID.28s.29)
            *   [6.16.1.2 Step 2: change "Home" permissions](#Step_2:_change_.22Home.22_permissions)
        *   [6.16.2 In Arch](#In_Arch)
    *   [6.17 Avoid long EFI wait before booting](#Avoid_long_EFI_wait_before_booting)
    *   [6.18 Mute startup chime](#Mute_startup_chime)
    *   [6.19 kworker using high CPU](#kworker_using_high_CPU)
*   [7 rEFIt](#rEFIt)
    *   [7.1 Problems with rEFIt](#Problems_with_rEFIt)
        *   [7.1.1 Mavericks upgrade breaks Arch boot option](#Mavericks_upgrade_breaks_Arch_boot_option)
*   [8 Model-specific information](#Model-specific_information)
    *   [8.1 MacBook](#MacBook)
        *   [8.1.1 April 2016 12" - Version 9,1](#April_2016_12.22_-_Version_9.2C1)
        *   [8.1.2 Mid 2007 13" - Version 2,1](#Mid_2007_13.22_-_Version_2.2C1)
    *   [8.2 MacBook Pro](#MacBook_Pro)
        *   [8.2.1 Early 2015 13"/15" - Version 12,x/11,4+](#Early_2015_13.22.2F15.22_-_Version_12.2Cx.2F11.2C4.2B)
            *   [8.2.1.1 Wireless](#Wireless)
            *   [8.2.1.2 Bluetooth](#Bluetooth_2)
            *   [8.2.1.3 Suspend & Power Off (11,4+)](#Suspend_.26_Power_Off_.2811.2C4.2B.29)
            *   [8.2.1.4 Keyboard & Trackpad](#Keyboard_.26_Trackpad)
            *   [8.2.1.5 Graphics](#Graphics)
        *   [8.2.2 2012 - 2014 models](#2012_-_2014_models)
    *   [8.3 MacBook Air](#MacBook_Air)
        *   [8.3.1 Early 2014 11" - Version 6,1](#Early_2014_11.22_-_Version_6.2C1)
        *   [8.3.2 Mid 2013 13" - Version 6,2](#Mid_2013_13.22_-_Version_6.2C2)
            *   [8.3.2.1 Installing and booting](#Installing_and_booting)
            *   [8.3.2.2 Arch Only Installation](#Arch_Only_Installation)
            *   [8.3.2.3 Stability problems](#Stability_problems)
            *   [8.3.2.4 Marvell ATA suspend bugs](#Marvell_ATA_suspend_bugs)
            *   [8.3.2.5 Suspend/Resume](#Suspend.2FResume)
            *   [8.3.2.6 WiFi](#WiFi)
            *   [8.3.2.7 Touchpad](#Touchpad_2)
            *   [8.3.2.8 Audio](#Audio)
        *   [8.3.3 Mid 2012 13" — version 5,2](#Mid_2012_13.22_.E2.80.94_version_5.2C2)
        *   [8.3.4 Mid 2012 11.5" — Version 5,1](#Mid_2012_11.5.22_.E2.80.94_Version_5.2C1)
        *   [8.3.5 Mid 2011 — version 4,x](#Mid_2011_.E2.80.94_version_4.2Cx)
        *   [8.3.6 Early 2008 — version 1,1](#Early_2008_.E2.80.94_version_1.2C1)
*   [9 See also](#See_also)

## Overview

Specifically, the procedure for installing Arch Linux on a MacBook is:

1.  **[Firmware updates](#Firmware_updates)**: It always helps to start from a clean, backed up, and up-to-date install of OS X.
2.  **[Partition](#Partitions)**: Resizing or deleting the OS X partition to create partitions for Arch Linux.
3.  **[Setup bootloader](#Setup_bootloader)**: Making sure that the new partition is bootable.
4.  **[Install Arch Linux](#Installation)**: Actually installing Arch Linux.
5.  **[Post-installation](#Post-installation)**: MacBook-specific configuration.

## Firmware updates

Before proceeding with the installation of Arch Linux, it is important to ensure that the latest firmware updates for you MacBook are installed. This procedure requires OS X. In OS X, open the App Store and check for updates. If your mac finds and installs any updates, make sure to **reboot** your computer, and then check again for updates to make sure that you installed everything.

**Note:** If you uninstalled OS X or want to reinstall it, [Apple](https://support.apple.com/en-us/HT204904) has great instructions.

It is advisable to keep OS X installed, because MacBook firmware updates can only be installed using OS X. However, if you plan to remove OS X completely, make backups of these files, which you will need in Linux for adjusting the [color profile](#Color_Profile):

```
/Library/ColorSync/Profiles/Displays/*

```

Continue to [#Partitions](#Partitions)

## Partitions

Partitioning of the storage drive is no different from any other PC or laptop. However, if you plan on keeping OS X for dual booting, you should consider that, by default, a MacBook's drive is formatted using GPT and contains at least 3 partitions:

*   **EFI**: the ~200 MB [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition").
*   **OS X**: the main partition containing your OS X installation. It is formatted using [HFS+](/index.php/File_systems "File systems").
*   **Recovery**: A recovery partition present in almost all MacBooks running OS X 10.7 or newer. It is usually hidden from OS X but can be viewed with partitioning tools.

**Note:** In Macs that use the [Apple Fusion Drive](/index.php/Apple_Fusion_Drive "Apple Fusion Drive"), the partition scheme could be different.

How to partition depends on how many operating systems you want install. The following options will be explained:

*   Single boot: [#Arch Linux only](#Arch_Linux_only)
*   Dual boot: [#Arch Linux with OS X or other operating systems](#Arch_Linux_with_OS_X_or_other_operating_systems) *(recommended so you can still return to OS X when needed)*
*   Triple boot: [#OS X, Windows XP, and Arch Linux triple boot](#OS_X.2C_Windows_XP.2C_and_Arch_Linux_triple_boot)

### Arch Linux only

This situation is the easiest to deal with. Partitioning is the same as any other hardware that Arch Linux can be installed on. Please refer to the standard [Installation guide](/index.php/Installation_guide "Installation guide") for details.

**Note:** It is advisable to **disable** the MacBook startup sound before proceeding with partitioning. Just boot in OS X, mute your system sound and reboot again to the Arch Linux Installation media. Please keep in mind that the volume of the startup sound can only be modified reliably in OS X.

If you want to configure you system in order to have full-disk encryption, please look at the [Dm-crypt/Encrypting an entire system](/index.php/Dm-crypt/Encrypting_an_entire_system "Dm-crypt/Encrypting an entire system") page for details.

An example for a very basic partitioning, that does not consider a separate `/home` partition nor encryption or LVM, is the following:

```
partition  mountpoint  size    type  label
/dev/sda1  /boot       200MiB  vfat  EFI
/dev/sda2  /swap       adjust  swap  swap
/dev/sda3  /           remain  ext4  root

```

*   Done, you can continue to [#Installation](#Installation)

### Arch Linux with OS X or other operating systems

You need to partition your hard drive while keeping the partitions used for OS X/Windows. If you wish to keep OS X, the easiest way is to use partitioning tools in OS X and then finish with Arch Linux tools.

**Warning:** If you OS X partition is encrypted with FileVault 2, you **must** disable the disk encryption before proceeding. After the OS X partition has been resized, FileVault 2 can be re-enabled.

**Procedure**:

*   In OS X, run *Disk Utility.app* (located in `/Applications/Utilities`)
*   Select the drive to be partitioned in the left-hand column (not the partitions!). Click on the **Partition** button.
*   Add a new partition by pressing the **+** button and choose how much space you want to leave for OS X, and how much for the new partition. Keep in mind the new partition will be formatted in Arch Linux, so you can choose any partition type you want.
*   If the above completed successfully, then you can continue. If not, then you may need to fix your partitions from within OS X first.
*   Boot the Arch installation media or [LiveUSB](/index.php/USB_flash_installation_media "USB flash installation media") by holding down the `Alt` **during boot**. Proceed with [#Installation](#Installation).

It is possible to resize the newly created partition from within the Arch installation media, or delete it in order to proceed with the creation of other partitions (eg. swap).

**Tip:** Instead of cluttering your drive with different partition, it is possible to use a [swapfile](/index.php/Swapfile "Swapfile") instead of a dedicated partition. Another solution can be setting up [LVM](/index.php/LVM "LVM") in order to use the newly-created partition as a container. Please refer to the linked articles.

#### Option 1: EFI

*   Run *cgdisk*

*   Delete the partition you made in *Disk Utility.app* and create the necessary partitions for Arch Linux. OS X likes to see a 128 MiB gap after partitions, so when you create the first partition after the last OS X-partition, type in **+128M** when cgdisk asks for the first sector for the partition. More information about Apple's partitioning policy can be read [here](https://developer.apple.com/library/mac/technotes/tn2166/_index.html#//apple_ref/doc/uid/DTS10003927-CH1-SUBSECTION5). A simple example (no LVM, crypto):

**Note:**

*   The swap partition is optional on machines with 4GB of RAM or more. A **[swap file](/index.php/Swap_file "Swap file")** can be created later.
*   The easiest dual-boot option is to install rEFInd from inside OS X, to its root directory (default for `install.sh`). Following that, copy the driver folder from the installation tarball into the new rEFInd location, and uncomment the lines *"scan_all_linux_kernels"* and *"also_scan_dirs"* options in `refind.conf`. Configuration of boot options can then be done from a `refind_linux.conf` in Arch's `/boot` directory.
*   If you want to be able to boot GRUB from the Apple boot loader, you can create a small hfs+ partition (for convenience, use OS X to format it in *Disk Utility.app* afterwards). Follow the GRUB EFI install procedure, and mount your `/boot/efi` directory to the hfs+ partition you created. Finally, finish up again in OS X by blessing the partition. This will set GRUB as the default boot option (holding alt at startup goes to the mac boot options screen still. See [http://mjg59.dreamwidth.org/7468.html](http://mjg59.dreamwidth.org/7468.html)).,
*   OS X's EFI partition can be shared with Arch Linux, making the creation of an additional EFI partition dedicated to Arch completely optional.

**Note:** For more information on partitioning, see [Partitioning](/index.php/Partitioning "Partitioning")

```
partition  mountpoint  size       type  label
/dev/sda1  /boot/efi   200MiB     vfat  EFI
/dev/sda2  -           ?          hfs+  OS X
/dev/sda3  -           ?          hfs+  Recovery
/dev/sda4  -           100MiB     hfs+  Boot Arch Linux from the Apple boot loader (optional)
/dev/sda5  /boot       100MiB     boot  boot
/dev/sda6  -           ?          swap  swap (optional)
/dev/sda7  /           10GiB      ext4  root
/dev/sda8  /home       remaining  ext4  home

```

*   Done, you can continue to [#Installation](#Installation)

#### Option 2: BIOS-compatibility

*   Run *parted* as root.

*   Delete the empty space partition and partition the space as you would for any other installation. Note that MBR is limited to 4 primary partitions (including the efi partition). That leaves 2 primary partitions for Arch. One strategy is to have a system and home partition, and use a swap file (I have not tried to use logical partitions). Another is to dedicate one partition to a shared partition (see below).

*   Next, create new filesystems on those partitions which need them, especially the partition which will contain `/boot`. If you are not sure how to do this using `mkfs.ext2` (or whatever), run `/arch/setup` and work through until you get to Prepare Hard Drive and use the *"Manually configure block devices..."* option, then exit the installer. This is necessary so that rEFIt will set the right partition type in the MBR in the next step (without an existing filesystem, it seems to ignore the partition type set by parted), without which GRUB will refuse to install to the right partition.

*   At this point you should reboot your computer and have rEFIt fix the partition tables on your hard drive. (If you do not do this, you may have to reinstall GRUB later on in order to have your Mac recognize the Linux partition.) When you are into the rEFIt menu, select **update partition table**, then press `y`. Reboot.

*   Done, you can continue with [#Installation](#Installation).

### OS X, Windows XP, and Arch Linux triple boot

This may not work for everyone but it has been successfully tested on a MacBook from late 2009.

The easiest way to partition your hard drive, so that all these operating systems can co-exist, is to use disk utility in OS X, use the formatter on windows XP, install XP and then finish with Arch Linux tools.

**Warning:** It is highly recommended that this only be attempted after a clean install of OS X. Using these methods on a pre-existing system may have undesired results. At least back your stuff up with timemachine or clonezilla before you begin.

**Procedure**:

*   In OS X, run **Disk Utility** (located in `/Applications/Utilities`).

*   Select the drive to be partitioned in the left-hand column (not the partitions!). Click on the **partition** tab on the right.

*   Select the volume to be resized in the **volume scheme.**

*   Decide how much space you wish to have for your OS X partition, how much for XP, and how much for Arch Linux. Remember that a typical installation of OS X requires around 15-20 GiB, and XP about the same, depending on the number of software applications and files. Something like OS X 200Gb, XP 25Gb, Arch 25Gb should be fine.

*   Put your decisions into action by pressing the + button and adding the new partitions, Label them as you like and make sure that your XP partition is the last one on the disk and is formatted for FAT32\. It is probably best to have Arch formatted in HFS format as to not confuse you later, it will be reformatted anyway.

So in linux terms your partitions will be something like:

*   sda (disk)
*   sda1 (Mac boot partition - you cannot see this one in OS X)
*   sda2 (OS X install in HFS+)
*   sda3 (Arch install temporarly in HFS)
*   sda4 (XP install in FAT32)

*   Finally, click **apply**. This will create a new partition out of the empty space.

**Note:** Using this method you may not be able to have a shared partition between OS X and Arch Linux, this is because the mac will only allow for 4 active partitions. You will however be able to mount a HFS partition in Arch for one workaround. There are other workarounds possible also.

*   If the above completed successfully, you can continue. If not, then you may need to fix your partitions from within OS X first.

*   You will not be needing boot camp this way, the program rEFIt is much more flexible (though not as flexible as GRUB). Download and install rEFIt [[1]](http://refit.sourceforge.net/)

*   Go into a terminal in OS X and perform the following, this will enable the rEFIt boot manager.

```
cd /efi/refit
./enable.sh

```

*   Reboot to check the rEFIt is working, it should appear on boot. When it comes up go to the rEFIt partition manager and agree to the changes.

*   Put your XP install CD and boot it with rEFIt - You may have to reboot a few times until it is recognized by the boot loader. Install XP and once it is installed use the OS X installation CD to get your drivers running nicely in XP.
    *   Note: when installing XP make sure you select your XP partition and format it again inside the XP installer. If you do not reformat it will not work.

*   Boot the Arch install CD, log in as root and run `# /arch/setup`.

*   Follow the install as normal but note that you will have to tell that arch installer to mount sda3 as the root partition and format it as ext3, there will not be a /boot or swap partition so ignore those warnings.

*   At this point, if you are dual booting, you should reboot your computer and have rEFIt fix the partition tables on your hard drive. (If you do not do this, you may have to reinstall GRUB later on in order to have your Mac recognize the Linux partition.) When you are into the rEFIt menu, select **update partition table**, then press Y.

```
# reboot

```

*   Done! You can continue to [#Installation](#Installation).

## Setup bootloader

### Using the native Apple bootloader with systemd-boot (Recommended)

Apple's native EFI bootloader reads `.efi` files located inside the [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition") at `/EFI/BOOT/BOOTX64.EFI`. Luckily, this is also the default install location for the [systemd-boot](/index.php/Systemd-boot "Systemd-boot") binary. This means that booting linux using *systemd-boot* is very simple.

*   First, make sure you mounted the EFI System Partition at `/boot`
*   Proceed with [#Installation](#Installation) normally
*   Once inside the chrooted enviroment, type the following command to install *systemd-boot*:

 `# bootctl --path=/boot install` 

The above command will copy the *systemd-boot* binary to `/boot/EFI/BOOT/BOOTX64.EFI` and add *systemd-boot* itself as the default EFI application (default boot entry) loaded by the EFI Boot Manager.

*   Proceed to [systemd-boot#Configuration](/index.php/Systemd-boot#Configuration "Systemd-boot") in order to correctly set up the bootloader

At the next reboot, the Apple Boot Manager, shown when holding down the option key when booting the MacBook, should display Arch Linux (it will be displayed as `EFI Boot` as a possible boot option.

**Tip:** If you installed Arch Linux alongside OS X, you will be able to change the default boot location from system Settings inside OS X. If Arch Linux does not show up as a possible boot option, you will have to mount the EFI System Partition inside OS X before selecting your boot option: `$ diskutil mount disk0s1` 

### Using the native Apple bootloader with GRUB

Despite using UEFI, the MacBook's native EFI bootloader [does not use the EFI partition for booting](http://refit.sourceforge.net/myths/). Instead, it looks for .efi files inside all the partitions in internal and external drives and shows them as possible boot options if certain conditions are satisfied. For example, MacBooks can detect an existing OSX installation after checking that:

*   there is a partition formatted as HFS+
*   the partition contains the partition id `af00`
*   in the root of that partition, there is a file called `mach_kernel`
*   inside that partition, there a `boot.efi` file inside `/System/Library/CoreServices`

This means that configuring an Arch installation to be automatically recognized by the MacBook bootloader is possible. Moreover, it simply requires a properly-formatted HFS+ `/boot` partition and does not require meddling with the EFI system partition. The advantage of this method is that it can coexist with OS X nicely and allows to avoid other bootloaders such as rEFInd. However, this requires manual configuration. The following steps will illustrate how to perform this configuration using GRUB.

*   First, while configuring a new Arch installation, create a separate `/boot` partition. Many tools are available in the Arch ISO, for example **cgdisk**.
*   Make sure the partition is at least ~250 MB in size, since it will be used to store the kernel as well as any custom kernel you will install in the future. Moreover, make sure the partition type is set as Apple HFS/HFS+ (it will appear as `Apple HFS/HFS+` in fdisk/cgdisk or `af00` in gdisk)
*   Since the Arch installation ISO does not include the [hfsprogs](https://aur.archlinux.org/packages/hfsprogs/) package, we need to install it in the installation environment before proceeding with formatting the new partition as HFS+

```
 # pacman -Sy hfsprogs
 # modprobe hfsplus
 # mkfs.hfsplus /dev/sd**X** -v "Arch Linux"

```

Note: replace /dev/sd**X** with the correct device as appropriate

*   Done, proceed with [#Installation](#Installation)

**Warning:**

Once inside the chrooted enviroment, don’t forget to install the [hfsprogs](https://aur.archlinux.org/packages/hfsprogs/) package on the newly installed system as well. After the installation of the package, regenerate the initramfs while chrooted

```
 # mkinitcpio -p linux

```

*   Once inside the chrooted enviroment, install the [grub](https://www.archlinux.org/packages/?name=grub) and [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) packages. The following steps install the GRUB UEFI application to `/boot/EFI/arch/System/Library/CoreServices/boot.efi` and install its modules to `/boot/grub/x86_64-efi`.

```
 # grub-install --target=x86_64-efi --efi-directory=/boot

```

After that, remember to create a standard configuration file:

```
 # grub-mkconfig -o /boot/grub/grub.cfg

```

As you can see, the directory structure of the `boot.efi` is not correct, as the `/System/Library/CoreServices` directory is not supposed to be a subdirectory of the `/boot/EFI/` folder. For this reason, we need to relocate the `boot.efi` stub in a location the MacBook bootloader is able to recognize:

```
 # mv /boot/EFI/arch/System/ /boot/
 # rm -r /boot/EFI/

```

Also, create a dummy `mach_kernel` file

```
 # touch /boot/mach_kernel

```

After that, you need to create the following file

 `# nano /boot/System/Library/CoreServices/SystemVersion.plist` 
```
<?xml version="1.0" encoding="UTF-8"?>
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

At the next reboot, the Apple Boot Manager, shown when holding down the option key when booting the MacBook, should display Arch Linux as a possible boot option. Selecting that option will boot GRUB.

Done! GRUB can now be selected on the standard MacBook bootloader and you can boot into your newly installed Arch Linux.

**Tip:** After the installation, it is optionally possible to set a custom icon that will be displayed in the MacBook boot loader. In order to do that, you need to install the [wget](https://www.archlinux.org/packages/?name=wget), [librsvg](https://www.archlinux.org/packages/?name=librsvg) and [libicns](https://aur.archlinux.org/packages/libicns/) packages. After that, just follow the following commands:
```
 $ wget -O /tmp/archlinux.svg [https://www.archlinux.org/logos/archlinux-icon-crystal-64.svg](https://www.archlinux.org/logos/archlinux-icon-crystal-64.svg)
 $ rsvg-convert -w 128 -h 128 -o /tmp/archlogo.png /tmp/archlinux.svg
 $ sudo png2icns /boot/.VolumeIcon.icns /tmp/archlogo.png
 $ rm /tmp/archlogo.png
 $ rm /tmp/archlinux.svg

```

Obviously, you can replace the Arch logo with any other icon you like.

### Other methods

**Tip:** rEFIt is a popular bootloader for EFI-firmware computers (including Macs). It can be installed at any time during the installation. For instructions, please see [#rEFIt](#rEFIt).

If you are going for an Arch Linux-only setup, installing the bootloader is no different than on any other machine: Install [systemd-boot](/index.php/Systemd-boot "Systemd-boot"), [rEFInd](/index.php/REFInd "REFInd") or other bootloader of your choice.

If, on the other hand, you are dual/triple booting, then read on.

### Installing GRUB to EFI partition directly

*   If you would like to use GRUB as your main bootloader and use the "boot while holding the Alt/Option key" method to go back to OS X rather than using alternatives such as rEFIt ([http://refit.sourceforge.net/](http://refit.sourceforge.net/), mentioned previously in [#Option 2: BIOS-compatibility](#Option_2:_BIOS-compatibility) and [#OS X, Windows XP, and Arch Linux triple boot](#OS_X.2C_Windows_XP.2C_and_Arch_Linux_triple_boot)) then you must install [grub](https://www.archlinux.org/packages/?name=grub) to your Mac's **already-existing** EFI partition (see below).

**Note:** These instructions are known to work on a MacBook Pro (Early 2011). Please read the procedure carefully **as well as the details following it**.

**Note:** With a new MacBook Pro (Mid 2014), this procedure worked only after installing the [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) package.

**Procedure**:

*   Install [grub](https://www.archlinux.org/packages/?name=grub)

*   Make a directory named `efi` in `/boot`

*   Mount the **already-existing** EFI partition on your Mac to this `/boot/efi` directory

*   Install GRUB to this directory

*   Make a directory named `locale` in `/boot/grub`

*   Copy `grub.mo` from `/usr/share/locale/en\@quot/LC_MESSAGES/` to `/boot/grub/locale`

*   Generate a configuration for GRUB

*   Done! GRUB will now start on reboot and you can boot into your newly installed Arch Linux.

*   Remember to hold ALT/Option key **while** starting your computer if you want to boot back into OS X.

**Details (quoted from [GRUB EFI Examples#M5A97](/index.php/GRUB_EFI_Examples#M5A97 "GRUB EFI Examples")):**

Finish the standard Arch install procedures, making sure that you install [grub](https://www.archlinux.org/packages/?name=grub) and partition your boot hard disk as GPT.

From [GRUB#UEFI systems](/index.php/GRUB#UEFI_systems "GRUB"):

The UEFI system partition will need to be mounted at `/boot/efi/` for the GRUB install script to detect it:

```
# mkdir -p /boot/efi
# mount -t vfat /dev/sdXY /boot/efi

```

Where X is your boot hard disk and Y is the efi partition you created earlier.

Install GRUB UEFI application to and its modules to `/boot/grub/x86_64-efi` using:

```
# modprobe dm-mod
# grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=arch_grub --recheck --debug
# mkdir -p /boot/grub/locale
# cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo

```

Generate a configuration for GRUB

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

### Using blessing

It is possible to boot directly from GRUB in EFI mode without using rEFIt through what is known as "blessing" after placing GRUB on a **separate partition**. These instructions are known to work on a MacBook7,1\. It is advisable to host GRUB on either a FAT32 or HFS+ partition, but ext2 or ext3 may also work. GRUB's appleloader command does not currently work with the 7,1, but support can be added with the patch available [here](https://savannah.gnu.org/bugs/index.php?33185).

After the GRUB install is in the desired location, the firmware needs to be instructed to boot from that location. This can be done from either an existing OS X install or an OS X install disk. The following command assumes that the GRUB install is in `/efi/grub` on an existing OS X partition:

```
 # bless --folder /efi/grub --file /efi/grub/grub.efi

```

### Compilation

Some models may need EFI_ARCH set to i386.

```
 bzr branch --revision -2 bzr://bzr.savannah.gnu.org/grub/trunk/grub grub
 cd grub
 ./autogen.sh
 patch -p1 < appleloader_macbook_7_1.patch
 export EFI_ARCH=x86_64
 ./configure --with-platform=efi --target=${EFI_ARCH} --program-prefix=""
 make
 cd grub-core
 ../grub-mkimage -O ${EFI_ARCH}-efi -d . -o grub.efi -p "" part_gpt part_msdos ntfs ntfscomp hfsplus fat ext2 normal chain boot configfile linux multiboot
 cp grub.efi *.mod *.lst yourinstalllocation

```

## Installation

**Note:** This section is only required if you want to have OS X installed along with Arch Linux. If not, follow the steps in the official install guide, then skip to [#Post-installation](#Post-installation).

*   Boot from the Arch Linux install CD, or from a [manually created](/index.php/USB_flash_installation_media#Using_manual_formatting "USB flash installation media") bootable USB drive.

**Note:**

*   On a MacBookPro7,1, I had an error booting the installation media Version 2012.12.01: "unable to handle kernel NULL pointer dereference at 0000000000000010" during pacpi_set_dmamode. To fix this problem, boot with the option: acpi=off. After chrooting, add MODULES="ata_generic" into /etc/mkinitcpio.conf and execute mkinitcpio -p linux, see: [Installation Guide, 9 Configure the system](/index.php/Installation_guide#Configure_the_system "Installation guide").
*   Some MacBook users report strange keyboard output such as long delays and character doubling. To fix this problem, boot with the following options: arch noapic irqpoll acpi=force

*   Proceed through the installation as described in the [Installation guide](/index.php/Installation_guide "Installation guide") **except** in the following areas:
    *   Skip the [partition the disks](/index.php/Installation_guide#Partition_the_disks "Installation guide") stage, do only the [partition formatting](/index.php/Installation_guide#Format_the_partitions "Installation guide") and [mounting](/index.php/Installation_guide#Mount_the_file_systems "Installation guide") steps, taking care to assign the correct partitions. Partitions have already been created if you followed [#Partitions](#Partitions)
    *   **(for booting with EFI**) After the [install boot loader](/index.php/Installation_guide#Boot_loader "Installation guide") stage, exit the installer and install [GRUB](/index.php/GRUB "GRUB").
    *   **(for booting with BIOS-compatibility)** In the [install boot loader](/index.php/Installation_guide#Boot_loader "Installation guide") stage, edit the menu.lst file and add **reboot=pci** to the end of the **kernel** lines, for example: `kernel /vmlinuz-linux root=/dev/sda5 ro reboot=pci` This will allow your MacBook to reboot correctly from Arch.
    *   **(for booting with BIOS-compatibility)** Also in the [install boot loader](/index.php/Installation_guide#Boot_loader "Installation guide") stage, install GRUB on whatever partition that `/boot` is on.
        **Warning:** Do not install GRUB onto */dev/sda* !!! Doing so is likely to lead to an unstable post-environment.

    *   In the [configure system](/index.php/Installation_guide#Configure_the_system "Installation guide") stage, edit /etc/mkinitcpio.conf and ensure the **keyboard** hook is in the **HOOKS** line somewhere after the **autodetect** hook. This will load the drivers for your keyboard in case you need to use it before Arch boots (e.g. entering a [LUKS](/index.php/LUKS "LUKS") password or using the troubleshooting shell).

*   When the install process is complete, reboot your computer.

*   If using optical media, hold down the eject key as your MacBook starts, this should eject the Arch Linux install disk.

*   If dual-booting OS X and Arch Linux, hold down the alt (option) key while the system boots to use the Mac bootloader to select which OS to boot.

## Post-installation

See [General recommendations](/index.php/General_recommendations "General recommendations") for system management directions and post-installation tutorials like setting up a graphical user interface, sound or a touchpad.

#### Video

Different MacBook models have different graphic cards. To see which graphics card you have type:

```
$ lspci | grep VGA

```

*   If it returns a string containing **Intel**, read [Intel graphics](/index.php/Intel_graphics "Intel graphics").

*   If it returns **NVIDIA**, read [NVIDIA](/index.php/NVIDIA "NVIDIA").

*   Otherwise if it returns **ATI** or **AMD**, read [ATI](/index.php/ATI "ATI").

##### NVIDIA note

**Tip:** If you have installed OS in EFI mode and NVIDIA binary drivers are working only in BIOS mode (e.g. you get black screen on EFI boot), try this approach: [http://askubuntu.com/a/613573/492886](http://askubuntu.com/a/613573/492886)

For MacBooks with NVIDIA graphics, for the backlight to work properly you may need the [nvidia-bl](https://aur.archlinux.org/packages/nvidia-bl/) package.

**Tip:**

*   If backlight control does not work after installing nvidia-bl, you should [blacklist](/index.php/Blacklist "Blacklist") apple_bl kernel module.
*   If backlight control does not work even this way, try setting module parameters. Uncommenting `options nvidia_bl max_level=0x1ffff shift=11` in `/etc/modprobe.d/nvidia_bl.conf` should do the trick.
*   Alternatively, you can choose to use the [pommed-light](https://aur.archlinux.org/packages/pommed-light/) package. If you do so, you may wish to change the step settings in `/etc/pommed.conf.mactel` to something around 5000-10000 depending on how many levels of brightness you desire. The max brightness is around 80000, so take that into account.

#### Touchpad

The touchpad should have basic functionality by default. A true multitouch driver which behaves very similarly to native OS X is included in the [xf86-input-mtrack-git](https://aur.archlinux.org/packages/xf86-input-mtrack-git/) package. Configuration options are documented in the [readme](https://github.com/BlueDragonX/xf86-input-mtrack).

The following mtrack options work well on a MacBook7,1:

```
 Option "Thumbsize" "50"
 Option "ScrollDistance" "100"

```

Probably, you also need to add:

```
 MatchDevicePath "/dev/input/event10"

```

To disable tap-to-click (that is, to press down to click) by default, add the following to your mtrack configuration section

```
   Option          "TapButton1" "0"  
   Option          "TapButton2" "0"
   Option          "TapButton3" "0"

```

**Natural scrolling:** To configure natural two finger scrolling similar to [OS X](http://www.apple.com/au/osx/what-is/gestures.html#gallery-gestures-scroll), refer to [Touchpad Synaptics#Natural scrolling](/index.php/Touchpad_Synaptics#Natural_scrolling "Touchpad Synaptics").

If you are using [xf86-input-mtrack-git](https://aur.archlinux.org/packages/xf86-input-mtrack-git/), you can simply swap the scroll up and scroll down buttons (along with the scroll left and scroll right):

 `/etc/X11/xorg.conf.d/10-mtrack.conf` 
```
  ...
  Option "ScrollUpButton" "5"
  Option "ScrollDownButton" "4"
  Option "ScrollLeftButton" "7"
  Option "ScrollRightButton" "6"
  ...
```

**Special Note About Older Macbook Models (confirmed on MacBook2,1):** On older Macbook models (pre-multitouch), the touchpad will not function properly until you install the xf86-input-synaptics package. Please see [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") for more information on installing and configuring this package.

**Note on MacBookPro5,5:** I found it is much simpler to use the [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) in Extra. Although it does not have much function as 3 finger swipe, this driver provides faster response. [gpointing-device-settings](https://aur.archlinux.org/packages/gpointing-device-settings/) also provides a simple GUI config. Below is a Xorg config file /etc/X11/xorg.conf.d/60-synaptics.conf for reference only.

```
 Section "InputClass"
       Identifier "touchpad catchall"
       Driver "synaptics"
       MatchIsTouchpad "on"
       MatchDevicePath "/dev/input/event*"
       Option "SHMConfig" "on"
       Option "TapButton1" "1"
       Option "TapButton2" "3"
       Option "TapButton3" "2"
       Option "PalmDetect" "on"
       Option "VertEdgeScroll" "off"
       Option "HorizEdgeScroll" "off"
       Option "CornerCoasting" "off"
       Option "EdgeMotionUseAlways" "off"
       Option "AreaLeftEdge" "10"
       Option "AreaRightEdge" "1270"
 EndSection

```

**For some users, the two-finger right-click may not work correctly and trackpad may also become less responsive after these settings. For me, removing the 'AreaLeftEdge' and 'AreaRightEdge', solved that problem.** **OS X like MultiTouch Gestures** *currently broken due to newer synaptic drivers!* For users looking to add more of OS X's multitouch gestures to Arch, [xSwipe](https://github.com/iberianpig/xSwipe) is a highly customisable, light weight perl script, which does just that. Once installed and configured (see xSwipe wiki on Github) I would recommend adding xSwipe as a [start up item](/index.php/Autostarting "Autostarting").

#### Keyboard

MacBook keyboards work by default. For swaping fn keys with Fx keys see [Apple Keyboard](/index.php/Apple_Keyboard "Apple Keyboard").

To enable it you can map with right application like **xbindkeys** or through DE preferences; but another very good way, that we recommend, is to install the [pommed-light](https://aur.archlinux.org/packages/pommed-light/) package.

Edit the `/etc/pommed.conf` according to your hardware on MacBook, building it from `/etc/pommed.conf.mac` or `/etc/pommed.conf.ppc` example files.

Note that you can also run it without a configuration file, the defaults may work for you. Then [enable](/index.php/Enable "Enable") and start `pommed.service`.

**Tip:** if you are using Gnome or KDE you can easily configure *3rd level functionality*, *multimedia key*, etc. in Keyboard Preferences.

**Note:** See the [Xorg input hotplugging](/index.php/Xorg_input_hotplugging "Xorg input hotplugging") page for other configuration information.

##### Keyboard Backlight

The keyboard backlight is controlled by `/sys/class/leds/smc::kbd_backlight`. Write the desired value to `brightness` in that directory.

Both [acpilight](https://aur.archlinux.org/packages/acpilight/) or [kbdlight](https://aur.archlinux.org/packages/kbdlight/) (stalled since 2015) allow to control keyboard backlight though scripts. With the appropriate udev rules or [sxhkd](/index.php/Sxhkd "Sxhkd") they allow light-level changes without being root.

As of 2017-11-12, [acpilight](https://aur.archlinux.org/packages/acpilight/) provides a "just-works" solution tested on a MacbookPro 8,1\.

Alternatively you might want to check out the [Keyboard backlight](/index.php/Keyboard_backlight "Keyboard backlight") wiki page.

###### NVIDIA note

If the brightness does not function correctly through pommed, make sure you have installed the [nvidia-bl](https://aur.archlinux.org/packages/nvidia-bl/) package and insert

```
find . -name "*" -exec sed -i 's/mbp_backlight/nvidia_backlight/' '{}' \;

```

into the second line of the pommed PKGBUILD build() function and remake the package. From [this forum post](https://bbs.archlinux.org/viewtopic.php?id=105091).

Another possible solution is to modify the pommed PKGBUILD build():

```
find . -name "*" -exec sed -i 's/nvidia_backlight/apple_backlight/' '{}' \;

```

If the previous does not work try the following,

run nvidia-settings, edit the file '/etc/X11/xorg.conf' and add this line into the Device section:

```
Option "RegistryDwords" "EnableBrightnessControl=1"

```

Save and reboot and check backlight buttons work. More information available at [Ubuntu MacBookPro5,5](https://help.ubuntu.com/community/MacBookPro5-5/Precise#LCD)

### Wi-Fi

Different MacBook models have different wireless cards.

You can easily check what card do your MacBook have by:

```
# lspci | grep Network

```

*   If you have an Atheros card, all should work out-of-the-box.

*   If you have a Broadcom card, follow the [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless") page.

*   5.0 and 6.0 generation MacBooks may have a BCM43xx, follow the instructions for the broadcom-wl driver on the [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless") page. The interfaces can swap during reboot so its best to define them in a udev rule (instructions on the [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless") page).

*   8.1 generation MacBooks have BCM4331, for which support is not present in either Linux (3.0 and 3.1) or the proprietary drivers by Broadcom. There is however preliminary support for it in Linux 3.2\. To run the drivers on earlier kernels, you will need to use [compat-drivers](https://backports.wiki.kernel.org/index.php/Documentation/compat-drivers)

*   If you have the correct broadcom DKMS driver (i.e. broadcom-wl-dkms) installed and your wifi card is still not being recognised, try rebuilding the driver (See [Dynamic Kernel Module Support](/index.php/Dynamic_Kernel_Module_Support "Dynamic Kernel Module Support")).

**Note:**

*   If your connection frequently drops, you may have to turn off Wi-Fi power management.
*   Eduroam or similar may crash your network manager. Simply delaying the connection after login should do the trick

### Power management

[Powerdown](/index.php/Powerdown "Powerdown") is a very simple to set up set of scripts what will maximize your battery duration. A MacBook Air 2013 with powerdown provides about 11 hours of light usage with just powerdown installed. All the usual [power management](/index.php/Power_management "Power management") recomendations apply as well.

Adding 'acpi_osi=' to kernel parameters reportedly brings the battery life of a MacBook Air 2013 from 5 hours to 11-12 hours. See [this forum post](https://bbs.archlinux.org/viewtopic.php?pid=1530283#p1530283) for more information.

#### Suspend and Hibernate

Suspending (suspend to ram) and hibernating (suspend to disk) work fine out of the box:

```
   systemctl suspend

```

Issues were reported where the machine would "suspend immediately after resume" in certain conditions when suspending by closing the lid. This was solved by setting the option "sleep-inactive-ac-type" to "nothing" using dconf-editor, option path: org → gnome → settings-daemon → plugins → power).

See [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate") for details on how to configure hibernation. Noticably, you'll need a swap partition or file (see the mentioned article for further instructions).

If after suspend laptop is woken up after few seconds, may help to disable all stuff in /proc/acpi/wakeup, exclude LID0:

```
# echo XHC1 > /proc/acpi/wakeup
$ cat /proc/acpi/wakeup
Device	S-state	  Status   Sysfs node
P0P2	  S3	*disabled
EC	  S3	*disabled
HDEF	  S3	*disabled  pci:0000:00:1b.0
RP01	  S3	*disabled  pci:0000:00:1c.0
RP02	  S3	*disabled  pci:0000:00:1c.1
RP03	  S3	*disabled  pci:0000:00:1c.2
ARPT	  S4	*disabled  pci:0000:03:00.0
RP05	  S3	*disabled  pci:0000:00:1c.4
RP06	  S3	*disabled  pci:0000:00:1c.5
SPIT	  S3	*disabled
XHC1	  S3	*disabled  pci:0000:00:14.0
ADP1	  S3	*disabled
LID0	  S3	*enabled

```

And for permanent disabling:

```
$ cat /etc/udev/rules.d/90-xhc_sleep.rules 

# disable wake from S3 on XHC1
SUBSYSTEM=="pci", KERNEL=="0000:00:14.0", ATTR{power/wakeup}="disabled"

```

If this does not work, check that ARPT is disabled, and add a corresponding rule to udev, like this:

```
SUBSYSTEM=="pci", KERNEL=="0000:03:00.0", ATTR{power/wakeup}="disabled"

```

If this still does not work, try disabling LID0. This way suspending via lid-closing should be made impossible, so you might want to follow the instructions in [this forum post](https://bbs.archlinux.org/viewtopic.php?pid=1556046#p1556046) to make suspending via both lid-closing and systemd possible, by using systemd services.

### Light sensor

The values can be read from:

```
 /sys/devices/platform/applesmc.768/light

```

A "cat" on this path returns two-tuples like (4,0). The below referenced lighter script ignores the second value - which always seems to be 0 - and uses the first number as measured environment lighting brightness value.

If you want to use the built in light sensor to automatically adjust screen and keyboard backlight brightness check out **Lighter** [[2]](https://github.com/Janhouse/lighter) (simple perl script, easy to fine-tune) and **Lightum** [[3]](https://github.com/poliva/lightum) (Requires Gnome or KDE but is older and more complete than Lighter).

### Sound

**Tip:** If using [ALSA](/index.php/ALSA "ALSA"), the internal speaker might not be disabled when using the headphone jack. To solve this, enable "Auto-mute" using `alsamixer`

First of all follow [ALSA](/index.php/ALSA "ALSA") wiki page, then if something does not work correctly, continue reading this part.

Edit your `/etc/modprobe.d/50-sound.conf` or `/etc/modprobe.d/modprobe.conf` appending this line:

```
options snd_hda_intel model=intel-mac-auto

```

This should automatically specify the codec in your MacBook. If you have a MacBookPro12,1, you might need

```
 options snd-hda-intel index=1,0

```

instead. Alternatively, for MacBookPro5,X, you can use:

```
options snd_hda_intel model=mb5

```

(note that the jack output is controlled with "HP").

If you have an iMac8,1, you should instead use

```
options snd-hda-intel model=mbp3 position_fix=2

```

For Aluminium iMacs, see [iMac Aluminium#Getting sound to work right](/index.php/IMac_Aluminium#Getting_sound_to_work_right "IMac Aluminium")

You can try to specify other options, that depend on your hardware. All other possible settings are listed in Kernel Documentation, avaible online:

*   [ALSA-Configuration.txt](http://www.kernel.org/doc/Documentation/sound/alsa/ALSA-Configuration.txt)
*   [HD-Audio.txt](http://www.kernel.org/doc/Documentation/sound/alsa/HD-Audio.txt)
*   [HD-Audio-Models.txt](http://www.kernel.org/doc/Documentation/sound/alsa/HD-Audio-Models.txt).}}

Then, reboot.

### Bluetooth

Bluetooth should work out-of-the box. See the article on [Bluetooth](/index.php/Bluetooth "Bluetooth") to install and configure all software needed.

### Magic Mouse

If you use a magic mouse you will find it works nicely out of the box. You might want to tweak some settings such as *scroll-speed* or *acceleration*. There is no GUI for this at this time. The only way to set these settings is to instruct the kernel driver (`hid_magicmouse`) with parameters. Create a modprobe config file for your mouse.

 `/etc/modprobe.d/magicmouse.conf`  `options hid_magicmouse scroll-speed=55 scroll-acceleration=1 emulate_3button=0` 

This will instruct the driver to have a fast scroll-speed, do exponential acceleration and do not emulate a 3 button mouse. You can find an overview of all parameters and their current settings in `/sys/module/hid_magicmouse/parameters`.

To play with the settings without rebooting you can also set them through the command line, like so:

```
# echo 55 > /sys/module/hid_magicmouse/parameters/scroll_speed

```

**Note:** Using kernel *4.10.10-1-macbook* the Magic Mouse (*hid_magicmouse*) will cause a lot of system lock ups. If you experience random lock ups, try a different, wired, mouse to see if this is the case for you as well.

### Webcam

#### iSight

**Note:** Linux kernel from 2.6.26 includes the Linux UVC driver natively. **MBP 6,2+ (Kernel ~2.6.37+) iSight works out of the box** without the need to use firmware from OS X. Only use `isight-firmware-tools` if it doesn't work normally.

iSight webcams on MacBooks or pre 6,2 MacBook Pros (6,2 came out around 2010) require the Apple's proprietary firmware that cannot be redistributed. It must be extracted from OS X and loaded onto Arch.

You will need to install [isight-firmware-tools](https://aur.archlinux.org/packages/isight-firmware-tools/) to extract the firmware. This package also includes a udev rule and ELF binary that are necessary, even once you have extracted the firmware file into `/lib/firmware/isight.fw`, for the file to be loaded every time you boot your computer (namely `/etc/udev/rules.d/isight.rules` which uses `/usr/lib/udev/ift-load`).

Instructions:

First you need to get the firmware out of a particular file located on your OS X install. It is located in `/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/AppleUSBVideoSupport.kext/Contents/MacOS/AppleUSBVideoSupport`.

**Tip:** The `AppleUSBVideoSupport` file from a OS X 10.6 (Snow Leopard) installation may not work properly. If possible, use the file from OS X 10.5 or earlier.

To mount the OS X drive if multi-booting:

```
# mkdir /media/OSX
# mount -t hfsplus /dev/sda2 /media/OSX

```

Then, install the [isight-firmware-tools](https://aur.archlinux.org/packages/isight-firmware-tools/) package.

Locate the `AppleUSBVideoSupport` file in the OS X directory listed above. Either copy it over to your Arch system (Any OS X installation should do, such as an iMac, not just one specific to your system) or, if multi-booting, mount the OS X drive and navigate to the directory. (On 10.7 (Lion) the directory is `/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/AppleUSBVideoSupport.kext/Contents/MacOS`.) In that directory you can go ahead and extract the driver:

```
# ift-extract --apple-driver AppleUSBVideoSupport

```

When it's done, check that the firmware has been found:

```
# ls /lib/firmware/isight.fw

```

Once successful, completely **SHUTDOWN** your Mac and start it back up again (to clear the hardware state of the webcam). Do *not* reboot.

It should be automatically loaded at boot; if it isn't you can load the **uvcvideo** module [manually or load it at boot](/index.php/Kernel_modules "Kernel modules").

You can use many applications to test the webcam:

*   MPlayer

```
# mplayer tv:// -tv driver=v4l2:width=320:height=240:device=/dev/video0 -fps 30

```

*   Cheese
*   Skype
*   Ekiga

A simple solution to take snapshots is:

```
# mplayer tv:// -vf screenshot

```

and the pressing the s key to take a snapshot. Files are of the format `shot\d\d\d\d.png` and are reported in the standard output.

#### Facetime HD

According to Apple, all recent MacBook models contain a Facetime HD camera instead of the iSight. The following list is an example:

*   iMac (21,5" mid 2011)
*   iMac (27" mid 2011)
*   MacBook Air (mid 2011)
*   MacBook Pro (15" early 2011)
*   MacBook Pro (17" early 2011)
*   MacBook Pro (13" early 2011)

If your MacBook is more recent than the models listed above, it is likely equipped with the Facetime HD camera as well.

In order to make the camera work, you need to install the [bcwc-pcie-git](https://aur.archlinux.org/packages/bcwc-pcie-git/) package. This will enable camera video support through the `facetimehd` kernel module.

In order to verify if the Facetime camera is working after the installation of both packages, you'll need to reboot your system.

**Note:** Keep in mind that, although working, this is a reverse-engineered driver. PC suspension is not supported if a program that is keeping the camera active is running.

### Temperature Sensors

For reading temperature just install [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors). See the [lm_sensors](/index.php/Lm_sensors "Lm sensors") page for more information.

### Color Profile

We can use color profiles from OS X.

First, install the [xcalib](https://aur.archlinux.org/packages/xcalib/) package.

Second copy pre-saved color profiles placed in `/Library/ColorSync/Profiles/Displays/` on OS X partition to `~/colorprofiles/` for example.

There are color profile files agree with in MacBook models; select the right one:

*   **Color LCD-4271800.icc** for MacBook Pro with CoreDuo CPU
*   **Color LCD-4271880.icc** for MacBook with Core2Duo
*   **Color LCD-4271780.icc** for MacBook (non-Pro) based on CoreDuo or Core2Duo.

**Tip:** Also OS X allows to save current color profile from *Displays > Color* section of the *Mac OS System Preferences*, in this case file is saved to `/Users/<username>/Library/ColorSync/Profiles`.

Finally you can activate it by running

```
# xcalib ~/colorprofile.icc

```

**Note:** Previous command set the color profile only for the current session; this mean that you must run it every time you login in your system. For automating it you can execute the command by **Autostart Application**, concording with your DE (or add the command to your login manager's initialization script, e.g. /etc/gdm/Init/Default).

**Warning:** GNOME will revert the profile set by xcalib. It's preferable to set the profile using **Color** in settings.

### Apple Remote

First, to correctly install and configure the **lirc** software that control IR see [LIRC](/index.php/LIRC "LIRC") wiki.

Then make LIRC use `/dev/usb/hiddev0` (or `/dev/hiddev0`) by editing `/etc/conf.d/lircd`. Here is how mine look:

```
#
# Parameters for lirc daemon
#
LIRC_DEVICE="/dev/usb/hiddev0"
LIRC_DRIVER="macmini"
LIRC_EXTRAOPTS=""
LIRC_CONFIGFILE="/etc/lirc/lircd.conf"

```

Use **irrecord** (available when installing **lirc**) to create a configuration file matching your remote control signals (alternatively, you can try to use the `lircd.conf` below):

```
# irrecord -d /dev/usb/hiddev0 -H macmini output_conf_file

```

Start **lircd** and use **irw** to check if it works.

Example of an `/etc/lirc/lircd.conf`:

```
begin remote

  name  lircd.conf.macbook
  bits            8
  eps            30
  aeps          100

  one             0     0
  zero            0     0
  pre_data_bits   24
  pre_data       0x87EEFD
  gap          211994
  toggle_bit_mask 0x87EEFD01

      begin codes
          Repeat                   0x01
          Menu                     0x03
          Play                     0x05
          Prev                     0x09
          Next                     0x06
          Up                       0x0A
          Down                     0x0C
      end codes

end remote

```

### HFS partition sharing

First, install the [hfsprogs](https://aur.archlinux.org/packages/hfsprogs/) package.

we have to list our partitions. Use

```
fdisk -l /dev/sda

```

example output:

```
# fdisk -l /dev/sda
    Device  Boot     Start         End      Blocks   Id  Type
 /dev/sda1               1          26      204819   ee  GPT
 /dev/sda2              26       13602   109051903+  af  Unknown
 /dev/sda3   *       13602       14478     7031250   83  Linux
 /dev/sda4           14478       14594      932832+  82  Linux swap / Solaris

```

As we see, the "Unknown" partition is our OS X partition, which is located in `/dev/sda2`.

Create a "mac" folder in /media:

```
# mkdir /media/mac

```

Add at the end of */etc/fstab* this line:

```
/dev/sda2    /media/mac     hfsplus auto,user,rw,exec   0 0

```

Mount it :

```
mount /media/mac

```

and check it:

```
ls /media/mac

```

### HFS+ Partitions

#### Journaling

HFS+ partitions, now the default in OS X, are not fully supported by Linux and are mounted as read-only by default. In order to write to an HFS+ partition, the safe way is to disable journaling. This can be accomplished using the OS X Disk Utility. Refer to this [Apple support page](http://support.apple.com/kb/ht2355) for more information or try to do it from the command line:

Find your partition:

 `# diskutil list` 
```
/dev/disk0
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                        *750.2 GB   disk0
   1:                        EFI EFI                     209.7 MB   disk0s1
   2:                  Apple_HFS OSX                     149.5 GB   disk0s2
   3:                  Apple_HFS Macintosh HD            599.2 GB   disk0s3
   4:                 Apple_Boot Recovery HD             650.0 MB   disk0s4

```

In this example we will use *disk0s3* partition named as *Macintosh HD*. To know if journaling is activate or not you could execute:

 `# diskutil info /dev/disk0s3 | grep -i journal` 
```
    File System Personality:  Journaled HFS+
    Name (User Visible):      Mac OS Extended (Journaled)
    Journal:                  Journal size 49152 KB at offset 0x1176000

```

As you can read the journaling is active. To turn off the journaling you could execute:

```
# diskutil disableJournal disk0s3

```

To verify it is done execute the info command again.

If you get noting as output, then journaling is disabled.

However, if you fail to disable journaling. You can change "auto,user,rw,exec" in `/etc/fstab` to "auto,user,force,rw,exec" and mount it.

#### Yosemite and later

Since Yosemite, HFS+ partitions are now wrapped a CoreStorage volume. Verify that you have an CoreStorage volume.

```
# fdisk -l /dev/sdX
 Disk /dev/sdX: 298.1 GiB, 320072933376 bytes, 625142448 sectors
 Units: sectors of 1* 512 = 512 bytes
 Sector size (logical/physical): 512 bytes / 4096 bytes
 I/O size (minimum/optimal): 4096 bytes / 4096 bytes
 Disklabel type: gpt
 Device      Start      End         Sectors    Size     Type
 /dev/sdX1   40         409639      409600     200M     EFI System
 /dev/sdX2   409640     623872871   623463232  297.3G   Apple Core storage
 /dev/sdX3   623872872  625142407   1269536    916.0M   Apple boot

```

HFS+ uses two volume headers, one 1024 bytes into the device and one 1024 from the end of the device. With the HFS+ partition wrapped in the CoreStorage volume the end of the partition is not actually 1024 bytes from the end of the `/dev/sdX2` partition. To fix this you need to specify `sizelimit=X` when mounting.

To determine `sizelimit` do the following:

1.  Run `testdisk /dev/sdX` and select your drive
2.  Select `EFI GPT`
3.  Select `Analyse` and then `Quick Search`

Sample output:

```
 TestDisk 7.0, Data Recovery Utility, April 2015
 Christophe GRENIER <grenier@cgsecurity.org>
 [http://www.cgsecurity.org](http://www.cgsecurity.org)

 Disk /dev/sdX  - 320 GB / 298 GiB - CHS 38913 255 63
     Partition     Start      End        Size in sectors
 P  EFI System     40         409639     409600  [EFI]
 P  Mac HFS        409640     623147815  622738176
 P  Mac HFS        623872872  625142407  1269536

```

What you see now is the output of the HFS partition itself without the CoreStorage volume. Take the size in sectors (622738176 in this example) and multiply by the number of bytes in your logical sector size (512 in this example).

622738176 * 512 = 318841946112

Finally, mount your disk with the `sizelimit=X` option.

```
 mount /dev/sdX -t hfsplus -o ro,sizelimit=318841946112

```

### Home Sharing

***UID Synchronization***

#### In OS X

**Note:** It is strongly recommended that UID/GID manipulation be done immediately after a new user account is created, in OS X as well as in Arch Linux. If you installed OS X from scratch, then this operation is guaranteed to work after logging into your account for the first time.

##### Step 1: change UID and GID(s)

***Pre-Leopard***

1.  Open **NetInfo Manager** located in the */Applications/Utilities* folder.
2.  If not done for you already, enable access to user account transactions by clicking on the closed lock at the bottom of the window, and entering your account password, or root password if you have created a root account.
3.  Navigate to */users/<new user name>* where <new user name> is the name of the account that will have read/write access to the folder that will be shared with the primary user in Arch.
4.  Change the **UID** value to 1000 (the value used by default for first user created in Arch).
5.  Also change the **GID** value to 1000 (the value used by default for user account creation in Arch).
6.  Navigate to `/groups/<new user name>`, automatically saving the changes you have made so far.

**Note:** If you get an error message that the transaction is not allowed, log out and log back in.

***Leopard***

In Leopard, the **NetInfo Manager** application is not present. A different set of steps is required for UID synchronization:

1.  Open **System Preferences**.
2.  Click on **Users & Groups**.
3.  Unlock the pane if not already done so.
4.  Right-click on the desired user and select **Advanced Options**.
5.  Write down the value of the **User ID** field, you will need it later on. Change both the UID and GID to match the UID and GID of the account wished to be shared with in Arch (1000 by default for the first user created in Arch).

##### Step 2: change "Home" permissions

1.  Open up **Terminal** in the `/Applications/Utilities` folder.

1.  Enter the following command to reclaim the permission settings of your home folder, replacing <your user name>, <your user group> and <your old UID> with the user name whose UID and GID values you just changed, the group name whose GID value you just changed and the old UID number, respectively.

```
# find /User/<your user name> -user <your old UID> -exec chown <your user name>:<your user group> {} \;

```

#### In Arch

To synchronize your UID in Arch Linux, you are advised to perform this operation *while creating a new user account*. It is therefore recommended that you do this as soon as you install Arch Linux.

Now you must substitute Arch's home with OS X's home, by modify entries of `/etc/fstab`.

### Avoid long EFI wait before booting

If your MacBook spends 30 seconds with "white screen" before booting you need to tell the firmware where is the booting partition.

Boot OS X, if do not have it installed, you can use the install DVD (select language, then click Utilities->Terminal), or another MacBook with OS X (connect the two computers via firewire or thunderbolt, start the other MacBook keeping pressed T, boot your MacBook keeping pressed Options).

Either way, once you got a OS X terminal running on your MacBook you need to execute, as root, a different command if the boot partition is EFI or it is not:

```
# bless --device /dev/disk0s1 --setBoot            # if the booting partition is EFI

```

or

```
# bless --device /dev/disk0s1 --setBoot --legacy   # if the booting partition is not EFI

```

(given that if your GRUB or EFI is on sda1, /dev/disk1s2 if it is on sdb2, etc). See also [https://bbs.archlinux.org/viewtopic.php?pid=833215](https://bbs.archlinux.org/viewtopic.php?pid=833215) and [https://support.apple.com/kb/HT1533](https://support.apple.com/kb/HT1533) .

### Mute startup chime

The startup chime volume is controlled by the EFI variable *SystemAudioVolume-7c436110-ab2a-4bbb-a880-fe41995c9f82*. So it can be muted with

```
# printf "\x07\x00\x00\x00\x00" > /sys/firmware/efi/efivars/SystemAudioVolume-7c436110-ab2a-4bbb-a880-fe41995c9f82

```

Alternatively, you can use a OS X install disk to mute the chime. Boot from it, select language, then click *Utilities > Terminal*, and enter

```
# /usr/sbin/nvram SystemAudioVolume=%01

```

(or whatever volume you want).

**Note:** Required formatting of the value provided for key SystemAudioVolume may differ depending on MacBook model and perhaps the version of OS X install media. If the above command fails to work, try enclosing the value in double quotes.

### kworker using high CPU

Sometime with the addition of Yosemite, some users found that kworker CPU usage will spike, as disccused [here](https://bbs.archlinux.org/viewtopic.php?id=171883&p=11). This is sometimes the result of runaway ACPI interrupts.

To check and see, you can count the number of recent ACPI interrupts and see if any of them are out of control.

```
   grep . -r /sys/firmware/acpi/interrupts/

```

If you see that one particular interrupt is out of control (possibly GPE66), i.e., registering hundreds of thousands of lines, you can try disabling it (replace XX with the runaway interrupt):

```
   echo "disable" > /sys/firmware/acpi/interrupts/gpeXX

```

Disabling random ACPI interrupts could cause all kinds of problems, so do this at your own risk. If this fixes the problem, there is discussion about how to make a systemd service that automatically disables an interrupt at every boot [here](https://bbs.archlinux.org/viewtopic.php?pid=1488371).

## rEFIt

**Note:**

*   You probably want to have a look at [rEFInd](http://www.rodsbooks.com/refind/), which is some type of successor of rEFIt.
*   This is not a requirement. It only gives you a menu to choose between OS X and Arch Linux upon every boot.

For more see, [rEFIt myths](http://refit.sourceforge.net/myths/).

In OS X, download the ".dmg" from [rEFIt Homepage](http://refit.sourceforge.net/) and install it.

**Note:** If you have already partitioned your hard disk in preparation for the Arch installation, rEFIt may not be enabled by default. You will have to run the "enable.sh" script installed in /efi/refit/.

Open up **Terminal** and enter:

```
cd /efi/refit;
./enable.sh

```

### Problems with rEFIt

If you experience problems after the install of Arch or rEFIt, especially is the right OS is not showing up to boot to or if it dumps you at a GRUB prompt stuck like the following:

```
GRUB>_

```

Then have a look at this link:

[http://mac.linux.be/content/problems-refit-and-grub-after-installation](http://mac.linux.be/content/problems-refit-and-grub-after-installation)

It can give you a basic idea on how to boot off the Arch live cd, mount the problem Arch install, chroot, use gptsync, and reinstall GRUB. This is probably for more advanced users who can translate the commands from a debian system to an Arch system and also apply it to the partitions on their machine. Be careful not to install GRUB in the wrong spot.

If you need a copy of gptsync you can wget it from here: [http://packages.debian.org/sid/gptsync](http://packages.debian.org/sid/gptsync) or try these, for 64 bit:

wget [http://ftp.us.debian.org/debian/pool/main/r/refit/gptsync_0.14-2_amd64.deb](http://ftp.us.debian.org/debian/pool/main/r/refit/gptsync_0.14-2_amd64.deb)

and for i386:

```
wget [http://ftp.us.debian.org/debian/pool/main/r/refit/gptsync_0.14-2_i386.deb](http://ftp.us.debian.org/debian/pool/main/r/refit/gptsync_0.14-2_i386.deb)

```

since they are .deb packages you will need the program [deb2targz](https://aur.archlinux.org/packages/deb2targz/).

#### Mavericks upgrade breaks Arch boot option

For some multi-boot users who utilize a separate Linux boot partition, the OS X Mavericks upgrade may overwrite the boot partition with Apple's own recovery boot filesystem. This breaks the Arch Linux boot option in rEFIt/rEFInd. The best way to proceed in this situation is to abandon a separate boot partition and use the EFI system partition (ESP) to install the bootloader of your choice. It is also recommended that you use rEFInd instead of rEFIt as development on the latter has halted.

Assuming grub2 as the bootloader:

Use the Arch LiveCD to boot to a shell and [chroot](/index.php/Chroot "Chroot") to your broken Arch Linux environment.

Mount the ESP on /boot.

Edit the fstab and remove the old boot partition and make ESP the new boot partition. Now mount the ESP as the new /boot parition.

```
# mount -a

```

[Reinstall](/index.php/Install "Install") the [linux](https://www.archlinux.org/packages/?name=linux) package.

Create a new initramfs and vmlinuz in /boot.

```
# mkinitcpio -p linux

```

Install grub.

```
# grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=grub --recheck --debug

```

Create a new grub.cfg file.

```
# grub-mkconfig -o /boot/EFI/grub/grub.cfg

```

Make sure that grub.cfg is in the same directory as grubx64.efi.

Generate a new refind_linux.conf file in /boot simply by running mkrlconf.sh which comes with rEFInd.

Exit the chroot environment.

Reboot. You should see a new entry for Arch Linux in rEFInd and it should boot to your Arch Linux installation.

## Model-specific information

### MacBook

#### April 2016 12" - Version 9,1

*   Booting from USB via EFI works fine, when giving the `intremap=nosid` kernel option. (On Ubuntu, also `noacpi nomodeset` seem to be necessary.) Remember to hold the Alt key on booting to enter the boot menu.

*   The wireless card works out of the box with `brcmfmac`.

*   Suspend / hibernate does not work. The problem seems to be the NVMe that does not wake up. When booting from an external drive, suspend / hibernate works out of the box.

*   Audio recording works out of the box. Audio playback works, but the built-in speakers don't (no solution yet).

*   The keyboard and the touchpad do *not* work out of the box. There is a work-in-progress driver available that works well: [macbook12-spi-driver-dkms](https://aur.archlinux.org/packages/macbook12-spi-driver-dkms/). Sometimes the touchpad does not work after booting but this can be fixed by reloading the driver with `rmmod applespi && modprobe applespi`.

*   The keyboard backlight does not work (no solution yet).

#### Mid 2007 13" - Version 2,1

**Note:** I used the 201212 ISO image.

Since older Macbooks have a 32bit EFI running, the usual installation image is not recognized. You need to either remove the UEFI support from the disc ([Unified Extensible Firmware Interface#Remove_UEFI_boot_support_from_ISO](/index.php/Unified_Extensible_Firmware_Interface#Remove_UEFI_boot_support_from_ISO "Unified Extensible Firmware Interface")) or build a 32bit EFI version of the disc. The paragraphs below will take the first path to success, booting into BIOS mode and its pitfalls. For a try the other way round, read [Unified Extensible Firmware Interface#Create UEFI bootable USB from ISO](/index.php/Unified_Extensible_Firmware_Interface#Create_UEFI_bootable_USB_from_ISO "Unified Extensible Firmware Interface") first.

First prepare your harddisc according to your wishes. In this scenario it was a "Linux only" approach with

```
/dev/sda1 HFS+ AF00 200M -> EFI boot system on Apple HFS+ partition
/dev/sda2 ext4 8300 147G -> arch system
/dev/sda3 swap 8200 1G   -> swap

```

The [hfsprogs](https://aur.archlinux.org/packages/hfsprogs/) package contains the tools to handle HFS/HFS+ filesystems. The rEFInd bootloader recognizes it on its own. Usually the partition for the EFI bootloader is a FAT32 (vfat) partition. In this case I tried rEFIt first, which apparently needs the HFS+ filesystem to work, and kept it at that.

The mount points are:

```
/dev/sda2 -> /
/dev/sda1 -> /boot

```

The bootloader in use was [rEFInd](http://www.rodsbooks.com/refind/index.html) instead of rEFIt. To install it, the rEFInd homepage provides a good guide. Usually it is simply done by copying rEFInd:

```
mkdir /boot/EFI
cp -vr /usr/share/refind/drivers_ia32 /boot/EFI/refind/
cp -vr /usr/share/refind/tools_ia32 /boot/EFI/refind/
cp -vr /usr/share/refind/fonts /boot/EFI/refind/
cp -vr /usr/share/refind/icons /boot/EFI/refind/
cp -v /usr/share/refind/refind_ia32.efi /boot/EFI/refind/
cp -v /usr/share/refind/refind.conf-sample /boot/EFI/refind/refind.conf
cp -v /usr/share/refind/refind_linux.conf-sample /boot/refind_linux.conf

```

**Note:** I'm using the 32bit version of Arch and refind, since the EFI of the old MacBooks is 32bit. I'm not sure about 32bit rEFInd booting a 64bit Arch...

The pitfall here is, that the system bootet in BIOS compatibility mode and not in EFI mode. You cannot therefore use `efibootmgr`, because the EFI variables (even with 'modprobe efivars') are not available. While installing the system get [mactel-boot](https://aur.archlinux.org/packages/mactel-boot/). The `hfs-bless` utility comes in handy, when blessing the EFI bootloader. This is done by calling:

```
hfs-bless /boot/EFI/refind/refind_ia32.efi

```

Since the Linux kernel does come with EFI stub enabled, it seems a good idea to run it through a bootloader first. Especially if it runs not out of the box. But using rEFInd makes GRUB (or any other bootloader) obsolete, because of that.

**Note:** In the refind_linux.conf you add any kernel option you may want as long as you use the EFI stub of your kernel. In refind.conf you adjust your needs for the bootloader itself, like menu entries. If you use them (menu entries), rEFInd should not look for these EFI stub kernels itself, so blacklist the directories used in here, like `/boot/`.

Not running out of the box is unfortunately the initial stage for the kernel. Since we installed it in BIOS mode, two modules are missing to grant access to the root partition while booting. Hence the 'initfsram-linux.img' can not be found/loaded. Adding the following modules to your 'MODULES' line in `/etc/mkinitcpio.conf` solved this ([original post](https://bbs.archlinux.org/viewtopic.php?pid=1139226#p1139226)).

 `/etc/mkinitcpio.conf`  `MODULES="ahci sd_mod"` 

Rebuild your kernel image:

```
mkinitcpio -p linux

```

The bootloader rEFInd can scan kernels even out of the '/boot/...' directory and assumes an efi kernel even without the extension '.efi'. If you do not want to try out special kernels, this should work without the hassle to copy each kernel after building to some spot special.

If you happen to get multiple entries for one boot image, it often results of a previous installation of a bootloader within the MBR. To remove that, try the following - taken from the [original post](http://ubuntuforums.org/showpost.php?p=7828260&postcount=4). This is valid for GPT partitioned discs, so please check your environment and save your MBR first.

```
# dd if=/dev/zero of=/dev/sda bs=440 count=1

```

### MacBook Pro

#### Early 2015 13"/15" - Version 12,x/11,4+

##### Wireless

The `brcmfmac` driver is working as of 2015-11-20, with newer firmware necessary for working 5GHz support ([see here.](https://bugzilla.kernel.org/show_bug.cgi?id=100201#c65))

**Note:** On the Macbook Pro 12,1 if the `brcmfmac` driver can not be started and the following errors occur in the journal:
```
brcmfmac: brcmf_chip_recognition: chip backplane type 15 is not supported
brcmfmac: brcmf_pcie_probe: failed 14e4:43ba

```

then check whether [PCI runtime power management](/index.php/Power_management#PCI_Runtime_Power_Management "Power management") is enabled on the device, and disable it if so.

##### Bluetooth

Bluetooth is fully supported starting from kernel-4.4.0.

##### Suspend & Power Off (11,4+)

The 11,4 and 11,5 MacBook Pros do not shutdown or suspend correctly with the default kernel. This issue is being addressed in [Bug 103211](https://bugzilla.kernel.org/show_bug.cgi?id=103211) and a temporary patch is currently available in [linux-macbook](https://aur.archlinux.org/packages/linux-macbook/). Note that [Linux 4.13.0](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/arch/x86/pci/fixup.c?h=v4.13-rc1&id=13cfc732160f7bc7e596128ce34cda361c556966) has this patch included, and will be released shortly.

##### Keyboard & Trackpad

Haptic feedback works out of the box due to the trackpad's built-in firmware.

There are several drivers available that provide multitouch support. The following have been confirmed working with the MacBookPro12,1.

For [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) the following configuration emulates some features from the OS X functionality. For more options see [libinput(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libinput.4).

 `/etc/X11/xorg.conf.d/90-libinput.conf` 
```
Section "InputClass"
    Identifier "libinput touchpad catchall"
    MatchIsTouchpad "on"
    MatchDevicePath "/dev/input/event*"
    Driver "libinput"
    Option "NaturalScrolling" "true"
EndSection
```

For [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) the following configuration is necessary to make the touchpad work fully.

 `/etc/X11/xorg.conf.d/60-magictrackpad.conf` 
```
Section "InputClass"
    Identifier "Trackpad"
    Driver "synaptics"
    MatchIsTouchpad "on"
    MatchDevicePath "/dev/input/event*"
EndSection
```

Further, some US/ANSI keyboards suffer from an issue where the tilde key (~, the key vertically between Esc and Tab) registers as < and >. The following config file fixes this issue.

 `/etc/modprobe.d/hid_apple.conf`  `options hid_apple iso_layout=0` 

See [this kernel bugzilla](https://bugzilla.kernel.org/show_bug.cgi?id=96771) for more details and the relevant patches for earlier kernels.

##### Graphics

For Intel-only graphics, install the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) package. For more information or OpenGL/3D support, follow instructions at [Intel graphics](/index.php/Intel_graphics "Intel graphics").

As of [linux](https://www.archlinux.org/packages/?name=linux) kernel 4.16.6 dual graphics switching does work on the 11,5 (2015) with Intel modesetting and the AMD GPU utilizing the radeon driver (amdgpu is untested). See [MacBookPro11,x#Graphics](/index.php/MacBookPro11,x#Graphics "MacBookPro11,x") to enable the integrated graphics. Once the laptop boots with integrated graphics enabled you can use VGA Switcheroo controls to power down the discrete GPU. However, if you keep it powered on you will be able to utilize HDMI connections and using [switcheroo-control](https://aur.archlinux.org/packages/switcheroo-control/) you can run applications on the AMD GPU.

**Note:** The kernel parameters *acpi_backlight*, *i915.lvds_downclock*, *i915.enable_ips*, and *intel_iommu* are no longer necessary as of kernel 4.2.

**Note:** (Kernel 4.10.8, MacBook Pro 11,4+) If you experience system lock ups and/or tearing in Xorg, remove the .[xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) completely, including any config file you made for it. Xorg will default to its modesetting DDX driver. The performance of this driver is good and the locks go away. See also: [Intel graphics](/index.php/Intel_graphics "Intel graphics")

**Note:** If you are experiencing flickering issues with Xorg, you can set *i915.enable_rc6* to 0 parameter into the kernel parameters which will disable to power saving of [Intel graphics](/index.php/Intel_graphics "Intel graphics").

#### 2012 - 2014 models

*   [MacBookPro11,x](/index.php/MacBookPro11,x "MacBookPro11,x") (Late 2013—Mid 2014)
*   [MacBookPro10,x](/index.php/MacBookPro10,x "MacBookPro10,x") (Mid 2012—Early 2013)

### MacBook Air

#### Early 2014 11" - Version 6,1

This is almost the same as the 2013 version, where the only known difference is a slightly faster processor. The version numbers have not been changed since the 2013 version.

It works excellently after following the instructions for the MBA 2013 13" here and in the forum thread. Bluetooth, which has been reported not working for some people with the 2013 version, works without trouble for the 2014 version, although it should be excactly the same.

**Note:** Unless you have a local repository on a USB disk, you need a USB to ethernet adaptor or a USB wireless adaptor supported natively by the kernel to easily install Arch Linux, since you have to install the [broadcom-wl-dkms](https://www.archlinux.org/packages/?name=broadcom-wl-dkms) package to make the internal wireless adaptor work.

Unresolved issues:

*   There is no driver for the webcam yet.
*   rEFInd uses 30 seconds to start booting. Using the bless trick stops rEFInd from loading, and it has to be re-installed.

#### Mid 2013 13" - Version 6,2

[Dedicated forum thread](https://bbs.archlinux.org/viewtopic.php?id=165899)

##### Installing and booting

Booting from a normal 2013.6 USB key works fine, but I could not seem to get either GRUB or Syslinux working.

I was able to boot by first installing Arch Linux following the MacBook guide at the wiki (having a separate FAT32 /boot partition). Skip the bootloader installation.

Installing [rEFInd](http://www.rodsbooks.com/refind/getting.html) from OS X (important!) and installing the EFI stub loader made me able to boot fine.

[Dedicated thread](https://bbs.archlinux.org/viewtopic.php?id=165710).

**Note:** Installing [rEFInd](http://www.rodsbooks.com/refind/getting.html) from Linux (or from OS X, but to the esp) also works fine

##### Arch Only Installation

This method works without rEFInd and uses grub to boot EFI. Partition as follows:

```
 /dev/sda1 200M Microsoft basic data
 /dev/sda2 256M Linux filesystem
 /dev/sda3 4G Linux swap
 /dev/sda4 108.6G Linux filesystem

```

sda1 can also be a HFS+ partition for EFI. This example chooses to use FAT32 (vfat). Although swap is optional, it is required for hibernation. Instead of sda4 for root and home, an alternative partition scheme would be to make sda4 as root and sda5 as home.

Format and mount:

```
 mkfs.vfat -F 32 /dev/sda1
 mkfs.ext2 /dev/sda2
 mkswap /dev/sda3
 swapon /dev/sda3
 mkfs.ext4 /dev/sda4

```

```
 mount /dev/sda4 /mnt
 mkdir /mnt/boot
 mount/dev/sda2 /mnt/boot
 mkdir /mnt/boot/efi
 mount /dev/sda1 /mnt/boot/efi

```

Finish the installation according to the [Installation guide](/index.php/Installation_guide "Installation guide") and skip anything after the bootloader. After you have generated your initramfs and set root passwd follow below to setup grub:

```
 pacman -S grub efibootmgr
 mount -t efivarfs efivarfs /sys/firmware/efi/efivars
 grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=grub --recheck --debug
 grub-mkconfig -o /boot/efi/EFI/grub/grub.cfg
 cp /boot/efi/EFI/grub/grub.cfg /boot/grub/grub.cfg
 cp /boot/efi/EFI/grub/grubx64.efi /boot/efi/EFI/boot/bootx64.efi}}

```

Now you can exit/unmount/reboot:

```
 exit
 umount -R /mnt
 reboot

```

##### Stability problems

**Note:** Passing `libata.force=1:noncq` to the kernel parameters solves the problem.

This is the big worry for me. Every now and then my system hangs for a brief moment and everything involving net or disk access just hangs there for a while and then it seems to work. So far it only seems to happen when I run something disk- or CPU-intensive. Also had an occassion when I could not start X and just got this repeating all over my screen:

```
ata1.00: failed command: WRITE FPDMA QUEUED
ata1.00: cmd 61/08:f0:10:8c:c2/00:00:0b:00:00/40 tag 30 ncq 4096 out
res 40/00:00:00:00:00/00:00:00:00:00/00 Emask 0x4 (timeout)
ata1.00: status: { DRDY }

```

On the next attempt it worked fine. I did SMART short and long tests on my disk and they returned fine:

[smartctl -a](http://pastebin.com/vRE4T2Ld)

There are some messages in my boot that indicate this could be disk and/or ACPI related.

These are with 2013-06 ISO, 3.9.7-1 2013 x86_64 kernel.

[journalctl -b](http://pastebin.com/mjTJaPFa) Seems to only work with the headphone jack, not with the speakers.

[dmesg](http://pastebin.com/SdAcHuKh)

**Note:** Same problem in 2017 with a Macbook Air early 2014\. Updating the firmware (via migration to macOS Sierra) solved the issue.

##### Marvell ATA suspend bugs

If you have 2013 MacBook Air with a Marvell 128 or 256 GB drive, you might get the following ata errors instead after pm-suspend/resumes:

```
ata1: exception Emask 0x10 SAct 0x0 SErr 0x10000 action 0xe frozen
ata1: irq_stat 0x00400000, PHY RDY changed
ata1: SError: { PHYRdyChg }
ata1: hard resetting link
ata1: SATA link up 1.5 Gbps (SStatus 113 SControl 310)
ata1.00: unexpected _GTF length (8)
ata1.00: unexpected _GTF length (8)
ata1.00: configured for UDMA/33
ata1: EH complete

```

Try what Patrick and Tejun figured out on the [linux bug](https://bugzilla.kernel.org/show_bug.cgi?id=62351). I followed what Patrick describes with sata_alpm, and I haven't seen the issue since.

There are more steps on how to resolve this issue in [this thread on the Arch forum](https://bbs.archlinux.org/viewtopic.php?pid=1562168#p1562168)

##### Suspend/Resume

Brightness is either 0% or 100% after resuming from suspend. Until the kernel is fixed, use patjak's fix by installing [mba6x_bl-dkms](https://aur.archlinux.org/packages/mba6x_bl-dkms/). Patjak's github is at [[4]](https://github.com/patjak/mba6x_bl).

##### WiFi

WiFi does not work out of the box. Install [broadcom-wl-dkms](https://www.archlinux.org/packages/?name=broadcom-wl-dkms) to connect to a network.

##### Touchpad

Since 3.10.3 kernel touchpad works perfectly with [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics).

##### Audio

As of Linux 3.12, sound works out of the box. If you do not get sound with only [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils), you may need to create a /etc/asound.conf with below entries:

```
 defaults.pcm.card 1
 defaults.pcm.device 0
 defaults.ctl.card 1

```

#### Mid 2012 13" — version 5,2

Kernel panics using default boot media under arch kernel 3.5\. Adding `intremap=off` fixes this. Additionally, there are problems loading the `applesmc` module (meaning the temperature sensors, fan, and keyboard backlight do not work). These problems are fixed in the linux 3.6-rc4 mainline kernel (I have tested).

#### Mid 2012 11.5" — Version 5,1

If you have issues with waking from sleep while in X11 such as a black screen or showing the console with a frozen mouse cursor then remove [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) and install [xf86-input-mtrack-git](https://aur.archlinux.org/packages/xf86-input-mtrack-git/). This fixed errors such as

```
 (EE) [dix] bcm5974: unable to find touch point 0

```

and backtraces that causes X11 to crash. This might apply to Version 5,2 assuming they use the same trackpad.

#### Mid 2011 — version 4,x

Works out-of-the-box since kernel 3.2\.

#### Early 2008 — version 1,1

Everything works out of the box though you will need the [b43-fwcutter](https://www.archlinux.org/packages/?name=b43-fwcutter) package (or simply [b43-firmware](https://aur.archlinux.org/packages/b43-firmware/)) for the wireless adapter to work.

Since this model has only one USB port, you may find it easiest to install Arch with a powered USB hub. Plug a USB network adapter (wireless or ethernet adapter to plug into a USB port) and your Arch installation media into the USB hub.

If you can't get any result by scanning wireless network after boot, unload modules `b43` and `ssb` and load them again:

```
   rmmod ssb
   rmmod b43
   modprobe b43

```

There is a good chance you will find what's wrong with DMA from the dmesg log.

Even if you can scan wireless networks after reloading the modules, it's still possible that you will only be able to connect to some networks, but not all of them. According to a more detailed discussion here: [http://crunchbang.org/forums/viewtopic.php?id=17368](http://crunchbang.org/forums/viewtopic.php?id=17368), adding `pio=1,qos=0` options to the b43 module can solve this problem.

I tested this for a 13' MacBookAir1,1 with a BCM4321 chipset, and it works.

## See also

*   **MacBook Air**
    *   [Macbook Air Early 2014 — dabase.com](http://dabase.com/blog/Macbook_Air_Early_2014_Archlinux/)
    *   [Installing Archlinux on Macbook Air 2013 — Frank Shin](http://www.frankshin.com/installing-archlinux-on-macbook-air-2013/)
    *   [Arch Linux Installation with OS X on Macbook Air (Dual Boot) — Pankaj Kumar](http://blog.panks.me/posts/2013/06/arch-linux-installation-with-os-x-on-macbook-air-dual-boot/)
    *   [Arch Linux – MacBook Air 2013 — Ryan Gehrig](http://ryangehrig.com/index.php/arch-linux-on-macbook-air-2013/)
    *   [Installing Linux on a Macbook Air (4,2) — Nico Schottelius](http://www.nico.schottelius.org/blog/macbook-air-42-archlinux/)
    *   [Arch linux single, pure efi boot on the macbook air3,1/3,2 — DIMENSION9](http://www.dm9.se/?p=398)
*   **MacBook Pro**
    *   [http://www.netsoc.tcd.ie/~theorie/interblag/2010/01/30/installing-arch-linux-on-a-mac-pro/](http://www.netsoc.tcd.ie/~theorie/interblag/2010/01/30/installing-arch-linux-on-a-mac-pro/)
    *   [http://allanmcrae.com/2010/04/installing-arch-on-a-macbook-pro-5-5/](http://allanmcrae.com/2010/04/installing-arch-on-a-macbook-pro-5-5/)
    *   [http://allanmcrae.com/2012/04/installing-arch-on-a-macbook-pro-8-1/](http://allanmcrae.com/2012/04/installing-arch-on-a-macbook-pro-8-1/)
    *   [http://linux-junky.blogspot.com/2011/08/triple-boot-archlinux-windows-7-and-mac.html](http://linux-junky.blogspot.com/2011/08/triple-boot-archlinux-windows-7-and-mac.html)