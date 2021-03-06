**[Package creation guidelines](/index.php/Arch_packaging_standards "Arch packaging standards")**

* * *

[32-bit](/index.php/32-bit_package_guidelines "32-bit package guidelines") – [CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Electron](/index.php/Electron_package_guidelines "Electron package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – <a class="mw-selflink selflink">Nonfree</a> – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [R](/index.php/R_package_guidelines "R package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [Rust](/index.php/Rust_package_guidelines "Rust package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

For many applications (most of which are Windows ones) there are neither sources nor tarballs available. Many of such applications can not be freely distributed because of license restrictions and/or lack of legal ways to obtain installer for no fee. Such software obviously can not be included into the [official repositories](/index.php/Official_repositories "Official repositories") but due to nature of [AUR](/index.php/AUR "AUR") it is still possible to privately [build packages](/index.php/Makepkg "Makepkg") for it, manageable with [pacman](/index.php/Pacman "Pacman").

**Note:** All information here is package-agnostic, for information specific to the most typical nonfree software see [Wine PKGBUILD guidelines](/index.php/Wine_PKGBUILD_guidelines "Wine PKGBUILD guidelines").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Rationale](#Rationale)
*   [2 Common rules](#Common_rules)
    *   [2.1 Avoid nonfree software when possible](#Avoid_nonfree_software_when_possible)
    *   [2.2 Use open source variants where possible](#Use_open_source_variants_where_possible)
    *   [2.3 Keep it simple](#Keep_it_simple)
*   [3 Package naming](#Package_naming)
*   [4 File placement](#File_placement)
*   [5 Missing files](#Missing_files)
    *   [5.1 Files can only be obtained in a distributed archive/installer](#Files_can_only_be_obtained_in_a_distributed_archive/installer)
        *   [5.1.1 Scheme to choose](#Scheme_to_choose)
    *   [5.2 Files can only be obtained in an distributed compact-disk or other type of optical disk media](#Files_can_only_be_obtained_in_an_distributed_compact-disk_or_other_type_of_optical_disk_media)
    *   [5.3 Files can be obtained from several ways](#Files_can_be_obtained_from_several_ways)
*   [6 Advanced topics](#Advanced_topics)
    *   [6.1 Custom DLAGENTS](#Custom_DLAGENTS)
    *   [6.2 Unpacking](#Unpacking)
    *   [6.3 Getting icons for .desktop files](#Getting_icons_for_.desktop_files)

## Rationale

There are multiple reasons for packaging even non-packageable software:

*   Simplification of installation/removal process

	This is applicable even to the simplest of apps, which consist of a single script to be installed into `/usr/bin`. Instead of issuing:

	 `$ chmod +x *filename*` 

	 `$ chown root:root *filename*` 

	 `# cp *filename* /usr/bin/` 

	you can type just

	 `$ makepkg -i` 

	Most non-free applications are obviously much more complicated, but the burden of downloading an archive/installer from a homepage (often full of advertising), unpacking/decrypting it, hand-writing stereotypical launcher scripts and doing other similar tasks can be effectively lightened by a well-written packaging script.

*   Utilizing pacman capabilities

	The ability to track state, perform automatic updates of any installed piece of software, determine ownership of every single file, and store compressed packages in a well-organized cache is what makes GNU/Linux distributions so powerful.

*   Sharing code and knowledge

	It is simpler to apply tweaks, fix bugs and seek/provide help in a single public place like the AUR versus submitting patches to proprietary developers who may have ceased support or asking vague questions on general purpose forums.

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

Before choosing a name on your own, search in the AUR for existing versions of the software you want to package. Try to use established naming conventions (e.g. do not create something like [gish-hb](https://aur.archlinux.org/packages/gish-hb/) when there are already packages for [aquaria-hib](https://aur.archlinux.org/packages/aquaria-hib/), [penumbra-overture-hib](https://aur.archlinux.org/packages/penumbra-overture-hib/) and [uplink-hib](https://aur.archlinux.org/packages/uplink-hib/)). Use the suffix `-bin` **always** unless you are sure there will never be a source-based package—its creator would have to ask you (or in the worst case a TU) to orphan the existing package for him and you both will end up with PKGBUILDs cluttered with additional `replaces` and `conflicts`.

## File placement

Again, analyze existing packages (if present) and decide whether or not you want to conflict with them. Do not place things under `/opt` unless you want to use some ugly hacks like giving ownership `root:games` to the package directory (so users in group `games` running the game can write files in the game's own folder).

## Missing files

For most commercial games there is no way to (legally) download game files, which is the preferable way to get them for normal packages. Even when it is possible to download files after providing a password (like with all [Humble Indie Bundle](https://en.wikipedia.org/wiki/Humble_Indie_Bundle "wikipedia:Humble Indie Bundle") games) asking user for this password and downloading somewhere in `build` function is not recommended for a variety of reasons (for example, the user may have no Internet access but have all files downloaded and stored locally).

The subsections below provide recommendations for a few situations you may encounter.

### Files can only be obtained in a distributed archive/installer

The software is only available via that archive/installer file, which must be obtained in order to get the missing files.

Add the required archive/installer to the `source` array, renaming the source filename so the source's link in the AUR web interface looks different from names of files included in the source tarball:

 `sources=(... "*originalname*::**local:**//*originalname*")` 

Also add a pinned comment like the one below to the package page in the AUR, and explain the details in the PKGBUILD:

 `Need archive/installer to work.` 

#### Scheme to choose

In case you use the **local://** scheme in a source array, makepkg behaves as though no scheme were specified, and the file must be manually placed in the same directory as the PKGBUILD.

In case you use the **file://** scheme, you can additionally specify DLAGENTS for the file protocol, so it may be obtained in a special way. See examples [below](#Custom_DLAGENTS).

However, there are still no clear rules which of these schemes you should use.

### Files can only be obtained in an distributed compact-disk or other type of optical disk media

The software is only available via an optical disk media (e.g. CD, DVD, Bluray etc.), which must be inserted into the optical disk drive in order get the missing files.

Add an installer script and an `.install` file to the package contents, like [tsukihime-en](https://aur.archlinux.org/packages/tsukihime-en/).

### Files can be obtained from several ways

Copying files from disk, downloading from Net or getting from archive during the `build` phase may look like a good idea but it is not recommended because it limits the user's possibilities and makes package installation interactive (which is generally discouraged and just annoying). Again, a good installer script and `.install` file can work instead.

Few examples of various strategies for obtaining files required for package:

*   [worldofgoo](https://aur.archlinux.org/packages/worldofgoo/) – dependency on user-provided file
*   [umineko-en](https://aur.archlinux.org/packages/umineko-en/) – combining files from freely available patch and user-provided compact-disk
*   [worldofgoo-demo](https://aur.archlinux.org/packages/worldofgoo-demo/) – autonomic fetching installer during build phase
*   [ut2004-anthology](https://aur.archlinux.org/packages/ut2004-anthology/) – searching for disk via mountpoints

## Advanced topics

### Custom DLAGENTS

Some software authors aggressively protect their software from automatic downloading: ban certain "User-Agent" strings, create temporary links to files etc. You can still conveniently download these files by using `DLAGENTS` variable in the PKGBUILD (see [makepkg.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/makepkg.conf.5)). This is used by some packages in [official repositories](/index.php/Official_repositories "Official repositories"), for example in previous version of [ttf-baekmuk](https://git.archlinux.org/svntogit/community.git/tree/trunk/PKGBUILD?h=packages/ttf-baekmuk&id=bacc6309c858c2c78d1ed17151301d496c7d87ea).

Please pay attention, if you want to have a customized user-agent string, if the latter contains spaces, parentheses, or slashes in it (or actually anything that can break parsing), this will not work. There's no workaround, this is the nature of arrays in bash and the way DLAGENTS was designed to be consumed in makepkg. The following example will thus **not work**:

```
DLAGENTS=("http::/usr/bin/curl -A 'Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)' -fLC - --retry 3 --retry-delay 3 -o %o %u")

```

Shorten it to the following which is working:

```
DLAGENTS=("http::/usr/bin/curl -A 'Mozilla' -fLC - --retry 3 --retry-delay 3 -o %o %u")

```

And the following allows to extract temporary link to file from download page:

```
DLAGENTS=("http::/usr/bin/wget -r -np -nd -H %u")

```

In order to download temporary links to files or get past an interactive download, it is possible to analyze the HTTP request used to create the final download link, and then create a DLAGENTS that emulates this using curl. See for example [blackmagic-decklink-sdk](https://aur.archlinux.org/packages/blackmagic-decklink-sdk/) or [jlink-software-and-documentation](https://aur.archlinux.org/packages/jlink-software-and-documentation/).

Alternatively, the DLAGENTS can be used to provide a more informative error message to the user when a file is missing. See for example [ttf-ms-win10](https://aur.archlinux.org/packages/ttf-ms-win10/).

### Unpacking

Many proprietary programs are shipped in nasty installers which sometimes do not even run in Wine. The following tools may be of some help:

*   [unzip](https://www.archlinux.org/packages/?name=unzip) and [unrar](https://www.archlinux.org/packages/?name=unrar) unpack executable SFX archives, based on this formats
*   [cabextract](https://www.archlinux.org/packages/?name=cabextract) can unpack most `.cab` files (including ones with `.exe` extension)
*   [unshield](https://www.archlinux.org/packages/?name=unshield) can extract CAB files from InstallShield installers
*   [p7zip](https://www.archlinux.org/packages/?name=p7zip) unpacks not only many archive formats but also [NSIS](https://en.wikipedia.org/wiki/NSIS "wikipedia:NSIS")-based `.exe` installers
    *   it even can extract single sections from common PE (`.exe` & `.dll`) files!
*   [upx](https://www.archlinux.org/packages/?name=upx) is sometimes used to compress above-listed executables and can be used for decompressing them as well
*   [innoextract](https://www.archlinux.org/packages/?name=innoextract) can unpack `.exe` installers created with [Inno Setup](https://en.wikipedia.org/wiki/Inno_Setup "wikipedia:Inno Setup") (used for example by GOG.com games)
*   [libarchive](https://www.archlinux.org/packages/?name=libarchive) contains *bsdtar*, which can extract `.iso` images and `.AppImage` files (which are actually hybrid self-executable iso9660)

In order to determine exact type of file run `file *file_of_unknown_type*`.

### Getting icons for .desktop files

Proprietary software often have no separate icon files, so there is nothing to use in [.desktop](/index.php/.desktop ".desktop") file creation. Happily `.ico` files can be easily extracted from executables using programs from the [icoutils](https://www.archlinux.org/packages/?name=icoutils) package. You can even do it on the fly during the `build` phase, for example:

```
$ wrestool -x --output=*icon.ico* -t14 *executable.exe*

```