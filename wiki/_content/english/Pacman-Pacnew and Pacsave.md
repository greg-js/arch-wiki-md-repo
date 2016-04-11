See [pacman](/index.php/Pacman "Pacman") for the main article.

When *pacman* removes a package that has a configuration file, it normally creates a backup copy of that config file and appends *.pacsave* to the name of the file. Likewise, when *pacman* upgrades a package which includes a new config file created by the maintainer differing from the currently installed file, it writes a *.pacnew* config file. *pacman* provides notice when these files are written.

## Contents

*   [1 Why these files are created](#Why_these_files_are_created)
*   [2 Package backup files](#Package_backup_files)
*   [3 Types explained](#Types_explained)
    *   [3.1 .pacnew](#.pacnew)
    *   [3.2 .pacsave](#.pacsave)
*   [4 Locating .pac* files](#Locating_.pac.2A_files)
*   [5 Managing .pacnew files](#Managing_.pacnew_files)
*   [6 See also](#See_also)

## Why these files are created

A *.pacnew* file may be created during a package upgrade (`pacman -Syu`, `pacman -Su` or `pacman -U`) to avoid overwriting a file which already exists and was previously modified by the user. When this happens a message like the following will appear in the output of pacman:

```
warning: /etc/pam.d/usermod installed as /etc/pam.d/usermod.pacnew

```

A *.pacsave* file may be created during a package removal (`pacman -R`), or by a package upgrade (the package must be removed first). When the pacman database has record that a certain file owned by the package should be backed up it will create a *.pacsave* file. When this happens pacman outputs a message like the following:

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

For each `backup` file in a package being upgraded, pacman cross-compares three [md5sums](https://en.wikipedia.org/wiki/Md5sum "wikipedia:Md5sum") generated from the file's contents: one sum for the version originally installed by the package, one for the version currently in the filesystem, and one for the version in the new package. If the version of the file currently in the filesystem has been modified from the version originally installed by the package, pacman cannot know how to merge those changes with the new version of the file. Therefore, instead of overwriting the modified file when upgrading, pacman saves the new version with a *.pacnew* extension and leaves the modified version untouched.

Going into further detail, the 3-way MD5 sum comparison results in one of the following outcomes:

	original = *X*, current = *X*, new = *X* 

	All three versions of the file have identical contents, so overwriting is not a problem. Overwrite the current version with the new version and do not notify the user (although the file contents are the same, this overwrite will update the filesystem's information regarding the file's installed, modified, and accessed times, as well as ensure that any file permission changes are applied).

	original = *X*, current = *X*, new = *Y* 

	The current version's contents are identical to the original's, but the new version is different. Since the user has not modified the current version and the new version may contain improvements or bugfixes, overwrite the current version with the new version and do not notify the user. This is the only auto-merging of new changes that pacman is capable of performing.

	original = *X*, current = *Y*, new = *X* 

	The original package and the new package both contain exactly the same version of the file, but the version currently in the filesystem has been modified. Leave the current version in place and discard the new version without notifying the user.

	original = *X*, current = *Y*, new = *Y* 

	The new version is identical to the current version. Overwrite the current version with the new version and do not notify the user (although the file contents are the same, this overwrite will update the filesystem's information regarding the file's installed, modified, and accessed times, as well as ensure that any file permission changes are applied).

	original = *X*, current = *Y*, new = *Z* 

	All three versions are different, so leave the current version in place, install the new version with a *.pacnew* extension and warn the user about the new version. The user will be expected to manually merge any changes necessary from the new version into the current version.

### .pacsave

If the user has modified one of the files specified in `backup` then that file will be renamed with a *.pacsave* extension and will remain in the filesystem after the rest of the package is removed.

**Note:** Use of the `-n` option with `pacman -R` will result in complete removal of *all* files in the specified package, therefore no *.pacsave* files will be created.

## Locating .pac* files

Pacman does not deal with *.pacnew* files automatically: you will need to maintain these yourself. A few tools are presented in the next section. To do this manually, first you will need to locate them. When upgrading or removing a large number of packages, updated `*.pac*` files may be missed. To discover whether any `*.pac*` files have been installed, use one of the following:

*   To just search where most global configurations are stored: `$ find /etc -regextype posix-extended -regex ".+\.pac(new|save)" 2> /dev/null` or the entire disk: `$ find / -regextype posix-extended -regex ".+\.pac(new|save)" 2> /dev/null` 
*   Use [locate](/index.php/Locate "Locate") if you have installed it. First re-index the database: `# updatedb` Then: `$ locate --existing --regex "\.pac(new|save)$"` 
*   Use pacman's log to find them: `$ grep --extended-regexp "pac(new|save)" /var/log/pacman.log` Note that the log does not keep track of which files are currently in the filesystem nor of which files have already been removed; the above command will list all `*.pac*` files that have ever existed on your system. Use the `tail` command to get the 10 most recent `*.pac*` files: `$ grep --extended-regexp "pac(new|save)" /var/log/pacman.log | tail` 

## Managing .pacnew files

Pacman includes the simple *pacdiff* tool for managing pacnew/pacsave files. It will search all `pacnew` and `pacsave` files and ask for any actions on them. It uses [vimdiff](/index.php/Vim#Merging_files "Vim") by default, but you may specify a different tool with `DIFFPROG=your_editor pacdiff`. See [List of applications/Utilities#Comparison, diff, merge](/index.php/List_of_applications/Utilities#Comparison.2C_diff.2C_merge "List of applications/Utilities") for other common comparison tools.

A few third-party utilities providing various levels of automation for these tasks are available from the [AUR](/index.php/AUR "AUR").

You can use one of the following tools:

*   **diffpac** — Standalone pacdiffviewer replacement

	[https://github.com/bruenig/diffpac](https://github.com/bruenig/diffpac) || [diffpac](https://aur.archlinux.org/packages/diffpac/)

*   **[Dotpac](/index.php/Dotpac "Dotpac")** — Basic interactive script with ncurses-based text interface and helpful walkthrough. No merging or auto-merging features.

	[https://github.com/AladW/dotpac](https://github.com/AladW/dotpac) || [dotpac](https://aur.archlinux.org/packages/dotpac/)

*   **etc-update** — Arch port of Gentoo's *etc-update* utility, providing a simple CLI to view, merge and interactively edit changes. Trivial changes (such as comments) can be merged automatically.

	[https://wiki.gentoo.org/wiki/Handbook:Parts/Portage/Tools#etc-update](https://wiki.gentoo.org/wiki/Handbook:Parts/Portage/Tools#etc-update) || [etc-update](https://aur.archlinux.org/packages/etc-update/)

*   **pacdiffviewer** — Fully-featured interactive CLI script with automatic merging. Part of [Yaourt](/index.php/Yaourt "Yaourt").

	[http://archlinux.fr/yaourt-en](http://archlinux.fr/yaourt-en) || [yaourt](https://aur.archlinux.org/packages/yaourt/)

*   **pacmerge-git** — Interactive CLI merge program.

	[https://gitorious.org/pacmerge](https://gitorious.org/pacmerge) || [pacmerge-git](https://aur.archlinux.org/packages/pacmerge-git/)

*   **pacnew-auto** — Automatic `pacnew` merging using [git](https://www.archlinux.org/packages/?name=git) rebase.

	[https://github.com/joanrieu/pacnew-auto](https://github.com/joanrieu/pacnew-auto) || [pacnew-auto-git](https://aur.archlinux.org/packages/pacnew-auto-git/)

*   **pacnews-git** — A simple script aimed at finding all *.pacnew* files, then editing them with [vimdiff](/index.php/Vim#Merging_files "Vim").

	[https://github.com/pbrisbin/scripts/blob/master/pacnews](https://github.com/pbrisbin/scripts/blob/master/pacnews) || [pacnews-git](https://aur.archlinux.org/packages/pacnews-git/)

## See also

*   Arch Linux Forum: [Dealing with .pacnew files](https://bbs.archlinux.org/viewtopic.php?id=53532)