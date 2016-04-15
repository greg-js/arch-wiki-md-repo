This article is about using [rsync](/index.php/Rsync "Rsync") to transfer a copy of your "/" tree, excluding a few select folders. This approach is considered to be better than [disk cloning](/index.php/Disk_cloning "Disk cloning") with `dd` since it allows for a different size, partition table and filesystem to be used, and better than copying with `cp -a` as well, because it allows greater control over file permissions, attributes, Access Control Lists (ACLs) and extended attributes. [[1]](http://www.bestbits.at/acl/about.html)

Either method will work even while the system is running. Since it's going to take a while, you may freely browse the web during this time. Worst case scenario you will not get the same opened tabs when you restore the backup (or boot from it) because they were not saved. Not a big deal.

## Contents

*   [1 With a single command](#With_a_single_command)
*   [2 Boot requirements](#Boot_requirements)
    *   [2.1 Update the fstab](#Update_the_fstab)
    *   [2.2 Update the bootloader's configuration file](#Update_the_bootloader.27s_configuration_file)
*   [3 First boot](#First_boot)
*   [4 See also](#See_also)

## With a single command

This command depends on brace expansion available in both the [bash](https://www.gnu.org/software/bash/manual/html_node/Brace-Expansion.html) and [zsh](http://zsh.sourceforge.net/Doc/Release/Expansion.html#Brace-Expansion) shells. When using a different [shell](/index.php/Shell "Shell"), `--exclude` patterns should be repeated manually.

```
# rsync -aAXv --exclude={"/dev/*","/proc/*","/sys/*","/tmp/*","/run/*","/mnt/*","/media/*","/lost+found"} / */path/to/backup/folder*

```

Using the `-aAX` set of options, the files are transferred in archive mode, ensuring that symbolic links, devices, permissions and ownerships, modification times, [ACLs](/index.php/ACL "ACL") and extended attributes are preserved.

The `--exclude` option will cause files that match the given patterns to be excluded. The contents of `/dev`, `/proc`, `/sys`, `/tmp` and `/run` were excluded because they are populated at boot (while the folders themselves are *not* created), `/lost+found` is filesystem-specific. Quoting the exclude patterns will avoid expansion by [shell](/index.php/Shell "Shell"), which is necessary e.g. when backing up over [SSH](/index.php/SSH "SSH"). Ending the excluded paths with `*` will still ensure that the directories themselves are created if not already existing.

Be aware that you will need a Linux compatible file system, eg: `ext4` to maintain symlinks etc, when using the `-aAX` options.

**Note:**

*   If you plan on backing up your system somewhere other than `/mnt` or `/media`, do not forget to add it to the list of exclude patterns to avoid an infinite loop.
*   If there are any bind mounts in the system, they should be excluded as well, so that the bind mounted contents is copied only once.
*   If you use a [swap file](/index.php/Swap_file "Swap file"), make sure to exclude it as well.
*   Consider also if you want to backup the `/home/` folder. If it contains your data, it might be considerably larger than the system. Otherwise consider excluding unimportant subdirectories such as `/home/*/.thumbnails/*`, `/home/*/.cache/mozilla/*`, `/home/*/.cache/chromium/*`, `/home/*/.local/share/Trash/*`, depending on software installed on the system. If [GVFS](/index.php/GVFS "GVFS") is installed, `/home/*/.gvfs` must be excluded to prevent rsync errors.

You may want to include additional [rsync](/index.php/Rsync "Rsync") options, such as the following (see `man rsync` for the full list):

*   If you are a heavy user of hardlinks, you might consider adding the `-H` option, which is turned off by default as memory expensive, but nowadays it should be no problem on most modern machines. There are a lot of hard links below the `/usr/` folder, which save disk space.
*   You may want to add rsync's `--delete` option if you are running this multiple times to the same backup folder. In this case make sure that the source path does not end with `/*`, or this option will only have effect on the files inside the subdirectories of the source directory, but no effect on the files residing directly inside the source directory.
*   If you use any sparse files, such as virtual disks, [Docker](/index.php/Docker "Docker") images and similar, you should add the `-S` option.
*   The `--numeric-ids` option will disable mapping of user and group names, numeric group and user IDs will be transfered instead. This is useful when backing up over [SSH](/index.php/SSH "SSH") or when using a live system to backup different system disk.
*   Choosing `--info=progress2` option instead of `-v` will show overal progress info and transfer speed instead of huge list of files.

If you wish to restore the backup use the same rsync command that was executed, but with the source and destination reversed.

## Boot requirements

Having a bootable backup can be useful in case the filesystem becomes corrupt or if an update breaks the system. The backup can also be used as a test bed for updates, with the [testing] repo enabled, etc. If you transferred the system to a different partition or drive and you want to boot it, the process is as simple as updating the backup's `/etc/fstab` and your bootloader's configuration file.

### Update the fstab

Without rebooting, edit the backup's [fstab](/index.php/Fstab "Fstab") to reflect the changes:

 `/path/to/backup/etc/fstab` 
```
tmpfs        /tmp          tmpfs     nodev,nosuid             0   0

<font color="#888888">*/dev/sda1    /boot         ext2      defaults                 0   2
/dev/sda5    none          swap      defaults                 0   0
/dev/sda6    /             ext4      defaults                 0   1
/dev/sda7    /home         ext4      defaults                 0   2*</font>
```

Because rsync has performed a recursive copy of the *entire* root filesystem, all of the `sda` mountpoints are problematic and booting the backup will fail. In this example, all of the offending entries are replaced with a single one:

 `/path/to/backup/etc/fstab` 
```
tmpfs        /tmp          tmpfs     nodev,nosuid             0   0

/dev/**sdb1**    /             ext4      defaults                 0   1
```

Remember to use the proper device name and filesystem type.

### Update the bootloader's configuration file

This section assumes that you backed up the system to another drive or partition, that your current bootloader is working fine, and that you want to boot from the backup as well.

For [Syslinux](/index.php/Syslinux "Syslinux"), all you need to do is duplicate the current entry, except pointing to a different drive or partition.

**Tip:** Instead of editing `syslinux.cfg`, you can also temporarily edit the menu during boot. When the menu shows up, press the `Tab` key and change the relevant entries. Partitions are counted from one, drives are counted from zero.

For [GRUB](/index.php/GRUB "GRUB"), it is recommended that you automatically [re-generate the main configuration file](/index.php/GRUB#Generate_the_main_configuration_file "GRUB").

Also verify the new menu entry in `/boot/grub/grub.cfg`. Make sure the UUID is matching the new partition, otherwise it could still boot the old system. Find the UUID of a partition as follows:

```
# lsblk -no NAME,UUID /dev/sdb3

```

where you substitute the desired partition for /dev/sdb3\. To list the UUIDs of partitions grub thinks it can boot, use grep:

```
# grep UUID= /boot/grub/grub.cfg

```

If the one you found from lsblk is not found by grep, then grub-mkconfig did not work. Most likely, you will have to [Change root](/index.php/Change_root "Change root") into the duplicate file system and then use [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"). For example, if you had used rsync to duplicate root on /dev/sdb3 then change root and use mkinitcpio as follows:

```
# mkdir /mnt/arch
# mount /dev/sdb3 /mnt/arch
# cd /mnt/arch
# mount -t proc proc proc/
# mount --rbind /sys sys/
# mount --rbind /dev dev/
# chroot /mnt/arch /bin/bash
# mkinitcpio -p linux

```

After exiting, verify the new UUID is included.

## First boot

Reboot the computer and select the right entry in the bootloader. This will load the system for the first time. All peripherals should be detected and the empty folders in `/` will be populated.

Now you can re-edit `/etc/fstab` to add the previously removed partitions and mount points.

If you transferred the data from HDD to SSD (solid state drive), do not forget to activate TRIM. Also consider using HDD and tmpfs mount points to reduce SSD wearing - see [Maximizing performance#Relocate files to tmpfs](/index.php/Maximizing_performance#Relocate_files_to_tmpfs "Maximizing performance") and [Solid State Drives#Tips for minimizing disk reads/writes](/index.php/Solid_State_Drives#Tips_for_minimizing_disk_reads.2Fwrites "Solid State Drives").

**Note:** You may have to reboot again in order to get all services and daemons working correctly. Personally, pulseaudio would not initialise because of a module loading error. I restarted the dbus.service to make it work.

## See also

*   [Howto – local and remote snapshot backup using rsync with hard links](http://blog.pointsoftware.ch/index.php/howto-local-and-remote-snapshot-backup-using-rsync-with-hard-links/) Includes file deduplication with hard-links, MD5 integrity signature, 'chattr' protection, filter rules, disk quota, retention policy with exponential distribution (backups rotation while saving more recent backups than older)