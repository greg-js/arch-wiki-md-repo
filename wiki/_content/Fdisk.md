# Fdisk

Related articles

*   [parted](/index.php/Parted "Parted")
*   [GParted](/index.php/GParted "GParted")
*   [Partitioning](/index.php/Partitioning "Partitioning")

## Contents

*   [1 Using GPT - modern method](#Using_GPT_-_modern_method)
    *   [1.1 Gdisk usage summary](#Gdisk_usage_summary)
*   [2 Using MBR - legacy method](#Using_MBR_-_legacy_method)
    *   [2.1 Fdisk usage summary](#Fdisk_usage_summary)
*   [3 Using cgdisk to create GPT partitions](#Using_cgdisk_to_create_GPT_partitions)
*   [4 Using fdisk to create MBR partitions](#Using_fdisk_to_create_MBR_partitions)

## Using GPT - modern method

### Gdisk usage summary

Using GPT, the utility for editing the partition table is called _gdisk_. It can perform partition alignment automatically on a 2048 sector (or 1024KiB) block size base which should be compatible with the vast majority of SSDs if not all. GNU parted also supports GPT, but is [less user-friendly](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=601813) for aligning partitions. The environment provided by the Arch install ISO includes the _gdisk_ command. If you need it later on in the installed system, _gdisk_ is available in the [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) package.

A summary of the typical usage of _gdisk_:

*   Start _gdisk_ against your drive as root (_disk-device_ may be e.g. `/dev/sda`):

	 `# gdisk _disk-device_` 

*   If the drive is brand new or if you are wanting to start over, create a new empty GUID partition table with the `o` command.
*   Create a new partition with the `n` command (primary type/1st partition).
*   Assuming the partition is new, _gdisk_ will pick the highest possible alignment. Otherwise, it will pick the largest power of two that divides all partition offsets.
*   If choosing to start on a sector before the 2048th _gdisk_ will automatically shift the partition start to the 2048th disk sector. This is to ensure a 2048-sectors alignment (as a sector is 512B, this is a 1024KiB alignment which should fit any SSD NAND erase block).
*   Use the `+_x_{M,G}` format to extend the partition _x_ mebibytes or gibibytes, if choosing a size that is not a multiple of the alignment size (1024kiB), _gdisk_ will shrink the partition to the nearest inferior multiple. For example, if you want to create a 15GiB partition, you would enter `+15G`. To take all of the remaining space, press enter right away, or enter `+0` instead.
*   Select the partition's type id, the default, `Linux filesystem` (code `8300`), should be fine for most use. Press `L` to show the codes list. If planning to use LVM select `Linux LVM` (`8e00`).
*   Assign other partitions in a like fashion.
*   Write the table to disk and exit via the `w` command.
*   Format the new partitions with a [file system](/index.php/File_system "File system").

## Using MBR - legacy method

Using MBR, the utility for editing the partition table is called _fdisk_. Recent versions of _fdisk_ have abandoned the deprecated system of using cylinders as the default display unit, as well as MS-DOS compatibility by default. The latest _fdisk_ automatically aligns all partitions to 2048 sectors, or 1024 KiB, which should work for all EBS sizes that are known to be used by SSD manufacturers. This means that the default settings will give you proper alignment.

Note that in the olden days, _fdisk_ used cylinders as the default display unit, and retained an MS-DOS compatibility quirk that messed with SSD alignment. Therefore one will find many guides around the internet from around 2008-2009 making a big deal out of getting everything correct. With the latest _fdisk_, things are much simpler, as reflected in this guide.

### Fdisk usage summary

*   Start _fdisk_ against your drive as root (_disk-device_ may be e.g. `/dev/sda`):

	 `# fdisk _disk-device_` 

*   If the drive is brand new or if you are wanting to start over, create a new empty DOS partition table with the `o` command.
*   Create a new partition with the `n` command (primary type/1st partition).
*   Use the `+_x_G` format to extend the partition _x_ gibibytes. For example, if you want to create a 15GiB partition, you would enter `+15G`
*   Change the partition's system id from the default type of Linux (`type 83`) to the desired type via the `t` command. This is an optional step should the user wish to create another type of partition for example, swap, NTFS, LVM, etc. Note that a complete listing of all valid partition types is available via the `l` command.
*   Assign other partitions in a like fashion.
*   Write the table to disk and exit via the `w` command.

## Using cgdisk to create GPT partitions

Launch _cgdisk_ with:

```
# cgdisk /dev/sda

```

**Tip:** If cgdisk cannot change your disk to GPT, [parted](https://www.archlinux.org/packages/?name=parted) can.

**Root:**

*   Choose _New_ (or press `N`) – `Enter` for the first sector (2048) – type in `15G` – `Enter` for the default hex code (8300) – `Enter` for a blank partition name.

**Home:**

*   Press the down arrow a couple of times to move to the larger free space area.
*   Choose _New_ (or press `N`) – `Enter` for the first sector – `Enter` to use the rest of the drive (or you could type in the desired size; for example `30G`) – `Enter` for the default hex code (8300) – `Enter` for a blank partition name.

Here is what it should look like:

```
Part. #     Size        Partition Type            Partition Name
----------------------------------------------------------------
            1007.0 KiB  free space
   1        15.0 GiB    Linux filesystem
   2        123.45 GiB  Linux filesystem

```

Double check and make sure that you are happy with the partition sizes as well as the partition table layout before continuing.

If you would like to start over, you can simply select _Quit_ (or press `Q`) to exit without saving changes and then restart _cgdisk_.

If you are satisfied, choose _Write_ (or press `Shift+W`) to finalize and to write the partition table to the drive. Type `yes` and choose _Quit_ (or press `Q`) to exit without making any more changes.

## Using fdisk to create MBR partitions

Launch _fdisk_ with:

```
# fdisk /dev/sda

```

Create the partition table:

*   `Command (m for help):` type `o` and press `Enter`

Then create the first partition:

1.  `Command (m for help):` type `n` and press `Enter`
2.  Partition type: `Select (default p):` press `Enter`
3.  `Partition number (1-4, default 1):` press `Enter`
4.  `First sector (2048-209715199, default 2048):` press `Enter`
5.  `Last sector, +sectors or +size{K,M,G,T,P} (2048-209715199....., default 209715199):` type `+15G` and press `Enter`

Then create a second partition:

1.  `Command (m for help):` type `n` and press `Enter`
2.  Partition type: `Select (default p):` press `Enter`
3.  `Partition number (1-4, default 2):` press `Enter`
4.  `First sector (31459328-209715199, default 31459328):` press `Enter`
5.  `Last sector, +sectors or +size{K,M,G,T,P} (31459328-209715199....., default 209715199):` press `Enter`

Now preview the new partition table:

*   `Command (m for help):` type `p` and press `Enter`

```
Disk /dev/sda: 107.4 GB, 107374182400 bytes, 209715200 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x5698d902

   Device Boot     Start         End     Blocks   Id  System
/dev/sda1           2048    31459327   15728640   83   Linux
/dev/sda2       31459328   209715199   89127936   83   Linux

```

Then write the changes to disk:

*   `Command (m for help):` type `w` and press `Enter`

If everything went well fdisk will now quit with the following message:

```
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks. 

```

In case this does not work because _fdisk_ encountered an error, you can use the `q` command to exit.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Fdisk&oldid=391664](https://wiki.archlinux.org/index.php?title=Fdisk&oldid=391664)"