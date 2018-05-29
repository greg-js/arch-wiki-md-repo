The [Advanced Format](https://en.wikipedia.org/wiki/Advanced_Format "wikipedia:Advanced Format") is a generic term pertaining to any disk sector format used to store data on magnetic disks in [hard disk drives](https://en.wikipedia.org/wiki/hard_disk_drives "w:hard disk drives") (HDDs) that uses 4 kilobyte sectors instead of the traditional 512 byte sectors. The main idea behind using 4096-byte sectors is to increase the bit density on each track by reducing the number of gaps which hold Sync/DAM and ECC (Error Correction Code) information between data sectors. The old format gave a format efficiency of 88.7%, whereas Advanced Format results in a format efficiency of 97.3%.

There are two types of AF drives:

*   Advanced Format drives, marked with an orange "AF" logo: internally, they use 4k sectors, but provide an emulation layer for compatibility with OSes which lack support for them.
*   Advanced Format 4k native drives, marked with a blue "4Kn" logo: they require OS support (Windows 8+, or Linux 2.6.31+). Because they don't need a translation layer, they are cheaper, however they might be incompatible with old tools.

## How to determine if HDD employ a 4k sector

The physical and logical sector size of hard disk `/dev/sd*X*` can be determined by reading the following sysfs entries:

```
$ cat /sys/class/block/sd*X*/queue/physical_block_size
$ cat /sys/class/block/sd*X*/queue/logical_block_size

```

Drives with a translation layer (see above) will usually report a logical block size of 512 (for backwards compatibility) and a physical block size of 4096 (indicating they are AF drives).

Tools which will report the physical sector of a drive (provided the drive will report it correctly) includes

*   smartmontools (since 5.41 ; `smartctl -a`, in information section)
*   hdparm (since 9.12 ; `hdparm -I`, in configuration section)

Note that both works even for USB-attached discs (if the USB bridge supports SAT aka SCSI/ATA Translation, ANSI INCITS 431-2007).

## See also

*   [Western Digital’s Advanced Format: The 4K Sector Transition Begins](http://www.anandtech.com/Show/Index/2888)
*   [White paper entitled "Advanced Format Technology."](http://www.wdc.com/wdproducts/library/WhitePapers/ENG/2579-771430.pdf)
*   Failure to align one's HDD results in poor read/write performance. See [this article](http://www.linuxconfig.org/linux-wd-ears-advanced-format) for specific examples.