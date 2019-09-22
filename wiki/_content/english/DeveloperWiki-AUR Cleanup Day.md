<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 About](#About)
*   [2 Template (Package list)](#Template_(Package_list))
    *   [2.1 Candidates](#Candidates)
    *   [2.2 Possible reasons](#Possible_reasons)
*   [3 Template (TU)](#Template_(TU))
    *   [3.1 Packages to Remove](#Packages_to_Remove)
    *   [3.2 Packages to Keep](#Packages_to_Keep)
    *   [3.3 Possible reasons](#Possible_reasons_2)

## About

AUR Cleanup Day is a bi-yearly event on the 20th of September. The next one will be in 2019.

The [AUR](/index.php/AUR "AUR") has a large number of obsolete packages which could use cleaning up. Post suggestions of packages below, submit them to the [aur-general mailing list](https://mailman.archlinux.org/mailman/listinfo/), or file [requests](/index.php/AUR_submission_guidelines#Requests "AUR submission guidelines") directly. [Trusted Users](/index.php/Trusted_Users "Trusted Users") will get together and confirm which packages should be removed.

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
*   old dev-version (cvs/svn/etc), PACKAGENAME project uses Git now
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