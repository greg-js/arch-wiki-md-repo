# JFS Filesystem

Related articles

*   [File systems](/index.php/File_systems "File systems")

This article introduces the reader to the JFS file system. In particular, procedures for implementation, maintenance and optimization will be presented along with background information on the file system itself and some cautionary notes on precarious implementations.

## Contents

*   [1 Background](#Background)
    *   [1.1 GNU/Linux development team](#GNU.2FLinux_development_team)
    *   [1.2 Technical features](#Technical_features)
*   [2 Implementing on GNU/Linux](#Implementing_on_GNU.2FLinux)
*   [3 Optimizations](#Optimizations)
    *   [3.1 Defragmenting JFS](#Defragmenting_JFS)
    *   [3.2 Deadline I/O scheduler](#Deadline_I.2FO_scheduler)
    *   [3.3 External journal](#External_journal)
    *   [3.4 noatime fstab attribute](#noatime_fstab_attribute)
    *   [3.5 Journal modes](#Journal_modes)
    *   [3.6 Variable block sizes](#Variable_block_sizes)
*   [4 fsck and recovery](#fsck_and_recovery)
*   [5 Cautionary notes](#Cautionary_notes)
    *   [5.1 JFS root mounts read only on startup](#JFS_root_mounts_read_only_on_startup)
    *   [5.2 JFS and secure deletions](#JFS_and_secure_deletions)
    *   [5.3 Forced fsck on JFS root file system](#Forced_fsck_on_JFS_root_file_system)
    *   [5.4 JFS losing files](#JFS_losing_files)
*   [6 Benchmarks](#Benchmarks)
*   [7 Conclusions](#Conclusions)
*   [8 See also](#See_also)

## Background

The Journaled File System (JFS) is a [journaling file system](https://en.wikipedia.org/wiki/Journaling_file_system "wikipedia:Journaling file system") that was open-sourced by IBM in 1999 and support for which has been available in the Linux kernel since 2002\.

*   In 1990, JFS1, (then simply called JFS), was released for AIX version 3.1\. The filesystem was closely tied to its targeted hardware, IBM's AIX line of UNIX servers, being a proprietary design.
*   In 1995, heavy development began on improving JFS, focusing on scalability and expanded features.
*   In 1997, parallel development began on moving the improved JFS source back to AIX.
*   In 1999, the improved JFS design was released for OS/2.
*   In 2001, the improved filesystem (newly termed JFS2), was released for AIX 5L.
*   The current GNU/Linux version is a port based on JFS for OS/2.

**Note:** While there are potential issues, JFS file systems for OS/2 and GNU/Linux are inter-operable.[[1]](http://72.14.253.104/search?q=cache:xrFItCW2XdUJ:osdir.com/ml/file-systems.jfs.general/2006-02/msg00008.html+jfs+os/2+linux&hl=en&ct=clnk&cd=1&gl=au&client=firefox-a).

While it is difficult to make general comparisons between JFS and other file systems available on UNIX and UNIX-like operating systems, it is claimed that JFS uses less CPU resources than other GNU/Linux file systems [[2]](http://www.debian-administration.org/articles/388). With certain optimizations, JFS has also been claimed to be faster for certain file operations, as compared to other GNU/Linux file systems (see [[3]](http://www.redhat.com/archives/ext3-users/2005-July/msg00018.html),[Benchmarks](#Benchmarks)).

### GNU/Linux development team

The development of the GNU/Linux JFS port is headed by

*   Dave Kleikamp (dave dot kleikamp at oracle dot com)
*   HP: [http://jfs.sourceforge.net/](http://jfs.sourceforge.net/)

### Technical features

JFS is a modern file system supporting many features, a few of which are listed here.

*   fully 64-bit.
*   dynamic space allocation for i-nodes, i.e. no running out of i-nodes on file systems with large number of small files.
*   Directory structures designed for speed and efficiency:

	- directories with eight or fewer entries have their contents storied inline within that directory's i-node.

	- directories with more than eight entries have their contents stored in a [B+ tree](https://en.wikipedia.org/wiki/B%2B_tree "wikipedia:B+ tree") keyed on name.

*   JFS utilizes extents for allocating blocks for large files.
*   Support for extended attributes in addition to standard Unix-style permissions.
*   Support for both internal and external logs ([see below](#External_journal)).
*   Extremely Scalable; Consistent performance from minimum file size up to 4 petabytes.
*   Algorithms designed for high performance on very large systems.
*   Performance tuned for GNU/Linux.
*   Designed from the ground up to provide Transaction/Log (not an add-on).
*   Restarts after a system failure < 1 sec.
*   Proven Journaling FS technology (10+ years in AIX).
*   Original design goals: Performance, Robustness, SMP.
*   Team members from the original AIX JFS Designed/Developed this file system.
*   Designed to operate on SMP hardware, with code optimized for at least a 4-way SMP machine.
*   TRIM support (since Kernel 3.7).

**Note:** JFS uses a journal to maintain consistency of metadata _only_. Thus, only consistency of metadata (and not actual file contents) can be assured in the case of improper shutdown. This is also the case for XFS and ReiserFS. Ext3, on the other hand, does support journaling of _both_ metadata and data [[4]](http://www.thehackademy.net/madchat/ebooks/FileSystem/up2-6Galli.pdf), though with a significant performance penalty, and not by default.

A more comprehensive (and technical) overview of the features in JFS can be found in the [JFS Overview](http://jfs.sourceforge.net/project/pub/jfs.pdf) authored by developer Steve Best.

## Implementing on GNU/Linux

Implementing a JFS file system is just like implementing most other file systems under GNU/Linux. JFS was merged into the Linux kernel as of version 2.4 [[5]](http://kerneltrap.org/node/385). The JFS driver is built as a module in the standard Arch kernel packages. If building a custom kernel on a machine that will be (or does) use JFS file systems, be sure to enable JFS in your kernel config:

```
File systems
        ---> [*/M] JFS filesystem support

```

If extended attributes are desired, one will also need to enable "JFS POSIX Access Control Lists" and/or "JFS Security Labels"

```
File systems
    ---> [*/M] JFS filesystem support 
        ---> [*] JFS POSIX Access Control Lists
        ---> [*] JFS Security Labels

```

Next, the [jfsutils](https://www.archlinux.org/packages/?name=jfsutils) package will be needed to perform all file system related tasks.

Actual creation of a JFS file system can be done with the either:

```
# mkfs.jfs /dev/target_dev

```

or:

```
# jfs_mkfs /dev/target_dev

```

Both commands are equivalent.

## Optimizations

There are several concepts that can be implemented with a JFS filesystem to boost its performance:

*   Periodic defragmentation of the file system.
*   Using the deadline I/O scheduler.
*   Utilizing an external journal.
*   Attaching the _noatime_ attribute the the file system in `/etc/fstab`.

### Defragmenting JFS

JFS, like all file systems, will degrade in performance over time due to file fragmentation [[6]](http://docs.hp.com/en/5576/JFS_Tuning.pdf). While there is in-place defragmentation code in the JFS utilities, this is code held over from the OS/2 port and has yet to be implemented [[7]](http://www.mail-archive.com/jfs-discussion@lists.sourceforge.net/msg00573.html). For file systems that can be taken off-line for a time, one can execute a script like the following to defragment their JFS file system

**Warning:** This script is **dangerous** and may result in the wiping of an entire hard disk, if arguments get switched! Doing this type of operation is only recommended for people who have confidence in doing backups and file system operations.

```
umount /dev/hdc1
dd bs=4k if=/dev/hdc1 of=/dev/hdj1
jfs_fsck /dev/hdj1
mount -o ro /dev/hdj1 /fs/hdj1
jfs_mkfs /dev/hdc1
mount -o rw /dev/hdc1 /fs/hdc1
(cd /fs/hdj1 && tar -cS -b8 --one -f - .) | (cd /fs/hdc1 && tar -xS -b8 -p -f -)
umount /dev/hdj1

```

In this example, `/dev/hdc1` is the device with the data that needs backing up and `/dev/hdj1` is the device that holds the backup.

Basically, this script copies the data off the JFS file system to a backup drive, formats the original JFS file system and finally writes back the data from the backup to the freshly formatted drive in a way that JFS will write its allocation trees in a defragmentated way.

**Warning:** If a VMWare session is sitting on an underlying JFS partition that is highly fragmented, performance of the virtual machine may be significantly degraded.

### Deadline I/O scheduler

JFS seems to perform better when the kernel has been configured to use the _Deadline I/O Scheduler_. Indeed, JFS's performance seems to exceed that of other GNU/Linux file systems with this particular scheduler being employed [[8]](http://www.redhat.com/archives/ext3-users/2005-July/msg00018.html). There are several ways to utilize this scheduler. One is to recompile with the Deadline I/O scheduler set to the default:

```
Block layer
    ---> I/O Schedulers
        ---> [*] Deadline I/O scheduler
        ---> Default I/O scheduler (Deadline) --->

```

If you are using a generic Arch package for your kernel, you can simply append _elevator=deadline_ to the kernel line commandline or permenantly to kernel line in your _/etc/default/grub_ and run _grub-mkconfig -o /boot/grub/grub.cfg_. The kernel entry would look something like:

```
# (0) Arch 2.6.22
title   Arch Linux
root    (hd0,0)
kernel  /vmlinuz-linux root=/dev/sda3 elevator=deadline
initrd /initramfs-linux.img

```

It is also possible to enable the Deadline I/O scheduler for specific devices by invoking the following command:

```
echo deadline > /sys/block/sda/queue/scheduler 

```

This sets the Deadline scheduler as the default for `/dev/sda` (the entire physical device).

### External journal

**Warning:** As this is a relatively new feature to the GNU/Linux port of JFS, it is recommended to upgrade to the very latest version of jfsutils before attempting to implement an external journal (earlier versions seem to give errors when trying to create the journal device).

As with any journaled file system, a journal is constantly accessed in accordance with disk activity. Having the journal log on the same device as the its corresponding file system thus can cause a degradation in I/O throughput. This degradation can be alleviated by putting the journal log on a separate device all together.

To make a journal device, first create a partition that is 128MB. Using a partition that is bigger than 128MB results in the excess being ignored, according to mkfs.jfs. You can either create an external log for an already-existing JFS file system by executing the following:

```
# mkfs.jfs -J journal_dev /dev/external_journal             # creates a journal on device /dev/external_journal
# mkfs.jfs -J device=/dev/external_journal /dev/jfs_device  # attaches the external journal to the existing file 
                                                          #   system on /dev/jfs_device

```

or a command can be issued to create both a new external journal and its corresponding JFS file system:

```
# mkfs.jfs -j /dev/external_journal /dev/jfs_device

```

This last command formats BOTH the external journal and the JFS file system.

**Note:** Obviously, an external journal is only effective if the journal and its file system exists on separate _physical_ devices.

### noatime fstab attribute

Every time a file is accessed (read or write) the default for most file systems is to append the metadata associated with that file with an updated access time. Thus, even read operations incur an overhead associated with a write to the file system. This can lead to a significant degradation in performance in some usage scenarios. Appending _noatime_ to the fstab line for a JFS file system stops this action from happening. As access time is of little importance in most scenarios, this alteration has been widely touted as a fast and easy way to get a performance boost out of one's hardware. Even Linus Torvalds seems to be a proponent of this optimization [[9]](http://kerneltrap.org/node/14148).

**Note:**

*   One may also specify a **relatime** option which updates the atime if the previous atime is older than the mtime or ctime [[10]](http://kerneltrap.org/node/14148). In terms of performance, this will not be as fast as the _noatime_ mount option, but is useful if using applications that need to know when files were last read (like _mutt_).
*   Using the _noatime/relatime_ option can improve disk performance with any file system, not just JFS.

Here is an example `/etc/fstab` entry with the **noatime** tag:

```
/dev/sdb1 /media/backup jfs rw,users,noauto,noatime 0  0

```

One may also mount a file system with the **noatime** attribute by invoking something similar to the following:

```
# mount -o noatime -t jfs /dev/jfs_dev /mnt/jfs_fs

```

**Note:** Access time is NOT the same as the _last-modified_ time. Disabling access time will still enable you to see when files were last modified by a write operation.

### Journal modes

JFS does not support various journal modes like [ext3](/index.php/Ext3 "Ext3"). Thus, passing the mount option _data=writeback_ with _mount_ or in `/etc/fstab` will have no effect on a JFS file system. JFS's current journaling mode is similar to Ext3's default journaling mode: _ordered_ [[11]](http://www.ibm.com/developerworks/linux/linux390/perf/tuning_res_journaling.html).

### Variable block sizes

While the OS/2 port of JFS supports block sizes of 512, 1024, 2048, and 4096 bytes, the Linux port of JFS is only able to use 4k blocks. Even though code exists in JFS utilities that correspond to file systems using variable size blocks, this has yet to be implemented [[12]](http://osdir.com/ml/file-systems.jfs.general/2003-02/msg00017.html). As larger block sizes tend to favor performance (smaller ones favor efficient space usage), implementing smaller block sizes for JFS in Linux has been given a low priority for implementation by JFS developers.

## fsck and recovery

In the event that the file system does not get properly unmounted before being powered down, one will usually have to run **fsck** on a JFS file system in order to be able to remount it. This procedure usually only takes a few seconds, unless the log has been damaged. If running fsck returns an unrecognized file system error, try running **fsck.jfs** on the target device. Normally, _fsck_ is all that is needed.

If the superblock on your file system gets destroyed, it may be possible to recover some parts of the file system. Currently, the only tool able to do this is a utility called **jfsrec**. JFSrec is currently available from the AUR using the [jfsrec-svn](https://aur.archlinux.org/packages/jfsrec-svn/)<sup><small>AUR</small></sup> package.

There is also an AUR package called _jfsrec_, but this is merely a placeholder for _jfsrec-svn_ as JFSrec is currently only in its seventh SVN revision. Once installed, one simply need to type:

```
# jfsrec

```

to get a help menu explaining how to use this utility.

**Warning:** As stated above, JFSrec is only in its seventh SVN revision; and it is not known how actively the project is maintained. So use JFSrec with caution.

## Cautionary notes

While JFS is very stable in its current stage of development, there are some cautionary notes on using this file system.

### JFS root mounts read only on startup

Occasionally, a JFS root partition will be unable to mount in normal read-write mode. This is usually due to the fact that the JFS root file system fails its fsck after an unclean shutdown. It is rare that JFS fails out of fsck, and it's usually due to the JFS log itself being corrupted.

All that is required in this scenario is to boot your machine with a relatively recent Arch Linux LiveCD. Booting an Arch Linux livecd will give you access to all the JFS utilities and will load a kernel that is able to recognize JFS file systems. After booting the CD simply run _fsck_ (or possibly _fsck.jfs_) on your JFS root and it should recover just fine (even though the fsck will probably take longer than normal due to the log probably being damaged). Once the _fsck_ finishes, you should be able to boot your machine like normal.

**Note:** This scenario happens less than 10% of the time in the case of an improper shutdown.

### JFS and secure deletions

**Note:** This section applies to any journaled file system, not just JFS.

The effectiveness of deleting files by overwriting their corresponding file system blocks with random data (i.e. using utilities like _shred_) can not be assured [[13]](http://lists.kde.org/?l=kfm-devel&m=105770965822522&w=2). Given the design of journaled file systems, maintenance issues, and performance liabilities; reliable shredding of files as a deletion method does not sit highly on the priority list for implementation on any journaled file system.

### Forced fsck on JFS root file system

One may force a fsck file system check on the root file system by entering:

```
touch /forcefsck

```

and rebooting. On Arch linux systems with a JFS root on a partition under control of _device-mapper_ (i.e. the root device is a _lvm_ or a LUKS encrypted one), forcing an fsck can sometimes remove the _/usr/man/man3_ directory. The reason for this issue is not clear, but the problem has been able to be replicated [[14]](https://bbs.archlinux.org/viewtopic.php?id=41261).

It is suggested to get a list of Arch Packages that use `/usr/man/man3` by issuing a command similar to

```
find /var/lib/pacman/local/ -name files | xargs fgrep /man/man3/ | cut -d: -f1 | sort -u | awk -F/ '{print $6}' > man3_pkg_list

```

before attempting a forced fsck on a JFS root partition ([[15]](https://bbs.archlinux.org/viewtopic.php?id=41261) post #1). If `/usr/man/man3` does indeed disappear, simply reinstall all the packages listed in _man3_pkg_list_.

**Note:** If this problem does indeed happen, reinstalling all the packages using _/usr/man/man3_ does appear to fix the issue ([[16]](https://bbs.archlinux.org/viewtopic.php?id=41261) post #4).

As stated above, the reason for this issue isn't clear at the moment; but it may have something to do with the fact that a forced fsck runs through higher phases of file system checks that only happen when a JFS log gets damaged in an improper dismounting of the partition.

### JFS losing files

In JFS; journal writes are indefinitely postponed until there is another trigger such as memory pressure or an unmount operation. This infinite write delay limits reliability, as a crash can result in data loss even for data that was written minutes or hours before.[[17]](https://www.usenix.org/events/usenix05/tech/general/full_papers/prabhakaran/prabhakaran.pdf)

## Benchmarks

As benchmarks measuring file system performance tend to be focused at specific types of disk usage, it is difficult to decipher good general comparisons rating how well JFS performs against other files systems. As mentioned before, it has been noted that JFS has a tendency to use less CPU resources than other GNU/Linux file systems and (with the right optimizations) is faster than other GNU/Linux file systems for certain types of file operations. It has been noted that JFS slows down when working with many files, however[[18]](http://fsbench.netnation.com/)[[19]](http://www.debian-administration.org/articles/388). In the references are some links to benchmarks; but as always, it is best to test and see what works best for your own system and work load.

## Conclusions

JFS is a stable, feature-rich file system that hasn't been publicized as much as some of the other Linux file systems. With optimizations, JFS is stable, CPU efficient and fast. In particular, VMWare sessions stand to benefit enormously from a properly optimized and defragmented, underlying JFS file system.

## See also

*   A more technical [overview](http://jfs.sourceforge.net/project/pub/jfs.pdf) of JFS
*   [30 days with JFS](http://www.linux.com/feature/119025)
*   JFS [Sourceforge](http://jfs.sourceforge.net/) page
*   Note on [defragmenting](http://www.sabi.co.uk/blog/anno06-2nd.html#060422b) JFS file systems
*   JFS Recovery [Sourceforge](http://sourceforge.net/projects/jfsrec) page
*   [Presentation](http://conferences.oreillynet.com/presentations/os2002/best_steve.pdf) on JFS given by Steve Best (pdf)
*   [Debian file system comparison](http://www.debian-administration.org/articles/388)
*   [Wikipedia:JFS (file system)](https://en.wikipedia.org/wiki/JFS_(file_system) "wikipedia:JFS (file system)")
*   Some [filesystem benchmarks](http://fsbench.netnation.com/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=JFS_Filesystem&oldid=410225](https://wiki.archlinux.org/index.php?title=JFS_Filesystem&oldid=410225)"