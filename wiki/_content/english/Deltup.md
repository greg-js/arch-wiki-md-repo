Delta updates can save time and size in downloading and updating the system. Packages that are downloaded will be a sort of "diff" of the new package, which will be used to patch the old package into the new package at the end of the download.

## Contents

*   [1 Install](#Install)
*   [2 Configuration](#Configuration)
*   [3 Comparisons](#Comparisons)
*   [4 Disadvantages](#Disadvantages)

## Install

[Install](/index.php/Install "Install") the [xdelta3](https://www.archlinux.org/packages/?name=xdelta3) package. This utility is required in order to apply the binary diffs that delta mirrors provide in addition to full packages.

## Configuration

The official mirrors are not obliged to provide package delta files. Add a new mirror entry to pacman's mirrorlist, choosing a mirror which provides deltas. See [Mirrors#Enabling a specific mirror](/index.php/Mirrors#Enabling_a_specific_mirror "Mirrors") for further direction on this. There are some delta-capable mirrors listed in [Mirrors#Unofficial mirrors](/index.php/Mirrors#Unofficial_mirrors "Mirrors").

Then edit `/etc/pacman.conf` uncommenting the option `UseDelta`:

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

This will instruct pacman to download and apply a package delta where one is advertised in the sync database, and it will apply to a version of the package currently in the local pacman package cache.

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

## Disadvantages

This method isn't fully supported in Arch Linux as opposed to [OpenSuSE](http://www.opensuse.org) or [Gentoo](http://www.gentoo.org) which use this as standard for their update system. Beacuse of this, there are only small number of mirrors supporting deltas.

When a system hasn't been kept fully up-to-date all of the time, then it is possible that there will be no delta available to patch between the old and current versions, but instead patches are only available for one or more versions of the package *in between* the installed and current versions. Thus, the more deltas the mirror provides between historic versions and the current version, the more likely it is that using deltas will reduce the total download size. However, mirrors currently available only host deltas for between 1 and 3 versions before the current. This can reduce the benefit to be seen on a system which not frequently updated.