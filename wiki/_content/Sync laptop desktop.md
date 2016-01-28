# Sync laptop desktop

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Sync laptop desktop#](https://wiki.archlinux.org/index.php/Talk:Sync_laptop_desktop))

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** first person (Discuss in [Talk:Sync laptop desktop#](https://wiki.archlinux.org/index.php/Talk:Sync_laptop_desktop))

It is not always possible to copy one computer's drive to the other. For example, some files must differ on both machines, or respective updates do not match.

## Contents

*   [1 Unison](#Unison)
    *   [1.1 Limitations](#Limitations)
*   [2 rsync](#rsync)
*   [3 rdiff-backup](#rdiff-backup)
*   [4 Syncthing](#Syncthing)

## Unison

[Unison](http://www.cis.upenn.edu/~bcpierce/unison/). [Screenshot](http://caml.inria.fr/about/successes-images/unison.jpg).

You need to have ssh on both machines, and (the same version of) unison installed on both machines (your laptop and desktop). Then with a few simple commands you can synchronise directories, and in a GUI you can select which things you wish to have synchronised and which not. You can also resolve conflicts.

**~/.unison/electra.prf** (laptop)

```
root = /home/hugo
root = ssh://pyros//home/hugo
follow = Path school
include common

```

**~/.unison/pyros.prf** (desktop)

```
root = /home/hugo
root = ssh://electra//home/hugo
follow = Path school
include common

```

**~/.unison/common**

```
ignore = Regex .*(cache|Cache|te?mp|history|thumbnails).*
ignore = Name sylpheed.log*
ignore = Name unison.log
ignore = Name .ICEauthority
ignore = Name .Xauthority
ignore = Path {.songinfo,.radinfo}
ignore = Path .adesklets
ignore = Path .Azureus
ignore = Path .forward
ignore = Path adesklets
ignore = Path .ethereal
ignore = Path .sheep
ignore = Path .xinitrc
ignore = Path .config
ignore = Path .xscreensaver
ignore = Path .xawtv
ignore = Path .radio
ignore = Path .forward
ignore = Path .dc++
ignore = Path .quodlibet
ignore = Path .tvtime
ignore = Path .config/graveman
ignore = Path .xmodmap
ignore = Path .java
ignore = Path .tvlist*
ignore = Path .thumbnails
ignore = Path .ssh
ignore = Path .viminfo
ignore = Path .vim/tmp
ignore = Path Desktop
ignore = Path .wine*
ignore = Path motion
ignore = Path src/ufobot/test_pipe
ignore = Path tmp
ignore = Path local
ignore = Path books
ignore = Path .mozilla/firefox/*/Cache*
ignore = Path .liferea/cache
ignore = Path .liferea/mozilla/liferea/Cache
ignore = Path .sylpheed-*/*.bak
ignore = Path .sylpheed-*/folderlist.xml*
ignore = Path .liferea/new_subscription
ignore = Path .mozilla/firefox/pluginreg.dat
ignore = Path .mozilla/firefox/*/lock
ignore = Path .mozilla/firefox/*/XUL.mfasl
ignore = Path .mozilla/firefox/*/xpti.dat
ignore = Path .mozilla/firefox/*/cookies.txt
ignore = Path .xbindkeysrc
ignore = Path .unison/ar*
ignore = Path .gaim/icons
ignore = Path .gaim/blist.xml
ignore = Path .asoundrc
ignore = Path .maillog
ignore = Path .openoffice2/.lock

```

As you can see, there are two different profiles, one for running from the laptop, and one for running the desktop. Files are posted here as example, they are nowhere essential for your configuration.

Bash aliases were created for quick usage. One example is:

```
alias unisync="unison-gtk2 electra -contactquietly -logfile /dev/null"

```

This starts unisync using profile 'electra', for when running the laptop.

A line in ~/Desktop/autostart automates the process when wanting to sync desktop with laptop:

```
xterm -e 'ping -q -W 2 -c 2 pyros &&
unison-gtk2 electra -contactquietly -logfile /dev/null &&
gxmessage -buttons no:0,yes:1  Syncing done. Shutdown pyros? ||
ssh pyros sudo halt' &

```

### Limitations

You can also use this tool with NFS shares, but you may find that it is slower, because using the ssh solution it asks the other side to check for updates, and thus not requiring network traffic for that part of the syncing process.

If you are using a ssh port different from the default (22), for example 1022, use this line in your prf file:

```
sshargs = -p 1022

```

If you are using symbolic links and want to synchronise your files on a vfat system (usb key for example), unison will not accept them and generate errors. You cannot just tell unison you do not want symbolic links, you have to name them all. To find them on your system, you can run

```
find ~/folder -type l

```

Unison is very sensitive and requires the **exact same versions** on [client and server](https://groups.yahoo.com/neo/groups/unison-users/conversations/topics/11439%7Cboth). Also, unison **must** be compiled against the same OCaml version on all peers too. Making it highly unfeasible for a heterogeneous network.

## rsync

See [rsync](/index.php/Rsync "Rsync")

## rdiff-backup

The following tool was used with the following backup script:

```
#!/bin/sh

mount /bak
#mount /boot
mount /mnt/win

rdiff-backup \
   --exclude-regexp 'cache$' \
   --exclude-regexp '(?i)/te?mp$' \
   --exclude /mnt \
   --exclude /vol \
   --exclude /bak \
   --exclude /usr/media \
   --exclude /usr/media/misc \
   --exclude /usr/lib \
   --exclude /tmp \
   --exclude /var/dl \
   --exclude /var/spool \
   --exclude /var/cache \
   --exclude /proc \
   --exclude /dev \
   --exclude /sys \
/ /bak/sys

echo "----------------------------------------"
echo " * Listing increments of backup"
echo "----------------------------------------"
rdiff-backup --list-increments /bak/sys

echo ""
echo "----------------------------------------"
echo " * Removing backups older than 5 Weeks"
echo "----------------------------------------"
rdiff-backup --force --remove-older-than 5W /bak/sys

##Force is necessary because:
#Fatal Error: Found 2 relevant increments, dated:
#Sat Apr 10 12:39:24 2004
#Sat Apr 17 04:15:01 2004
#If you want to delete multiple increments in this way, use the --force.

echo ""
echo "----------------------------------------"
echo " * Disk usage after backup"
echo "----------------------------------------"
df -h

umount /bak
#umount /boot
umount /mnt/win

```

## Syncthing

See [syncthing](/index.php/Syncthing "Syncthing")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Sync_laptop_desktop&oldid=396458](https://wiki.archlinux.org/index.php?title=Sync_laptop_desktop&oldid=396458)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Internet applications](/index.php/Category:Internet_applications "Category:Internet applications")

Hidden categories:

*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")
*   [Pages or sections flagged with Template:Style](/index.php/Category:Pages_or_sections_flagged_with_Template:Style "Category:Pages or sections flagged with Template:Style")