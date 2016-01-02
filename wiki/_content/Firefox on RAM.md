# Firefox on RAM

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Assuming that there is memory to spare, placing [Firefox](/index.php/Firefox "Firefox")'s cache or complete profile to RAM offers significant advantages. Even though opting for the partial route is an improvement by itself, the latter can make Firefox even more responsive compared to its stock configuration. Benefits include, among others:

*   reduced drive read/writes;
*   heightened responsive feel;
*   many operations within Firefox, such as quick search and history queries, are nearly instantaneous.

To do so we can make use of a [tmpfs](/index.php/Tmpfs "Tmpfs").

Because data placed therein cannot survive a shutdown, a script responsible for syncing back to drive prior to system shutdown is necessary if persistence is desired (which is likely in the case of profile relocation). On the other hand, only relocating the cache is a quick, less inclusive solution that will slightly speed up user experience while emptying Firefox cache on every reboot.

**Note:** Cache is stored **separately** from Firefox default profiles' folder (`/home/$USER/.mozilla/firefox/`): it is found by default in `/home/$USER/.cache/mozilla/firefox/<profile>`. This is similar to what Chromium and other browsers do. Therefore, sections [#Place profile in RAM using tools](#Place_profile_in_RAM_using_tools) and [#Place profile in RAM manually](#Place_profile_in_RAM_manually) **don't deal** with cache relocating and syncing but only with profile adjustments. See the note at [Profile-sync-daemon#Benefits of psd](/index.php/Profile-sync-daemon#Benefits_of_psd "Profile-sync-daemon") for more details. [Anything-sync-daemon](/index.php/Anything-sync-daemon "Anything-sync-daemon") may be used to achieve the same thing as Option 2 for cache folders.

## Contents

*   [1 Relocate cache only to RAM](#Relocate_cache_only_to_RAM)
*   [2 Place profile in RAM using tools](#Place_profile_in_RAM_using_tools)
*   [3 Place profile in RAM manually](#Place_profile_in_RAM_manually)
    *   [3.1 Before you start](#Before_you_start)
    *   [3.2 The script](#The_script)
    *   [3.3 Automation](#Automation)
        *   [3.3.1 cron job](#cron_job)
        *   [3.3.2 Sync at login/logout](#Sync_at_login.2Flogout)
*   [4 See also](#See_also)

## Relocate cache only to RAM

When a page is loaded, it can be cached so it doesn't need to be downloaded to be redisplayed. For e-mail and news, messages and attachments are cached as well. Firefox can be configured to use only RAM as cache storage. Configuration files, bookmarks, extensions etc. will be written to drive as usual. For this:

*   open `about:config` in the address bar
*   set `browser.cache.disk.enable` to "false" (double click the line)
*   verify that `browser.cache.memory.enable` is set to "true" ([default value](http://kb.mozillazine.org/Browser.cache.memory.enable))
*   add the entry (right click->new->integer) `browser.cache.memory.capacity` and set it to the amount of KB you'd like to spare, or to -1 for [automatic](http://kb.mozillazine.org/Browser.cache.memory.capacity#-1) cache size selection. (Skipping this step has the same effect as setting the value to -1.)

Main disadvantages of this method are that the content of currently browsed webpages is lost if browser crashes or after a reboot, and that the settings need to be configured for each user individually.

A workaround for the first drawback is to use [anything-sync-daemon](/index.php/Anything-sync-daemon "Anything-sync-daemon") or similar periodically-syncing script so that cache gets copied over to the drive on a regular basis.

## Place profile in RAM using tools

Relocate the browser profile to [tmpfs](/index.php/Tmpfs "Tmpfs") so as to globally improve browser's responsiveness. Another benefit is a reduction in drive I/O operations, of which [SSDs benefit the most](/index.php/SSD#Locate_High-Use_Files_to_RAM "SSD").

Use an active management script for maximal reliability and ease of use. Several are available from the AUR.

*   [profile-sync-daemon](https://aur.archlinux.org/packages/profile-sync-daemon/)<sup><small>AUR</small></sup> - refer to the [Profile-sync-daemon](/index.php/Profile-sync-daemon "Profile-sync-daemon") wiki article for additional info on it;
*   [firefox-sync](https://aur.archlinux.org/packages/firefox-sync/)<sup><small>AUR</small></sup>

## Place profile in RAM manually

### Before you start

Before potentially compromising Firefox's profile, be sure to make a backup for quick restoration. Replace `xyz.default` as appropriate and use `tar` to make a backup:

```
$ tar zcvfp ~/firefox_profile_backup.tar.gz ~/.mozilla/firefox/_xyz.default_

```

### The script

<small>_Adapted from [verot.net's Speed up Firefox with tmpfs](http://www.verot.net/firefox_tmpfs.htm)_</small>

The script will first move Firefox's profile to a new static location, make a sub-directory in `/dev/shm`, softlink to it and later populate it with the contents of the profile. As before, replace the bold sections to suit. The only value that absolutely needs to be altered is, again, `xyz.default`.

Be sure that [rsync](/index.php/Rsync "Rsync") is installed and save the script to `~/bin/firefox-sync`, for example:

 `firefox-sync` 

```
#!/bin/sh

static=_main_
link=_xyz.default_
volatile=_/dev/shm/firefox-$USER_

IFS=
set -efu

cd ~/.mozilla/firefox

if [ ! -r $volatile ]; then
	mkdir -m0700 $volatile
fi

if [ "$(readlink $link)" != "$volatile" ]; then
	mv $link $static
	ln -s $volatile $link
fi

if [ -e $link/.unpacked ]; then
	rsync -av --delete --exclude .unpacked ./$link/ ./$static/
else
	rsync -av ./$static/ ./$link/
	touch $link/.unpacked
fi

```

Close Firefox, make the script executable and test it:

```
$ killall firefox firefox-bin
$ chmod +x ~/bin/firefox-sync
$ ~/bin/firefox-sync

```

Run Firefox again to gauge the results. The second time the script runs, it will then preserve the RAM profile by copying it back to disk.

### Automation

Seeing that forgetting to sync the profile can lead to disastrous results, automating the process seems like a logical course of action.

#### cron job

Manipulate the user's [cron](/index.php/Cron "Cron") table using `crontab`:

```
$ crontab -e

```

Add a line to start the script every 30 minutes,

```
*/30 * * * * _~/bin/firefox-sync_

```

or add the following to do so every 2 hours:

```
0 */2 * * * _~/bin/firefox-sync_

```

#### Sync at login/logout

Deeming [bash](/index.php/Bash "Bash") is being used, add the script to the login/logout files:

```
$ echo '_~/bin/firefox-sync_' | tee -a ~/.bash_logout ~/.bash_login >/dev/null

```

**Note:** You may wish to use `~/.bash_profile` instead of `~/.bash_login` as bash will only read the first of these if both exist and are readable.

## See also

*   [Fstab#tmpfs](/index.php/Fstab#tmpfs "Fstab")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Firefox_on_RAM&oldid=414079](https://wiki.archlinux.org/index.php?title=Firefox_on_RAM&oldid=414079)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web browser](/index.php/Category:Web_browser "Category:Web browser")