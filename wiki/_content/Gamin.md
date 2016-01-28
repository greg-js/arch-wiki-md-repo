# Gamin

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [File manager functionality](/index.php/File_manager_functionality "File manager functionality").**

**Notes:** May be too short for a separate article. (Discuss in [Talk:File manager functionality#Udiskie](https://wiki.archlinux.org/index.php/Talk:File_manager_functionality#Udiskie))

[Gamin](https://en.wikipedia.org/wiki/Gamin "wikipedia:Gamin") is a file and directory monitoring system defined to be a subset of the FAM (File Alteration Monitor) system. It is a service provided by a library which allows for the detection of modification to a file or directory.

Gamin re-implements the [FAM](/index.php/FAM "FAM") specification with [inotify](https://en.wikipedia.org/wiki/inotify "wikipedia:inotify"). It is newer and more actively maintained than FAM, maintains compatibility with FAM and can replace it in almost every case. It is a [GNOME](/index.php/GNOME "GNOME") project, but does not have GNOME dependencies.

## Installation

If FAM is installed, first [disable](/index.php/Disable "Disable") `fam.service`; then remove the [fam](https://aur.archlinux.org/packages/fam/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/fam)]</sup> package, ignoring any reverse dependencies:

```
# pacman -Rdd fam

```

Now you can install the [gamin](https://www.archlinux.org/packages/?name=gamin) package.

## External links

*   [FAM, Gamin and inotify](http://www.noah.org/wiki/FAM,_Gamin,_inotify)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Gamin&oldid=399042](https://wiki.archlinux.org/index.php?title=Gamin&oldid=399042)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [File systems](/index.php/Category:File_systems "Category:File systems")

Hidden categories:

*   [Pages or sections flagged with Template:Merge](/index.php/Category:Pages_or_sections_flagged_with_Template:Merge "Category:Pages or sections flagged with Template:Merge")
*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")