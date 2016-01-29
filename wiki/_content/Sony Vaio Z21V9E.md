# Sony Vaio Z21V9E

## Installation

The only real hurdle with getting Arch Linux installed is the RAID configuration. There are several alternatives with various advantages and disadvantages. The easiest is to just leave the raid enabled as per factory settings and treat the resulting partition as a single drive.

 `lsblk` 

```
$ lsblk
NAME        MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINT
sda           8:0    0 119.2G  0 disk  
└─md126       9:126  0 238.5G  0 raid0 
  ├─md126p1 259:0    0  15.6G  0 md    /
  └─md126p2 259:1    0 221.9G  0 md    /home
sdb           8:16   0 119.2G  0 disk  
└─md126       9:126  0 238.5G  0 raid0 
  ├─md126p1 259:0    0  15.6G  0 md    /
  └─md126p2 259:1    0 221.9G  0 md    /home

```

As you can see the system contains two separate drives which have been used to create a single RAID partition, raid0\. When preparing your storage drive during installation, you would then treat that raid0 partition as the drive to install on.

 `cfdisk /dev/md126` 

```
                    Disk: /dev/md126
                                                             Size: 238.5 GiB, 256066453504 bytes, 500129792 sectors
                                                                       Label: dos, identifier: 0x000932f6

    Device                     Boot                                 Start                     End                 Sectors                Size              Id Type
    /dev/md126p1               *                                     2048                32770047                32768000               15.6G              83 Linux
    /dev/md126p2                                                 32770048               498081791               465311744              221.9G              83 Linux
>>  Free space                                                  498081792               500129791                 2048000               1000M                      

```

Alternatively, just disable the IRST and treat the two SSD drives separately.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Sony_Vaio_Z21V9E&oldid=349264](https://wiki.archlinux.org/index.php?title=Sony_Vaio_Z21V9E&oldid=349264)"