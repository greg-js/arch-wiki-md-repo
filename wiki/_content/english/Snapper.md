[Snapper](http://snapper.io) is a tool created by openSUSE's Arvin Schnell that helps with managing snapshots of [Btrfs](/index.php/Btrfs "Btrfs") subvolumes and [LVM](/index.php/LVM "LVM") volumes. It can create and compare snapshots, revert between snapshots, and supports automatic snapshots timelines.

## Contents

*   [1 Installation](#Installation)
*   [2 Create a new configuration](#Create_a_new_configuration)
*   [3 Automatic timeline snapshots](#Automatic_timeline_snapshots)
    *   [3.1 Enable/disable](#Enable.2Fdisable)
    *   [3.2 Set snapshot limits](#Set_snapshot_limits)
    *   [3.3 Change snapshot and cleanup frequencies](#Change_snapshot_and_cleanup_frequencies)
*   [4 Take a snapshot manually](#Take_a_snapshot_manually)
*   [5 List snapshots](#List_snapshots)
*   [6 Access for non-root users](#Access_for_non-root_users)
*   [7 Tips and tricks](#Tips_and_tricks)
    *   [7.1 Pacman](#Pacman)
        *   [7.1.1 Using a hook to automatically create a snapshot on pacman transaction](#Using_a_hook_to_automatically_create_a_snapshot_on_pacman_transaction)
        *   [7.1.2 Using a script and alias to create pre/post snapshots on a pacman transaction](#Using_a_script_and_alias_to_create_pre.2Fpost_snapshots_on_a_pacman_transaction)
        *   [7.1.3 Using pacupg to wrap pacman transactions in snapshots](#Using_pacupg_to_wrap_pacman_transactions_in_snapshots)
    *   [7.2 Suggested filesystem layout](#Suggested_filesystem_layout)
        *   [7.2.1 Configuration of snapper and mount point](#Configuration_of_snapper_and_mount_point)
        *   [7.2.2 Restoring / to a previous snapshot of subvol_root](#Restoring_.2F_to_a_previous_snapshot_of_subvol_root)
    *   [7.3 Deleting files from snapshots](#Deleting_files_from_snapshots)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 Snapper logs](#Snapper_logs)
    *   [8.2 IO error](#IO_error)
*   [9 Caveats](#Caveats)
    *   [9.1 Snapshots of root filesystem](#Snapshots_of_root_filesystem)
    *   [9.2 updatedb](#updatedb)

## Installation

[Install](/index.php/Install "Install") the [snapper](https://www.archlinux.org/packages/?name=snapper) package. The development version [snapper-git](https://aur.archlinux.org/packages/snapper-git/) is also available.

Additionally, a GUI is available with [snapper-gui-git](https://aur.archlinux.org/packages/snapper-gui-git/).

## Create a new configuration

To create a new configuration use the `snapper create-config` command.

**Note:** To create a configuration, you must first create a subvolume. `btrfs subvolume create /my/directory`. This directory must not exist. You do not have to do this for `/`, as `/` is already a subvolume when you setup btrfs. [Btrfs#Creating sub-volumes](/index.php/Btrfs#Creating_sub-volumes "Btrfs") for more information

Example for a subvolume mounted as `/`

```
# snapper -c root create-config /

```

This will

*   create a config file in `/etc/snapper/configs/root` based on the default template from `/etc/snapper/config-templates`
*   create a subvolume `.snapshots` in the root of the subvolume (/.snapshots in this case)
*   add "root" to SNAPPER_CONFIGS in `/etc/conf.d/snapper`

At this point, the configuration is active. If your [cron](/index.php/Cron "Cron") daemon is running, snapper will take [#Automatic timeline snapshots](#Automatic_timeline_snapshots).

See `man snapper-configs`.

## Automatic timeline snapshots

By default, snapper is set to create a snapshot timeline with a configurable number of snapshots kept per hour/day/month/year when a new configuration is created.

The implementation works as follows:

*   By default a snapshot gets created once an hour
*   Once a day the "old and unwanted" snapshots get cleaned up by the timeline cleanup algorithm.

Snapshots are stored into `$BTRFS_ROOT/.snapshots` or, more precisely, the subvolume path is `$BTRFS_ROOT/.snapshots/$SNAPHOST_ID/snapshot`. See this [forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1458872#p1458872).

### Enable/disable

If you have [cronie](https://www.archlinux.org/packages/?name=cronie) installed, this feature should start automatically. To disable it, edit the configuration file corresponding with the subvolume you do not want to have this feature and set:

 `TIMELINE_CREATE="no"` 

If you do not have [cronie](https://www.archlinux.org/packages/?name=cronie), you can use the provided systemd units. [Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `snapper-timeline.timer` to start the automatic snapshot timeline. Additionally, [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `snapper-cleanup.timer` to periodically cleanup older snapshots.

### Set snapshot limits

The default settings will keep 10 hourly, 10 daily, 10 monthly and 10 yearly snapshots. You may want to change this in the configuration, especially on busy subvolumes like /. See [#Caveats](#Caveats).

Here is an example for a configuration with only 5 hours of snapshots, 7 daily ones, no monthly and no yearly ones:

 `/etc/snapper/configs/root` 
```
TIMELINE_MIN_AGE="1800"
TIMELINE_LIMIT_HOURLY="5"
TIMELINE_LIMIT_DAILY="7"
TIMELINE_LIMIT_WEEKLY="0"
TIMELINE_LIMIT_MONTHLY="0"
TIMELINE_LIMIT_YEARLY="0"
```

### Change snapshot and cleanup frequencies

If you are using the provided systemd timers, you can [Systemd#Editing_provided_units|edit] them to change the snapshot and cleanup frequency.

For example, when editing the `snapper-timeline.timer`, add the following to make the frequency every five minutes, instead of hourly:

```
[Timer]
OnCalendar=*:0/5

```

**Note:** The configuration parameter `TIMELINE_LIMIT_HOURLY` is tied to the above setting. In the above example it now refers to how many 5-minute snapshots are kept.

When editing `snapper-cleanup.timer`, you need to change `OnUnitActiveSec`. To make cleanups occur every hour instead of every day, add:

```
[Timer]
OnUnitActiveSec=1h

```

See [Systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers") and [Systemd#Drop-in_snippets](/index.php/Systemd#Drop-in_snippets "Systemd").

## Take a snapshot manually

To take a snapshot of a subvolume manually, do:

```
 # snapper -c *config* create --description *description*

```

where *config* is the snapper configuration file corresponding with the subvolume you wish to take the snapshot of.

## List snapshots

To list snapshots taken for a given configuration *config* do:

```
 # snapper -c *config* list

```

## Access for non-root users

Each config is created with the root user, and by default, only root can see and access it.

To be able to list the snapshots for a given config for a specific user, simply change the value of `ALLOW_USERS` in your `/etc/snapper/configs/<config_name>` file. You should now be able to run `snapper -c <config_name> list` as a normal user.

Eventually, you want to be able to browse the `.snapshots` directory with a user, but the owner of this directory must stay root. Therefore, you should change the group owner by a group containing the user you are interested in, such as `users` for example:

```
# chmod a+rx .snapshots
# chown :users .snapshots

```

## Tips and tricks

### Pacman

There are several methods for automatically creating snapshots upon a pacman transaction.

#### Using a hook to automatically create a snapshot on pacman transaction

The following adds a hook for pacman to create a snapshot for the root configuration using snapper just before an upgrade, install, or removal occurs:

 `/usr/share/libalpm/hooks/snapshot.hook` 
```
[Trigger]
Operation = Upgrade
Operation = Install
Operation = Remove
Type = Package
Target = *

[Action]
Description = Btrfs snapshot before a transaction
Depends = snapper
When = PreTransaction
Exec = /usr/bin/snapper -c root create --description "pacman transaction"
```

See the man page for `alpm-hooks` for more options.

#### Using a script and alias to create pre/post snapshots on a pacman transaction

Snapper can create snapshots "tagged" as pre or post snapshots. This is handy when it comes to system upgrades. Using `NUMBER_CLEANUP="yes"` those can get cleaned up after a configurable number of snapshots using the number cleanup algorithm - see `man snapper` and `man snapper-configs` for details.

To use this feature with pacman, you will need some wrapper script. User [erikw](https://aur.archlinux.org/account/erikw/) created one for this purpose called [snp](https://gist.github.com/erikw/5229436).

Download it and put it somewhere in your `$PATH` (e.g. `/usr/local/bin/`) and make it executable. Usage example:

```
# snp pacman -Syu

```

If you like, you can create an [alias](/index.php/Alias "Alias"), similar to [plain pacman aliases](/index.php/Pacman_tips#Shortcuts "Pacman tips"):

```
alias sysupgrade='sudo snp pacman -Syu'

```

Then you can do system upgrades with pre-post snapshots using

```
$ sysupgrade

```

#### Using pacupg to wrap pacman transactions in snapshots

[Pacupg](https://aur.archlinux.org/packages/Pacupg/) is a script specifically designed to wrap a system upgrade in snapshots. In contrast with the above solution, it downloads the packages first (`pacman -Syuw`) and then only wraps the upgrade (`pacman -Su`) in snapshots so as to keep the differences between the pre and post snapshots to a minimum. It also detects if the user's `/boot` directory is on a separate partition and automatically makes a copy of it when it detects an upgrade to the Linux kernel. Additionally, it will avoid taking snapshots if there is nothing to upgrade and log all upgraded packages (with changed version numbers) to `/var/local/log/pacupg`. If [pacaur](https://aur.archlinux.org/packages/pacaur/) is installed, the script can also upgrade AUR packages. It builds them first, then takes a snapshot when they are ready to be installed thus keeping the pre-post snapshot differences minimal. As with regular packages, it logs all upgraded packages and will avoid taking snapshots if no packages are available to upgrade. The script now integrates with [grub-btrfs-git](https://aur.archlinux.org/packages/grub-btrfs-git/). If it is installed, `pacupg` will automatically regenerate your grub.cfg after every upgrade to include your snapshots as boot options.

As of version 0.0.9 snapper can run commands wrapped in pre-post-snapshots:

```
 snapper create --command "pacman -Su" --description "pacman system update"

```

See also the "How do I add pre and post hooks (like YaST)?" section in the official FAQ: [http://snapper.io/faq.html](http://snapper.io/faq.html)

The [pacupg](https://aur.archlinux.org/packages/pacupg/) script also allows for the easy rollback of snapshots. Running `pacupg -r` will bring up a menu that allows the user to rollback both pre-post snapshots (upgrades) or single snapshots (timeline snapshots).

### Suggested filesystem layout

Here is a suggested file system layout for easily restoring your `/` to a previous snapshot:

```
subvolid=5
   |
   ├── subvol_root
   |       |
   |       ├── /usr
   |       |
   |       ├── /bin
   |       |
   |       ├── /.snapshots
   |       |
   |       ├── ...
   |
   ├── subvol_snapshots
   |
   └── subvol_...

```

Where `/.snapshots` is a mountpoint for `subvol_snapshots`. `subvol_...` are subvolumes that you want to keep separate from the subvolume you'll be mounting as `/` (`subvol_root`). When taking a snapshot of `/`, these other subvolumes are not included. However, you can still snapshot these other subvolumes separately by creating other snapper configurations for them. Additionally, if you were to restore your system to a previous snapshots of `/`, these other subvolumes will remain unaffected.

For example if you want to be able restore `/` to a previous snapshot but keep your `/home` intact, you should create a subvolume that will be mounted at `/home`. See [Btrfs#Mounting subvolumes](/index.php/Btrfs#Mounting_subvolumes "Btrfs").

This layout allows the snapper utility to take regular snapshots of `/`, while at the same time making it easy to restore `/` from an Arch Live CD if it becomes unbootable.

In this sceneario, after the initial setup, snapper needs no changes, and will work as expected.

**Note:** Even if a subvolume is nested below `subvol_root`, a snapshot of `/` will *not* include it. Be sure to set up snapper for any additional subvolumes you want to keep snapshots of besides the one mounted at `/`.

#### Configuration of snapper and mount point

Make sure `/.snapshots` does *not* exist. Then [#Create a new configuration](#Create_a_new_configuration) for `/`.

Now that snapper is happy, delete the `/.snapshots` subvolume:

```
 # btrfs subvolume delete /.snapshots

```

Create the `/.snapshots` folder to use as a mount point. Give the folder `750` [permissions](/index.php/Permissions#Numeric_method "Permissions").

Now [mount](/index.php/Mount "Mount") `subvol_snapshots` to `/.snapshots`. For example, for a file system located on `/dev/sda1`:

```
 # mount -o subvol=subvol_snapshots /dev/sda1 /.snapshots

```

To make this mount permanent, add an entry to your [fstab](/index.php/Fstab "Fstab").

This will make all snapshots that snapper creates be stored outside of the `subvol_root` subvolume, so that `subvol_root` can easily be replaced anytime without losing the snapper snapshots.

#### Restoring `/` to a previous snapshot of `subvol_root`

If you ever want to restore `/` using one of snapper's snapshots, first boot into a live Arch Linux USB/CD.

[Mount](/index.php/Mount "Mount") the toplevel subvolume (subvolid=5). That is, omit any `subvolid` mount flags.

Find the snapshot you want to recover in `/mnt/subvol_snapshots/*/info.xml`.

**Tip:** You can use `vi` to easily browse through each file:
```
 # vi /mnt/subvol_snapshots/*/info.xml

```
Use `:n` to see the next file and `:rew` to go back to the first file.

Browse through the `<description>` tags and the `<date>` tags, and when you find the snapshot you wish to restore, remember the `<num>` number.

Now, move `subvol_root` to another location (*e.g.* `/subvol_root.broken`) to save a copy of the current system. Alternatively, simply delete `subvol_root` using `btrfs subvolume delete`.

Create a read-write snapshot of the read-only snapshot snapper took:

```
 # btrfs subvol snapshot /mnt/subvol_snapshots/*#*/snapshot /mnt/subvol_root

```

Where *#* is the number of the snapper snapshot you wish to restore. Your `/` has now been restore to the previous snapshot. Now just simply reboot.

For a more detailed description of the problem this layout solves, see: [https://bbs.archlinux.org/viewtopic.php?id=194491](https://bbs.archlinux.org/viewtopic.php?id=194491)

### Deleting files from snapshots

If you want to delete a specific file or folder from past snapshots without deleting the snapshots themselves, [snapperS](https://pypi.python.org/pypi/snapperS) is a script that adds this functionality to Snapper. This script can also be used to manipulate past snapshots in a number of other ways that Snapper does not currently support.

## Troubleshooting

### Snapper logs

Snapper writes all activity to `/var/log/snapper.log` - check this file first if you think something goes wrong.

If you have issues with hourly/daily/weekly snapshots, the most common cause for this so far has been that the cronie service (or whatever cron daemon you are using) was not running.

### IO error

If you get an 'IO Error' when trying to create a snapshot please make sure that the [.snapshots](https://bbs.archlinux.org/viewtopic.php?id=164404) directory associated to the subvolume you are trying to snapshot is a subvolume by itself.

Another possible cause is that .snapshots directory doesn't have root as an owner (You will find `Btrfs.cc(openInfosDir):219 - .snapshots must have owner root` in the `/var/log/snapper.log`).

## Caveats

### Snapshots of root filesystem

Keeping many of snapshots for a large timeframe on a busy filesystem (like `/`, where many system updates happen over time) can cause serious slowdowns. You can prevent it by:

*   Create subvolumes for things that are not worth to be snapshotted, like `/var/cache/pacman/pkg` and `/var/abs`.
*   Edit the default settings for hourly/daily/monthly/yearly snapshots when using [#Automatic timeline snapshots](#Automatic_timeline_snapshots).

### updatedb

By default, `updatedb` will also index the `.snapshots` directory created by snapper, which can cause serious slowdown and excessive memory usage if you have many snapshots. You can prevent `updatedb` from indexing over it by editing:

 `/etc/updatedb.conf`  `PRUNENAMES = ".snapshots"`