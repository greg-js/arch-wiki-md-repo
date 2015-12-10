# PsyBNC

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:PsyBNC#](https://wiki.archlinux.org/index.php/Talk:PsyBNC))

## Installing psyBNC

[psybnc](https://aur.archlinux.org/packages/psybnc/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/psybnc)]</sup> is available in the [AUR](/index.php/AUR "AUR").

## Post-Install

After you have installed psybnc you must run make menuconfig.

```
cd /usr/bin/psybnc
make menuconfig
```

This will spawn the psybnc configure program which requires ncurses. If you do not have ncurses use make menuconfig-curses. This will create a valid psybnc.conf. To use the default settings just hit exit as soon as it opens.

It is also suggested that you chown everything in /usr/bin/psybnc/ to the user that you will use to run psybnc.

If you would like to create psybnc.conf manually (or for more information about configuring psybnc), you may find [the official psybnc help](http://psybnc.at/help.html) and [LunarShells.com psybnc Tutorial](http://www.lunarshells.com/install_psybnc.php#setup) helpful.

Retrieved from "[https://wiki.archlinux.org/index.php?title=PsyBNC&oldid=392588](https://wiki.archlinux.org/index.php?title=PsyBNC&oldid=392588)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Internet Relay Chat](/index.php/Category:Internet_Relay_Chat "Category:Internet Relay Chat")