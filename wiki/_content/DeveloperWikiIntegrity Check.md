# DeveloperWiki:Integrity Check

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

## Contents

*   [1 Introduction](#Introduction)
*   [2 Bug Reports](#Bug_Reports)
    *   [2.1 depends](#depends)
    *   [2.2 NOTE : PKGBUILDs calling pacman -Q](#NOTE_:_PKGBUILDs_calling_pacman_-Q)

# Introduction

A tool was written to check the integrity of official pkgbuilds (core, extra and community repository) :

[https://projects.archlinux.org/?p=dbscripts.git;a=tree;f=cron-jobs/check_archlinux;hb=HEAD](https://projects.archlinux.org/?p=dbscripts.git;a=tree;f=cron-jobs/check_archlinux;hb=HEAD)

This tool is run automatically every Friday and the results for core and extra are sent to the [arch-dev-public ML](https://www.archlinux.org/mailman/listinfo/arch-dev-public), while the results for community are sent to the [aur-general ML](https://www.archlinux.org/mailman/listinfo/aur-general).

Example of the run on March 13th :

*   [Integrity Check i686 of core,extra](https://www.archlinux.org/pipermail/arch-dev-public/2009-March/010715.html)
*   [Integrity Check x86_64 of core,extra](https://www.archlinux.org/pipermail/arch-dev-public/2009-March/010716.html)
*   [Integrity Check i686 of community](https://www.archlinux.org/pipermail/aur-general/2009-March/004054.html)
*   [Integrity Check x86_64 of community](https://www.archlinux.org/pipermail/aur-general/2009-March/004055.html)

The purpose of this page is to maintain a list of the currently reported problems, with links to the [Arch Linux Bugtracker](https://bugs.archlinux.org/). This will help to detect the new problems which need to be reported.

# Bug Reports

## depends

*   extra/archboot - missing dependencies seem to be a feature

## NOTE : PKGBUILDs calling pacman -Q

The following PKGBUILDs call _pacman -Q_, so the result depends on the system where the PKGBUILD is parsed:

_find /var/abs -name PKGBUILD | xargs grep 'pacman.*-Q' | sed 's#/var/abs/# #'_

```
 community/sk1/PKGBUILD:  local _tclver=`pacman -Q tcl`
 community/open-vm-tools-modules/PKGBUILD:_kernver=`pacman -Q kernel26 | cut -d . -f 3 | cut -f 1 -d -`
 community/openmotif/PKGBUILD:_automakever=`pacman -Q automake | cut -f 2 -d \  | cut -f 1 -d -`
 community/qc-usb-messenger/PKGBUILD:_kernver=`pacman -Q kernel26 | cut -d . -f 3 | cut -f 1 -d -`
 community/cdfs/PKGBUILD:_kernver=`pacman -Q kernel26 | cut -d . -f 3 | cut -f 1 -d -`
 community/selinux-pam/PKGBUILD:provides=("pam=`pacman -Q pam | cut -f 2 -d \  | cut -f 1 -d -`")
 community/whitebox/PKGBUILD:  _automake_ver=`pacman -Q automake | cut -f 2 -d \  | cut -f 1 -d -`
 extra/kde-meta/PKGBUILD:              for j in $(pacman -Qgq ${_metaname} | sort -u); do
 extra/sbackup/PKGBUILD:  sed -i -e "s/dpkg --get-selections/pacman -Q/" sbackupd.py

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=DeveloperWiki:Integrity_Check&oldid=383073](https://wiki.archlinux.org/index.php?title=DeveloperWiki:Integrity_Check&oldid=383073)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Package development](/index.php/Category:Package_development "Category:Package development")