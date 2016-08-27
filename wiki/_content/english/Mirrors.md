This page is a guide to selecting and configuring your mirrors, and a listing of current available mirrors.

## Contents

*   [1 Official mirrors](#Official_mirrors)
    *   [1.1 IPv6-ready mirrors](#IPv6-ready_mirrors)
*   [2 Enabling a specific mirror](#Enabling_a_specific_mirror)
    *   [2.1 Force pacman to refresh the package lists](#Force_pacman_to_refresh_the_package_lists)
*   [3 Sorting mirrors](#Sorting_mirrors)
    *   [3.1 List by speed](#List_by_speed)
    *   [3.2 Server-side ranking](#Server-side_ranking)
    *   [3.3 List mirrors only for a specific country](#List_mirrors_only_for_a_specific_country)
*   [4 Troubleshooting](#Troubleshooting)
*   [5 Unofficial mirrors](#Unofficial_mirrors)
    *   [5.1 Austria](#Austria)
    *   [5.2 Canada](#Canada)
    *   [5.3 China](#China)
    *   [5.4 France](#France)
    *   [5.5 Germany](#Germany)
    *   [5.6 Indonesia](#Indonesia)
    *   [5.7 Iran](#Iran)
    *   [5.8 Italy](#Italy)
    *   [5.9 Japan](#Japan)
    *   [5.10 Malaysia](#Malaysia)
    *   [5.11 New Zealand](#New_Zealand)
    *   [5.12 Poland](#Poland)
    *   [5.13 Russia](#Russia)
    *   [5.14 South Africa](#South_Africa)
    *   [5.15 Sweden](#Sweden)
    *   [5.16 Thailand](#Thailand)
    *   [5.17 United States](#United_States)
    *   [5.18 Sourceforge (old ISOs)](#Sourceforge_.28old_ISOs.29)

## Official mirrors

The official Arch Linux mirror list is available from the [pacman-mirrorlist](https://www.archlinux.org/packages/?name=pacman-mirrorlist) package. To get an even more up-to-date list of mirrors, use the [Pacman Mirrorlist Generator](https://www.archlinux.org/mirrorlist/) page on the main site.

Check the status of the Arch mirrors by visiting the [Mirror Status](https://www.archlinux.org/mirrors/status/) page. It is recommended to only use mirrors that are up to date, i.e. not out of sync.

If you want your mirror to be added to the official list, see [DeveloperWiki:NewMirrors](/index.php/DeveloperWiki:NewMirrors "DeveloperWiki:NewMirrors"). In the meantime, add it to the [#Unofficial mirrors](#Unofficial_mirrors) list at the end of this page.

### IPv6-ready mirrors

The [Pacman Mirrorlist Generator](https://www.archlinux.org/mirrorlist/?ip_version=6) can also be used to find a list of current IPv6 mirrors.

## Enabling a specific mirror

To enable mirrors, edit `/etc/pacman.d/mirrorlist` and locate your geographic region. Uncomment mirrors you would like to use.

Example:

```
# Any
# Server = ftp://mirrors.kernel.org/archlinux/$repo/os/$arch
**Server = http://mirrors.kernel.org/archlinux/$repo/os/$arch**

```

See [#Sorting mirrors](#Sorting_mirrors) for tools that help choosing mirrors.

**Tip:**

*   Uncomment 5 favorite mirrors and place them at the top of the mirrorlist file. That way it's easy to find them and move them around if the first mirror on the list has problems. It also makes merging mirrorlist updates easier.
*   HTTP mirrors are faster than FTP due to [persistent HTTP connection](https://en.wikipedia.org/wiki/HTTP_persistent_connection "wikipedia:HTTP persistent connection"): with FTP, a new connection to server has to be established each time *pacman* requests a package to be downloaded, which results in a brief pause.

It is also possible to specify mirrors in `/etc/pacman.conf`. For the *[core]* repository, the default setup is:

```
[core]
Include = /etc/pacman.d/mirrorlist

```

To use the *HostEurope* mirror as a default mirror, add it before the `Include` line:

```
[core]
**Server = ftp://ftp.hosteurope.de/mirror/ftp.archlinux.org/core/os/$arch**
Include = /etc/pacman.d/mirrorlist

```

pacman will now try to connect to this mirror first. Proceed to do the same for *[testing]*, *[extra]*, and *[community]*, if applicable.

**Note:** If mirrors have been stated directly in `pacman.conf`, remember to use the same mirror for all repositories. Otherwise packages that are incompatible to each other may be installed, like linux from *[core]* and an older kernel module from *[extra]*.

### Force pacman to refresh the package lists

Mirrors can be out of sync and the package list from the old mirror may not correspond to the package list of the new mirror, even though the dates of the lists may suggest that they do.

After creating/editing `/etc/pacman.d/mirrorlist`, (manually or by using `rankmirrors`) issue the following command:

```
# pacman -Syyu

```

Passing two `--refresh` or `-y` flags forces pacman to refresh all package lists even if they are considered to be up to date. Issuing `pacman -Syyu` *whenever changing to a new mirror* is good practice and will avoid possible issues. See also [Is -Syy safe?](https://bbs.archlinux.org/viewtopic.php?id=163124).

## Sorting mirrors

When downloading packages pacman uses the mirrors in the order they are in `/etc/pacman.d/mirrorlist`. To set a priority to mirrors, the mirrorlist file has to be sorted manually or using a script.

It is not a good idea to just use the fastest mirrors, since the fastest mirrors might be out of sync. Instead, make a list of mirrors sorted by their [speed](#List_by_speed), then remove those from the list that are out of sync according to their [status](https://www.archlinux.org/mirrors/status/).

It is recommended to repeat this process before every system upgrade to keep `/etc/pacman.d/mirrorlist` up to date.

### List by speed

The [pacman](https://www.archlinux.org/packages/?name=pacman) package provides a Bash script, `/usr/bin/rankmirrors`, which can be used to rank the mirrors according to their connection and opening speeds to take advantage of using the fastest local mirror.

Back up the existing `/etc/pacman.d/mirrorlist`:

```
# cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.backup

```

Edit `/etc/pacman.d/mirrorlist.backup` and uncomment mirrors for testing with `rankmirrors`.

Optionally run the following `sed` line to uncomment every mirror:

```
# sed -i 's/^#Server/Server/' /etc/pacman.d/mirrorlist.backup

```

Finally, rank the mirrors. Operand `-n 6` means only output the 6 fastest mirrors:

```
# rankmirrors -n 6 /etc/pacman.d/mirrorlist.backup > /etc/pacman.d/mirrorlist

```

Run `rankmirrors -h` for a list of all the available options.

### Server-side ranking

The official [Pacman Mirrorlist Generator](https://www.archlinux.org/mirrorlist/) provides an easy way to obtain a ranked list of mirrors. Because all ranking is done on a single server that takes multiple factors into account, the amount of load on the mirrors and the clients is significantly lower compared to ranking on each individual client.

There are multiple scripts automating the update of the mirrorlist from the ranking server:

*   [Reflector](/index.php/Reflector "Reflector") retrieves the latest mirrorlist from the [MirrorStatus](https://www.archlinux.org/mirrors/status/) page, filters the most up-to-date mirrors, sorts them by speed and overwrites the `/etc/pacman.d/mirrorlist` file.
*   [update-pacman-mirrorlist](https://aur.archlinux.org/packages/update-pacman-mirrorlist/) is a minimalistic script that downloads a mirrorlist from a specified ranking server defaulting to the official [Pacman Mirrorlist Generator](https://www.archlinux.org/mirrorlist/). It also provides an optional [systemd timer](/index.php/Systemd/Timers "Systemd/Timers") to manage the mirrorlist automatically without intervention.
*   [armrr](https://github.com/Gen2ly/armrr) downloads a ranked mirrorlist for a specific country from the [Pacman Mirrorlist Generator](https://www.archlinux.org/mirrorlist/) and creates a backup of the previous mirrorlist.

### List mirrors only for a specific country

Can be useful to automate update of the mirror list only for a specific countries instead of making a speed test each time. Assumed that `mirrorlist.pacnew` exist, the file creates after installation of the [pacman-mirrorlist](https://www.archlinux.org/packages/?name=pacman-mirrorlist) update.

```
Cnt="China";
awk -v GG="$Cnt" '{if(match($0,GG) != "0")AA="1";if(AA == "1"){if( length($2) != "0"  )print substr($0,2) ;else AA="0"} }' \
 /etc/pacman.d/mirrorlist.pacnew
```

## Troubleshooting

In the unlikely scenario that you are without any configured mirrors and `pacman-mirrorlist` is not installed, run the following command:

```
# curl -o /etc/pacman.d/mirrorlist https://www.archlinux.org/mirrorlist/all/

```

Be sure to uncomment a preferred mirror as described above, then:

```
# pacman -Syu pacman-mirrorlist

```

If you get an error stating that the `$arch` variable is used but not defined, add the following to your `/etc/pacman.conf`:

```
Architecture = x86_64

```

**Note:** You can also use the values `auto` and `i686` for the `Architecture` variable.

## Unofficial mirrors

These mirrors are *not* listed in `/etc/pacman.d/mirrorlist`.

### Austria

*   [http://gd.tuwien.ac.at/opsys/linux/archlinux/](http://gd.tuwien.ac.at/opsys/linux/archlinux/) - *Vienna University of Technology*
*   [ftp://gd.tuwien.ac.at/opsys/linux/archlinux/](ftp://gd.tuwien.ac.at/opsys/linux/archlinux/)

### Canada

*   [https://na.mirrors.coltondrg.com/archlinux/](https://na.mirrors.coltondrg.com/archlinux/)

### China

**Telecom**

*   [http://mirror.bit.edu.cn/archlinux/](http://mirror.bit.edu.cn/archlinux/) - *Beijing Institute of Technology*
*   [http://mirrors.aliyun.com/archlinux/](http://mirrors.aliyun.com/archlinux/) - *Alibaba*

**Unicom**

*   [http://mirrors.sohu.com/archlinux/](http://mirrors.sohu.com/archlinux/)
*   [http://mirrors.yun-idc.com/archlinux/](http://mirrors.yun-idc.com/archlinux/)

**Cernet**

*   [http://mirrors.geekpie.org/archlinux/](http://mirrors.geekpie.org/archlinux/) - *Geek Pie Association @ ShanghaiTech University*
*   [http://ftp.sjtu.edu.cn/archlinux/](http://ftp.sjtu.edu.cn/archlinux/) - *Shanghai Jiaotong University*
*   [http://mirrors.4.tuna.tsinghua.edu.cn/archlinux/](http://mirrors.4.tuna.tsinghua.edu.cn/archlinux/) *(ipv4 only)*
*   [http://mirrors.6.tuna.tsinghua.edu.cn/archlinux/](http://mirrors.6.tuna.tsinghua.edu.cn/archlinux/) *(ipv6 only)*
*   [http://mirror.lzu.edu.cn/archlinux/](http://mirror.lzu.edu.cn/archlinux/) - *Lanzhou University*

### France

*   [http://delta.archlinux.fr/](http://delta.archlinux.fr/) - *With Delta package support. Needs [xdelta3](https://www.archlinux.org/packages/?name=xdelta3) to run.*
*   [https://eu.mirrors.coltondrg.com/archlinux/](https://eu.mirrors.coltondrg.com/archlinux/)

### Germany

*   [http://ftp.u-tx.net/archlinux/](http://ftp.u-tx.net/archlinux/)
*   [ftp://ftp.u-tx.net/archlinux/](ftp://ftp.u-tx.net/archlinux/)

### Indonesia

*   [http://kambing.ui.ac.id/archlinux/](http://kambing.ui.ac.id/archlinux/)

### Iran

*   [http://mirror.yazd.ac.ir/arch/](http://mirror.yazd.ac.ir/arch/)

### Italy

*   [http://mi.mirror.garr.it/mirrors/archlinux/](http://mi.mirror.garr.it/mirrors/archlinux/)

### Japan

*   [http://ftp.nara.wide.ad.jp/pub/Linux/archlinux/](http://ftp.nara.wide.ad.jp/pub/Linux/archlinux/) - *NAra Institute of Science and Technology*
*   [http://ftp.kddilabs.jp/Linux/packages/archlinux/](http://ftp.kddilabs.jp/Linux/packages/archlinux/)
*   [http://srv2.ftp.ne.jp/Linux/packages/archlinux/](http://srv2.ftp.ne.jp/Linux/packages/archlinux/)

### Malaysia

*   [http://mirror.oscc.org.my/archlinux/](http://mirror.oscc.org.my/archlinux/)

### New Zealand

*   [http://mirror.ece.auckland.ac.nz/archlinux/](http://mirror.ece.auckland.ac.nz/archlinux/) *NZ only*

### Poland

*   [ftp://ftp.icm.edu.pl/pub/Linux/dist/archlinux/](ftp://ftp.icm.edu.pl/pub/Linux/dist/archlinux/) - ICM UW
*   [http://ftp.icm.edu.pl/pub/Linux/dist/archlinux/](http://ftp.icm.edu.pl/pub/Linux/dist/archlinux/) - ICM UW
*   rsync://ftp.icm.edu.pl/pub/Linux/dist/archlinux/ - ICM UW

### Russia

*   [http://mirrors.krasinfo.ru/archlinux/](http://mirrors.krasinfo.ru/archlinux/) - *Krasnoyarsk, Classica-Service Ltd*

### South Africa

*   [http://ftp.leg.uct.ac.za/pub/linux/arch/](http://ftp.leg.uct.ac.za/pub/linux/arch/) - *University of Cape Town*
*   [ftp://ftp.leg.uct.ac.za/pub/linux/arch/](ftp://ftp.leg.uct.ac.za/pub/linux/arch/)
*   [http://mirror.ufs.ac.za/archlinux/](http://mirror.ufs.ac.za/archlinux/) - *University of the Free State*
*   [ftp://mirror.ufs.ac.za/os/linux/distros/archlinux/](ftp://mirror.ufs.ac.za/os/linux/distros/archlinux/)
*   [http://archlinux.mirror.ac.za](http://archlinux.mirror.ac.za) - *TENET - Tertiary Education and Research Network of South Africa*
*   [ftp://archlinux.mirror.ac.za](ftp://archlinux.mirror.ac.za)

### Sweden

*   [http://foss.dhyrule.se/linux/archlinux/](http://foss.dhyrule.se/linux/archlinux/)
*   [ftp://foss.dhyrule.se/linux/archlinux/](ftp://foss.dhyrule.se/linux/archlinux/)

### Thailand

*   [http://mirror1.ku.ac.th/archlinux/](http://mirror1.ku.ac.th/archlinux/)

### United States

*   [http://mirror.clarkson.edu/archlinux/](http://mirror.clarkson.edu/archlinux/)
*   [http://mirror.pointysoftware.net/archlinux/](http://mirror.pointysoftware.net/archlinux/)
*   [http://mirror.ziemer.bz/archlinux](http://mirror.ziemer.bz/archlinux)

### Sourceforge (old ISOs)

*   [http://sourceforge.net/projects/archlinux/files/](http://sourceforge.net/projects/archlinux/files/) - *ISO files only; Does not have any releases since 2006\. Use it only for getting older ISOs.*