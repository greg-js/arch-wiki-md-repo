Powerpill is a Pacman wrapper that uses parallel and segmented downloading to try to speed up downloads for Pacman. Internally it uses Aria2 and Reflector to achieve this. Powerpill can also use Rsync for official mirrors that support it. This can be efficient for users who already use full bandwidth when downloading from a single mirror. [Pacserve](/index.php/Pacserve "Pacserve") is also supported via the configuration file and will be used before downloading from external mirrors. Example: One wants to update and issues a *pacman -Syu* which returns a list of 20 packages that are available for update totally 200 megs. If the user downloads them via pacman, they will come down one-at-a-time. If the user downloads them via powerpill, they will come down simultaneously in many cases several times faster (depending on one's connection speed, the availability of packages on servers, and speed from server/load, etc.)

A test of pacman vs. powerpill on one system revealed a 4x speed up in the above scenario where the pacman downloads averages 300 kB/sec and the powerpill downloads averaged 1.2 MB/sec.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Using Reflector](#Using_Reflector)
*   [4 Using rsync](#Using_rsync)
*   [5 Basic usage](#Basic_usage)
    *   [5.1 System updating](#System_updating)
    *   [5.2 Installation of packages](#Installation_of_packages)
*   [6 Troubleshooting](#Troubleshooting)
*   [7 See also](#See_also)

## Installation

You can get it from [AUR](/index.php/AUR "AUR") [powerpill](https://aur.archlinux.org/packages/powerpill/) or directly from [Xyne's repository](http://xyne.archlinux.ca/repos/).

## Configuration

Powerpill has a single configure file `/etc/powerpill/powerpill.json` you can edit to your liking. Refer to the *powerpill.json* man page for details.

## Using Reflector

By default, Powerpill is configured to use [Reflector](/index.php/Reflector "Reflector") to retrieve the current list of mirrors from the Arch Linux server's web API and use them for parallel downloads. This is to make sure that there are enough servers in the list for significant speed improvements.

## Using rsync

Rsync support is available for some mirrors. When enabled, database synchronizations (`pacman -Sy`) and other operations may be much faster because a single connection is used. The *rsync* protocol itself also speeds up update checks and sometimes file transfers.

To find a suitable mirror with *rsync* support, use *reflector*:

```
$ reflector -p rsync

```

Alternatively, you can use this to filter the fastest *n* number of servers (option `-f`) as well as the *m* number of most recently updated servers (option `-l`):

```
$ reflector -p rsync -f *n* -l *m*

```

Select the mirror(s) you want to use. The `-c` option may also be used to filter by your nationality (`reflector --list-countries` to see a complete list, use quotes around the name, and this is case-sensitive!). Once done, edit `/etc/powerpill/powerpill.json`, scroll down to the *rsync* section, and add as many servers as you would like to the server field.

After that, all official database and packages will be downloaded from the *rsync* server whenever possible.

## Basic usage

For most operations, *powerpill* works just like pacman since it is a wrapper script for *pacman*.

### System updating

To update your system (sync and update installed packages) using powerpill, simply pass the `-Syu` options to it as you would with *pacman*:

```
# powerpill -Syu

```

### Installation of packages

To install a package and its deps, simply use powerpill with the `-S` option as you would with *pacman*:

```
# powerpill -S *package*

```

You may also install multiple packages with it the same way you would with *pacman*:

```
# powerpill -S *package1* *package2* *package3*

```

## Troubleshooting

In case you get an [err] for <repo>.db.sig files:

```
   b5d7d7|ERR |       0B/s|/var/lib/pacman/sync/extra.db.sig
   899e91|ERR |       0B/s|/var/lib/pacman/sync/multilib.db.sig
   8fcc32|ERR |       0B/s|/var/lib/pacman/sync/core.db.sig
   85eb3d|ERR |       0B/s|/var/lib/pacman/sync/community.db.sig

```

It is because signature files are missing for that repo and you have not set:

```
   SigLevel = PackageRequired

```

explicity in /etc/pacman.conf as explained in this post [Arch forum post](https://bbs.archlinux.org/viewtopic.php?pid=1254940#p1254940)

## See also

*   [Powerpill](http://xyne.archlinux.ca/projects/powerpill/) - official project page
*   [powerpill reborn](https://bbs.archlinux.org/viewtopic.php?id=153818) - powerpill is back :)