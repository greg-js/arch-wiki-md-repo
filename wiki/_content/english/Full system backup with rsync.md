This article is about using [rsync](/index.php/Rsync "Rsync") to transfer a copy of your entire `/` tree, except for a some specific directories. This approach is considered to be better than [disk cloning](/index.php/Disk_cloning "Disk cloning") with `dd`, since it allows for a different size, partition table, and filesystem to be used, and it allows for better copying with `cp -a` as well. Additionally it allows greater control over file permissions, attributes, [Access Control Lists](/index.php/Access_Control_Lists "Access Control Lists") and [extended attributes](/index.php/Extended_attributes "Extended attributes").

This method will work even while the system is running, but files changed during the transfer may or may not be transferred, which can cause undefined behavior of some programs using the transferred files.

This approach works well for migrating an existing installation to a new hard drive or [SSD](/index.php/SSD "SSD").

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

By using the `-aAX` set of options, the files are transferred in archive mode which ensures that symbolic links, devices, permissions, ownerships, modification times, [ACLs](/index.php/ACL "ACL"), and extended attributes are preserved, assuming that the target [file system](/index.php/File_system "File system") supports the feature.

The `--exclude` option causes files that match the given patterns to be excluded. The contents of `/dev`, `/proc`, `/sys`, `/tmp`, and `/run` are excluded in the above command, because they are populated at boot, although the folders themselves are *not* created. `/lost+found` is filesystem-specific. Quoting the exclude patterns will avoid expansion by the [shell](/index.php/Shell "Shell"), which is necessary, for example, when backing up over [SSH](/index.php/SSH "SSH"). Ending the excluded paths with `*` ensures that the directories themselves are created if they do not already exist.

**Note:**

*   If you plan on backing up your system somewhere other than `/mnt` or `/media`, do not forget to add it to the list of exclude patterns to avoid an infinite loop.
*   If there are any bind mounts in the system, they should be excluded as well so that the bind mounted contents is copied only once.
*   If you use a [swap file](/index.php/Swap_file "Swap file"), make sure to exclude it as well.
*   Consider if you want to backup the `/home/` folder. If it contains your data it might be considerably larger than the system. Otherwise consider excluding unimportant subdirectories such as `/home/*/.thumbnails/*`, `/home/*/.cache/mozilla/*`, `/home/*/.cache/chromium/*`, and `/home/*/.local/share/Trash/*`, depending on software installed on the system. If [GVFS](/index.php/GVFS "GVFS") is installed, `/home/*/.gvfs` must be excluded to prevent rsync errors.

You may want to include additional [rsync](/index.php/Rsync "Rsync") options, such as the following. See [rsync(1)](http://man7.org/linux/man-pages/man1/rsync.1.html) for the full list.

*   If you use many hard links, consider adding the `-H` option, which is turned off by default due to its memory expense; however, it should be no problem on most modern machines. Many hard links reside under the `/usr/` directory.
*   You may want to add rsync's `--delete` option if you are running this multiple times to the same backup folder. In this case make sure that the source path does not end with `/*`, or this option will only have effect on the files inside the subdirectories of the source directory, but it will have no effect on the files residing directly inside the source directory.
*   If you use any sparse files, such as virtual disks, [Docker](/index.php/Docker "Docker") images and similar, you should add the `-S` option.
*   The `--numeric-ids` option will disable mapping of user and group names; instead, numeric group and user IDs will be transfered. This is useful when backing up over [SSH](/index.php/SSH "SSH") or when using a live system to backup different system disk.
*   Choosing `--info=progress2` option instead of `-v` will show the overall progress info and transfer speed instead of the list of files being transferred.

If you wish to restore the backup, use the same rsync command that was executed but with the source and destination reversed.

## Boot requirements

Having a bootable backup can be useful in case the filesystem becomes corrupt or if an update breaks the system. The backup can also be used as a test bed for updates, with the *testing* repo enabled, etc. If you transferred the system to a different partition or drive and you want to boot it, the process is as simple as updating the backup's `/etc/fstab` and your bootloader's configuration file.

This section assumes that you backed up the system to another drive or partition, that your current bootloader is working fine, and that you want to boot from the backup as well.

### Update the fstab

Without rebooting, edit the backup's [fstab](/index.php/Fstab "Fstab") by commenting out or removing any existing entries. Add one entry for the partition containing the backup like the example here:

```
/dev/sda*X*    /             *ext4*      defaults                 0   1

```

Remember to use the proper device name and filesystem type.

### Update the bootloader's configuration file

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

## First boot

Reboot the computer and select the right entry in the bootloader. This will load the system for the first time. All peripherals should be detected and the empty folders in `/` will be populated.

Now you can re-edit `/etc/fstab` to add the previously removed partitions and mount points.

## See also

*   [Howto – local and remote snapshot backup using rsync with hard links](http://blog.pointsoftware.ch/index.php/howto-local-and-remote-snapshot-backup-using-rsync-with-hard-links/) Includes file deduplication with hard-links, MD5 integrity signature, 'chattr' protection, filter rules, disk quota, retention policy with exponential distribution (backups rotation while saving more recent backups than older)