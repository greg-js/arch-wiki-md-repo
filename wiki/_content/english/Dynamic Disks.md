[Dynamic disks](https://msdn.microsoft.com/en-us/library/windows/desktop/aa363785(v=vs.85).aspx#DYNAMIC_DISKS), enabled by the [Logical Disk Manager](https://en.wikipedia.org/wiki/Logical_Disk_Manager "wikipedia:Logical Disk Manager") (LDM), is a technology for Microsoft Windows that is similar to [LVM](/index.php/LVM "LVM") and [mdadm](/index.php/Mdadm "Mdadm").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 General consideration for Linux usage](#General_consideration_for_Linux_usage)
    *   [1.1 Usual course](#Usual_course)
*   [2 Terminology](#Terminology)
*   [3 Installing support for dynamic disks](#Installing_support_for_dynamic_disks)
    *   [3.1 Mandatory preparation](#Mandatory_preparation)
    *   [3.2 Other commands](#Other_commands)
*   [4 Systemd](#Systemd)
*   [5 See also](#See_also)

## General consideration for Linux usage

In general it is not recommended to convert the disk drive to host your Linux into a dynamic disk. This is because:

*   In a dynamic disk, an entire disk is put in a one, big partition. (More precisely, a GPT dynamic disk will have one big partition for data and the other, one small metadata partition. An MBR dynamic disk has a sole partition. See [How Dynamic Disks and Volumes Work](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc758035(v=ws.10)) in microsoft.com.)
*   To turn a disk to a dynamic disk, all existing partitions have to be recognized by Windows - Linux partitions (ext4, btrfs, lvm, you name it) are out!

Probably the sole case you want to use dynamic disks is when you use RAID in Windows.

Dynamic disks cannot be used on removable disks, either.

### Usual course

[LVM](/index.php/LVM "LVM") and [mdadm](/index.php/Mdadm "Mdadm") are the preferred tools under Arch Linux. However, if the system is being dual-booted with Windows, Windows will not be able to read these setups. The usual course then is to attempt to use [fakeraid](/index.php/Fakeraid "Fakeraid") using [dmraid](https://www.archlinux.org/packages/?name=dmraid) or to use network storage. However, network storage retrieval will be capped to 1Gb/s (119MiB/s) and getting RAID drivers loaded on an existing Windows installation can be daunting (if not impossible) if the Windows OS partition is installed on a drive that is on the very controller that you want to switch from AHCI to RAID. Even if you have a spare AHCI controller card, your system may not have enough space to hold two Option ROMs.

## Terminology

Read "spanned volume" of a dynamic disk as a "logical volume" in Linux LVM, and "striped volume" as RAID0.

## Installing support for dynamic disks

**Note:** This tool will only give you the ability to read and write dynamic disks in Arch Linux. For all other tasks, you will have to use Windows' Logical Disk Manager.

Install the [ldmtool](https://aur.archlinux.org/packages/ldmtool/) package. Once installed, `ldmtool` can be used to query and mount dynamic disks.

### Mandatory preparation

To create device mappers, simply do:

```
# ldmtool create all

```

This populates `/dev/mapper` with volumes under LDM. Once this is done, they become accessible in a usual manner, say by:

```
# mount -t ntfs /dev/mapper/<your ldm volume> /mnt/somewhere

```

### Other commands

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

## Systemd

To get dynamic disks behave like filesystems natively supported by the Linux kernel, use this systemd unit:

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

Once this setup is complete, you can add entries to `/etc/fstab` that reference dynamic disk volumes and have those mounted like any other volume.

## See also

*   [Basic and Dynamic Disks](https://docs.microsoft.com/en-us/windows/win32/fileio/basic-and-dynamic-disks) (Microsoft site)
*   [Working with Basic and Dynamic Disks](https://docs.microsoft.com/en-us/previous-versions/tn-archive/dd163552(v=technet.10)) (Microsoft site)
*   [wikipedia:Dynamic disk](https://en.wikipedia.org/wiki/Dynamic_disk "wikipedia:Dynamic disk")