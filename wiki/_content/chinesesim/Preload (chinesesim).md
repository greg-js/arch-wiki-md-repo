预加载的主要作用是让把文件放入RAM中，或者让文件保持在RAM中。这样做的好处是让应用预加载从而更快的打开，因为从内存读取要比从硬盘读取速度更快。虽然这样会使用一部分内存，但不会比应用打开后所需的内存多。所以，预加载最好用于大型的，经常打开的应用，比如 Firefox 和 LibreOffice。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Go-preload](#Go-preload)
    *   [1.1 配置](#配置)
*   [2 Preload](#Preload)
    *   [2.1 安装](#安装)
    *   [2.2 配置](#配置_2)
*   [3 参阅](#参阅)

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

It is advised to run gopreload-prepare after system upgrades to refresh the file lists. For the task, the following batch tool come handy:

```
# gopreload-batch-refresh.sh

```

Just let it run without using the system.

### 配置

The configuration file is located in `/etc/gopreload.conf`

## Preload

**preload** is a program written by Behdad Esfahbod which runs as a [daemon](/index.php/Daemon "Daemon") and records statistics about usage of programs using Markov chains; files of more frequently-used programs are, during a computer's spare time, loaded into memory. This results in faster startup times as less data needs to be fetched from disk.

### 安装

[Install](/index.php/Install "Install") the [preload](https://aur.archlinux.org/packages/preload/) package. You may now [start](/index.php/Daemon "Daemon") the [systemd](/index.php/Systemd "Systemd") service `preload`, and/or enable it in order to start at boot.

### 配置

The configuration file is located in `/etc/preload.conf`, it contains default settings that should be suitable for regular users. The `cycle` option lets you configure how often to ping the preload system to update its model of which applications and libraries to cache.

## 参阅

*   [wikipedia:Preload_(software)](https://en.wikipedia.org/wiki/Preload_(software) "wikipedia:Preload (software)")
*   [Improve boot performance](/index.php/Improve_boot_performance "Improve boot performance")