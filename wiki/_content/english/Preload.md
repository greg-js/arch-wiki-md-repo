Preloading is the action of putting and keeping target files into the RAM. The benefit is that preloaded applications start more quickly because reading from the RAM is always quicker than from the hard drive. However, part of your RAM will be dedicated to this task, but no more than if you kept the application open. Therefore preloading is best used with large and often-used applications like Firefox and LibreOffice.

## Contents

*   [1 Go-preload](#Go-preload)
*   [2 Preload](#Preload)
    *   [2.1 Installation](#Installation)
    *   [2.2 Configuration](#Configuration)
*   [3 See also](#See_also)

## Go-preload

[gopreload-git](https://aur.archlinux.org/packages/gopreload-git/) is a small daemon created in the [Gentoo forum](https://forums.gentoo.org/viewtopic-t-622085-highlight-preload.html). To use it, first run this command in a terminal for each program you want to preload at boot:

```
# gopreload-prepare *program*

```

For regular users, take ownership of `/usr/share/gopreload/enabled` and `/usr/share/gopreload/disabled`

```
# chown username:users /usr/share/gopreload/enabled /usr/share/gopreload/disabled

```

and then gopreload each program you want to preload:

```
$ gopreload-prepare *program*

```

Then, as instructed, press Enter when the program is fully loaded. This will add a list of files needed by the program in `/usr/share/gopreload/enabled`. To load all lists at boot, [enable](/index.php/Enable "Enable") the systemd service file `gopreload.service`.

To disable the loading of a program, remove the appropriate list in `/usr/share/gopreload/enabled` or move it to `/usr/share/gopreload/disabled`.

## Preload

**preload** is a program written by Behdad Esfahbod which runs as a [daemon](/index.php/Daemon "Daemon") and records statistics about usage of programs using Markov chains; files of more frequently-used programs are, during a computer's spare time, loaded into memory. This results in faster startup times as less data needs to be fetched from disk. *preload* is often paired with [prelink](/index.php/Prelink "Prelink").

### Installation

[Install](/index.php/Install "Install") the [preload](https://aur.archlinux.org/packages/preload/) package. You may now [start](/index.php/Daemon "Daemon") the [systemd](/index.php/Systemd "Systemd") service `preload`, and/or enable it in order to start at boot.

### Configuration

The configuration file is located in `/etc/preload.conf`, it contains default settings that should be suitable for regular users. The `cycle` option lets you configure how often to ping the preload system to update its model of which applications and libraries to cache.

## See also

*   [http://en.wikipedia.org/wiki/Preload_(software)](http://en.wikipedia.org/wiki/Preload_(software))
*   [http://techthrob.com/2009/03/02/drastically-speed-up-your-linux-system-with-preload/](http://techthrob.com/2009/03/02/drastically-speed-up-your-linux-system-with-preload/)
*   [Improve boot performance](/index.php/Improve_boot_performance "Improve boot performance")