Some of Btrfs's neat features like non-volatile rollback or automatic mounting of degraded Btrfs multi-device ([RAID](/index.php/RAID "RAID")) volumes need a special package from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") called [mkinitcpio-btrfs](https://aur.archlinux.org/packages/mkinitcpio-btrfs/). The package integrates some helpers in the boot process, to handle these features correctly.

**Note:**

*   This article assumes that you are creating a fresh install.
*   Arch's default mkinitcpio package contains a standard *btrfs* hook, which is enough to get multi-device ([RAID](/index.php/RAID "RAID")) support. Beside that, the kernel is capable of booting a single-device btrfs root without any hook.

## Contents

*   [1 Setup](#Setup)
*   [2 Configure the system](#Configure_the_system)
*   [3 Installation](#Installation)
*   [4 Install and configure a bootloader](#Install_and_configure_a_bootloader)
    *   [4.1 GRUB](#GRUB)
    *   [4.2 Syslinux EFI](#Syslinux_EFI)

## Setup

**Warning:**

*   Be aware of the differences between *partitions* and *sub-volumes*.
*   Having a separate */boot* **partition** is not supported by [mkinitcpio-btrfs](https://aur.archlinux.org/packages/mkinitcpio-btrfs/)
*   kexec is used to reload the kernel from the root partition to make sure it is rolled back also.
*   */boot* **can** be on a sub-volume within your `__active` sub-volume.

Create a *snapshot* of the current root directory. Creating a snapshot automatically creates a new sub-volume. Name this snapshot `__active`. Later on, this will serve as the system's new root directory.

```
# cd /mnt
# btrfs subvolume snapshot . __active

```

To use the rollback features of Btrfs, create a `__snapshot` directory for snapshot storage.

```
# cd /mnt
# mkdir __snapshot

```

**Note:**

*   The sub-volume and folder names are chosen for compatibility with [mkinitcpio-btrfs](https://aur.archlinux.org/packages/mkinitcpio-btrfs/).
*   Different names can be used if later specified in `/etc/default/btrfs_advanced` later.

You can create separate sub-volumes for important directories. This would additionally enable the ability to monitor and adjust the size allocations for each sub-volume using `btrfs quota`.

See [Btrfs#Subvolumes](/index.php/Btrfs#Subvolumes "Btrfs")

**Note:** For mkinitcpio-btrfs compatibility, set the default sub-volume to `__active`.

**Warning:** [mkinitcpio-btrfs](https://aur.archlinux.org/packages/mkinitcpio-btrfs/) may not handle sub-volumes correctly. See [here](https://github.com/xtfxme/mkinitcpio-btrfs/issues/6).

Next, mount the root sub-volume. See [Btrfs#Mount options](/index.php/Btrfs#Mount_options "Btrfs").

**Note:** If you did not set the default subvolume you need to add an additional `subvol=__active` mount option.

## Configure the system

Create a place where you mount the Btrfs root subvolume to create snapshots later.

```
# mkdir /var/lib/btrfs

```

**Note:** This should probably be `/mnt/var/lib/btrfs` as we haven't chrooted yet.

**Tip:** bind an empty folder over the `/var/lib/btrfs/__active` folder to prevent apps such as 'find' from complaining of any loops. `/var/lib/btrfs/empty /var/lib/btrfs/__active none bind 0 0`

## Installation

Install [mkinitcpio-btrfs](https://aur.archlinux.org/packages/mkinitcpio-btrfs/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

Modify `/etc/default/btrfs_advanced` as needed and add `btrfs_advanced` to the `HOOKS` section in `/etc/mkinitcpio.conf`.

Re-create the initial ramdisk environment. See [Mkinitcpio#Image creation and activation](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio")

## Install and configure a bootloader

See [Btrfs#Installation](/index.php/Btrfs#Installation "Btrfs")

### GRUB

**Tip:** To prevent tty1 to flush all boot messages before printing the login prompt, edit `/etc/systemd/system/getty.target.wants/getty@tty1.service` and change `TTYVTDisallocate` to `no`.

**Tip:** To have your multi-device Btrfs boot if your first device has failed, add the bootloader to the second device too.

Make sure that your Btrfs root is correctly added to the kernel commandline in `/boot/grub/grub.cfg`. Using UUIDs for device identification is especially useful for multi-device ([RAID](/index.php/RAID "RAID")) setups, because all Btrfs devices own the same UUID.

```
root=UUID=fd88d586-bb4c-4fc7-81a6-f675e2829581

```

**Warning:** If you've set the default subvolume you **MUST NOT** add `subvol=__active` to your `rootflags`.

**Note:** Having boot on a different partition in not supported with [mkinitcpio-btrfs](https://aur.archlinux.org/packages/mkinitcpio-btrfs/) >= 0.4.

### Syslinux EFI

To boot from Btrfs using syslinux EFI, you need to setup up a dedicated EFI partition in `/boot/efi`. This partition needs to be formated as FAT32 (or HPFS on MacBooks). You need to set up your Syslinux directories on that special partition as described in [Syslinux](/index.php/Syslinux "Syslinux").

**Warning:** The downside of this setup is, that you need to store a working kernel image and its initrd on the EFI partition, because Syslinux can not access Btrfs filesystems directly. [mkinitcpio-btrfs](https://aur.archlinux.org/packages/mkinitcpio-btrfs/) will then mount your Btrfs root and reload the kernel from your Btrfs `/boot` directory.

In `/boot/efi/EFI/syslinux/syslinux.cfg` make sure your Btrfs root is correctly added to the `APPEND` line.

```
APPEND root=UUID=978e3e81-8048-4ae1-8a06-aa727458e8ff rw

```

**Warning:** If you've set the default subvolume you **MUST NOT** add `subvol=__active` to your `APPEND` line.