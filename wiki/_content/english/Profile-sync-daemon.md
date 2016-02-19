[Profile-sync-daemon](https://aur.archlinux.org/packages/Profile-sync-daemon/) (psd) is a tiny pseudo-daemon designed to manage browser profile(s) in tmpfs and to periodically sync back to the physical disc (HDD/SSD). This is accomplished by an innovative use of rsync to maintain synchronization between a tmpfs copy and media-bound backup of the browser profile(s). Additionally, psd features several crash recovery features.

## Contents

*   [1 Design goals and benefits of psd](#Design_goals_and_benefits_of_psd)
*   [2 Setup and installation](#Setup_and_installation)
    *   [2.1 Edit the config file](#Edit_the_config_file)
*   [3 Supported browsers](#Supported_browsers)
*   [4 Using psd](#Using_psd)
    *   [4.1 Preview (parse) mode](#Preview_.28parse.29_mode)
    *   [4.2 Clean mode](#Clean_mode)
    *   [4.3 Start and stop psd](#Start_and_stop_psd)
    *   [4.4 Supported distros](#Supported_distros)
    *   [4.5 Sync at more frequent intervals (optional)](#Sync_at_more_frequent_intervals_.28optional.29)
*   [5 FAQ](#FAQ)
    *   [5.1 What is overlayfs mode?](#What_is_overlayfs_mode.3F)
    *   [5.2 I need more memory to accommodate my profile/profiles in /run/user/xxxx. How can I allocate more?](#I_need_more_memory_to_accommodate_my_profile.2Fprofiles_in_.2Frun.2Fuser.2Fxxxx._How_can_I_allocate_more.3F)
    *   [5.3 Why do I have another browser profile directory "foo-back-ovfs" when I enable overlayfs?](#Why_do_I_have_another_browser_profile_directory_.22foo-back-ovfs.22_when_I_enable_overlayfs.3F)
    *   [5.4 My system crashed and did not sync back. What do I do?](#My_system_crashed_and_did_not_sync_back._What_do_I_do.3F)
    *   [5.5 Where can I find this snapshot?](#Where_can_I_find_this_snapshot.3F)
    *   [5.6 How can I restore the snapshot?](#How_can_I_restore_the_snapshot.3F)
    *   [5.7 Can psd delete the snapshots automatically?](#Can_psd_delete_the_snapshots_automatically.3F)
*   [6 Support](#Support)
*   [7 psd on other distros](#psd_on_other_distros)
*   [8 See also](#See_also)

## Design goals and benefits of psd

1.  Transparent user experience
2.  Reduced wear to physical drives
3.  Speed

Since the profile(s), browser cache*, etc. are relocated into [tmpfs](/index.php/Tmpfs "Tmpfs") (RAM disk), the corresponding I/O associated with using the browser is also redirected from the physical drive to RAM, thus reducing wear to the physical drive and also greatly improving browser speed and responsiveness.

**Note:** Some browsers such as Chrome/Chromium, Firefox (since v21), Midori, and Rekonq actually keeps their cache directories **separately** from their profile directory. It is not within the scope of profile-sync-daemon to modify this behavior; users are encouraged to refer to the [Chromium tweaks#Cache in tmpfs](/index.php/Chromium_tweaks#Cache_in_tmpfs "Chromium tweaks") section for Chromium and to the [Firefox on RAM](/index.php/Firefox_on_RAM "Firefox on RAM") article for several workarounds. An easy fix is to move the various browsers' cache directory from their default location (e.g. `/home/$USER/.cache/<browser>/<profile>/`) to the corresponding profile directory, e.g. `/home/$USER/.mozilla/firefox/<profile>/cache`, and then symlink the new cache folder back to its original location. This way, profile-sync-daemon will automatically take into account the cache folder too.

## Setup and installation

[Install](/index.php/Install "Install") the [profile-sync-daemon](https://aur.archlinux.org/packages/profile-sync-daemon/) package.

### Edit the config file

Run psd the first time which will create `$XDG_CONFIG_HOME/psd/psd.conf` (referred to hereafter as as the config file) which contains all settings.

**Note:** Any edits made to this file while psd is active will be applied only after psd has been restarted from the systemd user service.

```
$ psd
First time running psd so please edit /home/facade/.config/psd/psd.conf to your liking and run again.

```

*   Optionally enable the use of overlayfs to improve sync speed and to use a smaller memory footprint. Do this in the USE_OVERLAYFS variable. The user will require sudo rights to `/usr/bin/psd-overlay-helper` to use this option and the kernel must support overlayfs version 22 or higher. See the FAQ below for additional details.
*   Optionally define which browsers are to be managed in the BROWSERS array. If none are defined, the default is all detected browsers.
*   Optionally disable the use of crash-recovery snapshots (not recommended). Do this in the USE_BACKUPS variable.

Example: Let's say that Chromium, Opera and Midori are installed but only Chromium and Opera are to be sync'ed to tmpfs since the user keeps Midori as a backup browser and it is seldom used:

```
# List browsers separated by spaces to include in the sync. Useful if you do not
# wish to have all possible browser profiles sync'ed.
#
# Possible values:
#  chromium
#  chromium-dev
#  conkeror.mozdev.org
#  epiphany
#  firefox
#  firefox-trunk
#  google-chrome
#  google-chrome-beta
#  google-chrome-unstable
#  heftig-aurora
#  icecat
#  luakit
#  midori
#  opera
#  opera-developer
#  opera-beta
#  qupzilla
#  palemoon
#  rekonq
#  seamonkey
#  vivaldi
#
# If the following is commented out (default), then all available/supported 
# browsers will be sync'ed, separated by comma
BROWSERS="chromium opera"

```

Beginning with version 5.54 of psd, native support for overlayfs is included. Uncomment the **USE_OVERLAYFS="yes"** line to enable it rather than the default full copy to reduce the memory costs and to improve sync/unsync operations.

**Note:** This feature requires a Linux kernel version of 3.18.0 or greater to work.

## Supported browsers

Currently, the following browsers are auto-detected and managed:

*   [Chromium](/index.php/Chromium "Chromium")
*   [chromium-dev](/index.php/AUR "AUR")
*   [conkeror-git](https://aur.archlinux.org/packages/conkeror-git/)
*   [Epiphany](/index.php/Epiphany "Epiphany")
*   [Firefox](/index.php/Firefox "Firefox") (all flavors including stable, beta, and aurora)
*   [google-chrome](https://aur.archlinux.org/packages/google-chrome/)
*   [google-chrome-beta](https://aur.archlinux.org/packages/google-chrome-beta/)
*   [google-chrome-dev](https://aur.archlinux.org/packages/google-chrome-dev/)
*   [heftig's version of Aurora](https://bbs.archlinux.org/viewtopic.php?id=117157): An Arch Linux-only browser
*   [icecat](https://aur.archlinux.org/packages/icecat/)
*   [Luakit](/index.php/Luakit "Luakit")
*   [Midori](/index.php/Midori "Midori")
*   [Opera](/index.php/Opera "Opera")
*   Qupzilla
*   [rekonq](https://www.archlinux.org/packages/?name=rekonq)
*   [seamonkey](https://www.archlinux.org/packages/?name=seamonkey)
*   [vivaldi](https://aur.archlinux.org/packages/vivaldi/)

## Using psd

### Preview (parse) mode

The 'parse' option can be called to show users exactly what *psd* will do/is doing based on `$XDG_CONFIG_HOME/psd/psd.conf` as well printout useful information such as profile size, paths, and if any recovery snapshots have been created.

```
$ psd p
Profile-sync-daemon v6.03 on Arch Linux.

 Systemd service is currently active.
 Systemd resync service is currently active.
 Overlayfs v23 is currently active.

Psd will manage the following per /home/facade/.config/psd/psd.conf settings:

 browser/psname:  chromium/chromium
 owner/group:     facade/100
 sync target:     /home/facade/.config/chromium
 tmpfs dir:       /run/user/1000/facade-chromium
 profile size:    93M
 overlayfs size:  39M
 recovery dirs:   2 <- delete with the c option
  dir path/size:  /home/facade/.config/chromium-backup-crashrecovery-20150117_171359 (92M)
  dir path/size:  /home/facade/.config/chromium-backup-crashrecovery-20150119_112204 (93M)

 browser/psname:  firefox/firefox
 owner/group:     facade/100
 sync target:     /mnt/data/docs/facade/mozilla/firefox/f8cv8bfu.default
 tmpfs dir:       /run/user/1000/facade-firefox-f8cv8bfu.default
 profile size:    145M
 overlayfs size:  13M
 recovery dirs:   none

```

As shown in the output and as stated above, if no specific browser or subset of browsers are defined in the BROWSERS array, *psd* will sync ALL supported profiles that it finds for the given user(s).

### Clean mode

The clean mode will delete ALL recovery snapshots that have accumulated. Run this only if you are sure that you want to delete them.

```
$ psd c

Profile-sync-daemon v6.03 on Arch Linux.

Deleting 2 crashrecovery dirs for profile /home/facade/.config/chromium
 /home/facade/.config/chromium-backup-crashrecovery-20150117_171359
 /home/facade/.config/chromium-backup-crashrecovery-20150119_112204

```

### Start and stop psd

With the release of the version 6.x series of psd, the only init system that is officially supported is systemd. Psd ships with a systemd user service to start or stop it (psd.service). Additionally, a provided resync-timer will run an hourly resync from tmpfs back to the disk. The resync-timer is started automatically with psd.service so there is no need to attempt to start the timer.

For users unfamiliar with systemd user mode, use the following commands to enable the psd service:

```
$ systemctl --user [option] psd.service

```

Available options: start stop enable disable status

### Supported distros

Since psd is just a bash script with a systemd service, it should run on any flavor of Linux running systemd. Around a dozen distros provide an official package or user-maintained option to install psd. One can also build psd from source. See the official website for available packages and installation instructions.

### Sync at more frequent intervals (optional)

The package provided re-sync timer triggers once per hour. Users may optionally redefine this behavior simply by [extending the systemd unit](/index.php/Systemd#Editing_provided_units "Systemd"). The example below changes the timer to sync once every ten minutes:

 `~/.config/systemd/user/psd-resync.timer.d/frequency.conf` 
```
--------------------------------------------------------
[Unit]
Description=Timer for Profile-sync-daemon
PartOf=psd.service

[Timer]
OnUnitActiveSec=10m

```

See `man systemd.timer` for additional options.

## FAQ

### What is overlayfs mode?

Overlayfs is a simple union file-system mainlined in the Linux kernel version 3.18.0\. Starting with psd version 5.54, overlayfs can be used to reduce the memory footprint of psd's tmpfs space and to speed up sync and unsync operations. The magic is in how the overlay mount only writes out data that has changed rather than the entire profile. The same recovery features psd uses in its default mode are also active when running in overlayfs mode. Overlayfs mode is enabled by uncommenting the USE_OVERLAYFS="yes" line in `$XDG_CONFIG_HOME/psd/psd.conf` followed by a restart of the daemon.

There are several versions of overlayfs available to the Linux kernel in production in various distros. Versions 22 and lower have a module called 'overlayfs' while newer versions (23 and higher) have a module called 'overlay' -- note the lack of the 'fs' in the newer version. Psd will automatically detect the overlayfs available to your kernel if it is configured to use one of them.

Since version 6.05 of psd, users wanting to take advantage of this mode MUST have sudo rights (without password prompt) to `/usr/bin/psd-overlay-helper` or global sudo rights. The following line in `/etc/sudoers` will supply your user with these rights. Add it using `/usr/bin/visudo` as root:

```
foo ALL=(ALL) NOPASSWD: /usr/bin/psd-overlay-helper

```

See the example in the PREVIEW MODE section above which shows a system using overlayfs to illustrate the memory savings that can be achieved. Note the "overlayfs size" report compared to the total "profile size" report for each profile. Be aware that these numbers will change depending on how much data is written to the profile, but in common use cases the overlayfs size will always be less than the profile size.

### I need more memory to accommodate my profile/profiles in /run/user/xxxx. How can I allocate more?

The standard way of controlling the size of /run/user is the RuntimeDirectorySize directive in `/etc/systemd/logind.conf` (see the man page for logind.conf for more). By default, 10% of physical memory is used but one can increase it safely. Remember that tmpfs only consumes what is actually used; the number specified here is just a maximum allowed.

### Why do I have another browser profile directory "foo-back-ovfs" when I enable overlayfs?

The way overlayfs works is to mount a read-only base copy (so-called lower dir) of the profile, and manage the new data on top of that. In order to avoid resyncing to the read-only file system, a copy is used instead. So using overlayfs is a trade off: faster initial sync times and less memory usage vs. disk space in the home dir.

### My system crashed and did not sync back. What do I do?

Odds are the "last good" backup of your browser profiles is just fine still sitting happily on your filesystem. Upon restarting `psd` (on a reboot for example), a check is preformed to see if the symlink to the tmpfs copy of your profile is invalid. If it is invalid, *psd* will snapshot the "last good" backup before it rotates it back into place. This is more for a sanity check that *psd* did no harm and that any data loss was a function of something else.

**Note:** Users can disable the snapshot/backup feature entirely by uncommenting and setting the USE_BACKUPS variable to 'no' in `$XDG_CONFIG_HOME/psd/psd.conf` if desired.

### Where can I find this snapshot?

It depends on the browser. You will find the snapshot in the same directory as the browser profile and it will contain a date-time-stamp that corresponds to the time at which the recovery took place. For example, chromium will be `~/.config/chromium-backup-crashrecovery-20130912_153310` -- of course, the date_time suffix will be different for you.

### How can I restore the snapshot?

*   Stop `psd`.
*   Confirm that there is no symlink to the tmpfs browser profile directory. If there is, *psd* did not stop correctly for other reasons.
*   Move the "bad" copy of the profile to a backup (do not blindly delete anything).
*   Copy the snapshot directory to the name that browser expects.

Example using Chromium:

```
mv ~/.config/chromium ~/.config/chromium-bad
cp -a ~/.config/chromium-backup-crashrecovery-20130912_153310 ~/.config/chromium

```

At this point you can launch chromium which will use the backup snapshot you just copied into place. If all is well, close the browser and restart psd. You may safely delete `~/.config/chromium-backup-crashrecovery-20130912_153310` at this point.

### Can psd delete the snapshots automatically?

Yes, run psd with the "clean" switch to delete snapshots.

## Support

Post in the [discussion thread](https://bbs.archlinux.org/viewtopic.php?pid=1026974) with comments or concerns.

## psd on other distros

*psd* is a bash script and should therefore run on any Linux distro. Around a dozen distros provide an official package or user-maintained option to install psd. See the [official website](https://github.com/graysky2/profile-sync-daemon#installation-from-distro-packages) for available packages and installation instructions.

## See also

*   [http://www.webupd8.org/2013/02/keep-your-browser-profiles-in-tmpfs-ram.html](http://www.webupd8.org/2013/02/keep-your-browser-profiles-in-tmpfs-ram.html)
*   [http://bernaerts.dyndns.org/linux/250-ubuntu-tweaks-ssd](http://bernaerts.dyndns.org/linux/250-ubuntu-tweaks-ssd)