# Local Mirror

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**Warning:** If you want to create an official mirror see [this page](https://wiki.archlinux.org/index.php/DeveloperWiki:NewMirrors).

## Contents

*   [1 STOP](#STOP)
    *   [1.1 Alternatives:](#Alternatives:)
*   [2 Local Mirror](#Local_Mirror)
    *   [2.1 Things to keep in mind:](#Things_to_keep_in_mind:)
    *   [2.2 Server Configuration](#Server_Configuration)
        *   [2.2.1 Building Rsync Command](#Building_Rsync_Command)
        *   [2.2.2 Example Script](#Example_Script)
        *   [2.2.3 Another mirror script using lftp](#Another_mirror_script_using_lftp)
        *   [2.2.4 Partial mirroring](#Partial_mirroring)
        *   [2.2.5 Serving](#Serving)
    *   [2.3 Client Configuration](#Client_Configuration)

## STOP

**Warning:** It is generally frowned upon to create a local mirror due the bandwidth that is required. One of the alternatives will likely fulfill your needs. Please look at the alternatives below.

#### Alternatives:

*   [Network Shared Pacman Cache](/index.php/Network_Shared_Pacman_Cache "Network Shared Pacman Cache")

## Local Mirror

### Things to keep in mind:

*   Bandwidth is not free for the mirrors. They must pay for all the data they serve you
    *   This still applies although you pay your ISP
    *   A full mirror (32+64 bit) is over 41GB in size (as of 2015-01-21)
*   There are many packages that will be downloaded that you will likely never use
*   Mirror operators will much prefer you to download only the packages you need
*   Really please look at the alternatives above

**If you are absolutely certain that a local mirror is the only sensible solution, then follow the pointers below.**

### Server Configuration

#### Building Rsync Command

*   Use the rsync arguments from [DeveloperWiki:NewMirrors](https://wiki.archlinux.org/index.php/DeveloperWiki:NewMirrors)
*   Select a server from the above article
*   Exclude folder/files you do not want by including `--exclude-from="/path/to/exclude.txt"` in the rsync arguments. Example contents might include:

```
iso

#Exclude i686 Packages
*/os/i686
pool/*/*-i686.pkg.tar.xz
pool/*/*-i686.pkg.tar.gz

#Exclude x86_64 Packages
*/os/x86_64
pool/*/*-x86_64.pkg.tar.xz
pool/*/*-x86_64.pkg.tar.gz

```

*   All packages reside in the pool directory. Symlinks are then created from pool to core/extra/testing/etc..
    *   As of 9/21/2010 this migration is not yet complete.
        *   There may be actual packages, instead of symlinks, in ${repo}/os/${arch}
*   Exclude any top-level directories that you do not need

Example: `rsync _$rsync_arguments_ --exclude-from="/path/to/exclude.txt" _rsync://example.com/_ /path/to/destination`

#### Example Script

**Warning:** DO NOT USE THIS SCRIPT UNLESS YOU HAVE READ WARNINGS AT THE START OF THIS ARTICLE

**Warning:** Only use this script to sync Core/Extra/Community! If you need Testing, gnome-unstable or any other repo, use rsync --exclude instead!

Yes, this script is partially broken **ON PURPOSE** to avoid people doing copy-and-paste to create their own mirror. It should be easy to fix if you REALLY want a mirror.

```
#!/bin/bash

#################################################################################################
### It is generally frowned upon to create a local mirror due the bandwidth that is required.
### One of the alternatives will likely fulfill your needs.
### REMEMBER:
###   * Bandwidth is not free for the mirrors. They must pay for all the data they serve you
###       => This still applies although you pay your ISP 
###       => There are many packages that will be downloaded that you will likely never use
###       => Mirror operators will much prefer you to download only the packages you need
###   * Really please look at the alternatives on this page:
###       [https://wiki.archlinux.org/index.php?title=Local_Mirror](https://wiki.archlinux.org/index.php?title=Local_Mirror)
### If you are ABSOLUTELY CERTAIN that a local mirror is the only sensible solution, then this
### script will get you on your way to creating it. 
#################################################################################################

# Configuration
SOURCE='rsync://mirror.example.com/archlinux'
DEST='/srv/mirrors/archlinux'
BW_LIMIT='500'
REPOS='core extra'
RSYNC_OPTS="-rtlHq --delete-after --delay-updates --copy-links --safe-links --max-delete=1000 --bwlimit=${BW_LIMIT} --delete-excluded --exclude=.*"
LCK_FLE='/var/run/repo-sync.lck'

PATH='/usr/bin'

# Make sure only 1 instance runs
if [ -e "$LCK_FLE" ] ; then
	OTHER_PID=$(cat $LCK_FLE)
	echo "Another instance already running: $OTHER_PID"
	exit 1
fi
echo $$ > "$LCK_FLE"

for REPO in $REPOS ; do
	echo "Syncing $REPO"
	rsync $RSYNC_OPTS ${SOURCE}/${REPO} ${DEST}
done

# Cleanup
rm -f "$LCK_FLE"

exit 0

```

#### Another mirror script using lftp

lftp can mirror via several different protocols: ftp, http, etc. It also restarts on error, and can run in the background. Put this into your $PATH for an easy way to mirror that continues if you log out.

```
#!/usr/bin/lftp -f
lcd /local/path/to/your/mirror
open ftp.archlinux.org (or whatever your favorite mirror is)
# Use 'cd' to change into the proper directory on the mirror, if necessary.
mirror -cve -x '.*i686.*' core &
mirror -cve -x '.*i686.*' extra &
mirror -cve -x '.*i686.*' community &
mirror -cve -x '.*i686.*' multilib &
lcd pool
cd pool
mirror -cve -x '.*i686.*' community &
mirror -cve -x '.*i686.*' packages &

```

if you want to see the current status of the mirror. open lftp on terminal and type 'attach <PID>'

#### Partial mirroring

Mirroring only some repositories is definitely not easy, due to the centralization of most packages in `pool/`. See [this blog post](http://blog.invokk.net/2012/01/mirroring-only-some-repositories-of-archlinux/) for an attempt at writing a script for this task.

If you can install all of the packages you wish to mirror, you can install them and set up an http server to share your package cache. An example lighttpd.conf would be:

```
   # This is a minimal example config
   # See /usr/share/doc/lighttpd
   # and [http://redmine.lighttpd.net/projects/lighttpd/wiki/Docs:ConfigurationOptions](http://redmine.lighttpd.net/projects/lighttpd/wiki/Docs:ConfigurationOptions)

   server.port             = 80
   server.username         = "http"
   server.groupname        = "http"
   server.document-root    = "/var/cache/pacman/pkg"
   server.errorlog         = "/var/log/lighttpd/error.log"
   dir-listing.activate    = "enable"
   index-file.names        = ( "index.html" )
   mimetype.assign         = ( ".html" => "text/html", ".txt" => "text/plain", ".jpg" => "image/jpeg", ".png" => "image/png", "" => "application/octet-stream" )

```

Then to update your partial mirror, simply execute pacman -Syu. Note this doesn't work for multiple architectures.

#### Serving

*   HTTP (LAN)
    *   [LAMP](/index.php/LAMP "LAMP")
    *   [Lighttpd](/index.php/Lighttpd "Lighttpd")
*   FTP (LAN)
    *   [vsftpd](/index.php/Vsftpd "Vsftpd")
*   Physical Media
    *   Flash Drive
    *   External HD

### Client Configuration

*   Add the proper Server= variable in /etc/pacman.d/mirrorlist
*   For physical media (such as flash drive) the following can be used: Server = file:///mnt/media/repo/$repo/os/$arch (_where /mnt/media/repo is directory where local mirror located_)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Local_Mirror&oldid=379973](https://wiki.archlinux.org/index.php?title=Local_Mirror&oldid=379973)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Package management](/index.php/Category:Package_management "Category:Package management")