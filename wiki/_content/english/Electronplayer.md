Related articles

*   [Electron](/index.php/Electron "Electron")

[electronplayer](https://aur.archlinux.org/packages/electronplayer/) Is an application using the [electron](https://www.archlinux.org/packages/?name=electron) app development framework. It is used for viewing Netflix, YouTube, Twitch and Floatplane. Most notably to isolate the cookies from these websites from your main web browser.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Sandboxing](#Sandboxing)
    *   [2.1 Create firejail profile for electronplayer](#Create_firejail_profile_for_electronplayer)
    *   [2.2 Create a soft link to electronplayer](#Create_a_soft_link_to_electronplayer)

## Installation

[Install](/index.php/Install "Install") the [electronplayer](https://aur.archlinux.org/packages/electronplayer/) package.

## Sandboxing

[electronplayer](https://aur.archlinux.org/packages/electronplayer/) Seems to be resistant to being sandboxed with [firejail](/index.php/Firejail "Firejail"), as it seems that it is installed by default in `/usr/bin/electronplayer` with a symlink to `/opt/electronplayer/electronplayer --no-sandbox`. Because of this, running:

```
$ ln -s /usr/bin/firejail /usr/local/bin/electronplayer 

```

and then running:

```
$ /usr/local/bin/electronplayer

```

will NOT sandbox electronplayer, it will immediately break out of the sandbox and begin running unconfined as if it were not being run with firejail. A workaround I've found for this problem is as follows:

#### Create firejail profile for electronplayer

```
$ touch /etc/firejail/electronplayer.profile

```

then:

```
$ chmod 644 /etc/firejail/electronplayer.profile

```

Then follow instructions in [firejail](/index.php/Firejail "Firejail") for details on how to create a custom firejail profile. This is the one I use:

```
# Firejail profile for electronplayer
include electronplayer.local
# Persistent global definitions
include globals.local

include disable-common.inc
include disable-passwdmgr.inc
include disable-programs.inc

noblacklist ${HOME}/.config/electronplayer
whitelist ${HOME}/.config/electronplayer

apparmor
caps.drop all
netfilter
nodbus
nodvd
nogroups
nonewprivs
noroot
notv
protocol unix,inet,inet6,netlink
seccomp

```

#### Create a soft link to electronplayer

Because `/usr/bin/electronplayer` already has a hard symlink to `/opt/electronplayer/electronplayer --no-sandbox`, the next step is to create a soft link to `/usr/bin/firejail /opt/electronplayer/electronplayer` in `/usr/local/bin`. First:

```
$ touch /usr/local/bin/electronplayer

```

then:

```
$ chmod 755 /usr/local/bin/electronplayer

```

then add the following text to `/usr/local/bin/electronplayer`, adding whatever arguments or options you like to either of the commands:

```
#!/bin/sh
/usr/bin/firejail /opt/electronplayer/electronplayer

```

**And that's it! Now you can watch videos isolated from you normal web browser from the safety of the firejail sandbox!**