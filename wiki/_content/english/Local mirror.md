**Warning:** If you want to create an official mirror see [this page](/index.php/DeveloperWiki:NewMirrors "DeveloperWiki:NewMirrors").

## Contents

*   [1 STOP](#STOP)
*   [2 Local mirror](#Local_mirror)
    *   [2.1 Things to keep in mind:](#Things_to_keep_in_mind:)
    *   [2.2 Server configuration](#Server_configuration)
        *   [2.2.1 Building rsync command](#Building_rsync_command)
        *   [2.2.2 Example script](#Example_script)
        *   [2.2.3 Partial mirroring](#Partial_mirroring)
        *   [2.2.4 Serving](#Serving)
    *   [2.3 Client configuration](#Client_configuration)

## STOP

**Warning:** It is generally frowned upon to create a local mirror due the bandwidth that is required. One of the alternatives will likely fulfill your needs. Please look [Pacman/Tips and tricks#Network shared pacman cache](/index.php/Pacman/Tips_and_tricks#Network_shared_pacman_cache "Pacman/Tips and tricks") for alternatives.

## Local mirror

### Things to keep in mind:

*   Bandwidth is not free for the mirrors. They must pay for all the data they serve you
    *   This still applies although you pay your ISP
    *   A full mirror is over 50GB in size
*   There are many packages that will be downloaded that you will likely never use
*   Mirror operators will much prefer you to download only the packages you need
*   Really please look at the alternatives above

**If you are absolutely certain that a local mirror is the only sensible solution, then follow the pointers below.**

### Server configuration

#### Building rsync command

*   Use the rsync arguments from [DeveloperWiki:NewMirrors](/index.php/DeveloperWiki:NewMirrors "DeveloperWiki:NewMirrors")
*   Select a server from the above article
*   Exclude folder/files you do not want by including `--exclude-from="/path/to/exclude.txt"` in the rsync arguments. Example contents might include:

```
/iso
/project
/staging
/testing
/*-staging
/*-testing
/*-unstable

```

*   All packages reside in the pool directory. Symlinks are then created from pool to core/extra/testing/etc..

Example: `rsync *$rsync_arguments* --exclude-from="/path/to/exclude.txt" *rsync://example.com/* /path/to/destination`

#### Example script

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

Any HTTP server should do. See [Category:Web server](/index.php/Category:Web_server "Category:Web server").

### Client configuration

*   Add the proper Server= variable in /etc/pacman.d/mirrorlist
*   For physical media (such as flash drive) the following can be used: Server = file:///mnt/media/repo/$repo/os/$arch (*where /mnt/media/repo is directory where local mirror located*)