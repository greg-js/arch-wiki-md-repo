`PKGBUILD` је Arch Linux фајл који описује изградњу пакета кад се креирају пакети. Овај чланак описује могуће `PKGBUILD` променљиве.

## Грађење пакета

Пакети се код Arch Linux-а граде уз помоћ [makepkg](/index.php/Makepkg "Makepkg") и информација које се налазе унутар `PKGBUILD` фајла. Кад се `makepkg` покрене, он тражи `PKGBUILD` у директоријуму у којем се тренутно налази и прати инструкције које се налазе у том фајлу да би компајлирао или прибавио неопходне фајлове који се пакују у пакет (`pkgname.pkg.tar.xz`). Пакет који се тиме добија садржи бинарне фајлове и инсталациона упутства; и спреман је за инсталацију уз помоћ [pacman](/index.php/Pacman "Pacman") софтвера.

Погледати:

*   [Creating packages](/index.php/Creating_packages "Creating packages") за више информација о креирању пакета; и
*   [Custom local repository](/index.php/Custom_local_repository "Custom local repository") за информације о коришћењу пакета пошто се креирају.

## Променљиве

Следеће промељиве се могу попунити у `PKGBUILD` фајлу:

	`pkgname` 

	Име пакета, Треба да садржи **алфанумеричке карактере и црте ('-')** и сва слова би требало да буду **мала**. Због доследности, `pkgname` би требало да се подудара са именом изворног tarball-а софтвера који се пакује. На пример, ако је софтвер `foobar-2.5.tar.gz`, `pkgname` вредност би требало да буде *foobar*. Тренутни радни директоријум за `PKGBUILD` фајл би такође требало да се подудара са `pkgname`.

	`pkgver` 

	Верзија пакета. Вредност би требала да буде иста као и верзија пакета који је издао аутор. Садржи слова, бројеве и тачке али **НЕ СМЕ** да садржи црту. Ако аутор пакета користи црту у шеми означавања верзије, треба је заменити са доњом цртом. На пример, ако је верзија *0.99-10*, требало би да се промени у *0.99_10*. Ако се pkgver променљива користи касније у PKGBUILD-у онда се доња црта лако мења цртом, нпр. овако:

```
 source=($pkgname-${pkgver//_/-}.tar.gz)

```

	`pkgrel` 

	Број издања пакета специфичног за Arch Linux. Ова вредност омогућава корисницима да разликују узастопне изградње исте верзије пакета. Када се нова верзија пакета први пут објави, **број издања почиње са 1**. Како се креирају поправке и оптимизације `PKGBUILD` фајла, пакет се **поново објављује** и **број издања** се повећава за 1\. Када нова верзија пакета изађе, број издања се враћа на 1.

	`epoch` 

	Целобројна вредност, специфична за Arch Linux, представља који 'животни век' да упореди са бројем верзије. Ова вредност дозвољава надјачавање нормалног поређења верзија за пакете који имају нередовно означавање верзија. Подразумевано, за пакете се претпоставља да имају epoch вредност *0*. Не користите ову променљиву осим уколико знате шта радите.

	`pkgdesc` 

	Опис пакета. Опис би требало да садржи око 80 или мање карактера и не би требало да укључује име пакета само-референтни начин. На пример, "Nedit is a text editor for X11" треба написати као "A text editor for X11."

	`arch` 

	Ред архитектура на којим `PKGBUILD` фајл може да се изгради и на којим ради. Тренутно, требало би да садржи **i686** и/или **x86_64**, `arch=('i686' 'x86_64')`. Вредност **any** се такође може користити за пакете који су независни од архитектуре. Овој вредности се може приступити променљивом `$CARCH` током изградње.

	`url` 

	URL адреса официјалног сајта софтвера који се пакује.

	`license` 

	Лиценца под којој се софтвер дистрибуира. [licenses](https://www.archlinux.org/packages/?name=licenses) пакет се креира у `[core]` који чува заједничке лиценце у `/usr/share/licenses/common`, нпр. `/usr/share/licenses/common/GPL`. Ако је пакет лиценциран под неком од ових лиценци, ова вредност би требало да се подеси да буде име тог директоријума, нпр. `license=('GPL')`. Ако одговарајућа лиценца није укључена у официјелни [licenses](https://www.archlinux.org/packages/?name=licenses) пакет, неколико ствари се мора урадити:

1.  Фајл(ови) лиценци се морају укључити у: `/usr/share/licenses/**pkgname**/`, нпр. `/usr/share/licenses/foobar/LICENSE`.
2.  Ако изворишни пакет **NЕ** садржи детаље о лиценци и ако је лиценца приказана само негде, нпр. на сајту пројекта, онда се лиценца мора копирати у фајл и укључити у директоријум.
3.  Додати **custom** у `license` низ. Опционо, може се заменити **custom** са **custom:име лиценце**. Једном када се лиценца користи у два или више пакета у официјелним ризницама (укључујући и `[community]`), она постаје део [licenses](https://www.archlinux.org/packages/?name=licenses) пакета.

*   [BSD](https://en.wikipedia.org/wiki/BSD_%D0%BB%D0%B8%D1%86%D0%B5%D0%BD%D1%86%D0%B0 "wikipedia:BSD лиценца"), [MIT](https://en.wikipedia.org/wiki/MIT_%D0%BB%D0%B8%D1%86%D0%B5%D0%BD%D1%86%D0%B0 "wikipedia:MIT лиценца"), [zlib/png](https://en.wikipedia.org/wiki/ZLIB_%D0%BB%D0%B8%D1%86%D0%B5%D0%BD%D1%86%D0%B0 "wikipedia:ZLIB лиценца") и [Python](https://en.wikipedia.org/wiki/Python_%D0%BB%D0%B8%D1%86%D0%B5%D0%BD%D1%86%D0%B0 "wikipedia:Python лиценца") су специјалне лиценце и не могу се укључити у [licenses](https://www.archlinux.org/packages/?name=licenses) пакет. Због `license` низа, третира се као обична лиценца (`license=('BSD')`, `license=('MIT')`, `license=('ZLIB')` и `license=('Python')`) али технички свака је лиценца кастм зато што свака од њих има своју copyright линију. Било који пакет лиценциран под неком од ове четири лиценце би требало да има своју јединствену лиценцу сачувану у `/usr/share/licenses/**pkgname**`. Неки пакети се не могу покрити једном лиценцом. У том случају, више уноса се додаје у license низ, нпр. `license=('GPL' 'custom:name of license')`.
*   Додатно, (L)GPL има много верзија и пермутација. За (L)GPL софтвер, постоји следећа конвенција:
    *   (L)GPL - (L)GPLv2 или нека каснија верзија
    *   (L)GPL2 - Само (L)GPL2
    *   (L)GPL3 - (L)GPL3 или било која друга каснија верзија

	`groups` 

	The group the package belongs in. For instance, when you install the [kdebase](https://www.archlinux.org/groups/x86_64/kdebase/) package, it installs all packages that belong in the *kde* group.

	`depends` 

	An array of package names that must be installed before this software can be run. If a software requires a minimum version of a dependency, the **>=** operator should be used to point this out, e.g. `depends=('foobar>=1.8.0')`. You do not need to list packages that your software depends on if other packages your software depends on already have those packages listed in their dependency. For instance, *gtk2* depends on *glib2* and *glibc*. However, *glibc* does not need to be listed as a dependency for *gtk2* because it is a dependency for *glib2*.

	`makedepends` 

	An array of package names that must be installed to build the software but unnecessary for using the software after installation. You can specify the minimum version dependency of the packages in the same format as the `depends` array.

**Warning:** The group "base-devel" is assumed already installed when building with makepkg . Members of "base-devel" **should not** be included in makedepends arrays.

	`optdepends` 

	An array of package names that are not needed for the software to function but provides additional features. A short description of what each package provides should also be noted. An `optdepends` may look like this:

```
optdepends=('cups: printing support'
'sane: scanners support'
'libgphoto2: digital cameras support'
'alsa-lib: sound support'
'giflib: GIF images support'
'libjpeg: JPEG images support'
'libpng: PNG images support')

```

	`provides` 

	An array of package names that this package provides the features of (or a virtual package such as *cron* or *sh*). If you use this variable, you should add the version (`pkgver` and perhaps the `pkgrel`) that this package will provide if dependencies may be affected by it. For instance, if you are providing a modified *qt* package named *qt-foobar* version 3.3.8 which provides *qt* then the `provides` array should look like `provides=('qt=3.3.8')`. Putting `provides=('qt')` will cause to fail those dependencies that require a specific version of *qt*. Do not add `pkgname` to your provides array, this is done automatically.

	`conflicts` 

	An array of package names that may cause problems with this package if installed. You can also specify the version properties of the conflicting packages in the same format as the `depends` array.

	`replaces` 

	An array of obsolete package names that are replaced by this package, e.g. `replaces=('ethereal')` for the [wireshark](https://www.archlinux.org/packages/?name=wireshark) package. After syncing with `pacman -Sy`, it will immediately replace an installed package upon encountering another package with the matching `replaces` in the repositories. If you are providing an alternate version of an already existing package, use the `conflicts` variable which is only evaluated when actually installing the conflicting package.

	`backup` 

	An array of files to be backed up as `file.pacsave` when the package is removed. This is commonly used for packages placing configuration files in `/etc`. The file paths in this array should be relative paths (e.g. `etc/pacman.conf`) not absolute paths (e.g. `/etc/pacman.conf`).

	`options` 

	This array allows you to override some of the default behavior of `makepkg`. To set an option, include the option name in the array. To reverse the default behavior, place an **!** at the front of the option. The following options may be placed in the array:

*   ***strip*** - Strips symbols from binaries and libraries.
*   ***docs*** - Save `/doc` directories.
*   ***libtool*** - Leave *libtool* (`.la`) files in packages.
*   ***emptydirs*** - Leave empty directories in packages.
*   ***zipman*** - Compress *man* and *info* pages with *gzip*.
*   ***ccache*** - Allow the use of `ccache` during build. More useful in its negative form `!ccache` with select packages that have problems building with `ccache`.
*   ***distcc*** - Allow the use of `distcc` during build. More useful in its negative form `!distcc` with select packages that have problems building with `distcc`.
*   ***makeflags*** - Allow the use of user-specific `makeflags` during build. More useful in its negative form `!makeflags` with select packages that have problems building with custom `makeflags`.

	`install` 

	The name of the `.install` script to be included in the package. *pacman* has the ability to store and execute a package-specific script when it installs, removes or upgrades a package. The script contains the following functions which run at different times:

*   ***pre_install*** - The script is run right before files are extracted. One argument is passed: new package version.
*   ***post_install*** - The script is run right after files are extracted. One argument is passed: new package version.
*   ***pre_upgrade*** - The script is run right before files are extracted. Two arguments are passed in the following order: new package version, old package version.
*   ***post_upgrade*** - The script is run after files are extracted. Two arguments are passed in the following order: new package version, old package version.
*   ***pre_remove*** - The script is run right before files are removed. One argument is passed: old package version.
*   ***post_remove*** - The script is run right after files are removed. One argument is passed: old package version.

	Each function is run chrooted inside the pacman install directory. See [this thread](https://bbs.archlinux.org/viewtopic.php?pid=913891).

**Tip:** A prototype `.install` is provided at `/usr/share/pacman/proto.install`.

	`source` 

	An array of files which are needed to build the package. It must contain the location of the software source, which in most cases is a full HTTP or FTP URL. The previously set variables `pkgname` and `pkgver` can be used effectively here (e.g. `source=(http://example.com/$pkgname-$pkgver.tar.gz)`)

**Note:** If you need to supply files which are not downloadable on the fly, e.g. self-made patches, you simply put those into the same directory where your `PKGBUILD` file is in and add the filename to this array. Any paths you add here are resolved relative to the directory where the `PKGBUILD` lies. Before the actual build process is started, all of the files referenced in this array will be downloaded or checked for existence, and `makepkg` will not proceed if any are missing.

**Note:** You can specify a different name for the downloaded file - if the downloaded file has a different name for some reason like the url had a GET parameter - using the following syntax: <filename>::<fileuri>, do not include the '<' and '>' characters

	`noextract` 

	An array of files listed under the `source` array which should not be extracted from their archive format by `makepkg`. This most commonly applies to certain zip files which cannot be handled by *bsdtar* because *libarchive* processes all files as streams rather than random access as *unzip* does. In these situations *unzip* should be added in the `makedepends` array and the first line of the `build()` function should contain:

```
cd $srcdir/$pkgname-$pkgver
unzip [source].zip

```

	`md5sums` 

	An array of MD5 checksums of the files listed in the `source` array. Once all files in the `source` array are available, an MD5 hash of each file will be automatically generated and compared with the values of this array in the same order they appear in the `source` array. While the order of the source files itself does not matter, it is important that it matches the order of this array since `makepkg` cannot guess which checksum belongs to what source file. You can generate this array quickly and easily using the command `makepkg -g` in the directory that contains the `PKGBUILD` file. Note that the MD5 algorithm is known to have weaknesses, so you should consider using a stronger alternative.

	`sha1sums` 

	An array of SHA-1 160-bit checksums. This is an alternative to md5sums described above, but is also known to have weaknesses, so you should consider using a stronger alternative. To enable use and generation of these checksums, be sure to set up the INTEGRITY_CHECK option in makepkg.conf. See man makepkg.conf.

	`sha256sums, sha384sums, sha512sums` 

	An array of SHA-2 checksums with digest sizes 256, 384 and 512 bits respectively. These are alternatives to md5sums described above and are generally believed to be stronger. To enable use and generation of these checksums, be sure to set up the INTEGRITY_CHECK option in makepkg.conf. See man makepkg.conf.

It is common practice to preserve the order of the `PKGBUILD` variables as shown above. However, this is not mandatory, as the only requirement in this context is correct [Bash](https://en.wikipedia.org/wiki/Bash "wikipedia:Bash") syntax.

## See also

*   [Example PKGBUILD file](http://pastebin.com/MeXiLDV9)
*   [Example .install file](http://seberm.pastebin.com/gP0tBqvs)
*   [Arch Packaging Standards](/index.php/Arch_packaging_standards "Arch packaging standards") for various guidelines