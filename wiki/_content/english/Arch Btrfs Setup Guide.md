This guide shows how to install [Arch Linux](/index.php/Arch_Linux "Arch Linux") using the advanced Btrfs layout found in openSuse. This will also allow the use of Snapper for snapshots and rollback.

**Note:** This wiki page is work-in-progress and will get expanded in the next days (+2017/11/23)

## Difficulties

*   pacstrap needs -d parameter (non-mount-point)
*   initial snapshot might be read-only, change with btrfs property
*   .snapshots btrfs volume needs fstab entry!

## Troubleshooting, Resources and Links

[https://github.com/openSUSE/snapper/issues/159](https://github.com/openSUSE/snapper/issues/159) [https://unix.stackexchange.com/questions/149932/how-to-make-a-btrfs-snapshot-writable](https://unix.stackexchange.com/questions/149932/how-to-make-a-btrfs-snapshot-writable)