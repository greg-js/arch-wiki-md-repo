# Introduction

This document outlines the process for Arch Linux package maintainers to add new packages to the official repositories. This article is part of the [DeveloperWiki](/index.php/DeveloperWiki "DeveloperWiki").

# Quick Instructions

**TODO:** Rewrite this section with steps for adding new packages to svn

# The BIG Picture

Generally speaking, new packages are submitted by Archlinux end users to the AUR's [unsupported] collection on [https://aur.archlinux.org/](https://aur.archlinux.org/). From there, one of the [Trusted Users](/index.php/Trusted_Users "Trusted Users") will take the package, test the PKGBUILD locally, fix any errors and make sure it conforms to Arch Linux package guidelines. When the TU has finished testing it, they will place the package in the [community] repo at [ftp://ftp.archlinux.org/community/](ftp://ftp.archlinux.org/community/)

When the package has been placed in the [community] repo, Arch Linux users have access to the package via [pacman](/index.php/Pacman "Pacman") (assuming the user hasn't disabled the [community] repo in **/etc/pacman.conf**). Once the package has lived bug-free in the [community] repo for a while, an Arch Linux package maintainer can elect to adopt the package and follow the procedure outlined above.

Trusted Users are selected users within the Arch Linux user community that show sound Linux knowledge and the ability to produce solid PKGBUILDs. The [community] repo is not officially supported by Arch Linux developers or package maintainers. The TUs are fully responsible for the packages found within it. It is not until a package is adopted into the official Arch Linux repos that the Arch Linux team becomes responsible for the package.