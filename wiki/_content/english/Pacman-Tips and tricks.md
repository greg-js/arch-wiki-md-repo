Related articles

*   [Mirrors](/index.php/Mirrors "Mirrors")
*   [Creating packages](/index.php/Creating_packages "Creating packages")

For general methods to improve the flexibility of the provided tips or *pacman* itself, see [Core utilities](/index.php/Core_utilities "Core utilities") and [Bash](/index.php/Bash "Bash").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Maintenance](#Maintenance)
    *   [1.1 Listing packages](#Listing_packages)
        *   [1.1.1 With size](#With_size)
            *   [1.1.1.1 Individual packages](#Individual_packages)
            *   [1.1.1.2 Packages and dependencies](#Packages_and_dependencies)
        *   [1.1.2 By date](#By_date)
        *   [1.1.3 Not in a specified group or repository](#Not_in_a_specified_group_or_repository)
        *   [1.1.4 Development packages](#Development_packages)
    *   [1.2 Browsing packages](#Browsing_packages)
    *   [1.3 Listing files owned by a package with size](#Listing_files_owned_by_a_package_with_size)
    *   [1.4 Identify files not owned by any package](#Identify_files_not_owned_by_any_package)
    *   [1.5 Tracking unowned files created by packages](#Tracking_unowned_files_created_by_packages)
    *   [1.6 Removing unused packages (orphans)](#Removing_unused_packages_(orphans))
    *   [1.7 Removing everything but base group](#Removing_everything_but_base_group)
    *   [1.8 Getting the dependencies list of several packages](#Getting_the_dependencies_list_of_several_packages)
    *   [1.9 Listing changed backup files](#Listing_changed_backup_files)
    *   [1.10 Backup the pacman database](#Backup_the_pacman_database)
    *   [1.11 Check changelogs easily](#Check_changelogs_easily)
*   [2 Installation and recovery](#Installation_and_recovery)
    *   [2.1 Installing packages from a CD/DVD or USB stick](#Installing_packages_from_a_CD/DVD_or_USB_stick)
    *   [2.2 Custom local repository](#Custom_local_repository)
    *   [2.3 Network shared pacman cache](#Network_shared_pacman_cache)
        *   [2.3.1 Read-only cache](#Read-only_cache)
        *   [2.3.2 Distributed read-only cache](#Distributed_read-only_cache)
        *   [2.3.3 Read-write cache](#Read-write_cache)
        *   [2.3.4 two-way with rsync](#two-way_with_rsync)
        *   [2.3.5 Dynamic reverse proxy cache using nginx](#Dynamic_reverse_proxy_cache_using_nginx)
        *   [2.3.6 Synchronize pacman package cache using synchronization programs](#Synchronize_pacman_package_cache_using_synchronization_programs)
        *   [2.3.7 Preventing unwanted cache purges](#Preventing_unwanted_cache_purges)
    *   [2.4 Recreate a package from the file system](#Recreate_a_package_from_the_file_system)
    *   [2.5 List of installed packages](#List_of_installed_packages)
    *   [2.6 Install packages from a list](#Install_packages_from_a_list)
    *   [2.7 Listing all changed files from packages](#Listing_all_changed_files_from_packages)
    *   [2.8 Reinstalling all packages](#Reinstalling_all_packages)
    *   [2.9 Restore pacman's local database](#Restore_pacman's_local_database)
    *   [2.10 Recovering a USB key from existing install](#Recovering_a_USB_key_from_existing_install)
    *   [2.11 Viewing a single file inside a .pkg file](#Viewing_a_single_file_inside_a_.pkg_file)
    *   [2.12 Find applications that use libraries from older packages](#Find_applications_that_use_libraries_from_older_packages)
    *   [2.13 Installing only content in required languages](#Installing_only_content_in_required_languages)
*   [3 Performance](#Performance)
    *   [3.1 Download speeds](#Download_speeds)
        *   [3.1.1 Powerpill](#Powerpill)
        *   [3.1.2 wget](#wget)
        *   [3.1.3 aria2](#aria2)
        *   [3.1.4 Other applications](#Other_applications)
*   [4 Utilities](#Utilities)
    *   [4.1 Graphical](#Graphical)

## Maintenance

**Note:** Instead of using *comm* (which requires sorted input with *sort*) in the sections below, you may also use `grep -Fxf` or `grep -Fxvf`.

See also [System maintenance](/index.php/System_maintenance "System maintenance").

### Listing packages

You may want to get the list of installed packages with their version, which is useful when reporting bugs or discussing installed packages.

*   List all explicitly installed packages: `pacman -Qe`.
*   List all packages in the group named `group`: `pacman -Sg group`
*   List all explicitly installed native packages (i.e. present in the sync database) that are not direct or optional dependencies: `pacman -Qent`.
*   List all foreign packages (typically manually downloaded and installed or packages removed from the repositories): `pacman -Qm`.
*   List all native packages (installed from the sync database(s)): `pacman -Qn`.
*   List packages by regex: `pacman -Qs *regex*`.
*   List packages by regex with custom output format: `expac -s "%-30n %v" *regex*` (needs [expac](https://www.archlinux.org/packages/?name=expac)).

#### With size

Figuring out which packages are largest can be useful when trying to free space on your hard drive. There are two options here: get the size of individual packages, or get the size of packages and their dependencies.

##### Individual packages

The following command will list all installed packages and their individual sizes:

```
$ pacman -Qi | awk '/^Name/{name=$3} /^Installed Size/{print $4$5, name}' | sort -h

```

##### Packages and dependencies

To list package sizes with their dependencies,

*   Install [expac](https://www.archlinux.org/packages/?name=expac) and run `expac -H M '%m\t%n' | sort -h`.
*   Run [pacgraph](https://www.archlinux.org/packages/?name=pacgraph) with the `-c` option.

To list the download size of several packages (leave `*packages*` blank to list all packages):

```
$ expac -S -H M '%k\t%n' *packages*

```

To list explicitly installed packages not in [base](https://www.archlinux.org/groups/x86_64/base/) nor [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) with size and description:

```
$ expac -H M "%011m\t%-20n\t%10d" $(comm -23 <(pacman -Qqen | sort) <(pacman -Qqg base base-devel | sort)) | sort -n

```

To list the packages marked for upgrade with their download size

```
$ pacman -Quq|xargs expac -S -H M '%k\t%n' | sort -sh

```

#### By date

To list the 20 last installed packages with [expac](https://www.archlinux.org/packages/?name=expac), run:

```
$ expac --timefmt='%Y-%m-%d %T' '%l\t%n' | sort | tail -n 20

```

or, with seconds since the epoch (1970-01-01 UTC):

```
$ expac --timefmt=%s '%l\t%n' | sort -n | tail -n 20

```

#### Not in a specified group or repository

**Note:** To get a list of packages installed as dependencies but no longer required by any installed package, see [#Removing unused packages (orphans)](#Removing_unused_packages_(orphans)).

List explicitly installed packages not in the [base](https://www.archlinux.org/groups/x86_64/base/) or [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) groups:

```
$ comm -23 <(pacman -Qeq | sort) <(pacman -Qgq base base-devel | sort)

```

List all installed packages unrequired by other packages, and which are not in the [base](https://www.archlinux.org/groups/x86_64/base/) or [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) groups:

```
$ comm -23 <(pacman -Qqt | sort) <(pacman -Sqg base base-devel | sort)

```

As above, but with descriptions:

```
$ expac -HM '%-20n\t%10d' $(comm -23 <(pacman -Qqt | sort) <(pacman -Qqg base base-devel | sort))

```

List all installed packages that are *not* in the specified repository *repo_name*

```
$ comm -23 <(pacman -Qq | sort) <(pacman -Slq *repo_name* | sort)

```

List all installed packages that are in the *repo_name* repository:

```
$ comm -12 <(pacman -Qq | sort) <(pacman -Slq *repo_name* | sort)

```

List all packages on the Arch Linux ISO that are not in the base group:

```
$ comm -23 <(curl https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) <(pacman -Qqg base | sort)

```

#### Development packages

To list all development/unstable packages, run:

```
$ pacman -Qq | grep -Ee '-(bzr|cvs|darcs|git|hg|svn)$'

```

### Browsing packages

To browse all installed packages with an instant preview of each package:

```
 $ pacman -Qq | fzf --preview 'pacman -Qil {}' --layout=reverse --bind 'enter:execute(pacman -Qil {} | less)'

```

This uses [fzf](/index.php/Fzf "Fzf") to present a two-pane view listing all packages with package info shown on the right.

Enter letters to filter the list of packages; use arrow keys (or `Ctrl-j`/`Ctrl-k`) to navigate; press `Enter` to see package info under *less*.

### Listing files owned by a package with size

This one might come in handy if you have found that a specific package uses a huge amount of space and you want to find out which files make up the most of that.

```
$ pacman -Qlq *package* | grep -v '/$' | xargs du -h | sort -h

```

### Identify files not owned by any package

If your system has stray files not owned by any package (a common case if you do not [use the package manager to install software](/index.php/Enhance_system_stability#Use_the_package_manager_to_install_software "Enhance system stability")), you may want to find such files in order to clean them up.

One method is to use `# pacreport --unowned-files` from [pacutils](https://www.archlinux.org/packages/?name=pacutils) which will list unowned files among other details.

Another is to list all files of interest and check them against pacman:

```
# find /etc /usr /opt /var | LC_ALL=C pacman -Qqo - 2>&1 > /dev/null | cut -d ' ' -f 5-

```

**Tip:** The [lostfiles](https://www.archlinux.org/packages/?name=lostfiles) script performs similar steps, but also includes an extensive blacklist to remove common false positives from the output.

### Tracking unowned files created by packages

Most systems will slowly collect several [ghost](http://ftp.rpm.org/max-rpm/s1-rpm-inside-files-list-directives.html#S3-RPM-INSIDE-FLIST-GHOST-DIRECTIVE) files such as state files, logs, indexes, etc. through the course of usual operation.

`pacreport` from [pacutils](https://www.archlinux.org/packages/?name=pacutils) can be used to track these files and their associations via `/etc/pacreport.conf` (see [pacreport(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacreport.1#FILES)).

An example may look something like this (abridged):

 `/etc/pacreport.conf` 
```
[Options]
IgnoreUnowned = usr/share/applications/mimeinfo.cache

[PkgIgnoreUnowned]
alsa-utils = var/lib/alsa/asound.state
bluez = var/lib/bluetooth
ca-certificates = etc/ca-certificates/trust-source/*
dbus = var/lib/dbus/machine-id
glibc = etc/ld.so.cache
grub = boot/grub/*
linux = boot/initramfs-linux.img
pacman = var/lib/pacman/local
update-mime-database = usr/share/mime/magic

```

Then, when using `# pacreport --unowned-files`, any unowned files will be listed if the associated package is no longer installed (or if any new files have been created).

Additionally, [aconfmgr](https://github.com/CyberShadow/aconfmgr) ([aconfmgr-git](https://aur.archlinux.org/packages/aconfmgr-git/)) allows tracking modified and orphaned files using a configuration script.

### Removing unused packages (orphans)

For recursively removing orphans and their configuration files:

```
# pacman -Rns $(pacman -Qtdq)

```

If no orphans were found *pacman* outputs `error: no targets specified`. This is expected as no arguments were passed to `pacman -Rns`.

**Note:** The arguments `-Qt` list only true orphans. To include packages which are *optionally* required by another package, pass the `-t` flag twice (*i.e.*, `-Qtt`).

### Removing everything but base group

If it is ever necessary to remove all packages except the base group, try this one-liner (requires [pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib)):

```
# pacman -R $(comm -23 <(pacman -Qq | sort) <((for i in $(pacman -Qqg base); do pactree -ul "$i"; done) | sort -u))

```

The one-liner was originally devised in [this discussion](https://bbs.archlinux.org/viewtopic.php?id=130176), and later improved in this article.

### Getting the dependencies list of several packages

Dependencies are alphabetically sorted and doubles are removed.

**Note:** To only show the tree of local installed packages, use `pacman -Qi`.

```
$ pacman -Si *packages* | awk -F'[:<=>]' '/^Depends/ {print $2}' | xargs -n1 | sort -u

```

Alternatively, with [expac](https://www.archlinux.org/packages/?name=expac):

```
$ expac -l '
' %E -S *packages* | sort -u

```

### Listing changed backup files

If you want to backup your system configuration files you could copy all files in `/etc/`, but usually you are only interested in the files that you have changed. Modified [backup files](/index.php/Pacnew_and_Pacsave_files#Package_backup_files "Pacnew and Pacsave files") can be viewed with the following command:

```
# pacman -Qii | awk '/^MODIFIED/ {print $2}'

```

Running this command with root permissions will ensure that files readable only by root (such as `/etc/sudoers`) are included in the output.

**Tip:** See [#Listing all changed files from packages](#Listing_all_changed_files_from_packages) to list all changed files *pacman* knows about, not only backup files.

### Backup the pacman database

The following command can be used to backup the local *pacman* database:

```
$ tar -cjf pacman_database.tar.bz2 /var/lib/pacman/local

```

Store the backup *pacman* database file on one or more offline media, such as a USB stick, external hard drive, or CD-R.

The database can be restored by moving the `pacman_database.tar.bz2` file into the `/` directory and executing the following command:

```
# tar -xjvf pacman_database.tar.bz2

```

**Note:** If the *pacman* database files are corrupted, and there is no backup file available, there exists some hope of rebuilding the *pacman* database. Consult [#Restore pacman's local database](#Restore_pacman's_local_database).

**Tip:** The [pakbak-git](https://aur.archlinux.org/packages/pakbak-git/) package provides a script and a [systemd](/index.php/Systemd "Systemd") service to automate the task. Configuration is possible in `/etc/pakbak.conf`.

### Check changelogs easily

When maintainers update packages, commits are often commented in a useful fashion. Users can quickly check these from the command line by installing [pacolog](https://aur.archlinux.org/packages/pacolog/). This utility lists recent commit messages for packages from the official repositories or the AUR, by using `pacolog <package>`.

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

**2.** Edit `pacman.conf` and add this repository *before* the other ones (e.g. extra, core, etc.). This is important. Do not just uncomment the one on the bottom. This way it ensures that the files from the CD/DVD/USB take precedence over those in the standard repositories:

 `/etc/pacman.conf` 
```
[custom]
SigLevel = PackageRequired
Server = file:///mnt/repo/Packages
```

**3.** Finally, synchronize the *pacman* database to be able to use the new repository:

```
# pacman -Syu

```

### Custom local repository

Use the *repo-add* script included with *pacman* to generate a database for a personal repository. Use `repo-add --help` for more details on its usage. To add a new package to the database, or to replace the old version of an existing package in the database, run:

```
$ repo-add */path/to/repo.db.tar.gz /path/to/package-1.0-1-x86_64.pkg.tar.xz*

```

**Note:** A package database is a tar file, optionally compressed. Valid extensions are *.db* or *.files* followed by an archive extension of *.tar*, *.tar.gz*, *.tar.bz2*, *.tar.xz*, or *.tar.Z*. The file does not need to exist, but all parent directories must exist.

The database and the packages do not need to be in the same directory when using *repo-add*, but keep in mind that when using *pacman* with that database, they should be together. Storing all the built packages to be included in the repository in one directory also allows to use shell glob expansion to add or update multiple packages at once:

```
$ repo-add */path/to/repo.db.tar.gz /path/to/*.pkg.tar.xz*

```

**Warning:** *repo-add* adds the entries into the database in the same order as passed on the command line. If multiple versions of the same package are involved, care must be taken to ensure that the correct version is added last. In particular, note that lexical order used by the shell depends on the locale and differs from the [vercmp](https://www.archlinux.org/pacman/vercmp.8.html) ordering used by *pacman*.

*repo-remove* is used to remove packages from the package database, except that only package names are specified on the command line.

```
$ repo-remove */path/to/repo.db.tar.gz pkgname*

```

Once the local repository database has been created, add the repository to `pacman.conf` for each system that is to use the repository. An example of a custom repository is in `pacman.conf`. The repository's name is the database filename with the file extension omitted. In the case of the example above the repository's name would simply be *repo*. Reference the repository's location using a `file://` url, or via FTP using [ftp://localhost/path/to/directory](ftp://localhost/path/to/directory).

If willing, add the custom repository to the [list of unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories"), so that the community can benefit from it.

### Network shared pacman cache

If you happen to run several Arch boxes on your LAN, you can share packages so that you can greatly decrease your download times. Keep in mind you should not share between different architectures (i.e. i686 and x86_64) or you will run into problems.

#### Read-only cache

If you are looking for a quick solution, you can simply run a standalone webserver which other computers can use as a first mirror:

```
# ln -s /var/lib/pacman/sync/*.db /var/cache/pacman/pkg
$ sudo -u http darkhttpd /var/cache/pacman/pkg --no-server-id

```

You could also run darkhttpd as a systemd service for convenience. Just add this server at the top of your `/etc/pacman.d/mirrorlist` in client machines with `Server = http://mymirror:8080`. Make sure to keep your mirror updated.

If you are already running a web server for some other purpose, you might wish to reuse that as your local repo server instead of darkhttpd. For example, if you already serve a site with [nginx](/index.php/Nginx "Nginx"), you can add an nginx server block listening on port 8080:

 `/etc/nginx/nginx.conf` 
```
server {
    listen 8080;
    root /var/cache/pacman/pkg;
    server_name myarchrepo.localdomain;
    try_files $uri $uri/;
}

```

Remember to restart nginx after making this change.

Whichever web server you use, remember to open port 8080 to local traffic (and you probably want to deny anything not local), so add a rule like the following to [iptables](/index.php/Iptables "Iptables"):

 `/etc/iptables/iptables.rules` 
```
-A TCP -s 192.168.0.0/16 -p tcp -m tcp --dport 8080 -j ACCEPT

```

Remember to restart iptables after making this change.

#### Distributed read-only cache

There are Arch-specific tools for automatically discovering other computers on your network offering a package cache. Try [pacredir](https://www.archlinux.org/packages/?name=pacredir), [pacserve](/index.php/Pacserve "Pacserve"), [pkgdistcache](https://aur.archlinux.org/packages/pkgdistcache/), or [paclan](https://aur.archlinux.org/packages/paclan/). pkgdistcache uses Avahi instead of plain UDP which may work better in certain home networks that route instead of bridge between WiFi and Ethernet.

Historically, there was [PkgD](https://bbs.archlinux.org/viewtopic.php?id=64391) and [multipkg](https://github.com/toofishes/multipkg), but they are no longer maintained.

#### Read-write cache

In order to share packages between multiple computers, simply share `/var/cache/pacman/` using any network-based mount protocol. This section shows how to use [shfs](/index.php/Shfs "Shfs") or [SSHFS](/index.php/SSHFS "SSHFS") to share a package cache plus the related library-directories between multiple computers on the same local network. Keep in mind that a network shared cache can be slow depending on the file-system choice, among other factors.

First, install any network-supporting filesystem packages: [shfs-utils](https://www.archlinux.org/packages/?name=shfs-utils), [sshfs](https://www.archlinux.org/packages/?name=sshfs), [curlftpfs](https://www.archlinux.org/packages/?name=curlftpfs), [samba](https://www.archlinux.org/packages/?name=samba) or [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils).

**Tip:**

*   To use *sshfs* or *shfs*, consider reading [Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys").
*   By default, *smbfs* does not serve filenames that contain colons, which results in the client downloading the offending package afresh. To prevent this, use the `mapchars` mount option on the client.

Then, to share the actual packages, mount `/var/cache/pacman/pkg` from the server to `/var/cache/pacman/pkg` on every client machine.

**Warning:** Do not make `/var/cache/pacman/pkg` or any of its ancestors (e.g., `/var`) a symlink. *Pacman* expects these to be directories. When *pacman* re-installs or upgrades itself, it will remove the symlinks and create empty directories instead. However during the transaction *pacman* relies on some files residing there, hence breaking the update process. Refer to [FS#50298](https://bugs.archlinux.org/task/50298) for further details.

#### two-way with rsync

Another approach in a local environment is [rsync](/index.php/Rsync "Rsync"). Choose a server for caching and enable the [Rsync#rsync daemon](/index.php/Rsync#rsync_daemon "Rsync"). On clients synchronize two-way with this share via rsync protocol. Filenames that contain colons are no problem for the rsync protocol.

Draft example for a client, using `uname -m` within the share name ensures an architecture dependant sync:

```
 # rsync rsync://server/share_$(uname -m)/ /var/cache/pacman/pkg/ ...
 # pacman ...
 # paccache ...
 # rsync /var/cache/pacman/pkg/ rsync://server/share_$(uname -m)/  ...

```

#### Dynamic reverse proxy cache using nginx

[nginx](/index.php/Nginx "Nginx") can be used to proxy package requests to official upstream mirrors and cache the results to the local disk. All subsequent requests for that package will be served directly from the local cache, minimizing the amount of internet traffic needed to update a large number of computers.

In this example, the cache server will run at `http://cache.domain.example:8080/` and store the packages in `/srv/http/pacman-cache/`.

Install [nginx](/index.php/Nginx "Nginx") on the computer that is going to host the cache. Create the directory for the cache and adjust the permissions so nginx can write files to it:

```
 # mkdir /srv/http/pacman-cache
 # chown http:http /srv/http/pacman-cache

```

Use the [nginx pacman cache config](https://github.com/nastasie-octavian/nginx_pacman_cache_config/blob/87d4897b8fa37e70da4238d7074c639c041daf39/nginx.conf) as a starting point for `/etc/nginx/nginx.conf`. Check that the `resolver` directive works for your needs. In the upstream server blocks, configure the `proxy_pass` directives with addresses of official mirrors, see examples in the config file about the expected format. Once you are satisfied with the configuration file [start and enable nginx](/index.php/Nginx#Running "Nginx").

In order to use the cache each Arch Linux computer (including the one hosting the cache) must have the following line at the top of the `mirrorlist` file:

 `/etc/pacman.d/mirrorlist` 
```
Server = http://cache.domain.example:8080/$repo/os/$arch
...

```

**Note:** You will need to create a method to clear old packages, as the cache directory will continue to grow over time. `paccache` (which is provided by [pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib)) can be used to automate this using retention criteria of your choosing. For example, `find /srv/http/pacman-cache/ -type d -exec paccache -v -r -k 2 -c {} \;` will keep the last 2 versions of packages in your cache directory.

#### Synchronize pacman package cache using synchronization programs

Use [Syncthing](/index.php/Syncthing "Syncthing") or [Resilio Sync](/index.php/Resilio_Sync "Resilio Sync") to synchronize the *pacman* cache folders (i.e. `/var/cache/pacman/pkg`).

#### Preventing unwanted cache purges

By default, `pacman -Sc` removes package tarballs from the cache that correspond to packages that are not installed on the machine the command was issued on. Because *pacman* cannot predict what packages are installed on all machines that share the cache, it will end up deleting files that should not be.

To clean up the cache so that only *outdated* tarballs are deleted, add this entry in the `[options]` section of `/etc/pacman.conf`:

```
CleanMethod = KeepCurrent

```

### Recreate a package from the file system

To recreate a package from the file system, use [fakepkg](https://aur.archlinux.org/packages/fakepkg/). Files from the system are taken as they are, hence any modifications will be present in the assembled package. Distributing the recreated package is therefore discouraged; see [ABS](/index.php/ABS "ABS") and [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive") for alternatives.

### List of installed packages

Keeping a list of all the explicitly installed packages can be useful, to backup a system for example or speed up installation on a new system:

```
$ pacman -Qqe > pkglist.txt

```

**Note:**

*   With option `-t`, the packages already required by other explicitly installed packages are not mentioned. If reinstalling from this list they will be installed but as dependencies only.
*   With option `-n`, foreign packages (e.g. from [AUR](/index.php/AUR "AUR")) would be omitted from the list.
*   Use `comm -13 <(pacman -Qqdt | sort) <(pacman -Qqdtt | sort) > optdeplist.txt` to also create a list of the installed optional dependencies which can be reinstalled with `--asdeps`.
*   Use `pacman -Qqem > foreignpkglist.txt` to create the list of AUR and other foreign packages that have been explicitly installed.

To keep an up-to-date list of explicitly installed packages (e.g. in combination with a versioned `/etc/`), you can set up a [hook](/index.php/Pacman#Hooks "Pacman"). Example:

```
[Trigger]
Operation = Install
Operation = Remove
Type = Package
Target = *

[Action]
When = PostTransaction
Exec = /bin/sh -c '/usr/bin/pacman -Qqe > /etc/pkglist.txt'

```

### Install packages from a list

To install packages from a previously saved list of packages, while not reinstalling previously installed packages that are already up-to-date, run:

```
# pacman -S --needed - < pkglist.txt

```

However, it is likely foreign packages such as from the AUR or installed locally are present in the list. To filter out from the list the foreign packages, the previous command line can be enriched as follows:

```
# pacman -S --needed $(comm -12 <(pacman -Slq | sort) <(sort pkglist.txt))

```

Eventually, to make sure the installed packages of your system match the list and remove all the packages that are not mentioned in it:

```
# pacman -Rsu $(comm -23 <(pacman -Qq | sort) <(sort pkglist.txt))

```

**Tip:** These tasks can be automated. See [bacpac](https://aur.archlinux.org/packages/bacpac/), [packup](https://aur.archlinux.org/packages/packup/), [pacmanity](https://aur.archlinux.org/packages/pacmanity/), and [pug](https://aur.archlinux.org/packages/pug/) for examples.

### Listing all changed files from packages

If you are suspecting file corruption (e.g. by software/hardware failure), but are unsure if files were corrupted, you might want to compare with the hash sums in the packages. This can be done with [pacutils](https://www.archlinux.org/packages/?name=pacutils):

```
# paccheck --md5sum --quiet

```

For recovery of the database see [#Restore pacman's local database](#Restore_pacman's_local_database). The `mtree` files can also be [extracted as `.MTREE` from the respective package files](#Viewing_a_single_file_inside_a_.pkg_file).

**Note:** This should **not** be used as is when suspecting malicious changes! In this case security precautions such as using a live medium and an independent source for the hash sums are advised.

### Reinstalling all packages

To reinstall all native packages, use:

```
# pacman -Qqn | pacman -S -

```

Foreign (AUR) packages must be reinstalled separately; you can list them with `pacman -Qqm`.

*Pacman* preserves the [installation reason](/index.php/Installation_reason "Installation reason") by default.

### Restore pacman's local database

See [Pacman/Restore local database](/index.php/Pacman/Restore_local_database "Pacman/Restore local database").

### Recovering a USB key from existing install

If you have Arch installed on a USB key and manage to mess it up (e.g. removing it while it is still being written to), then it is possible to re-install all the packages and hopefully get it back up and working again (assuming USB key is mounted in `/newarch`)

```
# pacman -S $(pacman -Qq --dbpath /newarch/var/lib/pacman) --root /newarch --dbpath /newarch/var/lib/pacman

```

### Viewing a single file inside a .pkg file

For example, if you want to see the contents of `/etc/systemd/logind.conf` supplied within the [systemd](https://www.archlinux.org/packages/?name=systemd) package:

```
$ bsdtar -xOf /var/cache/pacman/pkg/systemd-204-3-x86_64.pkg.tar.xz etc/systemd/logind.conf

```

Or you can use [vim](https://www.archlinux.org/packages/?name=vim) to browse the archive:

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

### Installing only content in required languages

Many packages attempt to install documentation and translations in several languages. Some programs are designed to remove such unnecessary files, such as [localepurge](https://aur.archlinux.org/packages/localepurge/), which runs after a package is installed to delete the unneeded locale files. A more direct approach is provided through the `NoExtract` directive in `pacman.conf`, which prevent these files from ever being installed. The example below installs English (US) files, or none at all:

 `/etc/pacman.conf` 
```
NoExtract = usr/share/help/* !usr/share/help/en*
NoExtract = usr/share/gtk-doc/html/*
NoExtract = usr/share/locale/* usr/share/X11/locale/* usr/share/i18n/* opt/google/chrome/locales/*
NoExtract = !*locale*/en*/* !usr/share/i18n/charmaps/UTF-8.gz !usr/share/*locale*/locale.*
NoExtract = !usr/share/*locales/en_?? !usr/share/*locales/i18n !usr/share/*locales/iso*
NoExtract = !usr/share/*locales/trans*
NoExtract = usr/share/qt4/translations/*
NoExtract = usr/share/man/* !usr/share/man/man*
NoExtract = usr/share/vim/vim*/lang/*
NoExtract = usr/lib/libreoffice/help/en-US/*
```

Some users noted that removing locales has resulted in [unintended consequences](https://wiki.archlinux.org/index.php?title=Talk:Pacman&oldid=460285#Dangerous_NoExtract_example).

## Performance

### Download speeds

**Note:** If your download speeds have been reduced to a crawl, ensure you are using one of the many [mirrors](/index.php/Mirrors "Mirrors") and not ftp.archlinux.org, which is [throttled since March 2007](https://www.archlinux.org/news/302/).

When downloading packages *pacman* uses the mirrors in the order they are in `/etc/pacman.d/mirrorlist`. The mirror which is at the top of the list by default however may not be the fastest for you. To select a faster mirror, see [Mirrors](/index.php/Mirrors "Mirrors").

*Pacman*'s speed in downloading packages can also be improved by using a different application to download packages, instead of *pacman*'s built-in file downloader.

In all cases, make sure you have the latest *pacman* before doing any modifications.

```
# pacman -Syu

```

#### Powerpill

[Powerpill](/index.php/Powerpill "Powerpill") is a *pacman* wrapper that uses parallel and segmented downloading to try to speed up downloads for *pacman*.

#### wget

This is also very handy if you need more powerful proxy settings than *pacman*'s built-in capabilities.

To use `wget`, first [install](/index.php/Install "Install") the [wget](https://www.archlinux.org/packages/?name=wget) package then modify `/etc/pacman.conf` by uncommenting the following line in the `[options]` section:

```
XferCommand = /usr/bin/wget --passive-ftp -c -O %o %u

```

Instead of uncommenting the `wget` parameters in `/etc/pacman.conf`, you can also modify the `wget` configuration file directly (the system-wide file is `/etc/wgetrc`, per user files are `$HOME/.wgetrc`.

#### aria2

[aria2](/index.php/Aria2 "Aria2") is a lightweight download utility with support for resumable and segmented HTTP/HTTPS and FTP downloads. aria2 allows for multiple and simultaneous HTTP/HTTPS and FTP connections to an Arch mirror, which should result in an increase in download speeds for both file and package retrieval.

**Note:** Using aria2c in *pacman*'s XferCommand will **not** result in parallel downloads of multiple packages. *Pacman* invokes the XferCommand with a single package at a time and waits for it to complete before invoking the next. To download multiple packages in parallel, see [Powerpill](/index.php/Powerpill "Powerpill").

Install [aria2](https://www.archlinux.org/packages/?name=aria2), then edit `/etc/pacman.conf` by adding the following line to the `[options]` section:

```
XferCommand = /usr/bin/aria2c --allow-overwrite=true --continue=true --file-allocation=none --log-level=error --max-tries=2 --max-connection-per-server=2 --max-file-not-found=5 --min-split-size=5M --no-conf --remote-time=true --summary-interval=60 --timeout=5 --dir=/ --out %o %u

```

**Tip:** [This alternative configuration for using *pacman* with aria2](https://bbs.archlinux.org/viewtopic.php?pid=1491879#p1491879) tries to simplify configuration and adds more configuration options.

See [OPTIONS](http://aria2.sourceforge.net/manual/en/html/aria2c.html#options) in [aria2c(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/aria2c.1) for used aria2c options.

*   `-d, --dir`: The directory to store the downloaded file(s) as specified by *pacman*.
*   `-o, --out`: The output file name(s) of the downloaded file(s).
*   `%o`: Variable which represents the local filename(s) as specified by *pacman*.
*   `%u`: Variable which represents the download URL as specified by *pacman*.

#### Other applications

There are other downloading applications that you can use with *pacman*. Here they are, and their associated XferCommand settings:

*   `snarf`: `XferCommand = /usr/bin/snarf -N %u`
*   `lftp`: `XferCommand = /usr/bin/lftp -c pget %u`
*   `axel`: `XferCommand = /usr/bin/axel -n 2 -v -a -o %o %u`
*   `hget`: `XferCommand = /usr/bin/hget %u -n 2 -skip-tls false` (please read the [documentation on the Github project page](https://github.com/huydx/hget) for more info)

## Utilities

*   **Lostfiles** — Script that identifies files not owned by any package.

	[https://github.com/graysky2/lostfiles](https://github.com/graysky2/lostfiles) || [lostfiles](https://www.archlinux.org/packages/?name=lostfiles)

*   **Pacmatic** — *Pacman* wrapper to check Arch News before upgrading, avoid partial upgrades, and warn about configuration file changes.

	[http://kmkeen.com/pacmatic](http://kmkeen.com/pacmatic) || [pacmatic](https://www.archlinux.org/packages/?name=pacmatic)

*   **pacutils** — Helper library for libalpm based programs.

	[https://github.com/andrewgregory/pacutils](https://github.com/andrewgregory/pacutils) || [pacutils](https://www.archlinux.org/packages/?name=pacutils)

*   **[pkgfile](/index.php/Pkgfile "Pkgfile")** — Tool that finds what package owns a file.

	[http://github.com/falconindy/pkgfile](http://github.com/falconindy/pkgfile) || [pkgfile](https://www.archlinux.org/packages/?name=pkgfile)

*   **pkgtools** — Collection of scripts for Arch Linux packages.

	[https://github.com/Daenyth/pkgtools](https://github.com/Daenyth/pkgtools) || [pkgtools](https://aur.archlinux.org/packages/pkgtools/)

*   **[Powerpill](/index.php/Powerpill "Powerpill")** — Uses parallel and segmented downloading through [aria2](/index.php/Aria2 "Aria2") and [Reflector](/index.php/Reflector "Reflector") to try to speed up downloads for *pacman*.

	[https://xyne.archlinux.ca/projects/powerpill/](https://xyne.archlinux.ca/projects/powerpill/) || [powerpill](https://aur.archlinux.org/packages/powerpill/)

*   **repoctl** — Tool to help manage local repositories.

	[https://github.com/cassava/repoctl](https://github.com/cassava/repoctl) || [repoctl](https://aur.archlinux.org/packages/repoctl/)

*   **repose** — An Arch Linux repository building tool.

	[https://github.com/vodik/repose](https://github.com/vodik/repose) || [repose](https://www.archlinux.org/packages/?name=repose)

*   **[snap-pac](/index.php/Snapper#Wrapping_pacman_transactions_in_snapshots "Snapper")** — Make *pacman* automatically use snapper to create pre/post snapshots like openSUSE's YaST.

	[https://github.com/wesbarnett/snap-pac](https://github.com/wesbarnett/snap-pac) || [snap-pac](https://www.archlinux.org/packages/?name=snap-pac)

*   **vrms-arch** — A virtual Richard M. Stallman to tell you which non-free packages are installed.

	[https://github.com/orospakr/vrms-arch](https://github.com/orospakr/vrms-arch) || [vrms-arch](https://aur.archlinux.org/packages/vrms-arch/)

### Graphical

**Warning:** PackageKit opens up system permissions by default, and is otherwise not recommended for general usage. See [FS#50459](https://bugs.archlinux.org/task/50459) and [FS#57943](https://bugs.archlinux.org/task/57943).

*   **Apper** — Qt 5 application and package manager using PackageKit written in C++. Supports [AppStream metadata](https://www.freedesktop.org/wiki/Distributions/AppStream/).

	[https://userbase.kde.org/Apper](https://userbase.kde.org/Apper) || [apper](https://www.archlinux.org/packages/?name=apper)

*   **Discover** — Qt 5 application manager using PackageKit written in C++/QML. Supports [AppStream metadata](https://www.freedesktop.org/wiki/Distributions/AppStream/), [Flatpak](/index.php/Flatpak "Flatpak") and [firmware updates](/index.php/Fwupd "Fwupd").

	[https://userbase.kde.org/Discover](https://userbase.kde.org/Discover) || [discover](https://www.archlinux.org/packages/?name=discover)

*   **GNOME PackageKit** — GTK+ 3 package manager using PackageKit written in C.

	[https://freedesktop.org/software/PackageKit/](https://freedesktop.org/software/PackageKit/) || [gnome-packagekit](https://www.archlinux.org/packages/?name=gnome-packagekit)

*   **GNOME Software** — GTK+ 3 application manager using PackageKit written in C. Supports [AppStream metadata](https://www.freedesktop.org/wiki/Distributions/AppStream/), [Flatpak](/index.php/Flatpak "Flatpak") and [firmware updates](/index.php/Fwupd "Fwupd").

	[https://wiki.gnome.org/Apps/Software](https://wiki.gnome.org/Apps/Software) || [gnome-software](https://www.archlinux.org/packages/?name=gnome-software)

*   **pcurses** — Curses TUI pacman wrapper written in C++.

	[https://github.com/schuay/pcurses](https://github.com/schuay/pcurses) || [pcurses](https://www.archlinux.org/packages/?name=pcurses)

*   **tkPacman** — Tk pacman wrapper written in Tcl.

	[https://sourceforge.net/projects/tkpacman](https://sourceforge.net/projects/tkpacman) || [tkpacman](https://aur.archlinux.org/packages/tkpacman/)