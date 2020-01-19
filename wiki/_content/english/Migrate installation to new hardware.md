Related articles

*   [Migrating between architectures](/index.php/Migrating_between_architectures "Migrating between architectures")
*   [Moving an existing install into (or out of) a virtual machine](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

This article discusses the steps required for moving an Arch Linux system to new hardware. The goal is to achieve the same ArchLinux installation, in terms of the installed software and configuration that is independent of the hardware.

**Warning:** Some of the following instructions can be dangerous: you are advised to backup all of your important data on the old system before continuing.

There are two different approaches to migrating an installation:

1.  *Bottom to Top*: Install a fresh Arch Linux system on the new hardware, afterwards restore the installed packages and configuration files, e.g. as describedn in [dotfiles](/index.php/Dotfiles "Dotfiles").
2.  *Top to Bottom*: Clone the old harddrive to the new harddrive, or place the old harddrive into the new system; modify configuration files where necessary.

The Top to bottom approach gives a more exact reproduction of the original system than the Bottom to Top approach.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Adapt to new hardware](#Adapt_to_new_hardware)
    *   [1.1 Hard drive vs. SSD](#Hard_drive_vs._SSD)
    *   [1.2 CPU vendor](#CPU_vendor)
    *   [1.3 GPU vendor](#GPU_vendor)
    *   [1.4 UEFI vs. MBR boot code booting](#UEFI_vs._MBR_boot_code_booting)
*   [2 Bottom to Top](#Bottom_to_Top)
    *   [2.1 On the old system](#On_the_old_system)
        *   [2.1.1 List of installed packages](#List_of_installed_packages)
        *   [2.1.2 pacman cache](#pacman_cache)
    *   [2.2 On the new system](#On_the_new_system)
        *   [2.2.1 Installation guide first half](#Installation_guide_first_half)
        *   [2.2.2 Copy pacman cache](#Copy_pacman_cache)
        *   [2.2.3 Installation guide second half](#Installation_guide_second_half)
        *   [2.2.4 Install previously installed software](#Install_previously_installed_software)
*   [3 Top to Bottom](#Top_to_Bottom)
    *   [3.1 Clean up the old system](#Clean_up_the_old_system)
    *   [3.2 Copy the system to a new drive](#Copy_the_system_to_a_new_drive)
        *   [3.2.1 Disk cloning](#Disk_cloning)
        *   [3.2.2 File copying](#File_copying)
        *   [3.2.3 Transport options](#Transport_options)
    *   [3.3 Update fstab](#Update_fstab)
    *   [3.4 Reconfigure the bootloader](#Reconfigure_the_bootloader)
    *   [3.5 Regenerate kernel image](#Regenerate_kernel_image)
    *   [3.6 Reconfigure audio](#Reconfigure_audio)
    *   [3.7 Reconfigure network](#Reconfigure_network)
*   [4 See also](#See_also)

## Adapt to new hardware

**Warning:** For both approaches we have to account for differences between the old and hardware and change the installed drivers and configuration accordingly.

Before you begin, research aspects of the new hardware and make a list of differences. Common differences are

### Hard drive vs. SSD

See the article [SSD](/index.php/SSD "SSD").

### CPU vendor

If you switch the CPU, to a CPU from another vendor (e.g. Intel to AMD), change the [Microcode](/index.php/Microcode "Microcode") configuration.

### GPU vendor

If you changed the GPU to a GPU from another vendor (e.g. from [Amd](/index.php/Amd "Amd") to [NVIDIA](/index.php/NVIDIA "NVIDIA")) change the graphics driver.

### UEFI vs. MBR boot code booting

If you switch to a more recent mainboard with UEFI, it might be preferable or required to switch from "MBR boot code" booting to [UEFI](/index.php/UEFI "UEFI") booting. In this case an new [EFI system partition](/index.php/EFI_system_partition "EFI system partition") is needed.

## Bottom to Top

### On the old system

We define here a minimal configuration that carries over from the old to the new system which differentiates this approach from the Installation guide. Think about the configuration files from `/etc` and dotfiles in `/home` that you want to copy to the new system, as well as user data files. If you will not have access to the old system from the new system then backup up all the files that you want to copy over.

#### List of installed packages

```
$ pacman -Qqen > pkglist.txt
$ pacman -Qqem > pkglist_aur.txt

```

gives you a nice list of explicitly installed packages from the repositories and from the [AUR](/index.php/AUR "AUR"). Include it in your backup if you make one.

You may also use the following script to give you a better overview of the binaries and libraries installed unbeknownst to pacman (e. g. installed via Steam, Desura or using their own install methods):

```
find / -regextype posix-extended -regex "/(sys|srv|proc)|.*/\.ccache/.*" -prune -o -type f \
-exec bash -c 'file "{}" | grep -E "(32|64)-bit"' \; | \
awk -F: '{print $1}' | \
while read -r bin; \
do pacman -Qo "$bin" &>/dev/null || echo "$bin"; \
done

```

#### pacman cache

Consider backing up `/var/cache/pacman/pkg` if you do not change architectures (for example from x86 to x86_64).

### On the new system

#### Installation guide first half

For basics about installing a new system, refer to the [Installation guide](/index.php/Installation_guide "Installation guide"). Follow the first half of the installation guide up to but excluding the pacstrap command.

#### Copy pacman cache

Copy the pacman cache found at `/var/cache/pacman/pkg` from the old to the new system, or from the backup to the new system.

#### Installation guide second half

Continue with the installation guide from, and including the pacstrap command, up to the end, but do not reboot. Do not skip the pacstrap command as it does additional work besides the installation of packages.

#### Install previously installed software

Edit pkglist.txt (and pkglist_aur.txt) and remove drivers that are not needed on the new system. Then install any other previously installed software with

```
# pacman -S --needed - < pkglist.txt

```

## Top to Bottom

There are two options for the Top to Bottom approach, you can either keep the drive where the system is already installed, and modify its contents, or you can copy the system to a new drive. If you keep the drive, and modify it, then place it back into the old system, the modifications will likely prevent the old system from booting.

### Clean up the old system

It is also worth to clean up your system before cloning it, as described in [System maintenance#Clean the filesystem](/index.php/System_maintenance#Clean_the_filesystem "System maintenance"). Make sure that the old system is still working as expected after the cleanup before moving on.

### Copy the system to a new drive

**Note:** If you are planning to keep the hard drive where the system is already installed, you can skip this section.

There are two fundamental methods for copying the system to a new drive, [disk cloning](/index.php/Disk_cloning "Disk cloning") and file copying.

#### Disk cloning

It is required to use a live linux system rather than the old ArchLinux system; for example you could use the ArchLinux [USB flash installation media](/index.php/USB_flash_installation_media "USB flash installation media"). The partition layout and filesystems of the old system will be reproduced.

#### File copying

*   Create new [partitions](/index.php/Partitions "Partitions") and [filesystems](/index.php/Filesystems "Filesystems") on the new drive. You can use the opportunity to chose a different partition layout and/or filesystems than before.
*   For each filesystem, copy the files from the old to the new drive, using [Rsync](/index.php/Rsync "Rsync") or other tools that preserve permissions, attributes, etc., see [Rsync#Full system backup](/index.php/Rsync#Full_system_backup "Rsync"), [Rsync#File system cloning](/index.php/Rsync#File_system_cloning "Rsync") for further details.

#### Transport options

There are many different methods for how to transport the data between the two drives:

*   Connect origin and destination HDDs to the same computer, either the old or the new one. Data link: old HDD -> computer -> new HDD.
*   Make use of temporary storage devices like external HDDs, or cloud backups. Data link: old HDD -> old computer -> storage -> new computer -> new HDD. For an overview see the article [System backup](/index.php/System_backup "System backup").
*   Transfer data over network, for example with [rsync](/index.php/Rsync "Rsync"). Data link: old HDD -> old computer -> network -> new computer -> new HDD.

For the first two options, consider that you might need adapters to connect the HDDs (PATA->SATA, USB-HDD-Cases, etc.), and choose a connection that is sufficiently fast. The last two options require you to use a live linux system on the new computer, as it is not possible to boot from the new hard drive at this point.

### Update fstab

**Warning:** Before doing this step please make sure that you do not wish to use this drive in the old system, as changing the [fstab](/index.php/Fstab "Fstab") file will likely prevent the system from booting in the old configuration.

If you are using an Arch Linux Installation Image, mount the new root partition to `/mnt`, and any other partitions required like you would in a normal install (see [Installation guide#Mount the file systems](/index.php/Installation_guide#Mount_the_file_systems "Installation guide")).

Insert an arbitrary comment such as `#end of old fstab` at the end of your `/mnt/etc/fstab`. Generate a new fstab file as indicated on [Installation guide#Fstab](/index.php/Installation_guide#Fstab "Installation guide"), appending it to the current fstab file. In general, always review the fstab file created by genfstab. In this case, check the older fstab entries before the comment, if they are outdated or duplicates then delete them, and if the old entries remain useful then keep them. For example, mount entries for network drives can be kept. In general it is recommended to use [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming").

### Reconfigure the bootloader

You might need to reinstall and/or reconfigure the [Bootloader](/index.php/Bootloader "Bootloader") for the following reasons:

*   Different disks, partition layout, or filesystem
*   Adding [UEFI](/index.php/UEFI "UEFI") boot entries into the new mainboard NVRAM
*   Migration from "MBR boot code" booting to UEFI booting
*   Migration from USB to SATA/NVMe
*   Updating the kernel commandline
    *   In case of a different GPU, update the framebuffer mode
    *   Update the [Microcode](/index.php/Microcode "Microcode") initramfs image

If you are using a Arch Linux live environment, then before configuring the bootloader, [change root](/index.php/Change_root "Change root") into the new system:

```
# arch-chroot /mnt

```

Refer to [Bootloader](/index.php/Bootloader "Bootloader") for how to reconfigure your bootloader.

### Regenerate kernel image

It is recommended to regenerate the initramfs image with [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"), although initially the fallback initramfs image may work.

### Reconfigure audio

*   alsamixer volume
    *   save settings

### Reconfigure network

If the old installation and the migrated installation shall coexist in the same network, set a new hostname with [hostnamectl](/index.php/Network_configuration#Set_the_hostname "Network configuration").

Also consider configuration changes that are required after a change in hostname:

*   /etc/hosts
*   other apps using hostname: synergy, nut (network ups tools)
*   `# grep -Ri 'hostname' /etc` should give some hints on the files to be updated

The network interface names may change when using [dhcpcd](/index.php/Dhcpcd "Dhcpcd") with named network interfaces.

*   `$ dmesg | grep 'renamed from eth'` might help to find the new interface name
*   remove old `# systemctl disable dhcpcd@enp*X*s0.service`
*   activate new `# systemctl start dhcpcd@enp*X*s0.service`

## See also

*   [Howto clone a linux system](http://positon.org/clone-a-linux-system-install-to-another-computer)
*   [[1]](https://bbs.archlinux.org/viewtopic.php?id=71038)
*   [[2]](https://bbs.archlinux.org/viewtopic.php?pid=543214)