# Snapper

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Btrfs](/index.php/Btrfs "Btrfs")
*   [mkinitcpio-btrfs](/index.php/Mkinitcpio-btrfs "Mkinitcpio-btrfs")
*   [Btrfs - Tips and tricks](/index.php/Btrfs_-_Tips_and_tricks "Btrfs - Tips and tricks")

[Snapper](http://snapper.io) is a tool created by openSUSE's Arvin Schnell that helps with managing snapshots of [Btrfs](/index.php/Btrfs "Btrfs") subvolumes and [LVM](/index.php/LVM "LVM") volumes. It can create and compare snapshots, revert between snapshots, and supports automatic snapshots timelines.

**Warning:**

In kernels 3.17 and 3.17-1, snapper in combination with [Btrfs](/index.php/Btrfs "Btrfs") using read-only snapshots will cause [random corruption](http://www.mail-archive.com/linux-btrfs@vger.kernel.org/msg38049.html) and affected snapshots cannot be deleted without recreating the filesystem. This bug is fixed as of 3.17-2.

## Contents

*   [1 Installation](#Installation)
*   [2 Create a new configuration](#Create_a_new_configuration)
*   [3 Automatic timeline snapshots](#Automatic_timeline_snapshots)
*   [4 Access for non-root users](#Access_for_non-root_users)
*   [5 Periodic launch without cron](#Periodic_launch_without_cron)
*   [6 Tips and Tricks](#Tips_and_Tricks)
    *   [6.1 Pre-post snapshots with pacman](#Pre-post_snapshots_with_pacman)
    *   [6.2 Wrapping upgrades in pre-post snapshots](#Wrapping_upgrades_in_pre-post_snapshots)
        *   [6.2.1 Easing the rollback process](#Easing_the_rollback_process)
    *   [6.3 Suggested Filesystem Layout](#Suggested_Filesystem_Layout)
        *   [6.3.1 Configuring Snapper](#Configuring_Snapper)
        *   [6.3.2 Restoring the entire system](#Restoring_the_entire_system)
    *   [6.4 Deleting files from snapshots](#Deleting_files_from_snapshots)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Snapper logs](#Snapper_logs)
    *   [7.2 IO Error](#IO_Error)
*   [8 Caveats](#Caveats)
    *   [8.1 Snapshots of root filesystem](#Snapshots_of_root_filesystem)
    *   [8.2 updatedb](#updatedb)

## Installation

The stable version [snapper](https://www.archlinux.org/packages/?name=snapper) can be installed from the [official repositories](https://wiki.archlinux.org/index.php/Official_repositories).

The development version [snapper-git](https://aur.archlinux.org/packages/snapper-git/)<sup><small>AUR</small></sup> is also available.

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

At this point, the configuration is active. If your cron daemon is running, snapper will start taking snapshots every hour. It is advised to review the configuration file and set the desired amount of snapshots to be kept.

**Note:** For informations on all settings in the config file see `man snapper-configs`.

## Automatic timeline snapshots

Snapper can create a snapshot timeline with a configurable number of snapshots kept per hour/day/month/year.

The implementation works as follows:

*   By default a snapshot gets created once an hour (cron.hourly)
*   Once a day the "old and unwanted" snapshots get cleaned up by the timeline cleanup algorithm (cron.daily)

When creating a new configuration with `snapper create-config` as shown above, this feature is enabled by default. To disable it, edit the configuration file and set

 `TIMELINE_CREATE="no"` 

The default settings will keep 10 hourly, 10 daily, 10 monthly and 10 yearly snapshots. You may want to change this, especially on busy subvolumes like /. See [#Caveats](#Caveats).

Here is an example for a configuration with only 5 hours of snapshots, 7 daily ones, no monthly and no yearly ones:

 `/etc/snapper/configs/root` 

```
# limits for timeline cleanup
TIMELINE_MIN_AGE="1800"
TIMELINE_LIMIT_HOURLY="5"
TIMELINE_LIMIT_DAILY="7"
TIMELINE_LIMIT_WEEKLY="0"
TIMELINE_LIMIT_MONTHLY="0"
TIMELINE_LIMIT_YEARLY="0"

```

The `snapper -c root list` output after some weeks:

 `# snapper -c root list` 

```
Type   | #    | Pre # | Date                     | User | Cleanup  | Description | Userdata
-------+------+-------+--------------------------+------+----------+-------------+---------
single | 0    |       |                          | root |          | current     |                                                                            
single | 3053 |       | Tue Oct 22 00:01:02 2013 | root | timeline | timeline    |                                                                            
single | 3077 |       | Wed Oct 23 00:01:01 2013 | root | timeline | timeline    |                                                                            
single | 3101 |       | Thu Oct 24 00:01:01 2013 | root | timeline | timeline    |                                                                            
single | 3125 |       | Fri Oct 25 00:01:01 2013 | root | timeline | timeline    |                                                                            
single | 3149 |       | Sat Oct 26 00:01:01 2013 | root | timeline | timeline    |                                                                            
single | 3173 |       | Sun Oct 27 00:01:01 2013 | root | timeline | timeline    |                                                                            
single | 3197 |       | Sun Oct 27 23:01:01 2013 | root | timeline | timeline    |                                                                            
single | 3198 |       | Mon Oct 28 00:01:01 2013 | root | timeline | timeline    |                                                                            
single | 3199 |       | Mon Oct 28 01:01:01 2013 | root | timeline | timeline    |                                                                            
single | 3200 |       | Mon Oct 28 02:01:01 2013 | root | timeline | timeline    |                                                                            
single | 3201 |       | Mon Oct 28 03:01:02 2013 | root | timeline | timeline    |                                                                            
single | 3202 |       | Mon Oct 28 04:01:01 2013 | root | timeline | timeline    |                                                                            
single | 3203 |       | Mon Oct 28 05:01:02 2013 | root | timeline | timeline    |         
single | 3204 |       | Mon Oct 28 06:01:01 2013 | root | timeline | timeline    |         
single | 3205 |       | Mon Oct 28 07:01:02 2013 | root | timeline | timeline    |         
single | 3206 |       | Mon Oct 28 08:01:01 2013 | root | timeline | timeline    |         
single | 3207 |       | Mon Oct 28 09:01:01 2013 | root | timeline | timeline    |         
single | 3208 |       | Mon Oct 28 10:01:01 2013 | root | timeline | timeline    |         
single | 3209 |       | Mon Oct 28 11:01:01 2013 | root | timeline | timeline    |         
single | 3210 |       | Mon Oct 28 12:01:01 2013 | root | timeline | timeline    |         
single | 3211 |       | Mon Oct 28 13:01:01 2013 | root | timeline | timeline    |         
single | 3212 |       | Mon Oct 28 14:01:01 2013 | root | timeline | timeline    |         
single | 3213 |       | Mon Oct 28 15:01:01 2013 | root | timeline | timeline    |         
single | 3214 |       | Mon Oct 28 16:01:01 2013 | root | timeline | timeline    |         
single | 3215 |       | Mon Oct 28 17:01:01 2013 | root | timeline | timeline    |         
single | 3216 |       | Mon Oct 28 18:01:01 2013 | root | timeline | timeline    |         
single | 3217 |       | Mon Oct 28 19:01:01 2013 | root | timeline | timeline    |         
single | 3218 |       | Mon Oct 28 20:01:01 2013 | root | timeline | timeline    |

```

Those snapshots are stored into $BTRFS_ROOT/.snapshots or, more precisely, the subvolume path is $BTRFS_ROOT/.snapshots/$SNAPHOST_ID/snapshot. See this [forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1458872#p1458872).

## Access for non-root users

Each config is created with the root user, and by default, only root can see and access it.

To be able to list the snapshots for a given config for a specific user, simply change the value of `ALLOW_USERS` in your `/etc/snapper/configs/<config_name>` file. You should now be able to run `snapper -c <config_name> list` as a normal user.

Eventually, you want to be able to browse the `.snapshots` directory with a user, but the owner of this directory must stay root. Therefore, you should change the group owner by a group containing the user you are interested in, such as `users` for example:

```
# chmod a+rx .snapshots
# chown :users .snapshots

```

## Periodic launch without cron

If you haven't installed `cronie`, the cron jobs will never be launched. However, you can benefit from the systemd timers installed along with snapper.

To start the timeline timer:

```
# systemctl start snapper-timeline.timer

```

You may also want to start `snapper-cleanup.timer`, and perhaps enable them, so that they start during boot.

## Tips and Tricks

### Pre-post snapshots with pacman

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

### Wrapping upgrades in pre-post snapshots

[Pacupg](https://aur.archlinux.org/packages/Pacupg/)<sup><small>AUR</small></sup> is a script specifically designed to wrap a system upgrade in snapshots. In contrast with the above solution, it downloads the packages first (`pacman -Syuw`) and then only wraps the upgrade (`pacman -Su`) in snapshots so as to keep the differences between the pre and post snapshots to a minimum. It also detects if the user's `/boot` directory is on a separate partition and automatically makes a copy of it when it detects an upgrade to the Linux kernel. Additionally, it will avoid taking snapshots if there is nothing to upgrade and log all upgraded packages (with changed version numbers) to `/var/local/log/pacupg`. If [pacaur](https://aur.archlinux.org/packages/pacaur/)<sup><small>AUR</small></sup> is installed, the script can also upgrade AUR packages. It builds them first, then takes a snapshot when they are ready to be installed thus keeping the pre-post snapshot differences minimal. As with regular packages, it logs all upgraded packages and will avoid taking snapshots if no packages are available to upgrade. The script now integrates with [grub-btrfs-git](https://aur.archlinux.org/packages/grub-btrfs-git/)<sup><small>AUR</small></sup>. If it is installed, `pacupg` will automatically regenerate your grub.cfg after every upgrade to include your snapshots as boot options.

#### Easing the rollback process

The [pacupg](https://aur.archlinux.org/packages/pacupg/)<sup><small>AUR</small></sup> script also allows for the easy rollback of snapshots. Running `pacupg -r` will bring up a menu that allows the user to rollback both pre-post snapshots (upgrades) or single snapshots (timeline snapshots).

### Suggested Filesystem Layout

```
subvolid=0
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

Where /.snapshots is a mountpoint for subvol_snapshots, and subvol_... is any number of subvolumes - one for every directory that you:

*   Do NOT wish for snapper to backup
*   Do NOT wish to lose the contents of when you restore an entire system from a snapshot

This layout allows the snapper utility to take regular system snapshots, while at the same time making it easy to restore the entire system from an Arch Live CD if it becomes unbootable.

In this sceneario, after the initial setup, snapper needs no changes, and will work as expected.

#### Configuring Snapper

Add this line to your /etc/fstab:

```
UUID=...        /.snapshots             btrfs   ...,subvol=subvol_snapshots    0       0

```

This will make all snapshots that snapper creates be stored outside of the subvol_root subvolume, so that subvol_root can easily be replaced anytime without losing the snapper snapshots.

Now, because snapper does not like /.snapshots to already exist when you run `snapper -c root create-config /`, do this:

Make sure /.snapshots does NOT exist

Create snapper config:

```
# snapper -c root create-config /

```

Now that snapper is happy, delete /.snapshots subvolume:

```
# btrfs subvolume delete /.snapshots

```

Create the /.snapshots folder to use as a mountpoint:

```
# mkdir /.snapshots
# chmod 750 /.snapshots

```

Mount subvol_snapshots at /.snapshots

```
# mount /.snapshots

```

**Note:** Since /.snapshots will be in your /etc/fstab at this point, you do not need to specify the device

#### Restoring the entire system

If you ever want to restore your entire system using one of snapper's snapshots, follow this procedure:

Boot Arch live CD

Mount btrfs device (subvolid=0):

```
# mount /dev/sdX /mnt

```

Find the snapshot you want to recover:

```
# vi /mnt/subvol_snapshots/*/info.xml

```

**Note:** Here, you can read the `<description>` tag and the `<date>` tag, and when you find it, remember the `<num>` number

**Note:** In vi, use `:n` to see the next file, `:rew` to go back to the first file, and `:q` to quit

Delete or move the root subvolume:

```
# mv /mnt/subvol_root /mnt/subvol_root.broken

```

**Note:** If you want to delete it instead, remember to use `btrfs subvol delete subvol_root` since subvolumes can't be deleted with rm like folders can

Create a read-write snapshot of the read-only snapshot snapper took:

```
# btrfs subvol snapshot /mnt/subvol_snapshots/#/snapshot /mnt/subvol_root

```

**Note:** Where `#` is the number of the snapper snapshot you found earlier using vi

Unmount the btrfs device and reboot:

```
# umount /mnt
# reboot

```

For a more detailed description of the problem this layout solves, see: [https://bbs.archlinux.org/viewtopic.php?id=194491](https://bbs.archlinux.org/viewtopic.php?id=194491)

### Deleting files from snapshots

If you want to delete a specific file or folder from past snapshots without deleting the snapshots themselves, [snapperS](https://pypi.python.org/pypi/snapperS) is a script that adds this functionality to Snapper. This script can also be used to manipulate past snapshots in a number of other ways that Snapper does not currently support.

## Troubleshooting

### Snapper logs

Snapper writes all activity to `/var/log/snapper.log` - check this file first if you think something goes wrong.

If you have issues with hourly/daily/weekly snapshots, the most common cause for this so far has been that the cronie service (or whatever cron daemon you are using) was not running.

### IO Error

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

Retrieved from "[https://wiki.archlinux.org/index.php?title=Snapper&oldid=413855](https://wiki.archlinux.org/index.php?title=Snapper&oldid=413855)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [File systems](/index.php/Category:File_systems "Category:File systems")