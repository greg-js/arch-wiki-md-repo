[PsyBNC](http://www.psybnc.at/) is a multi-user [IRC-Bouncer](https://en.wikipedia.org/wiki/BNC_(software) "w:BNC (software)") with many features.

## Installation

[Install](/index.php/Install "Install") [psybnc](https://aur.archlinux.org/packages/psybnc/).

## Configuration

After you have installed psybnc you must run make menuconfig.

```
cd /usr/bin/psybnc
make menuconfig

```

This will spawn the psybnc configure program which requires [ncurses](https://www.archlinux.org/packages/?name=ncurses). If it is not available, `make menuconfig-curses` is an alternative. Both will create a `/usr/share/psybnc/psybnc.conf` file. To use the default settings just hit exit as soon as it opens.

It is also suggested that you [chown](/index.php/Chown "Chown") everything in the `/usr/bin/psybnc` path to the user that will use to run psybnc.

If you would like to create a `psybnc.conf` manually (or for more information about configuring psybnc), you may find [the official psybnc help](http://psybnc.at/help.html) and [LunarShells.com psybnc Tutorial](http://www.lunarshells.com/install_psybnc.php#setup) helpful.