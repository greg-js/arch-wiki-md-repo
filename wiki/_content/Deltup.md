# Deltup

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Delta updates save time and size in downloading and updating the system. Packages that are downloaded will be a sort of "diff" of the new package, which will be used to patch the old package into the new package at the end of the download.

## Contents

*   [1 Install](#Install)
*   [2 Configuration](#Configuration)
*   [3 Comparisons](#Comparisons)
*   [4 Disadvantage](#Disadvantage)

## Install

[Install](/index.php/Install "Install") [xdelta3](https://www.archlinux.org/packages/?name=xdelta3) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Configuration

Edit `/etc/pacman.d/mirrorlist` and add the proper repository:

 `/etc/pacman.d/mirrorlist` 

```
##
## Arch Linux repository mirrorlist
## Generated on 2011-03-24
##

## Delta Archlinux.fr
Server = http://delta.archlinux.fr/$repo/os/$arch
.....
```

Then edit `/etc/pacman.conf` uncommenting (removing `#`) the option `UseDelta`:

 `/etc/pacman.conf` 

```
.....
# Misc options (all disabled by default)
#UseSyslog
ShowSize
UseDelta
TotalDownload
.....
```

## Comparisons

Check before activating the `UseDelta` option how much we need to download to full update the system.

 `#  pacman -Syu` 

```

 ...

 Total Download Size:   416,89 MB
 Total Installed Size:   1933,56 MB

 Proceed with installation? [Y/n]
```

Choose `n` and not confirm the update. As shown the package to be downloaded now are 416,89 MB.

After enabling delta, check again for the updates available (now the option `UseDelta` is enabled):

 `# pacman -Syu` 

```

 ...

 Total Download Size:   343,15 MB
 Total Installed Size:   1933,56 MB

 Proceed with installation? [Y/n]
```

In this way we do not need to download 416,89 MB of packages but only 343,15 MB, so we obtain a shorter time in the update process.

## Disadvantage

This method isn't fully supported in Arch Linux as opposed to [OpenSuSE](http://www.opensuse.org) or [Gentoo](http://www.gentoo.org) which use this as standard for their update system. In fact the available delta repository are just a few. The results can be much better if delta have more deltup packages between previous versions in the repositories. For example, in the repository the author uses, there is only -1 version of each package.

```
kdeartwork-kscreensaver-4.6.2-1_to_4.6.3-1-x86_64.delta	2011-May-06 22:35:41	301.8K	 application/octet-stream 
kdeartwork-kscreensaver-4.6.3-1-x86_64.pkg.tar.xz	2011-May-06 08:57:57	589.2K	 application/octet-stream

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Deltup&oldid=412061](https://wiki.archlinux.org/index.php?title=Deltup&oldid=412061)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Package management](/index.php/Category:Package_management "Category:Package management")