[GNU fdisk](https://www.gnu.org/software/fdisk/) is a dialogue-driven command-line utility that creates and manipulates partition tables and partitions on a hard disk. Hard disks are divided into partitions and this division is described in the partition table. Arch Linux needs at least one partition in order to be installed.

This article covers **fdisk** and its related **sfdisk** and **cfdisk** utilities from the [util-linux](https://www.archlinux.org/packages/?name=util-linux) package, as well as the analogous **gdisk**, **sgdisk** and **cgdisk** utilities from the [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) package

The first step to partitioning a disk is making a partition table. There are two different partition table types that Arch Linux can use, [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table") (GPT) and [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") (MBR). GPT is the more modern partition table type that supports larger disks and on disk partition table backups among others. MBR may be required if you [dual boot](/index.php/Dual_boot "Dual boot") with Microsoft Windows.

## Contents

*   [1 Usage](#Usage)
*   [2 Backup and restore](#Backup_and_restore)
    *   [2.1 Partition layout](#Partition_layout)
    *   [2.2 GPT partition table (sgdisk)](#GPT_partition_table_.28sgdisk.29)
    *   [2.3 MBR partition table (sfdisk)](#MBR_partition_table_.28sfdisk.29)
*   [3 Create a partition table](#Create_a_partition_table)
    *   [3.1 GPT (gdisk)](#GPT_.28gdisk.29)
        *   [3.1.1 Installation](#Installation)
        *   [3.1.2 gdisk usage summary](#gdisk_usage_summary)
    *   [3.2 MBR (fdisk)](#MBR_.28fdisk.29)
        *   [3.2.1 fdisk usage summary](#fdisk_usage_summary)
    *   [3.3 Convert between MBR and GPT](#Convert_between_MBR_and_GPT)
*   [4 Create partitions](#Create_partitions)
    *   [4.1 GPT (gdisk)](#GPT_.28gdisk.29_2)
    *   [4.2 GPT (cgdisk)](#GPT_.28cgdisk.29)
    *   [4.3 MBR (fdisk)](#MBR_.28fdisk.29_2)
    *   [4.4 MBR (cfdisk)](#MBR_.28cfdisk.29)

## Usage

To get a list of options when using *fdisk* you can list the help information:

```
# fdisk -h

```

To list partition tables and partitions on a device, you can run the following, where device is a name like `/dev/sda`:

```
# fdisk -l /dev/sda

```

## Backup and restore

Before making changes to a hard disk, you may want to backup the partition table and partition scheme of the drive. You can also use a backup to copy the same partition layout to numerous drives.

### Partition layout

For both GPT and MBR you can use *sfdisk* to save the partition layout of your device to a file with the `--dump` option. Run the following command for device `/dev/sda`:

```
# sfdisk -d /dev/sda > sda.dump

```

The file should look something like this for a single ext4 partition that is 1GB in size:

 `sda.dump` 
```
label: gpt
label-id: AAAAAAAA-BBBB-CCCC-DDDD-EEEEEEEEEEEE
device: /dev/sda
unit: sectors
first-lba: 34
last-lba: 1048576

/dev/sda1 : start=2048, size=1048576, type=0FC63DAF-8483-4772-8E79-3D69D8477DE4, uuid=BBF1CD36-9262-463E-A4FB-81E32C12BDE7

```

To later restore this layout you can run:

```
# sfdisk /dev/sda < sda.dump

```

### GPT partition table (sgdisk)

Using *sgdisk* you can create a binary backup consisting of the protective MBR, the main GPT header, the backup GPT header, and one copy of the partition table:

```
# sgdisk -b=sgdisk-sda.bak

```

You can later restore the backup by running:

```
# sgdisk -l=sgdisk-sda.bak

```

If you want to clone your current device's partition layout (/dev/sda in this case) to another drive (/dev/sdc) run:

```
# sgdisk -R=/dev/sdc /dev/sda

```

If both drives will be in the same computer, you need to randomize the GUID's:

```
# sgdisk -G /dev/sdc

```

### MBR partition table (sfdisk)

To create a raw binary backup of all the sectors where your partitions are stored on an MBR disk you can use the `--backup` option with *sfdisk*.

```
# sfdisk -b /dev/sda

```

This will create a file called `sfdisk-*device*-*offset*.bak`.

To restore the binary backup you can use [dd](/index.php/Dd "Dd"):

```
# dd if=sfdisk-sda-0x00000200.bak of=/dev/sda  bs=512 count=1

```

See also [Master Boot Record#Backup and restoration](/index.php/Master_Boot_Record#Backup_and_restoration "Master Boot Record").

## Create a partition table

### GPT (gdisk)

Using GPT, the utility for editing the partition table is called *gdisk*. It can perform partition alignment automatically on a 2048 sector (or 1024KiB) block size base which should be compatible with the vast majority of SSDs if not all. [GNU parted](/index.php/GNU_parted "GNU parted") also supports GPT, but is [less user-friendly](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=601813) for aligning partitions.

#### Installation

*gdisk* is available for use on the Arch install ISO but not installed by default on the regular system. The [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) package must be [installed](/index.php/Installed "Installed") explicitly.

#### gdisk usage summary

To use *gdisk*, run the program with the name of the device you want to change/edit. This example uses `/dev/sda`:

```
# gdisk /dev/sda
GPT fdisk (gdisk) version 1.0.1

Partition table scan:
  MBR: protective
  BSD: not present
  APM: not present
  GPT: present

Found valid GPT with protective MBR; using GPT.

Command (? for help): _

```

To create a new GPT partition table, type the `o` command. You should see something like this:

```
Command (? for help): o
This option deletes all partitions and creates a new protective MBR.
Proceed? (Y/N): _

```

Type `Y` and a new partition table will be created.

**Warning:** If you create a new partition table on a disk with data on it, it will erase all the data on the disk. Make sure this is what you want to do.

*   Create a new partition with the `n` command (primary type/1st partition).
*   Assuming the partition is new, *gdisk* will pick the highest possible alignment. Otherwise, it will pick the largest power of two that divides all partition offsets.
*   If choosing to start on a sector before the 2048th *gdisk* will automatically shift the partition start to the 2048th disk sector. This is to ensure a 2048-sectors alignment (as a sector is 512B, this is a 1024KiB alignment which should fit any SSD NAND erase block).
*   Use the `+*x*{M,G}` format to extend the partition *x* mebibytes or gibibytes, if choosing a size that is not a multiple of the alignment size (1024kiB), *gdisk* will shrink the partition to the nearest inferior multiple. For example, if you want to create a 15GiB partition, you would enter `+15G`. To take all of the remaining space, press enter right away, or enter `+0` instead.
*   Select the partition's type id, the default, `Linux filesystem` (code `8300`), should be fine for most use. Press `L` to show the codes list. If planning to use LVM select `Linux LVM` (`8e00`).
*   Assign other partitions in a like fashion.
*   Write the table to disk and exit via the `w` command.
*   Format the new partitions with a [file system](/index.php/File_system "File system").

### MBR (fdisk)

Using MBR, the utility for editing the partition table is called *fdisk*. Recent versions of *fdisk* have abandoned the deprecated system of using cylinders as the default display unit, as well as MS-DOS compatibility by default. The latest *fdisk* automatically aligns all partitions to 2048 sectors, or 1024 KiB, which should work for all EBS sizes that are known to be used by SSD manufacturers. This means that the default settings will give you proper alignment.

Note that in the olden days, *fdisk* used cylinders as the default display unit, and retained an MS-DOS compatibility quirk that messed with SSD alignment. Therefore one will find many guides around the internet from around 2008-2009 making a big deal out of getting everything correct. With the latest *fdisk*, things are much simpler, as reflected in this guide.

#### fdisk usage summary

Start *fdisk* against your drive as root, in this example we are using `/dev/sda`):

```
# fdisk /dev/sda

Welcome to fdisk (util-linux 2.27.1).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Command (m for help): _ 

```

This opens the *fdisk* dialogue where you can type in commands.

If the drive is brand new or if you are wanting to start over, create a new empty DOS partition table with the `o` command.

**Warning:** Creating a new partition table will erase the data on your drive, make sure this is what you want to do.

### Convert between MBR and GPT

To convert an MBR partition table to GPT, you need the tool *sgdisk*.

```
# sgdisk -g /dev/sda

```

To convert GPT to MBR use the `m` option. Note that it is not possible to convert more than four partitions from GPT to MBR.

```
# sgdisk -m /dev/sda

```

If the device will be bootable you will need to set the bootable flag with *fdisk*.

See also [GUID Partition Table#Convert from MBR to GPT](/index.php/GUID_Partition_Table#Convert_from_MBR_to_GPT "GUID Partition Table").

## Create partitions

### GPT (gdisk)

Launch *gdisk* against the device you want to partition. In this example we use `/dev/sda`:

```
# gdisk /dev/sda

```

You should see a dialogue like the following:

```
# gdisk /dev/sda
GPT fdisk (gdisk) version 1.0.1

Partition table scan:
  MBR: protective
  BSD: not present
  APM: not present
  GPT: present

Found valid GPT with protective MBR; using GPT.

Command (? for help): _

```

### GPT (cgdisk)

Launch *cgdisk* with:

```
# cgdisk /dev/sda

```

You should see a program similar to this on your screen:

```
                                                   cgdisk 1.0.1
                                               Disk Drive: /dev/sda
                                            Size: 234441648, 111.8 GiB

 Part. #     Size        Partition Type            Partition Name
 ----------------------------------------------------------------
             1007.0 KiB  free space
    1        512.0 MiB   BIOS boot partition
    2        111.3 GiB    free space

    [ Align  ]  [ Backup ]  [  Help  ]  [  Load  ]  [  **New**   ]  [  Quit  ]  [ Verify ]  [ Write  ]

                                      Create new partition from free space

```

**Root:**

*   Choose *New* (or press `N`) – `Enter` for the first sector (2048) – type in `15G` – `Enter` for the default hex code (8300) – `Enter` for a blank partition name.

**Home:**

*   Press the down arrow a couple of times to move to the larger free space area.
*   Choose *New* (or press `N`) – `Enter` for the first sector – `Enter` to use the rest of the drive (or you could type in the desired size; for example `30G`) – `Enter` for the default hex code (8300) – `Enter` for a blank partition name.

Here is what it should look like:

```
Part. #     Size        Partition Type            Partition Name
----------------------------------------------------------------
            1007.0 KiB  free space
   1        15.0 GiB    Linux filesystem
   2        123.45 GiB  Linux filesystem

```

Double check and make sure that you are happy with the partition sizes as well as the partition table layout before continuing.

If you would like to start over, you can simply select *Quit* (or press `Q`) to exit without saving changes and then restart *cgdisk*.

If you are satisfied, choose *Write* (or press `Shift+W`) to finalize and to write the partition table to the drive. Type `yes` and choose *Quit* (or press `Q`) to exit without making any more changes.

### MBR (fdisk)

Launch *fdisk* aginst the device you want to partition, in this example we use `/dev/sda`.

```
# fdisk /dev/sda

```

You should see a dialogue that looks like the following:

```
# fdisk /dev/sda

Welcome to fdisk (util-linux 2.27.1).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Command (m for help): _ 

```

*   To create a new partition, type `n` and hit enter.
*   When prompted, specify the partition type, type `p` to create a primary partition or `e` to create an extended one. There may be up to four primary partitions.
*   You then need to pick a partition number, the default should be fine.
*   Set the first sector for the new partition. Again the default should be fine so you can hit enter.
*   Set the size for your new partition.

The following is an example of the dialogue you would see when creating a new 15G partition.

```
Command (m for help): n ↵
Partition type (default p): p ↵
Partition number (1-4, default 1): ↵
First sector (2048-209715199, default 2048): ↵
Last sector, +sectors or +size{K,M,G,T,P} (2048-209715199....., default 209715199): +15G ↵

```

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

In case this does not work because *fdisk* encountered an error, you can use the `q` command to exit.

*   Create a new partition with the `n` command (primary type/1st partition).
*   Use the `+*x*G` format to extend the partition *x* gibibytes. For example, if you want to create a 15GiB partition, you would enter `+15G`
*   Change the partition's system id from the default type of Linux (`type 83`) to the desired type via the `t` command. This is an optional step should the user wish to create another type of partition for example, swap, NTFS, LVM, etc. Note that a complete listing of all valid partition types is available via the `l` command.
*   Assign other partitions in a like fashion.
*   Write the table to disk and exit via the `w` command.

### MBR (cfdisk)

```
                                   Disk: Disk: /dev/sda
                    Size: 111.8 GiB, 120034123776 bytes, 234441648 sectors
                 Label: mbr, identifier: AAAAAAAA-BBBB-CCCC-DDDD-EEEEEEEEEEEE

    Device                  Start            End        Sectors       Size Type
>>  Free space            1050624      234441648      233391024         119G                     
    /dev/sda1                2048        1050623        1048576       512M BIOS boot

                    [   **New**  ]  [  Quit  ]  [  Help  ]  [  Write ]  [  Dump  ]

                                Create new partition from free space

```