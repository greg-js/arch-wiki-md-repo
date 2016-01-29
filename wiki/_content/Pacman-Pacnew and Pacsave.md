# Pacman/Pacnew and Pacsave

See [pacman](/index.php/Pacman "Pacman") for the main article.

When _pacman_ removes a package that has a configuration file, it normally creates a backup copy of that config file and appends _.pacsave_ to the name of the file. Likewise, when _pacman_ upgrades a package which includes a new config file created by the maintainer differing from the currently installed file, it writes a _.pacnew_ config file. Occasionally, under special circumstances, a _.pacorig_ file is created. _pacman_ provides notice when these files are written.

## Contents

*   [1 Why these files are created](#Why_these_files_are_created)
*   [2 Package backup files](#Package_backup_files)
*   [3 Types explained](#Types_explained)
    *   [3.1 .pacnew](#.pacnew)
    *   [3.2 .pacsave](#.pacsave)
    *   [3.3 .pacorig](#.pacorig)
*   [4 Locating .pac* files](#Locating_.pac.2A_files)
*   [5 Managing .pacnew files](#Managing_.pacnew_files)
*   [6 See also](#See_also)

## Why these files are created

A _.pacnew_ file may be created during a package upgrade (`pacman -Syu`, `pacman -Su` or `pacman -U`) to avoid overwriting a file which already exists and was previously modified by the user. When this happens a message like the following will appear in the output of pacman:

```
warning: /etc/pam.d/usermod installed as /etc/pam.d/usermod.pacnew

```

A _.pacsave_ file may be created during a package removal (`pacman -R`), or by a package upgrade (the package must be removed first). When the pacman database has record that a certain file owned by the package should be backed up it will create a _.pacsave_ file. When this happens pacman outputs a message like the following:

```
warning: /etc/pam.d/usermod saved as /etc/pam.d/usermod.pacsave

```

These files require manual intervention from the user and it is good practice to handle them right after every package upgrade or removal. If left unhandled, improper configurations can result in improper function of the software, or the software being unable to run altogether.

## Package backup files

A package's `PKGBUILD` file specifies which files should be preserved or backed up when the package is upgraded or removed. For example, the `PKGBUILD` for `pulseaudio` contains the following line:

```
backup=('etc/pulse/client.conf' 'etc/pulse/daemon.conf' 'etc/pulse/default.pa')

```

## Types explained

### .pacnew

For each `backup` file in a package being upgraded, pacman cross-compares three [md5sums](https://en.wikipedia.org/wiki/Md5sum "wikipedia:Md5sum") generated from the file's contents: one sum for the version originally installed by the package, one for the version currently in the filesystem, and one for the version in the new package. If the version of the file currently in the filesystem has been modified from the version originally installed by the package, pacman cannot know how to merge those changes with the new version of the file. Therefore, instead of overwriting the modified file when upgrading, pacman saves the new version with a _.pacnew_ extension and leaves the modified version untouched.

Going into further detail, the 3-way MD5 sum comparison results in one of the following outcomes:

NaN

NaN

NaN

NaN

NaN

### .pacsave

If the user has modified one of the files specified in `backup` then that file will be renamed with a _.pacsave_ extension and will remain in the filesystem after the rest of the package is removed.

**Note:** Use of the `-n` option with `pacman -R` will result in complete removal of _all_ files in the specified package, therefore no _.pacsave_ files will be created.

### .pacorig

When a file (usually a configuration found in `/etc`) is encountered during package installation or upgrade that does not belong to any installed package but is listed in `backup` for the package in the current operation, it will be saved with a _.pacorig_ extension and replaced with the version of the file from the package. Usually this happens when a configuration file has been moved from one package to another. If such a file were not listed in `backup`, pacman would abort with a file conflict error.

**Note:** Because _.pacorig_ files tend to be created for special circumstances, there is no universal method for handling them. It may be helpful to consult the [Arch News](https://www.archlinux.org/news/) for handling instructions if it is a known case.

## Locating .pac* files

Pacman does not deal with _.pacnew_ files automatically: you will need to maintain these yourself. A few tools are presented in the next section. To do this manually, first you will need to locate them. When upgrading or removing a large number of packages, updated `*.pac*` files may be missed. To discover whether any `*.pac*` files have been installed, use one of the following:

*   To just search where most global configurations are stored: `$ find /etc -regextype posix-extended -regex ".+\.pac(new|save|orig)" 2> /dev/null` or the entire disk: `$ find / -regextype posix-extended -regex ".+\.pac(new|save|orig)" 2> /dev/null` 
*   Use [locate](/index.php/Locate "Locate") if you have installed it. First re-index the database: `# updatedb` Then: `$ locate -e --regex "\.pac(new|orig|save)$"` 
*   Use pacman's log to find them: `$ egrep "pac(new|orig|save)" /var/log/pacman.log` Note that the log does not keep track of which files are currently in the filesystem nor of which files have already been removed

## Managing .pacnew files

Pacman includes the simple _pacdiff_ tool for managing pacnew/pacorig/pacsave files. It will search all `pacnew` and `pacsave` files and ask for any actions on them. It uses [vimdiff](/index.php/Vim#Merging_files "Vim") by default, but you may specify a different tool with `DIFFPROG=your_editor pacdiff`. See [List of applications/Utilities#Comparison, diff, merge](/index.php/List_of_applications/Utilities#Comparison.2C_diff.2C_merge "List of applications/Utilities") for other common comparison tools.

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** The _.pacnew_ files on [filesystem](https://www.archlinux.org/packages/?name=filesystem) updates should be mentioned in a note (also with a link to [Users and groups](/index.php/Users_and_groups "Users and groups")); handling them wrong may damage the system. (Discuss in [ArchWiki:Requests#User_and_group_pacnew_files](https://wiki.archlinux.org/index.php/ArchWiki:Requests#User_and_group_pacnew_files))

A few third-party utilities providing various levels of automation for these tasks are available from the [AUR](/index.php/AUR "AUR").

You can use one of the following tools:

*   **diffpac** — Standalone pacdiffviewer replacement

NaN

*   **[Dotpac](/index.php/Dotpac "Dotpac")** — Basic interactive script with ncurses-based text interface and helpful walkthrough. No merging or auto-merging features.

NaN

*   **etc-update** — Arch port of Gentoo's _etc-update_ utility, providing a simple CLI to view, merge and interactively edit changes. Trivial changes (such as comments) can be merged automatically.

NaN

*   **pacdiffviewer** — Fully-featured interactive CLI script with automatic merging. Part of [Yaourt](/index.php/Yaourt "Yaourt").

NaN

*   **pacmerge-git** — Interactive CLI merge program.

NaN

*   **pacnew-auto** — Automatic `pacnew` merging using [git](https://www.archlinux.org/packages/?name=git) rebase.

NaN

*   **pacnews-git** — A simple script aimed at finding all _.pacnew_ files, then editing them with [vimdiff](/index.php/Vim#Merging_files "Vim").

NaN

## See also

*   Arch Linux Forum: [Dealing with .pacnew files](https://bbs.archlinux.org/viewtopic.php?id=53532)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Pacman/Pacnew_and_Pacsave&oldid=409373](https://wiki.archlinux.org/index.php?title=Pacman/Pacnew_and_Pacsave&oldid=409373)"