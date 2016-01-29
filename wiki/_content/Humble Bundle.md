# Humble Bundle

The [Humble Bundle](https://humblebundle.com) is a platform to sell collections of games (or "bundles") at a price determined by the purchaser. The website also maintains a storefront for traditional purchases.

## Linux Support

Many of the titles offered on the platform include Linux support, often distributing .debs for Debian/Ubuntu and .tar.gz archives for 'generic' Linux distribution. While it is certainly possible to extract and run the .tar.gz archives directly the game could fail to run due to missing dependencies. One could easily utilise [AUR](/index.php/AUR "AUR") packages for proper dependency handling and desktop integration. These AUR package names typically include the '-hib' suffix to denote that it expects sources from the Humble Bundle storefront.

## PKGBUILD Installation

One must download the packages from Humble Bundle's website in order for the PKGBUILD to build. There are a few ways to achieve this:

*   Manual: view the PKGBUILD and download the file it expects from humblebundle.com to your build directory. If using an [AUR helper](/index.php/AUR_helper "AUR helper"), the build directory will be located in a subdirectory of /tmp by default.

*   `hib:// DLAGENT`: by creating a `DLAGENT` in [makepkg](/index.php/Makepkg "Makepkg")'s configuration file, the process of giving the PKGBUILD the game files is entirely automated. The recommended package for such a scenario is [hib-dlagent](https://aur.archlinux.org/packages/hib-dlagent), available in the AUR.

After installing a dlagent helper, associate _hib://_ as a valid dlagent in _/etc/makepkg.conf_:

```
hib::/usr/bin/hib-dlagent -u USER-EMAIL -o %o %u

```

When set to download a package from Humble Bundle, your password will need to be supplied. If complete automation is desired one could include the password:

```
hib::/usr/bin/hib-dlagent -u USER-EMAIL -p PASSWORD -o %o %u

```

**Warning:** Be aware that any user on the system can read this file. This could expose your password.

For a per-user setup, the following could be added to _~/.makepkg.conf_:

```
DLAGENT+=('hib::/usr/bin/hib-dlagent -u USER-EMAIL -p PASSWORD -o %o %u')

```

Now installation of Humble Bundle games will be a simple installation command away (provided the associated PKGBUILD supports the _hib://_ scheme).

**Warning:** Since AUR automators will download files to the /tmp directory excessively large game files will likely cause /tmp to run out of room. The manual method is best for very large downloads.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Humble_Bundle&oldid=413439](https://wiki.archlinux.org/index.php?title=Humble_Bundle&oldid=413439)"