# Anything-sync-daemon

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Profile-sync-daemon](/index.php/Profile-sync-daemon "Profile-sync-daemon")

[Anything-sync-daemon](https://aur.archlinux.org/packages/Anything-sync-daemon/)<sup><small>AUR</small></sup> (asd) is a tiny pseudo-daemon designed to manage user specified directories referred to as sync targets from here on out, in tmpfs and to periodically sync them back to the physical disc (HDD/SSD). This is accomplished via a symlinking step and an innovative use of rsync to maintain synchronization between a tmpfs copy and media-bound backups. Additionally, asd features several crash recovery features.

## Contents

*   [1 Asd or Psd?](#Asd_or_Psd.3F)
*   [2 Benefits of Asd](#Benefits_of_Asd)
*   [3 Setup and Installation](#Setup_and_Installation)
    *   [3.1 Edit /etc/asd.conf](#Edit_.2Fetc.2Fasd.conf)
    *   [3.2 Using asd](#Using_asd)
    *   [3.3 Preview mode (parse)](#Preview_mode_.28parse.29)
    *   [3.4 Clean mode](#Clean_mode)
    *   [3.5 Running asd](#Running_asd)
    *   [3.6 Sync at more frequent intervals (optional)](#Sync_at_more_frequent_intervals_.28optional.29)
*   [4 FAQ](#FAQ)
    *   [4.1 What is overlayfs and why do I want to use it?](#What_is_overlayfs_and_why_do_I_want_to_use_it.3F)
    *   [4.2 My system crashed and did not sync back. What do I do?](#My_system_crashed_and_did_not_sync_back._What_do_I_do.3F)
    *   [4.3 Where can I find this snapshot?](#Where_can_I_find_this_snapshot.3F)
    *   [4.4 How can I restore the snapshot?](#How_can_I_restore_the_snapshot.3F)
    *   [4.5 Can asd delete the snapshots automatically?](#Can_asd_delete_the_snapshots_automatically.3F)
*   [5 Support](#Support)

## Asd or Psd?

**Warning:** If syncing browser profiles is desired, it is recommended NOT to use asd for this purpose. Instead, use [Profile-sync-daemon](/index.php/Profile-sync-daemon "Profile-sync-daemon") which has built in sanity checks for unique situations specific to running a browser profile in tmpfs. Anything-sync-daemon does not have these checks; under certain circumstances, browser profile data can be lost. You have been warned.

## Benefits of Asd

Design goals of asd:

1.  Completely transparent user experience.
2.  Reduced wear to physical discs,
3.  Speed,

Since the sync target(s) is relocated into tmpfs (RAM disk), the corresponding onslaught of I/O associated with system usage of them is also redirected from the physical disc to RAM, thus reducing wear to the physical disc and also improving speed and responsiveness. The access time of RAM is on the order of nanoseconds while the access time of physical discs is on the order of milliseconds. This is a difference of six orders of magnitude or 1,000,000 times faster.

## Setup and Installation

[Anything-sync-daemon](https://aur.archlinux.org/packages/Anything-sync-daemon/)<sup><small>AUR</small></sup> is available for download from the [AUR](/index.php/AUR "AUR").

### Edit /etc/asd.conf

User managed settings are defined in `/etc/asd.conf` which is included in the package.

*   At a minimum, define the sync target(s) to be managed by asd in the WHATTOSYNC array. Syntax below.
*   Optionally uncomment and define the location of your distro's tmpfs in the VOLATILE variable.
*   Optionally enable the use of overlayfs to improve sync speed even further and use a smaller memory footprint. Note that this option requires your kernel be configured to use either the 'overlay' (Arch default) or 'overlayfs' (Ubuntu <15.05) kernel module. See the FAQ below for additional details on this feature.

**Note:** The default value of "/dev/shm" should work just fine for the VOLATILE setting. Be aware that using software such as bleachbit with asd can be dangerous since bleachbit likes to remove files stored in /tmp. This is why a value of /dev/shm is recommended.

Example:

```
WHATTOSYNC=('/var/lib/monitorix' '/srv/http' '/foo/bar')

```

or

```
WHATTOSYNC=(
'/var/lib/monitorix'
'/srv/http'
'/foo/bar'
)

```

### Using asd

### Preview mode (parse)

The 'parse' option can be called to show users exactly what asd will do/is doing based on the entries in /etc/asd.conf as well as print out useful information such as dir size, paths, and if any recovery snapshots have been created.

```
$ asd p
Anything-sync-daemon v5.61 on Arch Linux.

Systemd service is currently active.
Systemd resync service is currently active.
Overlayfs v23 is currently active.

Asd will manage the following per /run/asd.conf settings:

owner/group id:     root/0
target to manage:   /srv/http/serve
sync target:        /srv/http/.serve-backup_asd
tmpfs target:       /dev/shm/asd-root/srv/http/serve
dir size:           21M
overlayfs size:     15M
recovery dirs:      2 <- delete with the c option
 dir path/size:     /srv/http/.serve-backup_asd-crashrecovery-20141105_124948 (17M)
 dir path/size:     /srv/http/.serve-backup_asd-crashrecovery-20150124_062311 (21M)

owner/group id:     facade/100
target to manage:   /home/facade/logs
sync target:        /home/facade/.logs-backup_asd
tmpfs target:       /dev/shm/asd-facadey/home/facade/logs
dir size:           1.5M
overlayfs size:     480K
recovery dirs:      none

```

### Clean mode

The clean mode will delete ALL recovery snapshots that have accumulated. Run this only if you are sure that you want to delete them.

**Note:** If a sync target is owned by root or another user, and if asd is called to clean, it will throw errors based on the permissions of the sync targets. One can call this function with sudo or as root to avoid these errors.

 `# asd c` 

```
Anything-sync-daemon v5.61 on Arch Linux.

Deleting 2 crashrecovery dir(s) for sync target /srv/http/serve
 /srv/http/.serve-backup_asd-crashrecovery-20141105_124948
 /srv/http/.serve-backup_asd-crashrecovery-20150124_062311

```

### Running asd

Do not call `/usr/bin/anything-sync-daemon` to sync or to unsync directly. Instead use the provided service files.

Both a [systemd](/index.php/Systemd "Systemd") [service](/index.php/Daemon "Daemon") file and a timer are provided and should be used to interact with _asd_. The role of the timer is update the tmpfs copy/copies back to the disk which it does once per hour. The timer starts automatically with `asd.service`.

[Start](/index.php/Start "Start") `asd.service` and [enable](/index.php/Enable "Enable") it to run at boot time/shutdown (**highly recommended**).

### Sync at more frequent intervals (optional)

The package provided timer syncs once per hour. Users may optionally redefine this behavior simply by [extending the systemd unit](/index.php/Systemd#Editing_provided_units "Systemd"). The example below changes the timer to sync once every ten minutes:

 `/etc/systemd/system/asd-resync.timer.d/frequency.conf` 

```
[Unit]
Description=Timer for Arofile-sync-daemon - 10min

[Timer]
# Empty value resets the list of timers
OnUnitActiveSec=
OnUnitActiveSec=10min

```

See `man systemd.timer` for additional options.

## FAQ

### What is overlayfs and why do I want to use it?

Overlayfs is a simple union file-system mainlined in the Linux kernel version 3.18.0\. Starting with asd version 5.54, overlayfs can be used to reduce the memory footprint of asd's tmpfs space and to speed up sync and unsync operations. The magic is in how the overlay mount only writes out data that has changed rather than the entire profile. The same recovery features asd uses in its default mode are also active when running in overlayfs mode. Overlayfs mode is enabled by uncommenting the USE_OVERLAYFS="yes" line in `/etc/asd.conf` followed by a restart of the daemon.

There are several versions of overlayfs available to the Linux kernel in production in various distros. Versions 22 and lower have a module called 'overlayfs' while newer versions (23 and higher) have a module called 'overlay' -- note the lack of the 'fs' in the newer version. Asd will automatically detect the overlayfs available to your kernel if it is configured to use one of them.

### My system crashed and did not sync back. What do I do?

Odds are the "last good" backup of your sync target(s) is just fine still sitting happily on your filesystem. Upon restarting asd (on a reboot for example), a check is preformed to see if the symlink to the tmpfs copy of your sync target is valid. If it is invalid, asd will snapshot the "last good" backup before it rotates it back into place. This is more for a sanity check that asd did no harm and that any data loss was a function of something else.

### Where can I find this snapshot?

You will find the snapshot in the same directory as the sync target and it will contain a date-time-stamp that corresponds to the time at which the recovery took place. For example, a /foo/bar snapshot will be /foo/.bar-backup_asd-crashrecovery-20141221_070112 -- of course, the date_time suffix will be different for you.

### How can I restore the snapshot?

*   Stop `asd`.
*   Confirm that there is no symlink to the sync target. If there is, _asd_ did not stop correctly for other reasons.
*   Move the "bad" copy of the sync target to a backup (do not blindly delete anything).
*   Copy the snapshot directory to the expected sync target.

Example using /foo/bar

```
mv /foo/bar /for/bar-bad
cp -a /foo/.bar-backup_asd-crashrecovery-20141221_070112 /foo/bar

```

### Can asd delete the snapshots automatically?

Yes, run asd with the "clean" switch to delete snapshots.

## Support

Post in the [discussion thread](https://bbs.archlinux.org/viewtopic.php?id=139141) with comments or concerns.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Anything-sync-daemon&oldid=411975](https://wiki.archlinux.org/index.php?title=Anything-sync-daemon&oldid=411975)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [System administration](/index.php/Category:System_administration "Category:System administration")