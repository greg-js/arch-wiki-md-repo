**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – **Nonfree** – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

For many applications (most of which are Windows ones) there are neither sources nor tarballs available. Many of such applications can not be freely distributed because of license restrictions and/or lack of legal ways to obtain installer for no fee. Such software obviously can not be included into the [official repositories](/index.php/Official_repositories "Official repositories") but due to nature of [AUR](/index.php/AUR "AUR") it is still possible to privately [build packages](/index.php/Makepkg "Makepkg") for it, manageable with [pacman](/index.php/Pacman "Pacman").

**Note:** All information here is package-agnostic, for information specific to the most typical nonfree software see [Wine PKGBUILD guidelines](/index.php/Wine_PKGBUILD_guidelines "Wine PKGBUILD guidelines").

## Contents

*   [1 Rationale](#Rationale)
*   [2 Common rules](#Common_rules)
    *   [2.1 Avoid nonfree software when possible](#Avoid_nonfree_software_when_possible)
    *   [2.2 Use open source variants where possible](#Use_open_source_variants_where_possible)
    *   [2.3 Keep it simple](#Keep_it_simple)
*   [3 Package naming](#Package_naming)
*   [4 File placement](#File_placement)
*   [5 Missing files](#Missing_files)
*   [6 Advanced topics](#Advanced_topics)
    *   [6.1 Custom DLAGENTS](#Custom_DLAGENTS)
    *   [6.2 Unpacking](#Unpacking)
    *   [6.3 Getting icons for .desktop files](#Getting_icons_for_.desktop_files)

## Rationale

There are multiple reasons for packaging even non-packageable software:

*   Simplification of installation/removal process

	This is applicable even to the simplest of apps, which consist of a single script to be installed into `/usr/bin`. Instead of issuing:

	 `$ chmod +x *filename*` 

	 `# cp *filename* /usr/bin/` 

	you can type just

	 `# makepkg -i` 

	Most non-free applications are obviously much more complicated, but the burden of downloading an archive/installer from a homepage (often full of advertising), unpacking/decrypting it, hand-writing stereotypical launcher scripts and doing other similar tasks can be effectively lightened by a well-written packaging script.

*   Utilizing pacman capabilities

	The ability to track state, perform automatic updates of any installed piece of software, determine ownership of every single file, and store compressed packages in a well-organized cache is what makes GNU/Linux distributions so powerful.

*   Sharing code and knowledge

	It is simpler to apply tweaks, fix bugs and seek/provide help in a single public place like AUR versus submitting patches to proprietary developers who may have ceased support or asking vague questions on general purpose forums.

## Common rules

### Avoid nonfree software when possible

Yes, it's better to leave this guide and spend some time searching (or maybe even creating) alternatives to an application you wanted to package because:

1.  It is better to support software that is owned by us all than software that is owned by a company
2.  It is better to support software that is actively maintained
3.  It is better to support software that can be fixed if just one person out of millions cares enough

### Use open source variants where possible

Many commercial games ([some are listed in this Wiki](/index.php/List_of_Applications/Games "List of Applications/Games")) have open source engines and many old games can be played with emulators such as [ScummVM](https://en.wikipedia.org/wiki/ScummVM "wikipedia:ScummVM"). Using open source engines together with the original game assets gives users access to bug fixes and eliminates several issues caused by binary packages.

### Keep it simple

If the packaging of some program requires more effort and hacks than buying and using the original version - do the simplest thing, it is Arch!

## Package naming

Before choosing a name on your own, search in AUR for existing versions of the software you want to package. Try to use established naming conversion (e.g. do not create something like [gish-hb](https://aur.archlinux.org/packages/gish-hb/) when there are already [aquaria-hib](https://aur.archlinux.org/packages/aquaria-hib/), [penumbra-overture-hib](https://aur.archlinux.org/packages/penumbra-overture-hib/) and [uplink-hib](https://aur.archlinux.org/packages/uplink-hib/)). Use suffix `-bin` **always** unless you are sure there will never be a source-based package—its creator would have to ask you (or in worst case TUs) to orphan existing package for him and you both will end up with PKGBUILDs cluttered with additional `replaces` and `conflicts`.

## File placement

Again, analyze existing packages (if present) and decide whether or not you want to conflict with them. Do not place things under `/opt` unless you want to use some ugly hacks like giving ownership `root:games` to the package directory (so users in group `games` running the game can write files in the game's own folder).

## Missing files

For most commercial games there is no way to (legally) download game files, which is the preferable way to get them for normal packages. Even when it is possible to download files after providing a password (like with all [Humble Indie Bundle](https://en.wikipedia.org/wiki/Humble_Indie_Bundle "wikipedia:Humble Indie Bundle") games) asking user for this password and downloading somewhere in `build` function is not recommended for a variety of reasons (for example, the user may have no Internet access but have all files downloaded and stored locally). The following options should be considered:

*   **There is only one way to obtain files**

*   Software is distributed in archive/installer

	Add the required file to `sources` array:

	 `sources=(... "*originalname*::**file://***originalname*")` 

	This way the link to file in AUR web interface will look different from names of files included in source tarball.

	Add following comment on package page:

	 `Need archive/installer to work.` 

	and explain the details in PKGBUILD source.

*   Software is distributed on compact-disk

	Add installer script and `.install` file to package contents, like in package [tsukihime-en](https://aur.archlinux.org/packages/tsukihime-en/).

*   **There are several ways to obtain files**

Copying files from disk / downloading from Net / getting from archive during `build` phase may look like a good idea but it is not recommended because it limits the user's possibilities and makes package installation interactive (which is generally discouraged and just annoying). Again, a good installer script and `.install` file can work instead.

Few examples of various strategies for obtaining files required for package:

*   [worldofgoo](https://aur.archlinux.org/packages/worldofgoo/) – dependency on user-provided file
*   [umineko-en](https://aur.archlinux.org/packages/umineko-en/) – combining files from freely available patch and user-provided compact-disk
*   [worldofgoo-demo](https://aur.archlinux.org/packages/worldofgoo-demo/) – autonomic fetching installer during build phase
*   [ut2004-anthology](https://aur.archlinux.org/packages/ut2004-anthology/) – searching for disk via mountpoints

## Advanced topics

### Custom DLAGENTS

Some software authors aggressively protect their software from automatic downloading: ban certain "User-Agent" strings, create temporary links to files etc. You can still conveniently download this files by using `DLAGENTS` variable in PKGBUILD (see `man makepkg.conf`). This is used by some packages in [official repositories](/index.php/Official_repositories "Official repositories"), for example [ttf-baekmuk](https://www.archlinux.org/packages/?name=ttf-baekmuk).

Please pay attention, if you want to have a customized user-agent string, if the latter contains spaces, parentheses, or slashes in it (or actually anything that can break parsing), this will not work. There's no workaround, this is the nature of arrays in bash and the way DLAGENTS was designed to be consumed in makepkg. The following example will thus **not work**:

```
DLAGENTS=("http::/usr/bin/curl -A 'Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)' -fLC - --retry 3 --retry-delay 3 -o %o %u")

```

Shorten it to the following which is working:

```
DLAGENTS=("http::/usr/bin/curl -A 'Mozilla' -fLC - --retry 3 --retry-delay 3 -o %o %u")

```

And following allows to extract temporary link to file from download page:

```
DLAGENTS=("http::/usr/bin/wget -r -np -nd -H %u")

```

### Unpacking

Many proprietary programs are shipped in nasty installers which sometimes do not even run in Wine. Following tools may be of some help:

*   [unzip](https://www.archlinux.org/packages/?name=unzip) and [unrar](https://www.archlinux.org/packages/?name=unrar) unpack executable SFX archives, based on this formats
*   [cabextract](https://www.archlinux.org/packages/?name=cabextract) can unpack most `.cab` files (including ones with `.exe` extension)
*   [unshield](https://www.archlinux.org/packages/?name=unshield) can extract CAB files from InstallShield installers
*   [p7zip](https://www.archlinux.org/packages/?name=p7zip) unpacks not only many archive formats but also [NSIS](https://en.wikipedia.org/wiki/NSIS "wikipedia:NSIS")-based `.exe` installers
    *   it even can extract single sections from common PE (`.exe` & `.dll`) files!
*   [upx](https://www.archlinux.org/packages/?name=upx) is sometimes used to encrypt above-listed executables and can be used for decryption as well
*   [innoextract](https://aur.archlinux.org/packages/innoextract/) can unpack `.exe` installers created with [Inno Setup](https://en.wikipedia.org/wiki/Inno_Setup "wikipedia:Inno Setup") (used for example by GOG.com games)

In order to determine exact type of file run `file *file_of_unknown_type*`.

### Getting icons for .desktop files

Proprietary software often have no separate icon files, so there is nothing to use in [.desktop](/index.php/.desktop ".desktop") file creation. Happily `.ico` files can be easily extracted from executables with programs from [icoutils](https://www.archlinux.org/packages/?name=icoutils) package. You can even do it on fly during `build` phase (example can be found in [sugarsdelight](https://aur.archlinux.org/packages/sugarsdelight/)).