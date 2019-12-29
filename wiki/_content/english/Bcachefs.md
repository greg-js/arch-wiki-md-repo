[Bcachefs](https://bcachefs.org/) is a next-generation CoW filesystem that aims to provide features from [Btrfs](/index.php/Btrfs "Btrfs") and [ZFS](/index.php/ZFS "ZFS") with a cleaner codebase, more stability, greater speed and a GPL-compatible license.

It is built upon [Bcache](/index.php/Bcache "Bcache") and is mainly developed by Kent Overstreet.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Setup](#Setup)
    *   [2.1 Single drive](#Single_drive)
    *   [2.2 Multiple drives in RAID0/1](#Multiple_drives_in_RAID0/1)
    *   [2.3 RAID0/1 with SSD caching](#RAID0/1_with_SSD_caching)
*   [3 Configuration](#Configuration)
    *   [3.1 Changing a device's group](#Changing_a_device's_group)
    *   [3.2 Adding a device](#Adding_a_device)
    *   [3.3 Removing a device](#Removing_a_device)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Documentation](#Documentation)
*   [5 See also](#See_also)

## Installation

Bcachefs is not in the upstream [Kernel](/index.php/Kernel "Kernel") yet but the [linux-bcachefs-git](https://aur.archlinux.org/packages/linux-bcachefs-git/) kernel can be installed from the [AUR](/index.php/AUR "AUR").

The Bcachefs userspace tools are available from [bcachefs-tools-git](https://aur.archlinux.org/packages/bcachefs-tools-git/).

## Setup

### Single drive

```
# bcachefs format /dev/sda
# mount -t bcachefs /dev/sda /mnt

```

### Multiple drives in RAID0/1

Bcachefs defines a replica as any instance of data, so 1 replica with 2 drives is equivalent to RAID0, 2 replicas with 2 drives is equivalent to RAID1, etc.

```
# bcachefs format /dev/sda /dev/sdb --replicas=*n*
# mount -t bcachefs /dev/sda1:/dev/sdb1 /mnt

```

### RAID0/1 with SSD caching

Bcachefs has 3 categories of storage: background, foreground, and promote. Writes to the filesystem prioritize the foreground drives, which are then moved to the background over time. Reads are cached on the promote drives.

A recommended configuration is to use an ssd group for the foreground and promote, and an hdd group for the background, as in the following example.

**Note:** These are not separated "tiers" of storage. They are just guidelines for a single large pool. Writes will go directly to the background if the foreground is full, or to promote if they both are. Metadata can be written to any of them. In this configuration, `metadata_replicas` should be at least 2, so that a cache drive may be able to fail without causing data loss.

```
# bcachefs format \
    --group=ssd /dev/sda /dev/sdb 
    --group=hdd /dev/sdc /dev/sdd /dev/sde /dev/sdf \
    --data_replicas=1 --metadata_replicas=2 \
    --foreground_target=ssd \
    --background_target=hdd \
    --promote-target=ssd
# mount -t bcachefs /dev/sda:/dev/sdb:/dev/sdc:/dev/sdd/dev/sde:/dev/sdf /mnt

```

## Configuration

Most options can be set at either during `bcachefs format`, at mount time (`mount -o option=value`), or through sysfs (`echo X > /sys/fs/bcachefs/*UUID*/options/*option*`). Setting the option during format or changing it through sysfs saves it in the filesystem's superblock, making it the default for those drives. Mount options override those defaults.

**Note:** The filesystem must be mounted for sysfs to be available. All operations except fsck are possible on a live filesystem

*   data_checksum, metadata_checksum (none, crc32c, crc64)
*   (foreground) compression, background_compression (none, lz4, gzip, zstd)
*   foreground_target, background_target, promote_target

The following can also be set on a per directory or per file basis with `bcachefs setattr *file* --option=value`

*   data_replicas
*   data_checksum
*   compression, background_compression
*   foreground_target, background_target, promote_target

**Note:** Disk usage reporting currently shows uncompressed size. Compression is otherwise complete.

### Changing a device's group

```
# echo *group* > /sys/fs/bcachefs/*filesystem_uuid*/dev-*X*/label

```

**Note:** This requires a remount to take effect.

### Adding a device

```
# bcachefs device add --group=*group* /mnt /dev/*device*

```

**Note:** Only new writes will be striped across added devices. Existing ones will be unchanged until disk usage reaches a certain threshold, when the disk rebalance is triggered. It is not currently possible to manually trigger a rebalance/restripe.

### Removing a device

If you already have at least 2 data and metadata replicas

```
# bcachefs device remove *device*
# bcachefs data rereplicate /mnt

```

Otherwise, first make sure there are at least 2 metadata replicas.

```
# echo 2 > /sys/fs/bcachefs/*UUID*/options/metadata_replicas
# bcachefs data rereplicate /mnt

```

Move the data off the device. This can take a very long time.

```
# bcachefs device set-state *device* readonly
# bcachefs device evacuate *device*

```

Finally remove it.

```
# bcachefs device remove *device*

```

## Tips and tricks

### Documentation

Up-to-date documentation is only available via `bcachefs --help`. The man page, for instance, includes the now-useless `--tier` option.

Check dmesg for more useful error messages.

## See also

*   [Kent Overstreet's Patreon page](https://www.patreon.com/bcachefs)
*   [Wikipedia:Bcachefs](https://en.wikipedia.org/wiki/Bcachefs "wikipedia:Bcachefs")