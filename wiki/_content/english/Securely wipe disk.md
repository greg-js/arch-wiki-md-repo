Related articles

*   [Securely wipe disk/Tips and tricks](/index.php/Securely_wipe_disk/Tips_and_tricks "Securely wipe disk/Tips and tricks")
*   [File recovery](/index.php/File_recovery "File recovery")
*   [Benchmarking/Data storage devices](/index.php/Benchmarking/Data_storage_devices "Benchmarking/Data storage devices")
*   [Frandom](/index.php/Frandom "Frandom")
*   [Disk encryption#Preparing the disk](/index.php/Disk_encryption#Preparing_the_disk "Disk encryption")
*   [dm-crypt](/index.php/Dm-crypt "Dm-crypt")

Wiping a disk is done by writing new data over every single bit.

**Note:** References to "disks" in this article also apply to loopback devices.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Common use cases](#Common_use_cases)
    *   [1.1 Wipe all data left on the device](#Wipe_all_data_left_on_the_device)
    *   [1.2 Preparations for block device encryption](#Preparations_for_block_device_encryption)
*   [2 Data remanence](#Data_remanence)
    *   [2.1 Operating system, programs and filesystem](#Operating_system,_programs_and_filesystem)
    *   [2.2 Hardware-specific issues](#Hardware-specific_issues)
        *   [2.2.1 Flash memory](#Flash_memory)
        *   [2.2.2 Marked Bad Sectors](#Marked_Bad_Sectors)
        *   [2.2.3 Residual magnetism](#Residual_magnetism)
*   [3 Select a target](#Select_a_target)
*   [4 Select a data source](#Select_a_data_source)
    *   [4.1 Zeros](#Zeros)
    *   [4.2 Random data](#Random_data)
*   [5 Select a block size](#Select_a_block_size)
    *   [5.1 Calculate blocks to wipe manually](#Calculate_blocks_to_wipe_manually)
*   [6 Overwrite the target](#Overwrite_the_target)
    *   [6.1 By redirecting output](#By_redirecting_output)
    *   [6.2 dd](#dd)
    *   [6.3 wipe](#wipe)
    *   [6.4 shred](#shred)
    *   [6.5 Badblocks](#Badblocks)
    *   [6.6 hdparm](#hdparm)
*   [7 See also](#See_also)

## Common use cases

### Wipe all data left on the device

The most common usecase for completely and irrevocably wiping a device will be when the device is going to be given away or sold. There may be (unencrypted) data left on the device and you want to protect against simple forensic investigation that is mere child's play with for example [File recovery](/index.php/File_recovery "File recovery") software.

If you want to quickly wipe everything from the disk, `/dev/zero` or simple patterns allow maximum performance while adequate randomness can be advantageous in some cases that should be covered up in [#Data remanence](#Data_remanence).

Every overwritten bit means to provide a level of data erasure not allowing recovery with normal system functions (like standard ATA/SCSI commands) and hardware interfaces. Any file recovery software mentioned above then would need to be specialized on proprietary storage-hardware features.

In case of a HDD data recreation will not be possible without at least undocumented drive commands or fiddling about the device’s controller or firmware to make them read out for example reallocated sectors (bad blocks that [S.M.A.R.T.](/index.php/S.M.A.R.T. "S.M.A.R.T.") retired from use).

There are different wiping issues with different physical storage technologies, most notably all Flash memory based devices and older magnetic storage (old HDD's, floppy disks, tape).

### Preparations for block device encryption

To prepare a drive for [block device encryption](/index.php/Disk_encryption#Block_device_encryption "Disk encryption") inside the wiped area afterwards, it is recommended to use [#Random data](#Random_data) generated by a cryptographically strong random number generator (referred to as RNG in this article from now on).

See also [Wikipedia:Random number generation](https://en.wikipedia.org/wiki/Random_number_generation "wikipedia:Random number generation").

**Warning:** If block device encryption is mapped on a partition that contains non-random or unencrypted data, the encryption is weakened and becomes comparable to filesystem-level encryption: disclosure of usage patterns on the encrypted drive becomes possible. Therefore, do not fill space with zeros, simple patterns (like badblocks) or other non-random data before setting up block device encryption if you are serious about it.

## Data remanence

See also [Wikipedia:Data remanence](https://en.wikipedia.org/wiki/Data_remanence "wikipedia:Data remanence"). The representation of data may remain even after attempts have been made to remove or erase the data.

### Operating system, programs and filesystem

The operating system, executed programs or [journaling file systems](https://en.wikipedia.org/wiki/Journaling_file_system "wikipedia:Journaling file system") may copy your unencrypted data throughout the block device. When writing to plain disks this should only be relevant in conjunction with one of the above.

If the data can get exactly located on the disk and was never copied anywhere else, wiping with random data can be thoroughgoing and impressively quick as long there is enough entropy in the pool.

A good example is cryptsetup using `/dev/urandom` for [wiping the LUKS keyslots](/index.php/Dm-crypt/Device_encryption#Key_management "Dm-crypt/Device encryption").

### Hardware-specific issues

#### Flash memory

[Write amplification](https://en.wikipedia.org/wiki/Write_amplification "wikipedia:Write amplification") and other characteristics make Flash memory, including SSDs, a stubborn target for reliable wiping. As there is a lot of transparent abstraction in between data as seen by a device's controller chip and the operating system sight data is never overwritten in place and wiping particular blocks or files is not reliable.

Other "features" like transparent compression (all SandForce SSD's) can compress your zeros or repetitive patterns so if wiping is fast beyond belief this might be the case.

Disassembling Flash memory devices, unsoldering the chips and analyzing data content without the controller in between is feasible without difficulty using [simple hardware](http://www.flash-extractor.com/manual/reader_models/). Data recovery companies do it for cheap money.

For more information see:

*   [Solid state drive/Memory cell clearing](/index.php/Solid_state_drive/Memory_cell_clearing "Solid state drive/Memory cell clearing")
*   [Reliably Erasing Data From Flash-Based Solid State Drives](http://www.usenix.org/events/fast11/tech/full_papers/Wei.pdf).
*   [#Select a target](#Select_a_target)

#### Marked Bad Sectors

If a hard drive marks a sector as bad, it cordons it off, and the section becomes impossible to write to via software. Thus a full overwrite would not reach it. However because of block sizes, these sections would only amount to a few theoretically recoverable KB.

#### Residual magnetism

A single, full overwrite with zeros or random data does not lead to any recoverable data on a modern high-density storage device. Note that repeating the operation should not be necessary nowadays. [[1]](http://www.howtogeek.com/115573/htg-explains-why-you-only-have-to-wipe-a-disk-once-to-erase-it/) Indications otherwise refer to single residual bits; reconstruction of byte patterns is generally not feasible.[[2]](https://web.archive.org/web/20120102004746/http://www.h-online.com/newsticker/news/item/Secure-deletion-a-single-overwrite-will-do-it-739699.html) See also [[3]](https://www.google.com/search?tbs=bks:1&q=isbn:9783540898610), [[4]](http://security.stackexchange.com/questions/26132/is-data-remanence-a-myth/26134#26134) and [[5]](http://www.nber.org/sys-admin/overwritten-data-guttman.html).

## Select a target

Use [fdisk](/index.php/Fdisk "Fdisk") to locate all read/write devices the user has read access to.

Check the output for lines that start with devices such as `/dev/sd"X"`.

This is an example for a HDD formatted to boot a linux system:

 `# fdisk -l` 
```
Disk /dev/sda: 250.1 GB, 250059350016 bytes, 488397168 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x00ff784a

   Device Boot      Start         End      Blocks   Id  System
/dev/sda1   *        2048      206847      102400   83  Linux
/dev/sda2          206848   488397167   244095160   83  Linux

```

Or another example with the Arch Linux image written to a 4GB USB thumb drive:

 `# fdisk -l` 
```
Disk /dev/sdb: 4075 MB, 4075290624 bytes, 7959552 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x526e236e

   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1   *           0      802815      401408   17  Hidden HPFS/NTFS

```

If you are worried about unintentional damage of important data on the primary computer, consider using an isolated environment such as a virtual environment (VirtualBox, VMWare, QEMU, etc...) with direct connected disk drives to it or a single computer only with a storage disk(s) that need to be wiped booted from a [Live Media](/index.php/Archiso "Archiso") (USB, CD, PXE, etc...) or use a script to [prevent wiping mounted partitions by typo](/index.php/Securely_wipe_disk/Tips_and_tricks#Prevent_wiping_mounted_partitions "Securely wipe disk/Tips and tricks").

## Select a data source

To wipe sensitive data, one can use any data pattern matching the needs.

### Zeros

Overwriting with `/dev/zero` or simple patterns is considered secure in most situations. With today's HDDs, it is deemed appropriate and fast for disk wiping.

However, a drive that is abnormally fast in writing patterns or zeroing could be doing transparent compression. It is obviously presumable not all blocks get wiped this way. Some [#Flash memory](#Flash_memory) devices do "feature" that.

To setup block device encryption afterwards, one should wipe the area with random data (see next section) to avoid weakening the encryption.

**Warning:** Subject to compression and to be used carefully with flash memory and SSDs, to be avoided for block encryption preparation as stated above.

### Random data

True random data source using `/dev/random` is impractical for wiping large capacities as it will take too long to wait for the entropy generation. `/dev/urandom` can be used as a reasonable source of pseudorandom data. For differences between random and pseudorandom data as source, please see [Random number generation](/index.php/Random_number_generation "Random number generation").

Another alternative for pseudorandom data generation is to use an encrypted datastream. For example, if one wants to prepare a device for block encryption and will use AES for the encrypted partition, it is appropriate to wipe it with a similar cipher prior to creating the filesystem to make the empty space not distinguishable from the used space.

## Select a block size

See also [Wikipedia:Dd (Unix)#Block size](https://en.wikipedia.org/wiki/Dd_(Unix)#Block_size "wikipedia:Dd (Unix)"), [blocksize io-limits](http://people.redhat.com/msnitzer/docs/io-limits.txt).

If you have an [Advanced Format](/index.php/Advanced_Format "Advanced Format") hard drive it is recommended that you specify a block size larger than the default 512 bytes. To speed up the overwriting process choose a block size matching your drive's physical geometry by appending the block size option to the *dd* command (i.e. `bs=4096` for 4KB).

*fdisk* prints physical and logical sector size for every disk. Alternatively sysfs does expose information:

```
/sys/block/sdX/size
/sys/block/sdX/queue/physical_block_size
/sys/block/sdX/queue/logical_block_size
/sys/block/sdX/sdXY/alignment_offset
/sys/block/sdX/sdXY/start
/sys/block/sdX/sdXY/size

```

**Warning:** These methods show the block size the drive reports to the kernel. However, many Advanced Format drives incorrectly understate the physical block size as 512.

**Tip:** The script [genwipe.sh](https://aur.archlinux.org/packages/genwipe.sh/) helps to calculate parameters to wipe a device/partition with *dd*, e.g.`genwipe.sh /dev/sd"XY"`.

### Calculate blocks to wipe manually

A block storage devices contains sectors and a size of a single sector that can be used to calculate the whole size of device in bytes. You can do it by multiplying sectors with size of the sector.

As an example we use the parameters with the *dd* command to wipe a partition:

```
# dd if=*data_source* of=/dev/sdX bs=*sector_size* count=*sector_number* seek=*partitions_start_sector* status=progress

```

Here, to illustrate with a practical example, we will show the output of the *fdisk* command on the partition `/dev/sdX`:

 `# fdisk -l /dev/sdX` 
```
Disk /dev/sdX: 1.8 TiB, **2000398934016** bytes, **3907029168** sectors
Disk model: ST3500413AS
Units: sectors of 1 * **512** = 512 bytes
Sector size (logical/physical): 512 bytes / **4096** bytes
...
Device     Boot      Start        End         Sectors     Size  Id Type
/dev/sdX1            2048         3839711231  3839709184  1,8T  83 Linux
/dev/sdX2            3839711232   3907029167  67317936    32,1G  5 Extended
```

*   The first line of the *fdisk* output shows the disk size in bytes and in logical sectors.
*   The size in bytes of the storage device or of the partition can also be obtained with the command `blockdev --getsize64 /dev/sdXY`.
*   The *Units* line of the *fdisk* output shows the size of single logical sector; the logical sector size can also be derived from the number of bytes divided by the number of logical sectors, here use: `echo $((2000398934016 / 3907029168))`.
*   To know the physical sector size in bytes (that will make it work faster), we can use the next line.
*   To get the disk size in physical sectors, one can divide the disk size in bytes by the size of a single physical sector, here `echo $((2000398934016 / 4096))`,

**Note:**

*   In the examples below we will use the logical sector size.
*   You can even wipe unallocated disk space with a `dd` command by calculating the difference between the end of one and start of the next partition.

To wipe partition `/dev/sdX1`, the example parameters with logical sectors would be used like follows.

*   By using the starting address of the partition on the device using the `seek=` parameter:

```
# dd if=*data_source* of=/dev/sdX bs=${BytesInSector} count=${End - Start} seek=${Start} status=progress

```

with `Start=2048`, `End=3839711231` and `BytesInSector=512`.

*   Or by using the partitions size in logical sectors:

```
# dd if=*data_source* of=/dev/sdX1 bs=${BytesInSector} count=${LogicalSectors} status=progress

```

with `LogicalSectors=3839709184`.

Or, to wipe the whole disk by using physical sectors:

```
# dd if=*data_source* of=/dev/sdX bs=${PhysicalSectorSizeBytes} count=${AllDiskPhysicalSectors} seek=0 status=progress

```

with `AllDiskPhysicalSectors=488378646` and `PhysicalSectorSizeBytes=4096`.

**Note:** The `count=` option is not necessary when wiping all the physical area e.g. `sdXY` or `sdX` from the start to the end but it shows an error about out of free space when it tries to write outside the limits.

## Overwrite the target

The chosen drive can be overwritten with several utilities, make your choice. If you only want to wipe a single file, [Securely wipe disk/Tips and tricks#Wipe a single file](/index.php/Securely_wipe_disk/Tips_and_tricks#Wipe_a_single_file "Securely wipe disk/Tips and tricks") has considerations in addition to the utilities mentioned below.

### By redirecting output

The redirected output can be used both for creation of the files to rewrite free space on the partition, wipe the whole device or a single partition on it.

In the following are examples that can be used to rewrite the partition or a block device by redirecting [stdout](http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO-3.html) from other utilities:

 `$ cat /dev/urandom > /dev/sd"XY"` 
```
cat: write error: No space left on device

```
 `$ xz -z0 /dev/urandom -c > /dev/sd"XY"` 
```
xz: (stdout): Write error: No space left on device

```
 `$ dd if=/dev/urandom > /dev/sd"XY"` 
```
dd: writing to ‘standard output’: No space left on device
20481+0 records in
20480+0 records out
10485760 bytes (10 MB, 10 MiB) copied, 2.29914 s, 4.6 MB/s
```

The file copy command `cp` can also be used to rewrite the device, because it ignores the type of the destination:

 `$ cp /dev/urandom /dev/sd"XY"` 
```
 cp: error writing ‘/dev/sd"XY"’: No space left on device
 cp: failed to extend ‘/dev/sd"XY"’: No space left on device

```

To show speed and time you can use [pv](https://www.archlinux.org/packages/?name=pv):

```
# pv --timer --rate --stop-at-size -s "$(blockdev --getsize64 /dev/sd"XY" )" /dev/zero > /dev/sd"XY"

```

### dd

See also [dd](/index.php/Dd "Dd") and [Securely wipe disk/Tips and tricks#Wipe a single file](/index.php/Securely_wipe_disk/Tips_and_tricks#Wipe_a_single_file "Securely wipe disk/Tips and tricks").

**Warning:** There is no confirmation regarding the sanity of this command so **repeatedly check** that the correct drive or partition has been targeted. Make certain that the `of=...` option points to the target drive and not to a system disk.

Zero-fill the disk by writing a zero byte to every addressable location on the disk using the [/dev/zero](https://en.wikipedia.org/wiki//dev/zero "wikipedia:/dev/zero") stream.

```
# dd if=/dev/zero of=/dev/sdX bs=4096 status=progress

```

Or the [/dev/urandom](https://en.wikipedia.org/wiki//dev/random "wikipedia:/dev/random") stream:

```
# dd if=/dev/urandom of=/dev/sdX bs=4096 status=progress

```

The process is finished when dd reports `No space left on device` and returns control back:

```
dd: writing to ‘/dev/sdX’: No space left on device
7959553+0 records in
7959552+0 records out
4075290624 bytes (4.1 GB, 3.8 GiB) copied, 1247.7 s, 3.3 MB/s

```

To speed up wiping a large drive, see also:

*   [Securely wipe disk/Tips and tricks#dd - advanced example](/index.php/Securely_wipe_disk/Tips_and_tricks#dd_-_advanced_example "Securely wipe disk/Tips and tricks") which uses OpenSSL,
*   [Securely wipe disk/Tips and tricks#Using a template file](/index.php/Securely_wipe_disk/Tips_and_tricks#Using_a_template_file "Securely wipe disk/Tips and tricks") which wipes with non-random preset data(e.g. overwrite a whole disk with a single file) but is very fast
*   [Dm-crypt/Drive preparation#dm-crypt specific methods](/index.php/Dm-crypt/Drive_preparation#dm-crypt_specific_methods "Dm-crypt/Drive preparation") which uses dm-crypt.

### wipe

Specialized on wiping files and is available as the [wipe](https://www.archlinux.org/packages/?name=wipe) package. To make a quick wipe of a destination you can use something like:

```
$ wipe -r /path/to/wipe

```

See also [wipe(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wipe.1). The tool was last updated in 2009\. Its [SourceForge page](http://wipe.sourceforge.net/) suggests that it is **currently unmaintained**.

### shred

[*shred*](https://www.gnu.org/software/coreutils/manual/html_node/shred-invocation.html) (from the [coreutils](https://www.archlinux.org/packages/?name=coreutils) package) is a Unix command that can be used to securely delete individual files or full devices so that they can be recovered only with great difficulty with specialised hardware, if at all. By default *shred* uses three passes, writing [pseudo-random data](/index.php/Random_number_generation "Random number generation") to the device during each pass. This can be reduced or increased.

The following command invokes shred with its default settings and displays the progress.

```
# shred -v /dev/sd*X*

```

Alternatively, shred can be instructed to do only one pass, with entropy from e.g. `/dev/urandom`.

```
# shred --verbose --random-source=/dev/urandom -n1 /dev/sd*X*

```

### Badblocks

The tool [badblocks](/index.php/Badblocks "Badblocks") from [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) is able to perform destructive read-write test, actually achieving the wiping of the device. By default it performs 4 passes and can take very long.

```
# badblocks -wsv /dev/*device*

```

### hdparm

**Warning:** Do not attempt to issue a Secure Erase ATA command on a device connected through USB; see [https://ata.wiki.kernel.org/index.php/ATA_Secure_Erase](https://ata.wiki.kernel.org/index.php/ATA_Secure_Erase) and [http://www.tomshardware.co.uk/answers/id-1984547/secure-erase-external-usb-hard-drive.html](http://www.tomshardware.co.uk/answers/id-1984547/secure-erase-external-usb-hard-drive.html) for details.

[hdparm](/index.php/Hdparm "Hdparm") supports [ATA Secure Erase](http://tinyapps.org/docs/wipe_drives_hdparm.html), which is functionally equivalent to zero-filling a disk. It is however handled by the hard-drive firmware itself, and includes "hidden data areas". As such, it can be seen as a modern-day "low-level format" command. [SSD](/index.php/SSD "SSD") drives reportedly achieve factory performance after issuing this command, but may not be sufficiently wiped (see [#Flash memory](#Flash_memory)).

Some drives support **Enhanced Secure Erase**, which uses distinct patterns defined by the manufacturer. If the output of `hdparm -I` for the device indicates a manifold time advantage for the **Enhanced** erasure, the device probably has a hardware encryption feature and the wipe will be performed to the encryption keys only.

For detailed instructions on using ATA Secure Erase, see [Solid state drive/Memory cell clearing](/index.php/Solid_state_drive/Memory_cell_clearing "Solid state drive/Memory cell clearing") and the [Linux ATA wiki](https://ata.wiki.kernel.org/index.php/ATA_Secure_Erase).

## See also

*   [Wipe free space in Linux](http://superuser.com/questions/19326/how-to-wipe-free-disk-space-in-linux)