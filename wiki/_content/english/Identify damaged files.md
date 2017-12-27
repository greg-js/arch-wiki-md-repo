This article gives details on how to find out which file owns a given block. The main purpose for doing so is finding out which file was damaged in the event a storage device develops any bad blocks (that way you'll know if you lost anything important).

For most of these commands you will have to be either root or a user that has direct read access to the drive you are checking (being a member of the disk group should be enough). As usual, a current backup is always a good idea, especially if imminent drive failure is suspected. [S.M.A.R.T.](/index.php/S.M.A.R.T. "S.M.A.R.T.") can help with determining that.

## Contents

*   [1 Finding bad blocks](#Finding_bad_blocks)
*   [2 Filesystems](#Filesystems)
    *   [2.1 btrfs](#btrfs)
        *   [2.1.1 Find damaged files](#Find_damaged_files)
    *   [2.2 Ext2, ext3, and ext4](#Ext2.2C_ext3.2C_and_ext4)
        *   [2.2.1 Debug the filesystem](#Debug_the_filesystem)
        *   [2.2.2 Find damaged files](#Find_damaged_files_2)
    *   [2.3 JFS](#JFS)
        *   [2.3.1 Debug the filesystem](#Debug_the_filesystem_2)
        *   [2.3.2 Find damaged files](#Find_damaged_files_3)
*   [3 Force the disk to reallocate bad block](#Force_the_disk_to_reallocate_bad_block)
*   [4 See also](#See_also)

#### Finding bad blocks

Just use the [badblocks](/index.php/Badblocks "Badblocks") command. There are a few scan modes supported by it. There's read-only mode (default) which is the least accurate. There is the destructive write-mode (`-w` option) which is the most accurate but takes longer and will (obviously) destroy all data on the drive, thus making it quite useless for matching blocks up to files. There is finally the non-destructive read-write mode which is probably as accurate as the destructive mode, the only real downside of which is it's probably the slowest. However, if a drive is known to be failing then read-only mode is probably still the safest.

To do a verbose (`-v` option), read-only scan, run one of these commands (with `x` being the drive letter and `y` being partition number you want to scan):

Whole disk scan:

```
# badblocks -v /dev/sdx

```

Single partition scan:

```
# badblocks -v /dev/sdxy

```

The downside to scanning the drive as a whole is that each filesystem is going to start its block count relative to the partition it's on. This means that if you have a bad block that happens to be on, let's say, the second partition, and that partition starts on block 1000, then you will have to subtract 1000 from your block number in order to get the number you want. So if a scan from the beginning of the disk results in block number 1005 being bad, then block 5 of the second partition is what you'll actually be using.

Otherwise, if you've found bad blocks after doing a full scan, you can simply figure out which partitions they're on, and rescan those in order to get the block number, rather than do any block math.

Another thing to note is that badblocks defaults to 1024 byte blocks so you will either have to change the default size with the `-b` option in order to match your filesystem or manually convert the block number(s) later.

If you need to figure out where your partitions start and end run [fdisk](/index.php/Fdisk "Fdisk").

**Note:** Older versions might have defaulted to cylinders, not sure. If so the `-u` option will change the default unit to sectors).

Make sure to note the block size [fdisk](/index.php/Fdisk "Fdisk") is using so that you can convert the block counts to match your scan.

 `# fdisk -l /dev/sdx` 
```
255 heads, 63 sectors/track, 19457 cylinders, total 312581808 sectors
**Units = sectors of 1 * 512 = 512 bytes**
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x00000000
```

After all this, you should have the block number(s) of your bad block(s), relative to the partition they exist on.

## Filesystems

### btrfs

Unlike other filesystem types, [btrfs](/index.php/Btrfs "Btrfs") has native support for reporting on damaged files. When scrubbing a partition, *btrfs* reads all data and metadata blocks and verifies checksums. It automatically repairs corrupted blocks if there’s a correct copy available in a RAID configuration. *btrfs* also reports any unreadable sector along with the affected file via system log.

#### Find damaged files

First of all, let's [scrub](/index.php/Btrfs#Scrub "Btrfs") the damaged partition:

 `# btrfs scrub start -Bd /dev/sdxy` 

The same partition can be scrubbed when mounted by providing its mount point:

 `# btrfs scrub start -Bd /mnt/point` 

Scrub reports can be retrieved as many times as need with the `status` subcommand:

 `# btrfs scrub status /mnt/point` 
```
scrub status for e11013b3-b244-4d1a-a9c7-3956db1a699c
        scrub started at Thu Apr 23 19:07:45 2015 and finished after 372 seconds
        total bytes scrubbed: 301.13GiB with 1 errors
        error details: read=1
        corrected errors: 0, uncorrectable errors: 1, unverified errors: 0
```

When done, search the kernel log for I/O errors:

 `$ journalctl --output cat | grep 'BTRFS .* i/o error' | sort | uniq | less`  `Jan 16 23:14:19 my_server kernel: BTRFS: i/o error at logical 398602014720 on dev /dev/sdxy, sector **4621320**, root 5, inode 23839, offset 4378624, length 4096, links 1 (path: **my/damaged/file**)` 

The output above reveals that sector `4621320` couldn't be read and it contains data for file `my/damaged/file`. The sector number can be directly used with [hdparm](/index.php/Hdparm "Hdparm") when reallocating (see [#Force the disk to reallocate bad block](#Force_the_disk_to_reallocate_bad_block)).

### Ext2, ext3, and ext4

#### Debug the filesystem

The *tune2fs* command will give you access to all the low level structures within any ext2/[ext3](/index.php/Ext3 "Ext3")/[ext4](/index.php/Ext4 "Ext4") filesystem.

The first thing we want to do is get the block size from the filesystem in question. Just run:

 `# tune2fs -l /dev/sdxy | grep Block` 
```
Block count:              29119820
**Block size:               4096**
```

In this case 4096 is the block size being used (it appears to be the default).

If you did not run [badblocks](/index.php/Badblocks "Badblocks") using the block size that your filesystem is using then you will need to convert your block number(s) to match it (remember to use the block number(s) relative to the partition they're on).

i.e. block number 100 with a block size of 1024 bytes becomes block number 25 at 4096 bytes. The formula is:

```
(original block number) / ((filesystem block size) / (badblocks block size))

```

Now the entire point of running this program (for the purpose of this article) is to get the *inode* number. Before continuing to debug it, unmount the partition. Then, run the command:

```
# debugfs

```

Then in the `debugfs` console, use the `open` command on the *ext* partition containing the bad sector:

```
debugfs:  open /dev/sdxy

```

Finally, use the `testb` command to get information about the block in question (in this example block 1000):

```
debugfs:  testb *blocknumber*

```

**Note:** If `debugfs` says that block isn't in use then that means the block is not allocated and is being used as free space. In that case this is a good thing as it means nothing important was damaged.

If the block is in use then run this command to get the *inode* number

```
icheck *blocknumber*

```

This will return two numbers. The block number and the *inode* number.

#### Find damaged files

Use the *inode* number (second number from the `icheck` command) with the `ncheck` command:

```
ncheck *inodenumber*

```

The `debugfs` console will give you the full pathname to the file using the bad block. Now you will know what was actually damaged.

If the *inode* number is very small and `ncheck` fails to return a path then it's probably the journal itself that is damaged. To delete the journal simply run this command on the partition:

```
# tune2fs -O ^has_journal /dev/sdxy

```

Run the `testb` command again from the `debugfs` console on the bad block and it should be no longer marked as used if it was indeed used by the journal. To build a new journal run:

```
# tune2fs -j /dev/sdxy

```

### JFS

#### Debug the filesystem

The *jfs_debugfs* tool will give you access to all the low level structures within any [JFS](/index.php/JFS "JFS") filesystem. Other filesystems such as the [ext3](/index.php/Ext3 "Ext3") and [ext4](/index.php/Ext4 "Ext4") filesystems have similar tools. It is probably a good idea to *umount* any filesystem before you run this on them. To use it just run:

```
# jfs_debugfs /dev/sdxy

```

This puts you into a command console. The first thing you should note is your aggregate block size. This is (presumably) the block size the filesystem is using. [JFS](/index.php/JFS "JFS") seems to default to 4096 bytes.

If you did not run [badblocks](/index.php/Badblocks "Badblocks") using the block size that your filesystem is using then you will need to convert your block number(s) to match it (remember to use the block number(s) relative to the partition they're on).

i.e. block number 100 with a block size of 1024 bytes becomes block number 25 at 4096 bytes. The formula is:

```
(original block number) / ((filesystem block size) / (badblocks block size))

```

Now the entire point of running this program (for the purpose of this article) is to get the *inode* number. To do this run the command:

```
d *blocknumber* 0 i

```

The syntax is the `d` command for display, the block number, the offset (just set it to 0), and the display format `i` for *inode*.

**Note:** If you get an error then that means the block is not allocated and is being used as free space. In that case this is a good thing as it means nothing important was damaged.

The decimal number that `di_number` is set to is the one we want. From here you type `x` to exit out of the display mode. Repeat the display command for each bad block that you have and note all of their *inode* numbers. For more info on the *inode* such as permissions and filetype type:

```
i *inodenumber*

```

When you have all the *inode* numbers type `q` to quit.

#### Find damaged files

Finally to find the damaged file you can simply use the gnu [find](/index.php/Find "Find") utility. Mount your filesystem and run:

```
# find / -inum *inodenumber*

```

Substitute `/` for the mountpoint of the filesystem that the *inode* belongs to. If you search root and have more than one filesystem mounted (who doesn't?) you can find multiple files with the same *inode* number on different filesystems, plus [find](/index.php/Find "Find") will take significantly longer. Remember, an *inode* is only unique to the filesystem that it's in.

## Force the disk to reallocate bad block

First you'll want to see how many badblocks the harddrive is aware of through the [smartctl](/index.php/S.M.A.R.T.#smartctl "S.M.A.R.T.") command:

```
# smartctl -t long /dev/sdx

```

Wait until test completes, then:

 `# smartctl -l selftest /dev/sdx` 
```
ID# ATTRIBUTE_NAME          FLAG     VALUE WORST THRESH TYPE      UPDATED  WHEN_FAILED RAW_VALUE
 **5 Reallocated_Sector_Ct   0x0033   100   100   005    Pre-fail  Always       -       0**
**196 Reallocated_Event_Count 0x0032   100   100   000    Old_age   Always       -       0**
197 Current_Pending_Sector  0x0022   100   100   000    Old_age   Always       -       0
**198 Offline_Uncorrectable   0x0008   100   100   000    Old_age   Offline      -       0**
```

To make the harddrive transparently map out the badblock with a spare good sector you will have to simply write zeros to the bad block using the [dd](/index.php/Dd "Dd") command as root. Remember that with this command you have to work with the same block size as your filesystem and the block as to be relative to the partition the filesystem is on and **not** the harddrive as a whole:

```
# dd if=/dev/zero of=/dev/sdxy bs=4096 count=1 seek=2269012
$ sync
```

Alternatively, [hdparm](/index.php/Hdparm "Hdparm") provides a couple of nice and simple options to read and write a given sector (4621327, in the following example):

```
# hdparm --read-sector 4621327 /dev/sdxy
# hdparm --repair-sector 4621327 --yes-i-know-what-i-am-doing /dev/sdxy
```

You can see if the harddrive did indeed map out an additional bad sector by checking with the [smartctl](/index.php/S.M.A.R.T.#smartctl "S.M.A.R.T.") command and seeing if the reallocated sector or event count went up:

 `# smartctl -A /dev/sdx` 
```
ID# ATTRIBUTE_NAME          FLAG     VALUE WORST THRESH TYPE      UPDATED  WHEN_FAILED RAW_VALUE
 **5 Reallocated_Sector_Ct   0x0033   100   100   005    Pre-fail  Always       -       1**
**196 Reallocated_Event_Count 0x0032   100   100   000    Old_age   Always       -       1**
197 Current_Pending_Sector  0x0022   100   100   000    Old_age   Always       -       0
**198 Offline_Uncorrectable   0x0008   100   100   000    Old_age   Offline      -       1**
```

To get `Offline_Uncorrectable` to go back to 0 you need to run a SMART long test and a selftest:

```
# smartctl -t long /dev/sdx

```

Wait until test completes, then:

```
# smartctl -l selftest /dev/sdx

```

## See also

*   [EXT2/3 badblocks howto](https://www.smartmontools.org/wiki/BadBlockHowto)