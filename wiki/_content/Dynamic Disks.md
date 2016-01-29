# Dynamic Disks

Dynamic Disks is a technology from Microsoft and Veritas Software (now owned by Symantec) that brings LVM and mdadm functionality to Windows. Dynamic Disks first appeared in Windows 2000, but the concept existed in a different implementation under Windows NT Server 4.0\. This feature has been limited to the Professional, Enterprise and/or Server versions of Windows until Windows 7, wherein Home Premium users can create Simple (single partition), Spanned (JBOD), or Striped (RAID0) volumes. Unlike LVM and mdadm, Dynamic Disks always take up the entire disk. If the Dynamic Disk uses MBR partitions, one large partition will hold the data while metadata is stored outside the partition at the end of the disk. If the Dynamic Disk uses GPT partitions, two partition will be used -- a small one at the beginning to hold the metadata and a large one for the data taking up the remainder of the disk space.

## Uses Under Arch Linux

[LVM](/index.php/LVM "LVM") and [mdadm](/index.php/Mdadm "Mdadm") are the preferred tools under Arch Linux. However, if the system is being dual-booted with Windows, Windows will not be able to read these setups. The usual course then is to attempt to use [fakeraid](/index.php/Fakeraid "Fakeraid") using [dmraid](https://www.archlinux.org/packages/?name=dmraid) or to use network storage. However, network storage retrieval will be capped to 1Gb/s (119MiB/s) and getting RAID drivers loaded on an existing Windows installation can be daunting (if not impossible) if the Windows OS partition is installed on a drive that's on the very controller that you want to switch from AHCI to RAID. Even if you have a spare AHCI controller card, your system may not have enough space to hold two Option ROMs.

## Installing Support for Dynamic Disks

**Note:** This tool will only give you the ability to use Dynamic Disks in Arch Linux. For all other tasks, you will have to use Windows' Logical Disk Manager.

Install the [ldmtool](https://aur.archlinux.org/packages/ldmtool/)<sup><small>AUR</small></sup> package. Once installed, `ldmtool` can be used to query and mount Dynamic Disks.

To find all disk groups:

```
# ldmtool scan

```

To find what volumes a disk group contains:

```
# ldmtool show diskgroup {diskgroup UUID}

```

To create individual device mappers:

```
# ldmtool create volume {volume name}

```

To create device mappers for all volumes in a disk group:

```
# ldmtool create volume {diskgroup UUID}

```

To create device mappers for all volumes in all discovered disk groups:

```
# ldmtool create all

```

## System Integration

To get Dynamic Disks to behave like filesystems natively supported by the Linux kernel, use this systemd unit:

 `/etc/systemd/system/ldmtool.service` 

```
[Unit]
Description=Windows Dynamic Disk Mount
Before=local-fs-pre.target
DefaultDependencies=no
[Service]
Type=simple
User=root
ExecStart=/usr/bin/ldmtool create all
[Install]
WantedBy=local-fs-pre.target

```

Then [enable](/index.php/Enable "Enable") `ldmtool.service`.

Once this setup is complete, you can add entries to `/etc/fstab` that reference Dynamic Disk volumes and have those mounted like any other volume.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dynamic_Disks&oldid=413580](https://wiki.archlinux.org/index.php?title=Dynamic_Disks&oldid=413580)"