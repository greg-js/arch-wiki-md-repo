Related articles

*   [Btrfs](/index.php/Btrfs "Btrfs")
*   [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")

[Snapper](http://snapper.io) is a tool created by openSUSE's Arvin Schnell that helps with managing snapshots of [Btrfs](/index.php/Btrfs "Btrfs") subvolumes and thin-provisioned [LVM](/index.php/LVM "LVM") volumes. It can create and compare snapshots, revert between snapshots, and supports automatic snapshots timelines.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Create a new configuration](#Create_a_new_configuration)
*   [3 Take snapshots](#Take_snapshots)
    *   [3.1 Automatic timeline snapshots](#Automatic_timeline_snapshots)
        *   [3.1.1 Enable/disable](#Enable/disable)
        *   [3.1.2 Set snapshot limits](#Set_snapshot_limits)
        *   [3.1.3 Change snapshot and cleanup frequencies](#Change_snapshot_and_cleanup_frequencies)
    *   [3.2 Manual snapshots](#Manual_snapshots)
        *   [3.2.1 Simple snapshots](#Simple_snapshots)
        *   [3.2.2 Pre/post snapshots](#Pre/post_snapshots)
    *   [3.3 Snapshots on boot](#Snapshots_on_boot)
*   [4 List snapshots](#List_snapshots)
*   [5 List configurations](#List_configurations)
*   [6 Delete a snapshot](#Delete_a_snapshot)
*   [7 Access for non-root users](#Access_for_non-root_users)
*   [8 Tips and tricks](#Tips_and_tricks)
    *   [8.1 Wrapping pacman transactions in snapshots](#Wrapping_pacman_transactions_in_snapshots)
        *   [8.1.1 Backup non-btrfs boot partition on pacman transactions](#Backup_non-btrfs_boot_partition_on_pacman_transactions)
    *   [8.2 Incremental backup to external drive](#Incremental_backup_to_external_drive)
    *   [8.3 Suggested filesystem layout](#Suggested_filesystem_layout)
        *   [8.3.1 Configuration of snapper and mount point](#Configuration_of_snapper_and_mount_point)
        *   [8.3.2 Restoring / to a previous snapshot of @](#Restoring_/_to_a_previous_snapshot_of_@)
    *   [8.4 Deleting files from snapshots](#Deleting_files_from_snapshots)
    *   [8.5 Preventing slowdowns](#Preventing_slowdowns)
        *   [8.5.1 updatedb](#updatedb)
    *   [8.6 Preserving log files](#Preserving_log_files)
    *   [8.7 Cleanup based on disk usage](#Cleanup_based_on_disk_usage)
*   [9 Troubleshooting](#Troubleshooting)
    *   [9.1 Snapper logs](#Snapper_logs)
    *   [9.2 IO error](#IO_error)
*   [10 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [snapper](https://www.archlinux.org/packages/?name=snapper) package. The development version [snapper-git](https://aur.archlinux.org/packages/snapper-git/) is also available.

Additionally, a GUI is available with [snapper-gui-git](https://aur.archlinux.org/packages/snapper-gui-git/).

## Create a new configuration

Before creating a snapper configuration for a btrfs subvolume, the subvolume must already exist. If it does not, you should [create](/index.php/Btrfs#Creating_a_subvolume "Btrfs") it before generating a snapper configuration.

To create a new snapper configuration named `*config*` for the btrfs subvolume at `*/path/to/subvolume*` do:

```
# snapper -c *config* create-config */path/to/subvolume*

```

This will:

*   create a configuration file at `/etc/snapper/configs/*config*` based on the default template from `/etc/snapper/config-templates`.
*   create a subvolume at `*/path/to/subvolume*/.snapshots` where future snapshots of for this configuration will be stored. A snapshot's path is `*/path/to/subvolume*/.snapshots/*#*/snapshot`, where `*#*` is the snapshot number.
*   add `*config*` to `SNAPPER_CONFIGS` in `/etc/conf.d/snapper`.

For example, to create a configuration file for the subvolume mounted at `/` do:

```
# snapper -c root create-config /

```

At this point, the configuration is active. If your [cron](/index.php/Cron "Cron") daemon is running, snapper will take [#Automatic timeline snapshots](#Automatic_timeline_snapshots). If you do not use a [cron](/index.php/Cron "Cron") daemon, you will need to use the systemd service and timer. See [#Enable/disable](#Enable/disable).

See [man page](/index.php/Man_page "Man page") for `snapper-configs`.

## Take snapshots

### Automatic timeline snapshots

A snapshot timeline can be created with a configurable number of snapshots kept per hour/day/month/year. When the timeline is enabled, by default a snapshot gets created once an hour. Once a day the snapshots get cleaned up by the timeline cleanup algorithm.

#### Enable/disable

If you have a [cron](/index.php/Cron "Cron") daemon, this feature should start automatically. To disable it, edit the configuration file corresponding with the subvolume you do not want to have this feature and set:

 `TIMELINE_CREATE="no"` 

If you do not have a [cron](/index.php/Cron "Cron") daemon, you can use the provided systemd units. [Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `snapper-timeline.timer` to start the automatic snapshot timeline. Additionally, [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `snapper-cleanup.timer` to periodically cleanup older snapshots.

**Note:** If you have a cron daemon and also enable the systemd units, this may result in duplicate snapshots being created. If you wish to disable cron integration while using the systemd units, one possible solution is not to install the snapper package's cron files via [pacman](/index.php/Pacman "Pacman")'s [NoExtract](/index.php/Pacman#Skip_files_from_being_installed_to_system "Pacman") and [NoUpgrade](/index.php/Pacman#Skip_file_from_being_upgraded "Pacman") configuration options. See [[1]](https://unix.stackexchange.com/questions/425570/snapper-has-recently-started-performing-duplicate-snapshots-each-hour)

#### Set snapshot limits

The default settings will keep 10 hourly, 10 daily, 10 monthly and 10 yearly snapshots. You may want to change this in the configuration, especially on busy subvolumes like `/`. See [#Preventing slowdowns](#Preventing_slowdowns).

Here is an example section of a configuration named `*config*` with only 5 hourly snapshots, 7 daily ones, no monthly and no yearly ones:

 `/etc/snapper/configs/*config*` 
```
TIMELINE_MIN_AGE="1800"
TIMELINE_LIMIT_HOURLY="5"
TIMELINE_LIMIT_DAILY="7"
TIMELINE_LIMIT_WEEKLY="0"
TIMELINE_LIMIT_MONTHLY="0"
TIMELINE_LIMIT_YEARLY="0"
```

#### Change snapshot and cleanup frequencies

If you are using the provided systemd timers, you can [edit](/index.php/Edit "Edit") them to change the snapshot and cleanup frequency.

For example, when editing the `snapper-timeline.timer`, add the following to make the frequency every five minutes, instead of hourly:

```
[Timer]
OnCalendar=
OnCalendar=*:0/5

```

**Note:** The configuration parameter `TIMELINE_LIMIT_HOURLY` is tied to the above setting. In the above example it now refers to how many 5-minute snapshots are kept.

When editing `snapper-cleanup.timer`, you need to change `OnUnitActiveSec`. To make cleanups occur every hour instead of every day, add:

```
[Timer]
OnUnitActiveSec=1h

```

See [Systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers") and [Systemd#Drop-in files](/index.php/Systemd#Drop-in_files "Systemd").

### Manual snapshots

#### Simple snapshots

By default snapper takes snapshots that are of the *simple* type, having no special relationship to other snapshots.

To take a snapshot of a subvolume manually, do:

```
 # snapper -c *config* create --description *desc*

```

The above command does not use any cleanup algorithm, so the snapshot is stored permanently or until [deleted](#Delete_a_snapshot).

To set a cleanup algorithm, use the `-c` flag after `create` and choose either `number`, `timeline`, `pre`, or `post`. `number` sets snapper to periodically remove snapshots that have exceeded a set number in the configuration file. For example, to create a snaphot that uses the `number` algorithm for cleanup do:

```
 # snapper -c *config* create -c number

```

See [#Automatic timeline snapshots](#Automatic_timeline_snapshots) for how `timeline` snapshots work and see [#Pre/post snapshots](#Pre/post_snapshots) on how `pre` and `post` work.

#### Pre/post snapshots

In addition to *simple* snapshots, you can also create *pre/post* snapshots where *pre* snapshots always have a corresponding *post* snapshot. The purpose of these pairs is to create a snapshot before and after a system modification.

To create a pre/post snapshot pair, first create a *pre* snapshot:

```
 # snapper -c *config* create -t pre -p

```

Note the number of the snapshot printed, as it is required for the post snapshot.

Then perform a system modification (*e.g.*, install a new program, upgrade, etc.).

Now create the *post* snapshot:

```
 # snapper -c *config* create -t post --pre-number *N*

```

where `*N*` is the corresponding *pre* snapshot number.

An alternative method is to use the `--command` flag for `create`, which wraps a command with pre/post snapshots:

```
 # snapper -c *config* create --command *cmd*

```

where `*cmd*` is the command you wish to wrap with pre/post snapshots.

See [#Wrapping pacman transactions in snapshots](#Wrapping_pacman_transactions_in_snapshots).

### Snapshots on boot

To have snapper take a snapshot of the `root` configuration, [enable](/index.php/Enable "Enable") `snapper-boot.timer`.

## List snapshots

To list snapshots taken for a given configuration *config* do:

```
 # snapper -c *config* list

```

## List configurations

To list all [configurations](#Create_a_new_configuration) you have created do:

```
 # snapper list-configs

```

## Delete a snapshot

To delete a snapshot number `*N*` do:

```
 # snapper -c *config* delete *N*

```

Multiple snapshots can be deleted at one time. For example, to delete snapshots 65 and 70 of the root configuration do:

```
 # snapper -c root delete 65 70

```

**Note:** When deleting a pre snapshot, you should always delete its corresponding post snapshot and vice versa.

## Access for non-root users

Each config is created with the root user, and by default, only root can see and access it.

To be able to list the snapshots for a given config for a specific user, simply change the value of `ALLOW_USERS` in your `/etc/snapper/configs/*config*` file. You should now be able to run `snapper -c *config* list` as a normal user.

Eventually, you want to be able to browse the `.snapshots` directory with a user, but the owner of this directory must stay root. Therefore, you should change the group owner by a group containing the user you are interested in, such as `users` for example:

```
# chmod a+rx .snapshots
# chown :users .snapshots

```

## Tips and tricks

### Wrapping pacman transactions in snapshots

There are a couple of packages used for automatically creating snapshots upon a pacman transaction:

*   **pacupg** — "Script that wraps package and AUR upgrades in btrfs snapshots and provides an easy way to roll them back."

	[https://github.com/crossroads1112/bin/tree/master/pacupg](https://github.com/crossroads1112/bin/tree/master/pacupg) || [pacupg](https://aur.archlinux.org/packages/pacupg/)

*   **snap-pac** — "Makes pacman automatically use snapper to create [#Pre/post snapshots](#Pre/post_snapshots) like openSUSE's YaST". Uses [Pacman#Hooks](/index.php/Pacman#Hooks "Pacman").

	[https://github.com/wesbarnett/snap-pac](https://github.com/wesbarnett/snap-pac) || [snap-pac](https://www.archlinux.org/packages/?name=snap-pac)

*   **snap-pac-grub** — "Additionally updates GRUB entries for [grub-btrfs](https://www.archlinux.org/packages/?name=grub-btrfs) after [snap-pac](https://www.archlinux.org/packages/?name=snap-pac) made the snapshots. Also uses [Pacman#Hooks](/index.php/Pacman#Hooks "Pacman").

	[snap-pac-grub](https://aur.archlinux.org/packages/snap-pac-grub/) || [snap-pac-grub](https://aur.archlinux.org/packages/snap-pac-grub/)

*   **snp** — wrap any shell command in a snapper pre-post snapshot, e.g. `$ snp pacman -Syu`

	[https://gist.github.com/erikw/5229436](https://gist.github.com/erikw/5229436) ||

#### Backup non-btrfs boot partition on pacman transactions

If your `/boot` partition is on a non btrfs filesystem (e.g. an [ESP](/index.php/ESP "ESP")) you are not able to do snapper backups with it. You can copy the boot partition automatically on a kernel update to your btrfs root with a hook. This also plays nice together with [snap-pac](https://www.archlinux.org/packages/?name=snap-pac).

 `/usr/share/libalpm/hooks/50_bootbackup.hook` 
```
[Trigger]
Operation = Upgrade
Operation = Install
Operation = Remove
Type = Package
Target = linux*

[Action]
Depends = rsync
Description = Backing up /boot...
When = PreTransaction
Exec = /usr/bin/rsync -a --delete /boot /.bootbackup
```

### Incremental backup to external drive

The following packages use `btrfs send` and `btrfs receive` to send backups incrementally to an external drive. Refer to their documenation to see differences in implementation, features, and requirements.

*   **buttersink** — "Buttersink is like rsync for btrfs snapshots."

	[https://github.com/AmesCornish/buttersink.git](https://github.com/AmesCornish/buttersink.git) || [buttersink-git](https://aur.archlinux.org/packages/buttersink-git/)

*   **snap-sync** — "Use snapper snapshots to backup to external drive."

	[https://github.com/wesbarnett/snap-sync.git](https://github.com/wesbarnett/snap-sync.git) || [snap-sync](https://www.archlinux.org/packages/?name=snap-sync)

*   **snapsync** — "A synchronization tool for snapper"

	[https://github.com/doudou/snapsync](https://github.com/doudou/snapsync) || [ruby-snapsync](https://aur.archlinux.org/packages/ruby-snapsync/)

### Suggested filesystem layout

**Note:** The following layout is intended *not* to be used with `snapper rollback`, but is intended to mitigate inherit problems with restoring `/` with that command. See [this forum thread](https://bbs.archlinux.org/viewtopic.php?id=194491).

Here is a suggested file system layout for easily restoring your `/` to a previous snapshot:

```
subvolid=5
   |
   ├── @
   |       |
   |       ├── /usr
   |       |
   |       ├── /bin
   |       |
   |       ├── /.snapshots
   |       |
   |       ├── ...
   |
   ├── @snapshots
   |
   └── @...

```

Where `/.snapshots` is a mountpoint for `@snapshots`. `@...` are subvolumes that you want to keep separate from the subvolume you will be mounting as `/` (`@`). When taking a snapshot of `/`, these other subvolumes are not included. However, you can still snapshot these other subvolumes separately by creating other snapper configurations for them. Additionally, if you were to restore your system to a previous snapshots of `/`, these other subvolumes will remain unaffected.

For example if you want to be able restore `/` to a previous snapshot but keep your `/home` intact, you should create a subvolume that will be mounted at `/home`. See [Btrfs#Mounting subvolumes](/index.php/Btrfs#Mounting_subvolumes "Btrfs").

This layout allows the snapper utility to take regular snapshots of `/`, while at the same time making it easy to restore `/` from an Arch Live CD if it becomes unbootable.

In this sceneario, after the initial setup, snapper needs no changes, and will work as expected.

**Note:** Even if a subvolume is nested below `@`, a snapshot of `/` will *not* include it. Be sure to set up snapper for any additional subvolumes you want to keep snapshots of besides the one mounted at `/`.

#### Configuration of snapper and mount point

Make sure `/.snapshots` is *not* mounted and does *not* exist as folder.

```
 # umount /.snapshots
 # rm -r /.snapshots

```

Then [#Create a new configuration](#Create_a_new_configuration) for `/`.

Now [mount](/index.php/Mount "Mount") `@snapshots` to `/.snapshots`. For example, for a file system located on `/dev/sda1`:

```
 # mount -o subvol=@snapshots /dev/sda1 /.snapshots

```

To make this mount permanent, add an entry to your [fstab](/index.php/Fstab "Fstab").

Or if you have an existing fstab entry remount the snapshot subvolume:

```
 # mount -a

```

Give the folder `750` [permissions](/index.php/Permissions#Numeric_method "Permissions").

This will make all snapshots that snapper creates be stored outside of the `@` subvolume, so that `@` can easily be replaced anytime without losing the snapper snapshots.

#### Restoring `/` to a previous snapshot of `@`

If you ever want to restore `/` using one of snapper's snapshots, first boot into a live Arch Linux USB/CD.

[Mount](/index.php/Mount "Mount") the toplevel subvolume (subvolid=5). That is, omit any `subvolid` mount flags.

Find the snapshot you want to recover in `/mnt/@snapshots/*/info.xml`.

**Tip:** You can use `vi` to easily browse through each file:
```
 # vi /mnt/@snapshots/*/info.xml

```
Use `:n` to see the next file and `:rew` to go back to the first file.

Browse through the `<description>` tags and the `<date>` tags, and when you find the snapshot you wish to restore, remember the `<num>` number.

Now, move `@` to another location (*e.g.* `/@.broken`) to save a copy of the current system. Alternatively, simply delete `@` using `btrfs subvolume delete`.

Create a read-write snapshot of the read-only snapshot snapper took:

```
 # btrfs subvol snapshot /mnt/@snapshots/*#*/snapshot /mnt/@

```

Where `*#*` is the number of the snapper snapshot you wish to restore. Your `/` has now been restore to the previous snapshot. Now just simply reboot.

### Deleting files from snapshots

If you want to delete a specific file or folder from past snapshots without deleting the snapshots themselves, [snapperS](https://pypi.python.org/pypi/snapperS) is a script that adds this functionality to Snapper. This script can also be used to manipulate past snapshots in a number of other ways that Snapper does not currently support.

If you want to remove a file without using an extra script, you just need to [make your snapshot subvolume read-write](http://unix.stackexchange.com/a/149933/3587), which you can do with:

```
# btrfs property set /path/to/.snapshots/<snapshot_num>/snapshot ro false

```

verify that <tt>ro=false</tt>:

```
# btrfs property get /path/to/.snapshots/<snapshot_num>/snapshot
ro=false

```

You can now modify files in <tt>/path/to/.snapshots/<snapshot_num>/snapshot</tt> like normal. You can use a shell loop to work on your snapshots in bulk.

### Preventing slowdowns

Keeping many of snapshots for a large timeframe on a busy filesystem like `/`, where many system updates happen over time, can cause serious slowdowns. You can prevent it by:

*   [Creating](/index.php/Btrfs#Creating_a_subvolume "Btrfs") subvolumes for things that are not worth being snapshotted, like `/var/cache/pacman/pkg`, `/var/abs`, `/var/tmp`, and `/srv`.
*   Editing the default settings for hourly/daily/monthly/yearly snapshots when using [#Automatic timeline snapshots](#Automatic_timeline_snapshots).

#### updatedb

By default, `updatedb` will also index the `.snapshots` directory created by snapper, which can cause serious slowdown and excessive memory usage if you have many snapshots. You can prevent `updatedb` from indexing over it by editing:

 `/etc/updatedb.conf`  `PRUNENAMES = ".snapshots"` 

### Preserving log files

It's recommended to create a subvolume for `/var/log` so that snapshots of `/` exclude it. That way if a snapshot of `/` is restored your log files will not also be reverted to the previous state. This make it easier to troubleshoot.

### Cleanup based on disk usage

## Troubleshooting

### Snapper logs

Snapper writes all activity to `/var/log/snapper.log` - check this file first if you think something goes wrong.

If you have issues with hourly/daily/weekly snapshots, the most common cause for this so far has been that the cronie service (or whatever cron daemon you are using) was not running.

### IO error

If you get an 'IO Error' when trying to create a snapshot please make sure that the [.snapshots](https://bbs.archlinux.org/viewtopic.php?id=164404) directory associated to the subvolume you are trying to snapshot is a subvolume by itself.

Another possible cause is that .snapshots directory does not have root as an owner (You will find `Btrfs.cc(openInfosDir):219 - .snapshots must have owner root` in the `/var/log/snapper.log`).

## See also

*   [Snapper homepage](http://snapper.io/)
*   [openSUSE Snapper portal](https://en.opensuse.org/Portal:Snapper)
*   [Btrfs homepage](https://btrfs.wiki.kernel.org/index.php/Main_Page)
*   [Linux.com: Snapper: SUSE's Ultimate Btrfs Snapshot Manager](https://www.linux.com/news/enterprise/systems-management/878490-snapper-suses-ultimate-btrfs-snapshot-manager/)