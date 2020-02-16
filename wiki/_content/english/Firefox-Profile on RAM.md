Assuming that there is memory to spare, placing [Firefox](/index.php/Firefox "Firefox")'s cache or complete profile to RAM offers significant advantages. Even though opting for the partial route is an improvement by itself, the latter can make Firefox even more responsive compared to its stock configuration. Benefits include, among others:

*   reduced drive read/writes;
*   heightened responsive feel;
*   many operations within Firefox, such as quick search and history queries, are nearly instantaneous.

To do so we can make use of a [tmpfs](/index.php/Tmpfs "Tmpfs").

Because data placed therein cannot survive a shutdown, a script responsible for syncing back to drive prior to system shutdown is necessary if persistence is desired (which is likely in the case of profile relocation). On the other hand, only relocating the cache is a quick, less inclusive solution that will slightly speed up user experience while emptying Firefox cache on every reboot.

**Note:** Cache is stored **separately** from Firefox default profiles' folder (`/home/$USER/.mozilla/firefox/`): it is found by default in `/home/$USER/.cache/mozilla/firefox/<profile>`. This is similar to what Chromium and other browsers do. Therefore, sections [#Place profile in RAM using tools](#Place_profile_in_RAM_using_tools) and [#Place profile in RAM manually](#Place_profile_in_RAM_manually) **don't deal** with cache relocating and syncing but only with profile adjustments. See the note at [Profile-sync-daemon#Design goals and benefits of psd](/index.php/Profile-sync-daemon#Design_goals_and_benefits_of_psd "Profile-sync-daemon") for more details. [Anything-sync-daemon](/index.php/Anything-sync-daemon "Anything-sync-daemon") may be used to achieve the same thing as Option 2 for cache folders.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Relocate cache to RAM only](#Relocate_cache_to_RAM_only)
*   [2 Place profile in RAM using tools](#Place_profile_in_RAM_using_tools)
*   [3 Place profile in RAM manually](#Place_profile_in_RAM_manually)
    *   [3.1 Before you start](#Before_you_start)
    *   [3.2 The script](#The_script)
    *   [3.3 Automation](#Automation)
        *   [3.3.1 systemd](#systemd)
        *   [3.3.2 cron job](#cron_job)
        *   [3.3.3 Sync at login/logout](#Sync_at_login/logout)
*   [4 See also](#See_also)

## Relocate cache to RAM only

See [Firefox/Tweaks#Turn off the disk cache](/index.php/Firefox/Tweaks#Turn_off_the_disk_cache "Firefox/Tweaks").

## Place profile in RAM using tools

Relocate the browser profile to [tmpfs](/index.php/Tmpfs "Tmpfs") so as to globally improve browser's responsiveness. Another benefit is a reduction in drive I/O operations, of which [SSDs benefit the most](/index.php/Improving_performance#Show_disk_writes "Improving performance").

Use an active management script for maximal reliability and ease of use. Several are available from the AUR.

*   [profile-sync-daemon](https://www.archlinux.org/packages/?name=profile-sync-daemon) - refer to the [Profile-sync-daemon](/index.php/Profile-sync-daemon "Profile-sync-daemon") wiki article for additional info on it;
*   [firefox-sync](https://aur.archlinux.org/packages/firefox-sync/) - sufficient for a user with a single profile; uses a script and systemd service similar to those below.

## Place profile in RAM manually

### Before you start

Before potentially compromising Firefox's profile, be sure to make a backup for quick restoration. Replace `xyz.default` as appropriate and use `tar` to make a backup:

```
$ tar zcvfp ~/firefox_profile_backup.tar.gz ~/.mozilla/firefox/*xyz.default*

```

### The script

<small>*Adapted from [verot.net's Speed up Firefox with tmpfs](http://www.verot.net/firefox_tmpfs.htm)*</small>

The script will first move Firefox's profile to a new static location, make a sub-directory in `/dev/shm`, softlink to it and later populate it with the contents of the profile. As before, replace the bold sections to suit. The only value that absolutely needs to be altered is, again, `xyz.default`.

Be sure that [rsync](/index.php/Rsync "Rsync") is installed and save the script to `~/.local/bin/firefox-sync`, for example:

 `firefox-sync` 
```
#!/bin/sh

static=*static-$1*
link=*$1*
volatile=*/dev/shm/firefox-$1-$USER*

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
$ chmod +x ~/.local/bin/firefox-sync
$ ls ~/.mozilla/firefox/
$ ~/.local/bin/firefox-sync <firefox-profile>

```

Run Firefox again to gauge the results. The second time the script runs, it will then preserve the RAM profile by copying it back to disk.

### Automation

Seeing that forgetting to sync the profile can lead to disastrous results, automating the process seems like a logical course of action.

#### systemd

Save the following script as `~/.config/systemd/user/firefox-profile@.service`

then use

```
systemctl --user daemon-reload
systemctl --user enable firefox-profile@<profile>.service
systemctl --user start firefox-profile@<profile>.service 

```

```
 [Unit]
 Description=Firefox profile memory cache

 [Install]
 WantedBy=default.target

 [Service]
 Type=oneshot
 RemainAfterExit=yes
 ExecStart=/home/matthew/.local/bin/firefox-sync %i
 ExecStop=/home/matthew/.local/bin/firefox-sync %i

```

#### cron job

Manipulate the user's [cron](/index.php/Cron "Cron") table using `crontab`:

```
$ crontab -e

```

Add a line to start the script every 30 minutes,

```
*/30 * * * * *~/.local/bin/firefox-sync*

```

or add the following to do so every 2 hours:

```
0 */2 * * * *~/.local/bin/firefox-sync*

```

#### Sync at login/logout

Assuming [bash](/index.php/Bash "Bash") is being used, add the script to the login/logout files:

```
$ echo '*~/.local/bin/firefox-sync*' | tee -a ~/.bash_logout ~/.bash_login >/dev/null

```

**Note:** You may wish to use `~/.bash_profile` instead of `~/.bash_login` as bash will only read the first of these if both exist and are readable.

## See also

*   [tmpfs](/index.php/Tmpfs "Tmpfs")