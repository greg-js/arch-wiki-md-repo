# Stata

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

STATA is a general-purpose statistical software package for *nix, Windows and Mac. In the following you'll be presented with how to install STATA and the needed libraries.

## Contents

*   [1 Needed libraries](#Needed_libraries)
*   [2 Installing Stata](#Installing_Stata)
*   [3 Tips and tricks](#Tips_and_tricks)
*   [4 Troubleshooting](#Troubleshooting)

## Needed libraries

You need to install a series of libraries to run Stata. Stata uses the GTK+ framework.

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** [libgtksourceviewmm](https://aur.archlinux.org/packages/libgtksourceviewmm/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/libgtksourceviewmm)]</sup> has no package() function and outdated depends. (Discuss in [Talk:Stata#](https://wiki.archlinux.org/index.php/Talk:Stata))

If you use GNOME, [install](/index.php/AUR "AUR") [libgtksourceviewmm](https://aur.archlinux.org/packages/libgtksourceviewmm/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/libgtksourceviewmm)]</sup> and [libgnomeprint](https://aur.archlinux.org/packages/libgnomeprint/)<sup><small>AUR</small></sup>.

## Installing Stata

After you have installed these packages, you need to insert your STATA DVD and mount it.

If you have been provided an ISO rather than a physical DVD you can mount it with the following command

```
# mount -o loop /path/to/file.iso /mnt

```

If you have been provided a DVD and it is not automatically mounted, you can use the following command to mount it to `/mnt`

```
# mount -t iso9660 -o ro /dev/cdrom /mnt

```

You then need to create a directory for Stata. Stata recommends putting it under `/usr/local/`. For example:

```
# mkdir /usr/local/stata12

```

Once you have created the directory, change into it:

```
$ cd /usr/local/stata12

```

and run the installer from the directory you mounted the CD into (`/mnt` in this guide):

```
# /mnt/installer

```

Follow the instructions and you will end up with Stata installed.

After you have installed Stata, change the permissions on `/usr/local/stata12` so you can execute it as a normal user:

```
# chmod -R 755 /usr/local/stata12

```

## Tips and tricks

To add Stata to your path, add the following to the end of your path in your [bashrc](/index.php/Bashrc "Bashrc"):

 `~/.bashrc` 

```
PATH=$PATH:/usr/local/stata12/

```

## Troubleshooting

Stata 12 and 13 at least were built on older versions of libpng and zlib. Thus, icons will be missing when launching Xstata, the graphical interface. The workaround is **NOT** to downgrade your system's libraries, but rather to follow the advice given by StataCorp's technical department [here](http://www.statalist.org/forums/forum/general-stata-discussion/general/2199-linux-stata-bug-libpng-on-newer-opensuse-possibly-other-distributions). It involves compiling the older versions of libpng and zlib and putting them in a folder that your system will not interact with. Then a wrapper for Stata needs to be made to reference these libraries. These steps have been automated by a script on bitbucket, located [here](https://bitbucket.org/vilhuberl/stata-png-fix).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Stata&oldid=402167](https://wiki.archlinux.org/index.php?title=Stata&oldid=402167)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Mathematics and science](/index.php/Category:Mathematics_and_science "Category:Mathematics and science")