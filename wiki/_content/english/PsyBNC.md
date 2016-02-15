## Installing psyBNC

[psybnc](https://aur.archlinux.org/packages/psybnc/) is available in the [AUR](/index.php/AUR "AUR").

## Post-Install

After you have installed psybnc you must run make menuconfig.

```
cd /usr/bin/psybnc
make menuconfig
```

This will spawn the psybnc configure program which requires ncurses. If you do not have ncurses use make menuconfig-curses. This will create a valid psybnc.conf. To use the default settings just hit exit as soon as it opens.

It is also suggested that you chown everything in /usr/bin/psybnc/ to the user that you will use to run psybnc.

If you would like to create psybnc.conf manually (or for more information about configuring psybnc), you may find [the official psybnc help](http://psybnc.at/help.html) and [LunarShells.com psybnc Tutorial](http://www.lunarshells.com/install_psybnc.php#setup) helpful.