# pacman/Tips and tricks

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [pacman](/index.php/Pacman "Pacman")
*   [Mirrors](/index.php/Mirrors "Mirrors")
*   [Creating packages](/index.php/Creating_packages "Creating packages")

See [pacman](/index.php/Pacman "Pacman") for the main article.

For general methods to improve the flexibility of the provided tips or pacman itself, see [Core utilities](/index.php/Core_utilities "Core utilities") and [Bash](/index.php/Bash "Bash").

## Contents

*   [1 Cosmetic and convenience](#Cosmetic_and_convenience)
    *   [1.1 Color output](#Color_output)
    *   [1.2 Operations and Bash syntax](#Operations_and_Bash_syntax)
    *   [1.3 Graphical front-ends](#Graphical_front-ends)
    *   [1.4 Utilities](#Utilities)
*   [2 Maintenance](#Maintenance)
    *   [2.1 Listing packages](#Listing_packages)
        *   [2.1.1 With size](#With_size)
        *   [2.1.2 Latest installed packages](#Latest_installed_packages)
        *   [2.1.3 All packages that nothing else depends on](#All_packages_that_nothing_else_depends_on)
        *   [2.1.4 Installed packages that are not in a specified group or repository](#Installed_packages_that_are_not_in_a_specified_group_or_repository)
    *   [2.2 Listing files owned by a package with size](#Listing_files_owned_by_a_package_with_size)
    *   [2.3 Identify files not owned by any package](#Identify_files_not_owned_by_any_package)
    *   [2.4 Removing unused packages](#Removing_unused_packages)
        *   [2.4.1 Orphans](#Orphans)
        *   [2.4.2 Explicitly installed](#Explicitly_installed)
    *   [2.5 Removing everything but base group](#Removing_everything_but_base_group)
    *   [2.6 Getting the dependencies list of several packages](#Getting_the_dependencies_list_of_several_packages)
    *   [2.7 Listing changed backup files](#Listing_changed_backup_files)
    *   [2.8 Back-up the pacman database](#Back-up_the_pacman_database)
        *   [2.8.1 Using systemd](#Using_systemd)
*   [3 Installation and recovery](#Installation_and_recovery)
    *   [3.1 Installing packages from a CD/DVD or USB stick](#Installing_packages_from_a_CD.2FDVD_or_USB_stick)
    *   [3.2 Custom local repository](#Custom_local_repository)
    *   [3.3 Network shared pacman cache](#Network_shared_pacman_cache)
        *   [3.3.1 Read-only cache](#Read-only_cache)
        *   [3.3.2 Read-write cache](#Read-write_cache)
        *   [3.3.3 Dynamic reverse proxy cache using nginx](#Dynamic_reverse_proxy_cache_using_nginx)
        *   [3.3.4 Synchronize pacman package cache using BitTorrent Sync](#Synchronize_pacman_package_cache_using_BitTorrent_Sync)
        *   [3.3.5 Preventing unwanted cache purges](#Preventing_unwanted_cache_purges)
    *   [3.4 Recreate a package from the file system](#Recreate_a_package_from_the_file_system)
    *   [3.5 Backing up and retrieving a list of installed packages](#Backing_up_and_retrieving_a_list_of_installed_packages)
    *   [3.6 Listing all changed files from packages](#Listing_all_changed_files_from_packages)
    *   [3.7 Reinstalling all packages](#Reinstalling_all_packages)
    *   [3.8 Restore pacman's local database](#Restore_pacman.27s_local_database)
        *   [3.8.1 Generating the package recovery list](#Generating_the_package_recovery_list)
        *   [3.8.2 Performing the recovery](#Performing_the_recovery)
    *   [3.9 Recovering a USB key from existing install](#Recovering_a_USB_key_from_existing_install)
    *   [3.10 Extracting contents of a .pkg file](#Extracting_contents_of_a_.pkg_file)
    *   [3.11 Viewing a single file inside a .pkg file](#Viewing_a_single_file_inside_a_.pkg_file)
    *   [3.12 Find applications that use libraries from older packages](#Find_applications_that_use_libraries_from_older_packages)
*   [4 Performance](#Performance)
    *   [4.1 Database access speeds](#Database_access_speeds)
    *   [4.2 Download speeds](#Download_speeds)
        *   [4.2.1 Powerpill](#Powerpill)
        *   [4.2.2 wget](#wget)
        *   [4.2.3 aria2](#aria2)
        *   [4.2.4 Other applications](#Other_applications)

## Cosmetic and convenience

### Color output

Pacman has a color option. Uncomment the "Color" line in `/etc/pacman.conf`.

### Operations and Bash syntax

In addition to pacman's standard set of features, there are ways to extend its usability through rudimentary [Bash](/index.php/Bash "Bash") commands/syntax.

*   To install a number of packages sharing similar patterns in their names -- not the entire group nor all matching packages; eg. [plasma](https://www.archlinux.org/groups/x86_64/plasma/):

```
# pacman -S plasma-{desktop,mediacenter,nm}

```

*   Of course, that is not limited and can be expanded to however many levels needed:

```
# pacman -S plasma-{workspace{,-wallpapers},pa}

```

*   Sometimes, `-s`'s builtin ERE can cause a lot of unwanted results, so it has to be limited to match the package name only; not the description nor any other field:

```
# pacman -Ss '^vim-'

```

*   pacman has the `-q` operand to hide the version column, so it is possible to query and reinstall packages with "compiz" as part of their name:

```
# pacman -S $(pacman -Qq | grep compiz)

```

*   Or install all packages available in a repository (infinality-bundle for example):

```
# pacman -S $(pacman -Slq infinality-bundle)

```

### Graphical front-ends

*   **Muon** — A collection of package management tools for KDE, using PackageKit.

[https://projects.kde.org/projects/extragear/sysadmin/muon](https://projects.kde.org/projects/extragear/sysadmin/muon) || [muon](https://www.archlinux.org/packages/?name=muon)

*   **GNOME Software** — Gnome Software App.

[https://wiki.gnome.org/Apps/Software](https://wiki.gnome.org/Apps/Software) || [gnome-software](https://www.archlinux.org/packages/?name=gnome-software)

*   **pcurses** — Package management in a curses frontend

[https://github.com/schuay/pcurses](https://github.com/schuay/pcurses) || [pcurses](https://www.archlinux.org/packages/?name=pcurses)

*   **tkPacman** — GUI front-end for pacman. Depends on Tcl/Tk and X11 but neither on GTK+, nor on QT. It only interacts with the package database via the CLI of 'pacman'. So, installing and removing packages with tkPacman or with pacman leads to exactly the same result.

[http://sourceforge.net/projects/tkpacman](http://sourceforge.net/projects/tkpacman) || [tkpacman](https://aur.archlinux.org/packages/tkpacman/)<sup><small>AUR</small></sup>

### Utilities

*   **Lostfiles** — Script for detecting orphaned files.

[https://github.com/graysky2/lostfiles](https://github.com/graysky2/lostfiles) || [lostfiles](https://aur.archlinux.org/packages/lostfiles/)<sup><small>AUR</small></sup>

*   **[Pacmatic](/index.php/Pacmatic "Pacmatic")** — Pacman wrapper to check Arch News before upgrading, avoid partial upgrades, and warn about configuration file changes.

[http://kmkeen.com/pacmatic](http://kmkeen.com/pacmatic) || [pacmatic](https://www.archlinux.org/packages/?name=pacmatic)

*   **[pkgfile](/index.php/Pkgfile "Pkgfile")** — Tool that finds what package owns a file.

[http://github.com/falconindy/pkgfile](http://github.com/falconindy/pkgfile) || [pkgfile](https://www.archlinux.org/packages/?name=pkgfile)

*   **[pkgtools](/index.php/Pkgtools "Pkgtools")** — Collection of scripts for Arch Linux packages.

[https://github.com/Daenyth/pkgtools](https://github.com/Daenyth/pkgtools) || [pkgtools](https://aur.archlinux.org/packages/pkgtools/)<sup><small>AUR</small></sup>

*   **srcpac** — Simple tool that automates rebuilding packages from source.

[https://projects.archlinux.org/srcpac.git](https://projects.archlinux.org/srcpac.git) || [srcpac](https://www.archlinux.org/packages/?name=srcpac)

## Maintenance

See also [System maintenance](/index.php/System_maintenance "System maintenance").

### Listing packages

You may want to get the list of installed packages with their version, which is useful when reporting bugs or discussing installed packages.

*   List all explicitly installed packages: `pacman -Qe` .
*   List all foreign packages (typically manually downloaded and installed): `pacman -Qm` .
*   List all native packages (installed from the sync database(s)): `pacman -Qn` .
*   List packages by regex: `pacman -Qs _regex_`.
*   List packages by regex with custom output format: `expac -s "%-30n %v" _regex_` (needs [expac](https://www.archlinux.org/packages/?name=expac)).

#### With size

To get a list of installed packages sorted by size, which may be useful when freeing space on your hard drive:

*   Install [expac](https://www.archlinux.org/packages/?name=expac) and run `expac -H M '%m\t%n' | sort -h`.
*   Run [pacgraph](https://www.archlinux.org/packages/?name=pacgraph) with the `-c` option.

To list the download size of several packages (leave `_packages_` blank to list all packages):

```
$ expac -S -H M '%k\t%n' _packages_

```

To list explicitly installed packages not in [base](https://www.archlinux.org/groups/x86_64/base/) nor [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) with size and description:

```
$ expac -H M "%011m\t%-20n\t%10d" $( comm -23 <(pacman -Qqen|sort) <(pacman -Qqg base base-devel|sort) ) | sort -n

```

#### Latest installed packages

Install [expac](https://www.archlinux.org/packages/?name=expac) and run `expac --timefmt='%Y-%m-%d %T' '%l\t%n' | sort | tail -20` or `expac --timefmt=%s '%l\t%n' | sort -n | tail -20`

#### All packages that nothing else depends on

If you want to generate a list of all installed packages that nothing else depends on, you can use the following script. This is very helpful if you are trying to free hard drive space and have installed a lot of packages that you may not remember. You can browse through the output to find packages which you no longer need.

**Note:** This script will show all packages that nothing else depends on, including those explicitly installed. To get a list of packages installed as dependencies but no longer required by any installed package, see [#Orphans](#Orphans).

```
ignoregrp="base base-devel"
ignorepkg=""

comm -23 <(pacman -Qqt | sort) <(echo $ignorepkg | tr ' ' '\n' | cat <(pacman -Sqg $ignoregrp) - | sort -u)

```

For list with descriptions for packages:

```
expac -HM "%-20n\t%10d" $( comm -23 <(pacman -Qqt|sort) <(pacman -Qqg base base-devel|sort) )

```

#### Installed packages that are not in a specified group or repository

The following command will list any installed packages that are not in either [base](https://www.archlinux.org/groups/x86_64/base/) or [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), and as such were likely installed manually by the user:

```
$ comm -23 <(pacman -Qeq | sort) <(pacman -Qgq base base-devel | sort)

```

List all installed packages that are not in specified repository (`_repo_name_` in example):

```
$ comm -23 <(pacman -Qtq | sort) <(pacman -Slq _repo_name_ | sort)

```

List all installed packages that are in the `_repo_name_` repository:

```
$ comm -12 <(pacman -Qtq | sort) <(pacman -Slq _repo_name_ | sort)

```

### Listing files owned by a package with size

This one might come in handy if you have found that a specific package uses a huge amount of space and you want to find out which files make up the most of that.

```
$ pacman -Qlq _package_ | grep -v '/$' | xargs du -h | sort -h

```

### Identify files not owned by any package

If your system has stray files not owned by any package (a common case if you do not [use the package manager to install software](/index.php/Enhance_system_stability#Use_the_package_manager_to_install_software "Enhance system stability")), you may want to find such files in order to clean them up. The general process for doing so is:

1.  Create a sorted list of the files you want to check ownership of: `$ find /etc /opt /usr | sort > all_files.txt` 
2.  Create a sorted list of the files tracked by pacman (and remove the trailing slashes from directories): `$ pacman -Qlq | sed 's|/$||' | sort > owned_files.txt` 
3.  Find lines in the first list that are not in the second: `$ comm -23 all_files.txt owned_files.txt` 

This process is tricky in practice because many important files are not part of any package (e.g. files generated at runtime, custom configs) and so will be included in the final output, making it difficult to pick out the files that can be safely deleted.

The [lostfiles](https://aur.archlinux.org/packages/lostfiles/)<sup><small>AUR</small></sup> script performs similar steps, but also includes an extensive blacklist to remove common false positives from the output.

### Removing unused packages

#### Orphans

For _recursively_ removing orphans and their configuration files:

```
# pacman -Rns $(pacman -Qtdq)

```

If no orphans were found, pacman errors with `error: no targets specified`. This is expected as no arguments were passed to `pacman -Rns`.

**Note:** Since pacman version 4.2.0 only true orphans are listed. To make pacman also list packages which are only optionally required by another package, pass the `-t`/`--unrequired` flag twice:

```
$ pacman -Qdttq

```

Use this carefully, as it is not taken into account whether the package is an optional dependency and therefore bears the risk to remove packages which actually are not real orphans.

#### Explicitly installed

Because a lighter system is easier to maintain, occasionally looking through explicitly installed packages and _manually_ selecting unused packages to be removed can be helpful.

To list explicitly installed packages available in the official repositories:

```
$ pacman -Qen

```

To list explicitly installed packages not available in official repositories:

```
$ pacman -Qem

```

### Removing everything but base group

If it is ever necessary to remove all packages except the base group, try this one liner:

```
# pacman -R $(comm -23 <(pacman -Qq|sort) <((for i in $(pacman -Qqg base); do pactree -ul $i; done)|sort -u|cut -d ' ' -f 1))

```

The one-liner was originally devised in [this discussion](https://bbs.archlinux.org/viewtopic.php?id=130176), and later improved in this article.

Notes:

1.  `comm` requires sorted input otherwise you get e.g. `comm: file 1 is not in sorted order`.
2.  `pactree` prints the package name followed by what it provides. For example:

 `$ pactree -lu logrotate` 

```
logrotate
popt
glibc
linux-api-headers
tzdata
dcron cron
bash
readline
ncurses
gzip
```

The `dcron cron` line seems to cause problems, that is why `cut -d ' ' -f 1` is needed - to keep just the package name.

### Getting the dependencies list of several packages

Dependencies are alphabetically sorted and doubles are removed. Note that you can use `pacman -Qi` to improve response time a little. But you will not be able to query as many packages. Unfound packages are simply skipped (hence the `2>/dev/null`).

```
$ pacman -Si $@ 2>/dev/null | awk -F ": " -v filter="^Depends" \ '$0 ~ filter {gsub(/[>=<][^ ]*/,"",$2) ; gsub(/ +/,"\n",$2) ; print $2}' | sort -u

```

Alternatively, you can use `expac`: `expac -l '\n' %E -S $@ | sort -u`.

### Listing changed backup files

If you want to backup your system configuration files you could copy all files in `/etc/`, but usually you are only interested in the files that you have changed. Modified [backup files](/index.php/Pacnew_and_Pacsave_files#Package_backup_files "Pacnew and Pacsave files") can be viewed with the following command:

```
# pacman -Qii | awk '/^MODIFIED/ {print $2}'

```

Running this command with root permissions will ensure that files readable only by root (such as `/etc/sudoers`) are included in the output.

**Tip:** See [#Listing all changed files from packages](#Listing_all_changed_files_from_packages) to list all changed files pacman knows, not only backup files.

### Back-up the pacman database

The following command can be used to back up the local pacman database:

```
$ tar -cjf pacman_database.tar.bz2 /var/lib/pacman/local

```

Store the backup pacman database file on one or more offline media, such as a USB stick, external hard drive, or CD-R. See also [Pacman tips#Backing up Local database with systemd](/index.php/Pacman_tips#Backing_up_Local_database_with_systemd "Pacman tips") for an alternative method.

The database can be restored by moving the `pacman_database.tar.bz2` file into the `/` directory and executing the following command:

```
# tar -xjvf pacman_database.tar.bz2

```

**Note:** If the pacman database files are corrupted, and there is no backup file available, there exists some hope of rebuilding the pacman database. Consult [Pacman tips#Restore pacman's local database](/index.php/Pacman_tips#Restore_pacman.27s_local_database "Pacman tips").

#### Using systemd

[systemd](/index.php/Systemd "Systemd") can take snapshots of the pacman local database, each time it is modified.

**Tip:** For a more configurable version, use: [pakbak-git](https://aur.archlinux.org/packages/pakbak-git/)<sup><small>AUR</small></sup>

Use the following scripts, changing the value of `$pakbak` for the backup location accordingly. The `pakbak.service` can also automaticall be [enabled](/index.php/Enable "Enable") on boot:

 `/usr/lib/systemd/scripts/pakbak_script` 

```
#!/bin/bash

declare -r pakbak=_"/pakbak.tar.xz"_;  ## set backup location
tar -cJf "$pakbak" "/var/lib/pacman/local";  ## compress & store pacman local database in $pakbak
```

 `/usr/lib/systemd/system/pakbak.service` 

```
[Unit]
Description=Back up pacman database

[Service]
Type=oneshot
ExecStart=/bin/bash /usr/lib/systemd/scripts/pakbak_script
RemainAfterExit=no
```

 `/usr/lib/systemd/system/pakbak.path` 

```
[Unit]
Description=Back up pacman database

[Path]
PathChanged=/var/lib/pacman/local
Unit=pakbak.service

[Install]
WantedBy=multi-user.target
```

## Installation and recovery

Alternative ways of getting and restoring packages.

### Installing packages from a CD/DVD or USB stick

To download packages, or groups of packages:

```
# cd ~/Packages
# pacman -Syw base base-devel grub-bios xorg gimp --cachedir .
# repo-add ./custom.db.tar.gz ./*

```

Then you can burn the "Packages" folder to a CD/DVD or transfer it to a USB stick, external HDD, etc.

To install:

**1.** Mount the media:

```
# mkdir /mnt/repo
# mount /dev/sr0 /mnt/repo    #For a CD/DVD.
# mount /dev/sdxY /mnt/repo   #For a USB stick.

```

**2.** Edit `pacman.conf` and add this repository _before_ the other ones (e.g. extra, core, etc.). This is important. Do not just uncomment the one on the bottom. This way it ensures that the files from the CD/DVD/USB take precedence over those in the standard repositories:

 `/etc/pacman.conf` 

```
[custom]
SigLevel = PackageRequired
Server = file:///mnt/repo/Packages
```

**3.** Finally, synchronize the pacman database to be able to use the new repository:

```
# pacman -Syu

```

### Custom local repository

Use the _repo-add_ script included with Pacman to generate a database for a personal repository. Use `repo-add --help` for more details on its usage. Simply store all of the built packages to be included in the repository in one directory, and execute the following command (where _repo_ is the name of the custom repository):

```
$ repo-add /path/to/repo.db.tar.gz /path/to/*.pkg.tar.xz

```

**Note:** A package database is a tar file, optionally compressed. Valid extensions are “.db” or “.files” followed by an archive extension of “.tar”, “.tar.gz”, “.tar.bz2”, “.tar.xz”, or “.tar.Z”. The file does not need to exist, but all parent directories must exist. Furthermore when using `repo-add` keep in mind that the database and the packages do not need to be in the same directory. But when using pacman with that database, they should be together.

To add a new package to the database, or to replace the old version of an existing package in the database, run:

```
$ repo-add /path/to/repo.db.tar.gz /path/to/packagetoadd-1.0-1-i686.pkg.tar.xz

```

_repo-remove_ is used in the exact same manner as _repo-add_, except that the packages listed on the command line are removed from the repository database.

Once the local repository database has been created, add the repository to `pacman.conf` for each system that is to use the repository. An example of a custom repository is in `pacman.conf`. The repository's name is the database filename with the file extension omitted. In the case of the example above the repository's name would simply be _repo_. Reference the repository's location using a `file://` url, or via FTP using [ftp://localhost/path/to/directory](ftp://localhost/path/to/directory).

If willing, add the custom repository to the [list of unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories"), so that the community can benefit from it.

### Network shared pacman cache

If you happen to run several Arch boxes on your LAN, you can share packages so that you can greatly decrease your download times. Keep in mind you should not share between different architectures (i.e. i686 and x86_64) or you'll get into troubles.

#### Read-only cache

If you are looking for a quick and dirty solution, you can simply run a standalone webserver which other computers can use as a first mirror: `darkhttpd /var/cache/pacman/pkg`. Just add this server at the top of your mirror list. Be aware that you might get a lot of 404 errors, due to cache misses, depending on what you do, but pacman will try the next (real) mirrors when that happens.

#### Read-write cache

**Tip:** See [pacserve](/index.php/Pacserve "Pacserve") for an alternative (and probably simpler) solution than what follows.

In order to share packages between multiple computers, simply share `/var/cache/pacman/` using any network-based mount protocol. This section shows how to use shfs or sshfs to share a package cache plus the related library-directories between multiple computers on the same local network. Keep in mind that a network shared cache can be slow depending on the file-system choice, among other factors.

First, install any network-supporting filesystem; for example [sshfs](/index.php/Sshfs "Sshfs"), [shfs](/index.php/Shfs "Shfs"), ftpfs, [smbfs](/index.php/Smbfs "Smbfs") or [nfs](/index.php/Nfs "Nfs").

**Tip:** To use sshfs or shfs, consider reading [Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys").

Then, to share the actual packages, mount `/var/cache/pacman/pkg` from the server to `/var/cache/pacman/pkg` on every client machine.

#### Dynamic reverse proxy cache using nginx

[nginx](/index.php/Nginx "Nginx") can be used to proxy requests to official upstream mirrors and cache the results to local disk. All subsequent requests for that file will be served directly from the local cache, minimizing the amount of internet traffic needed to update a large number of servers with minimal effort.

In this example, we will run the cache server on `http://cache.domain.local:8080/` and storing the packages in `/srv/http/pacman-cache/`.

Create the directory for the cache and adjust the permissions to nginx can write files to it:

```
 # mkdir /srv/http/pacman-cache
 # chown http:http /srv/http/pacman-cache

```

Next, configure nginx as our dynamic cache:

 `/etc/nginx/nginx.conf` 

```
http
{
    ...

    # Pacman Cache
    server
    {
        listen      8080;
        server_name cache.domain.local;
        root        /srv/http/pacman-cache;
        autoindex   on;

        # Requests for package db and signature files should redirect upstream
        #   without caching
        location ~ \.(db|sig)$ {
            resolver   8.8.8.8 8.8.4.4;
            proxy_pass $scheme://mirrors$request_uri;
        }

        # Requests for actual packages should be served directly if available;
        #   If not available, retrieve and save the package from an upstream
        #   mirror.
        location ~ \.tar\.xz$ {
            try_files $uri @pkg_mirror;
        }

        # Retrieve package from upstream mirrors, cache for future requests
        location @pkg_mirror {
            resolver 8.8.8.8 8.8.4.4;
            proxy_store on;
            proxy_store_access user:rw group:rw all:r;
            proxy_next_upstream error timeout http_404;
            proxy_pass http://mirrors$request_uri;
            proxy_redirect off;
        }
    }

    # Upstream Arch Linux Mirrors - Change these to your preferred servers
    upstream mirrors {
        server mirror.rit.edu;
        server mirrors.acm.wpi.edu backup;
        server lug.mtu.edu backup;
    }
}

```

Finally, update your other Arch Linux servers to use this new cache by adding the following line to the `mirrorlist` file:

 `/etc/pacman.d/mirrorlist` 

```
Server = http://cache.domain.local:8080/archlinux/$repo/os/$arch
...

```

**Warning:** A limitation of this method is that you must use mirrors that use the same relative path and you must configure your cache to use the same. In this example, we are using mirrors that use the relative path `/archlinux/$repo/os/$arch` and our cache's `Server` setting is configured similarly.

**Note:** You will need to create a method to clear old packages, as this directory will continue to grow over time.

#### Synchronize pacman package cache using BitTorrent Sync

[BitTorrent Sync](/index.php/BitTorrent_Sync "BitTorrent Sync") is a new way of synchronizing folder via network (it works in LAN and over the internet). It is peer-to-peer so you do not need to set up a server: follow the link for more information. How to share a pacman cache using BitTorrent Sync:

*   First install the [btsync](https://aur.archlinux.org/packages/btsync/)<sup><small>AUR</small></sup> package from the AUR on the machines you want to sync
*   Follow the installation instructions of the AUR package or on the [BitTorrent Sync](/index.php/BitTorrent_Sync "BitTorrent Sync") wiki page
    *   set up BitTorrent Sync to work for the root account. This process requires read/write to the pacman package cache.
    *   make sure to set a good password on btsync's web UI
    *   start the systemd daemon for btsync.
    *   in the btsync Web GUI add a new synchronized folder on the first machine and generate a new Secret. Point the folder to `/var/cache/pacman/pkg`
    *   Add the folder on all the other machines using the same Secret to share the cached packages between all systems. Or, to set the first system as a master and the others as slaves, use the Read Only Secret. Be sure to point it to `/var/cache/pacman/pkg`

Now the machines should connect and start synchronizing their cache. Pacman works as expected even during synchronization. The process of syncing is entirely automatic.

#### Preventing unwanted cache purges

By default, `pacman -Sc` removes package tarballs from the cache that correspond to packages that are not installed on the machine the command was issued on. Because pacman cannot predict what packages are installed on all machines that share the cache, it will end up deleting files that should not be.

To clean up the cache so that only _outdated_ tarballs are deleted, add this entry in the `[options]` section of `/etc/pacman.conf`:

```
CleanMethod = KeepCurrent

```

### Recreate a package from the file system

To recreate a package from the file system, use _bacman_ (included with pacman). Files from the system are taken as they are, hence any modifications will be present in the assembled package. Distributing the recreated package is therefore discouraged; see [ABS](/index.php/ABS "ABS") and [Arch Rollback Machine](/index.php/Arch_Rollback_Machine "Arch Rollback Machine") for alternatives.

**Tip:** _bacman_ honours the `PACKAGER`, `PKGDEST` and `PKGEXT` options from `makepkg.conf`. Custom options for the compression tools can be configured by exporting the relevant environment variable, for example `XZ_OPT="-T 0"` will enable parallel compression for _xz_.

An alternative tool would be [fakepkg](https://aur.archlinux.org/packages/fakepkg/)<sup><small>AUR</small></sup>. It supports parallelization through [parallel](https://www.archlinux.org/packages/?name=parallel) and can handle multiple input packages in one command, which _bacman_ both does not support.

### Backing up and retrieving a list of installed packages

**Tip:** You may want to use [pacbackup](https://aur.archlinux.org/packages/pacbackup/)<sup><small>AUR</small></sup> or [bacpac](https://bbs.archlinux.org/viewtopic.php?id=200067) to automatise the below tasks.

It is good practice to keep periodic backups of all pacman-installed packages. In the event of a system crash which is unrecoverable by other means, pacman can then easily reinstall the very same packages onto a new installation.

*   First, backup the current list of non-local packages: `$ pacman -Qqen > pkglist.txt`

*   Store the `pkglist.txt` on a USB key or other convenient medium or gist.github.com or Evernote, Dropbox, etc.

*   Copy the `pkglist.txt` file to the new installation, and navigate to the directory containing it.

*   Issue the following command to install from the backup list: `# pacman -S $(< pkglist.txt)`

In the case you have a list which was not generated like mentioned above, there may be foreign packages in it (i.e. packages not belonging to any repos you have configured, or packages from the AUR).

In such a case, you may still want to install all available packages from that list:

```
# pacman -S --needed $(comm -12 <(pacman -Slq|sort) <(sort badpkdlist) )

```

Explanation:

*   `pacman -Slq` lists all available softwares, but the list is sorted by repository first, hence the `sort` command.
*   Sorted files are required in order to make the `comm` command work.
*   The `-12` parameter display lines common to both entries.
*   The `--needed` switch is used to skip already installed packages.

Finally, you may want to remove all the packages on your system that are not mentioned in the list.

**Warning:** Use this command wisely, and always check the result prompted by pacman.

```
# pacman -Rsu $(comm -23 <(pacman -Qq|sort) <(sort pkglist))

```

### Listing all changed files from packages

If you are suspecting file corruption (e.g. by software / hardware failure), but don't know for sure whether / which files really got corrupted, you might want to compare with the hash sums in the packages. This can be done with the following script.

The script depends on the accuracy of pacman's database in `/var/lib/pacman/local/` and the used programs such as _bash_, _grep_ and so on. For recovery of the database see [#Restore pacman's local database](#Restore_pacman.27s_local_database). The `mtree` files can also be [extracted as `.MTREE` from the respective package files](#Viewing_a_single_file_inside_a_.pkg_file).

**Note:**

*   This should **not** be used as is when suspecting malicious changes! In this case security precautions such as using a live medium and an independent source for the hash sums are advised.
*   This could take a long time, depending on the hardware and installed packages.

```
#!/bin/bash -e

# Select the hash algorithm. Currently available (see mtree files and mtree(5)):
# md5, sha256
algo="md5"

for package in /var/lib/pacman/local/*; do
    [ "$package" = "/var/lib/pacman/local/ALPM_DB_VERSION" ] && continue

    # get files and hash sums
    zgrep " ${algo}digest=" "$package/mtree" | grep -Ev '^\./\.[A-Z]+' | \
        sed 's/^\([^ ]*\).*'"${algo}"'digest=\([a-f0-9]*\).*/\1 \2/' | \
        while read -r file hash
    do
        # expand "\nnn" (in mtree) / "\0nnn" (for echo) escapes of ASCII
        # characters (octal representation)
        for ascii in $(grep -Eo '\\[0-9]{1,3}' <<< "$file"); do
            file="$(sed "s/\\$ascii/$(echo -e "\0${ascii:1}")/" <<< "$file")"
        done

        # check file hash
        if [ "$("${algo}sum" /"$file" | awk '{ print $1; }')" != "$hash" ]; then
            echo "$(basename "$package")" /"$file"
        fi
    done
done

```

### Reinstalling all packages

To reinstall all native packages, use:

```
# pacman -Qenq | pacman -S -

```

Foreign (AUR) packages must be reinstalled separately; you can list them with `pacman -Qemq`.

Pacman preserves the installation reason by default.

### Restore pacman's local database

Signs that pacman needs a local database restoration:

*   `pacman -Q` gives absolutely no output, and `pacman -Syu` erroneously reports that the system is up to date.
*   When trying to install a package using `pacman -S package`, and it outputs a list of already satisfied dependencies.
*   When `testdb` (part of [pacman](https://www.archlinux.org/packages/?name=pacman)) reports database inconsistency.

Most likely, pacman's database of installed software, `/var/lib/pacman/local`, has been corrupted or deleted. While this is a serious problem, it can be restored by following the instructions below.

Firstly, make sure pacman's log file is present:

```
$ ls /var/log/pacman.log

```

If it does not exist, it is _not_ possible to continue with this method. You may be able to use [Xyne's package detection script](https://bbs.archlinux.org/viewtopic.php?pid=670876) to recreate the database. If not, then the likely solution is to re-install the entire system.

#### Generating the package recovery list

**Warning:** If for some reason your [pacman](/index.php/Pacman "Pacman") cache or [makepkg](/index.php/Makepkg "Makepkg") package destination contain packages for other architectures, remove them before continuation.

Run the script (optionally passing additional directories with packages as parameters):

```
$ paclog-pkglist /var/log/pacman.log | ./pacrecover >files.list 2>pkglist.orig

```

This way two files will be created: `files.list` with package files, still present on machine and `pkglist.orig`, packages from which should be downloaded. Later operation may result in mismatch between files of older versions of package, still present on machine, and files, found in new version. Such mismatches will have to be fixed manually.

Here is a way to automatically restrict second list to packages available in a repository:

```
$ { cat pkglist.orig; pacman -Slq; } | sort | uniq -d > pkglist

```

Check if some important _base_ package are missing, and add them to the list:

```
$ comm -23 <(pacman -Sgq base) pkglist.orig >> pkglist

```

Proceed once the contents of both lists are satisfactory, since they will be used to restore pacman's installed package database; `/var/lib/pacman/local/`.

#### Performing the recovery

Define bash alias for recovery purposes:

```
# recovery-pacman() {
    pacman "$@"       \
    --log /dev/null   \
    --noscriptlet     \
    --dbonly          \
    --force           \
    --nodeps          \
    --needed          \
    #
}

```

`--log /dev/null` allows to avoid needless pollution of pacman log, `--needed` will save some time by skipping packages, already present in database, `--nodeps` will allow installation of cached packages, even if packages being installed depend on newer versions. Rest of options will allow **pacman** to operate without reading/writing filesystem.

Populate the sync database:

```
# pacman -Sy

```

Start database generation by installing locally available package files from `files.list`:

```
# recovery-pacman -U $(< files.list)

```

Install the rest from `pkglist`:

```
# recovery-pacman -S $(< pkglist)

```

Update the local database so that packages that are not required by any other package are marked as explicitly installed and the other as dependences. You will need be extra careful in the future when removing packages, but with the original database lost is the best we can do.

```
# pacman -D --asdeps $(pacman -Qq)
# pacman -D --asexplicit $(pacman -Qtq)

```

Optionally check all installed packages for corruption:

```
# pacman -Qk

```

Optionally [#Identify files not owned by any package](#Identify_files_not_owned_by_any_package).

Update all packages:

```
# pacman -Su

```

### Recovering a USB key from existing install

If you have Arch installed on a USB key and manage to mess it up (e.g. removing it while it is still being written to), then it is possible to re-install all the packages and hopefully get it back up and working again (assuming USB key is mounted in /newarch)

```
# pacman -S $(pacman -Qq --dbpath /newarch/var/lib/pacman) --root /newarch --dbpath /newarch/var/lib/pacman

```

### Extracting contents of a .pkg file

The `.pkg` files ending in `.xz` are simply tar'ed archives that can be decompressed with:

```
$ tar xvf package.tar.xz

```

If you want to extract a couple of files out of a `.pkg` file, this would be a way to do it.

### Viewing a single file inside a .pkg file

For example, if you want to see the contents of `/etc/systemd/logind.conf` supplied within the [systemd](https://www.archlinux.org/packages/?name=systemd) package:

```
$ tar -xOf /var/cache/pacman/pkg/systemd-204-3-x86_64.pkg.tar.xz etc/systemd/logind.conf

```

Or you can use [vim](https://www.archlinux.org/packages/?name=vim), then browse the archive:

```
$ vim /var/cache/pacman/pkg/systemd-204-3-x86_64.pkg.tar.xz

```

### Find applications that use libraries from older packages

Even if you installed a package the existing long-running programs (like daemons and servers) still keep using code from old package libraries. And it is a bad idea to let these programs running if the old library contains a security bug.

Here is a way how to find all the programs that use old packages code:

```
# lsof +c 0 | grep -w DEL | awk '1 { print $1 ": " $NF }' | sort -u

```

It will print running program name and old library that was removed or replaced with newer content.

## Performance

### Database access speeds

Pacman stores all package information in a collection of small files, one for each package. Improving database access speeds reduces the time taken in database-related tasks, e.g. searching packages and resolving package dependencies. The safest and easiest method is to run as root:

```
# pacman-optimize

```

This will attempt to put all the small files together in one (physical) location on the hard disk so that the hard disk head does not have to move so much when accessing all the data. This method is safe, but is not foolproof: it depends on your filesystem, disk usage and empty space fragmentation. Another, more aggressive, option would be to first remove uninstalled packages from cache and to remove unused repositories before database optimization:

```
# pacman -Sc && pacman-optimize

```

### Download speeds

**Note:** If your download speeds have been reduced to a crawl, ensure you are using one of the many [mirrors](/index.php/Mirrors "Mirrors") and not ftp.archlinux.org, which is [throttled since March 2007](https://www.archlinux.org/news/302/).

When downloading packages pacman uses the mirrors in the order they are in `/etc/pacman.d/mirrorlist`. The mirror which is at the top of the list by default however may not be the fastest for you. To select a faster mirror, see [Mirrors](/index.php/Mirrors "Mirrors").

Pacman's speed in downloading packages can also be improved by using a different application to download packages, instead of Pacman's built-in file downloader.

In all cases, make sure you have the latest Pacman before doing any modifications.

```
# pacman -Syu

```

#### Powerpill

Powerpill is a full wrapper for Pacman that uses parallel and segmented downloads to speed up the download process. Normally Pacman will download one package at a time, waiting for it to complete before beginning the next download. Powerpill takes a different approach: it tries to download as many packages as possible at once.

The [Powerpill wiki page](/index.php/Powerpill "Powerpill") provides basic configuration and usage examples along with package and upstream links.

#### wget

This is also very handy if you need more powerful proxy settings than pacman's built-in capabilities.

To use `wget`, first [install](/index.php/Install "Install") the [wget](https://www.archlinux.org/packages/?name=wget) package then modify `/etc/pacman.conf` by uncommenting the following line in the `[options]` section:

```
XferCommand = /usr/bin/wget -c -q --show-progress --passive-ftp -O %o %u

```

Instead of uncommenting the `wget` parameters in `/etc/pacman.conf`, you can also modify the `wget` configuration file directly (the system-wide file is `/etc/wgetrc`, per user files are `$HOME/.wgetrc`.

#### aria2

[aria2](/index.php/Aria2 "Aria2") is a lightweight download utility with support for resumable and segmented HTTP/HTTPS and FTP downloads. aria2 allows for multiple and simultaneous HTTP/HTTPS and FTP connections to an Arch mirror, which should result in an increase in download speeds for both file and package retrieval.

**Note:** Using aria2c in Pacman's XferCommand will **not** result in parallel downloads of multiple packages. Pacman invokes the XferCommand with a single package at a time and waits for it to complete before invoking the next. To download multiple packages in parallel, see the [powerpill](#Using_Powerpill) section above.

Install [aria2](https://www.archlinux.org/packages/?name=aria2), then edit `/etc/pacman.conf` by adding the following line to the `[options]` section:

```
XferCommand = /usr/bin/aria2c --allow-overwrite=true --continue=true --file-allocation=none --log-level=error --max-tries=2 --max-connection-per-server=2 --max-file-not-found=5 --min-split-size=5M --no-conf --remote-time=true --summary-interval=60 --timeout=5 --dir=/ --out %o %u

```

**Tip:** [This alternative configuration for using pacman with aria2](https://bbs.archlinux.org/viewtopic.php?pid=1491879#p1491879) tries to simplify configuration and adds more configuration options.

See [OPTIONS](http://aria2.sourceforge.net/manual/en/html/aria2c.html#options) in `man aria2c` for used aria2c options.

`-d, --dir`

The directory to store the downloaded file(s) as specified by [pacman](/index.php/Pacman "Pacman").

`-o, --out`

The output file name(s) of the downloaded file(s).

`%o`

Variable which represents the local filename(s) as specified by pacman.

`%u`

Variable which represents the download URL as specified by pacman.

#### Other applications

There are other downloading applications that you can use with Pacman. Here they are, and their associated XferCommand settings:

*   `snarf`: `XferCommand = /usr/bin/snarf -N %u`
*   `lftp`: `XferCommand = /usr/bin/lftp -c pget %u`
*   `axel`: `XferCommand = /usr/bin/axel -n 2 -v -a -o %o %u`

Retrieved from "[https://wiki.archlinux.org/index.php?title=Pacman/Tips_and_tricks&oldid=410421](https://wiki.archlinux.org/index.php?title=Pacman/Tips_and_tricks&oldid=410421)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Package management](/index.php/Category:Package_management "Category:Package management")