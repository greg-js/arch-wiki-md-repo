Related articles

*   [Unofficial mirrors](/index.php/Unofficial_mirrors "Unofficial mirrors")
*   [pacman](/index.php/Pacman "Pacman")

This page is a guide to selecting and configuring your mirrors, and a listing of current available mirrors.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Official mirrors](#Official_mirrors)
    *   [1.1 IPv6-ready mirrors](#IPv6-ready_mirrors)
*   [2 Enabling a specific mirror](#Enabling_a_specific_mirror)
    *   [2.1 Force pacman to refresh the package lists](#Force_pacman_to_refresh_the_package_lists)
*   [3 Sorting mirrors](#Sorting_mirrors)
    *   [3.1 List by speed](#List_by_speed)
        *   [3.1.1 Ranking an existing mirror list](#Ranking_an_existing_mirror_list)
        *   [3.1.2 Fetching and ranking a live mirror list](#Fetching_and_ranking_a_live_mirror_list)
    *   [3.2 Server-side ranking](#Server-side_ranking)
*   [4 Troubleshooting](#Troubleshooting)
*   [5 See also](#See_also)

## Official mirrors

The official Arch Linux mirror list is available from the [pacman-mirrorlist](https://www.archlinux.org/packages/?name=pacman-mirrorlist) package. To get an even more up-to-date list of mirrors, use the [Pacman Mirrorlist Generator](https://www.archlinux.org/mirrorlist/) page on the main site.

Check the status of the Arch mirrors by visiting the [Mirror Status](https://www.archlinux.org/mirrors/status/) page. It is recommended to only use mirrors that are up to date, i.e. not out of sync.

If you want your mirror to be added to the official list, see [DeveloperWiki:NewMirrors](/index.php/DeveloperWiki:NewMirrors "DeveloperWiki:NewMirrors"). In the meantime, add it to the [Unofficial mirrors](/index.php/Unofficial_mirrors "Unofficial mirrors") article.

### IPv6-ready mirrors

The [Pacman Mirrorlist Generator](https://www.archlinux.org/mirrorlist/?ip_version=6) can also be used to find a list of current IPv6 mirrors.

## Enabling a specific mirror

To enable mirrors, edit `/etc/pacman.d/mirrorlist` and locate your geographic region. Uncomment mirrors you would like to use.

Example:

```
# Any
# Server = http://mirrors.kernel.org/archlinux/$repo/os/$arch
**Server = https://mirrors.kernel.org/archlinux/$repo/os/$arch**

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
**Server = http://ftp.hosteurope.de/mirror/ftp.archlinux.org/core/os/$arch**
Include = /etc/pacman.d/mirrorlist

```

pacman will now try to connect to this mirror first. Proceed to do the same for *[testing]*, *[extra]*, and *[community]*, if applicable.

**Note:** If mirrors have been stated directly in `pacman.conf`, remember to use the same mirror for all repositories. Otherwise packages that are incompatible to each other may be installed, like linux from *[core]* and an older kernel module from *[extra]*.

### Force pacman to refresh the package lists

Mirrors can be out of sync and the package list from the old mirror may not correspond to the package list of the new mirror, even though the dates of the lists may suggest that they do.

After creating/editing `/etc/pacman.d/mirrorlist`, issue the following command:

```
# pacman -Syyu

```

Passing two `--refresh`/`-y` flags forces pacman to refresh all package lists even if they are considered to be up to date. Issuing `pacman -Syyu` is an unnecessary waste of bandwidth in most cases, but can sometimes fix issues when switching from a broken mirror to a working mirror. See also [Is -Syy safe?](https://bbs.archlinux.org/viewtopic.php?id=163124).

**Warning:** In most cases if you force refresh the pacman database, you will want to force downgrade any potentially too-new packages to correspond to the versions offered by the new mirror. This prevents issues where packages are inconsistently upgraded, leading to a partial update.
```
# pacman -Syyuu

```

This is not necessary when using timestamps to ensure the mirrors are only upgraded.

## Sorting mirrors

When downloading packages, pacman uses the mirrors in the order they are listed in `/etc/pacman.d/mirrorlist`. The order servers appear in the list sets their priority.

It is not optimal to only rank mirrors based on speed since the fastest servers might be out-of-sync. Instead, make a list of mirrors sorted by their [speed](#List_by_speed), then remove those from the list that are out of sync according to their [status](https://www.archlinux.org/mirrors/status/).

It is recommended to repeat this process before every system upgrade to keep the list of mirrors up-to-date.

### List by speed

#### Ranking an existing mirror list

The [pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib) package provides a Bash script, `/usr/bin/rankmirrors`, which can be used to rank the mirrors according to their connection and opening speeds to take advantage of using the fastest local mirror.

Back up the existing `/etc/pacman.d/mirrorlist`:

```
# cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.backup

```

To prepare `mirrorlist.backup` for ranking with *rankmirrors*, the following actions can be carried out:

*   Edit `mirrorlist.backup` and uncomment the servers to be tested

*   If the servers in the file are grouped by country, one can extract all the servers of a specific country by using: `$ awk '/^## *Country Name*$/{f=1}f==0{next}/^$/{exit}{print substr($0, 2)}' /etc/pacman.d/mirrorlist.backup` 

*   To uncomment every mirror, run the following `sed` line: `# sed -i 's/^#Server/Server/' /etc/pacman.d/mirrorlist.backup` 

Finally, rank the mirrors, here with the operand `-n 6` to only output the 6 fastest mirrors:

```
# rankmirrors -n 6 /etc/pacman.d/mirrorlist.backup > /etc/pacman.d/mirrorlist

```

#### Fetching and ranking a live mirror list

In order to start with a shortlist of up-to-date mirrors based in some countries and feed it to *rankmirrors* one can fetch the list from the *Pacman Mirrorlist Generator*. The command below pulls the up-to-date mirrors in either *France* or the *United Kingdom* which support the *https* protocol, it uncomments the servers in the list and then ranks them and outputs the 5 fastest.

```
$ curl -s "[https://www.archlinux.org/mirrorlist/?country=FR&country=GB&protocol=https&use_mirror_status=on](https://www.archlinux.org/mirrorlist/?country=FR&country=GB&protocol=https&use_mirror_status=on)" | sed -e 's/^#Server/Server/' -e '/^#/d' | rankmirrors -n 5 -

```

**Tip:** This procedure can be done interactively by navigating to `[https://www.archlinux.org/mirrorlist](https://www.archlinux.org/mirrorlist)` with any text-based browser, for example [elinks(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/elinks.1).

### Server-side ranking

The official [Pacman Mirrorlist Generator](https://www.archlinux.org/mirrorlist/) provides an easy way to obtain a ranked list of mirrors. Because all ranking is done on a single server that takes multiple factors into account, the amount of load on the mirrors and the clients is significantly lower compared to ranking on each individual client.

Another popular alternative is the following tool:

**[Reflector](/index.php/Reflector "Reflector")** — Retrieves the latest mirrorlist from the [MirrorStatus](https://www.archlinux.org/mirrors/status/) page, filters and sorts them by speed and overwrites `/etc/pacman.d/mirrorlist`

	[https://xyne.archlinux.ca/projects/reflector/](https://xyne.archlinux.ca/projects/reflector/) || [reflector](https://www.archlinux.org/packages/?name=reflector)

## Troubleshooting

In the unlikely scenario that you are without any configured mirrors and `pacman-mirrorlist` is not installed, run the following command:

```
# curl -o /etc/pacman.d/mirrorlist https://www.archlinux.org/mirrorlist/all/

```

Be sure to uncomment a preferred mirror as described above, then:

```
# pacman -Syu pacman-mirrorlist

```

## See also

*   [GitHub archweb mirrorlist.py](https://github.com/archlinux/archweb/blob/master/mirrors/views/mirrorlist.py) - source code of the archweb mirrorlist generator