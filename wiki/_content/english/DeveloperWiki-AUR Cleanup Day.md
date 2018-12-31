## Contents

*   [1 About](#About)
*   [2 Template (Package list)](#Template_(Package_list))
    *   [2.1 Candidates](#Candidates)
    *   [2.2 Possible reasons](#Possible_reasons)
*   [3 Template (TU)](#Template_(TU))
    *   [3.1 Packages to Remove](#Packages_to_Remove)
    *   [3.2 Packages to Keep](#Packages_to_Keep)
    *   [3.3 Possible reasons](#Possible_reasons_2)

## About

AUR Cleanup Day is a bi-yearly event at the 20th of September.

Cleanup suggestions will be looked at sooner if you submit them to the [aur-general mailing list](https://mailman.archlinux.org/mailman/listinfo/). Some guidelines are listed [here](https://wiki.archlinux.org/index.php/AUR#Other_requests).

The AUR has a large number of obsolete packages which could use cleaning up. Examples of packages that may be cleaned up are:

*   Packages that have been renamed or replaced
*   Old and unmaintained developmental (cvs/svn/etc) packages

Post suggestions of packages on the AUR Cleanup Day pages below. Trusted Users will get together and go though the list in a couple of weeks after the event and confirm which packages should be removed.

Join [#archlinux-aur](/index.php/IRC_channel "IRC channel") to collaborate and chat.

## Template (Package list)

### Candidates

Check for the package in the sorted lists below before adding.

```
* [https://aur.archlinux.org/packages.php?ID=NNN packagename] - reason

<--informative separator-->

* [https://aur.archlinux.org/packages.php?ID=NNN packagename] - reason
```

<--Orphaned & out-of-date since before 2016-->

*   Up to page 10 [https://aur.archlinux.org/packages/?O=0&SeB=nd&K=&outdated=on&SB=l&SO=a&PP=50&do_Orphans=Orphans](https://aur.archlinux.org/packages/?O=0&SeB=nd&K=&outdated=on&SB=l&SO=a&PP=50&do_Orphans=Orphans)

<--Should be renamed-->

*   [firefox-extension- packages](https://aur.archlinux.org/packages/?O=0&K=firefox-extension) to `firefox-` - Uniformity with the [firefox-addons group](https://www.archlinux.org/groups/any/firefox-addons/) and similar packages in the AUR

### Possible reasons

*   doesn't work anymore
*   deprecated by [packagename](https://aur.archlinux.org/packages.php?ID=NNNN)
*   obsoleted by [packagename](https://aur.archlinux.org/packages.php?ID=NNNN)
*   replaced by [packagename](https://aur.archlinux.org/packages.php?ID=NNNN)
*   duplicate of [packagename](https://aur.archlinux.org/packages.php?ID=NNNN)
*   project page and sources aren't available
*   "dead" project; it's very old and doesn't work with the latest versions of its dependencies
*   "dead" project and too old to be useful
*   project page and sources aren't available
*   not needed anymore (it's for old PACKAGENAME), broken source link
*   old dev-version, PACKAGENAME project uses git now
*   is it needed in Arch Linux?
*   broken links (see comment by USERNAME)
*   outdated for a long time
*   this one should be renamed
*   deprecated by upstream
*   outdated, orphaned
*   broken links, too old, not maintained
*   included in extra/PACKAGENAME
*   already included in core/PACKAGENAME
*   old beta version, broken source link, replaced by [packagename](https://aur.archlinux.org/packages.php?ID=NNNN)
*   maintainer wrote that it may be deleted
*   dropped upstream
*   depends on [packagename](https://aur.archlinux.org/packages.php?ID=NNNN) and has not been updated for N years...
*   development discontinued, project page deleted and current version doesn't work
*   too old to be useful, broken source link -- hm, what is USERNAME's opinion?
*   this package is no longer needed (see comments)

## Template (TU)

**For editing by TUs only!** The wiki has a history so do not think you can get away with ignoring this... --[Allan](/index.php/User:Allan "User:Allan")

### Packages to Remove

In community:

*   [packagename](https://aur.archlinux.org/packages.php?ID=NNNN) - replaced by PACKAGENAME --[Allan](/index.php/User:Allan "User:Allan")

### Packages to Keep

*   [packagename](https://aur.archlinux.org/packages.php?ID=NNNN) - reason

### Possible reasons

*   It is for compiling old stuff, lets keep it, does not harm
*   Seems to be actively maintained
*   Seems to be actively maintained, no reason to delete
*   Still useful, because ...
*   So this package should maybe be orphaned, no obvious reason to delete it
*   Needed by PACKAGENAME
*   Package has new and active maintainer
*   No reason to delete, actively maintained by USERNAME
*   No, it seems to be down sometimes, but sometimes it works again. Package is maintained and has votes
*   Should be rewritten, not dropped
*   Actively maintained
*   PKGBUILD is maintained and maintainer is active
*   I orphaned the package
*   It's not dead, it only needs some changes to work again
*   Package builds with little tweaking
*   Builds fine with a little patch in pkgrel N