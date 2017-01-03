**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – **Wine**

Many Windows programs may still be useful in Linux and so we may want to have a package for them. The differences between the two operating systems make this task a little complex. In this guideline we will talk about Win32 binaries, since projects where source is available usually are ported to Linux.

## Contents

*   [1 Things to check outright](#Things_to_check_outright)
    *   [1.1 License](#License)
    *   [1.2 Installer](#Installer)
    *   [1.3 Portability and cleanness](#Portability_and_cleanness)
*   [2 The guideline in short](#The_guideline_in_short)
    *   [2.1 Installing](#Installing)
    *   [2.2 The /usr/bin script](#The_.2Fusr.2Fbin_script)
    *   [2.3 UnionFsFuse](#UnionFsFuse)
*   [3 One example](#One_example)
*   [4 Gecko and Mono](#Gecko_and_Mono)

## Things to check outright

*   License: does the license allow the program to be repackaged?
*   Installer: is it possible to install the program silently? Even better, does an installer-less version exist?
*   Portability and cleanness: is the program portable? It is clean?

Here we mean a program is portable if it *never* writes in the registry or outside its directory; we mean a program is clean if it *never* writes in its directory, but it may write its settings in the user folder. A program can be also both (e.g., it never writes settings) or neither (e.g., it writes in its directory, it writes around, it writes in the registry...)

### License

Usually licenses are in a text file in the install directory. If you can't find it, try following the screens during installation. If nothing is said about repackaging, go on. The author does not care. Otherwise the license usually does not allow removing files or does not allow repackaging at all. In the former case just be careful that the [makepkg](/index.php/Makepkg "Makepkg") process does not lose any file, you may delete unneeded files (e.g., uninstallers) in the `post_install` phase; in the latter case all the installing process must be done in the `post_install` phase. The `build` phase will only be for copying the install files.

### Installer

It is much easier to work with compressed files like `.zip` than with Windows installers. If you have no choice, since the author insists on distributing its program with an installer, search the Internet for if it is possible to silently install the software. [MSFN](http://unattended.msfn.org/unattended.xp/page/list/switch/) is usually a good place to search. If you cannot find a way, try to open the installer with different [unpacking utilities](/index.php/Nonfree_applications_package_guidelines#Unpacking "Nonfree applications package guidelines"); it may work.

### Portability and cleanness

A portable program does not need its own [Wine](/index.php/Wine "Wine") emulated file system, so check in [Portable Freeware](http://www.portablefreeware.com) if the program you are packaging is portable.

## The guideline in short

The idea behind packaging a Windows program is to use the program's files as mere data that Wine will interpret, just like JVM and Java bytecode.

So we will install the program in `/usr/share/"$pkgname"` and the program will write all what it needs in `"$HOME"/."$pkgname"`. Everything will be prepared by a small script saved in `/usr/bin/"$pkgname"` that will create the folder, prepare it if needed, and finally start the program.

In the next sections we will talk about every step.

This way every user will have their own settings and their decisions will not bother other users.

### Installing

If the program has no installer, the installation is a mere decompression of a file; unpack it to `"$pkgdir"/usr/share/$pkgname`, making sure that the permissions are correct. These commands will do:

```
$ find "$pkgdir"/usr/share -type f -exec chmod 644 "{}" \;
$ find "$pkgdir"/usr/share -type d -exec chmod 755 "{}" \;

```

If the program cannot be installed the easy way, you need to create a Wine environment:

```
$ install -m755 -d "$srcdir"/tmp "$srcdir"/tmp/env "$srcdir"/tmp/local
$ export WINEPREFIX="$srcdir"/tmp/env
$ export XDG_DATA_HOME="$srcdir"/tmp/local
$ wine "$srcdir"/installer.exe /silentoptions

```

We have not discussed portability yet, but if your program does not need the registry keys it modified, you can just copy the directory from the:

```
"$srcdir"/tmp/env/drive_c/Program\ Files/programname

```

Otherwise you need to copy all the registry files too and eventually the files the program installed around. The `"$srcdir"/tmp/local` will contains menu icons and desktop files, you may want to copy them in the package. If there does not exist a way to install the program silently... Maybe you can make a `.tar.gz` file and upload it somewhere? If nothing automated is possible, force the user to follow the installer and hope he does not mess up the installation, write some checks before blindly copying a folder that may not exist (e.g., the user pressed 'Cancel'.)

### The /usr/bin script

This script prepares the settings folder and starts the program. If your program is portable, it will look like this:

```
#!/bin/bash
unset WINEPREFIX
if [ ! -d "$HOME"/.programname ] ; then
   mkdir -p "$HOME"/.programname
   #prepare the environment here
fi
WINEDEBUG=-all wine "$HOME"/.programname/programname "$@"

```

If it is clean, it will look like this:

```
#!/bin/bash
export WINEPREFIX="$HOME"/.programname/wine
if [ ! -d "$HOME"/.programname ] ; then
   mkdir -p "$HOME"/.programname/wine
   wineboot -u
   #copy the registry file if needed
fi
WINEDEBUG=-all wine /usr/share/programname "$@"

```

As you can see, in the second case there is no environment preparation. In fact a clean application will be started directly from `/usr/share` since it will not need to write in its folder, so its settings will be written somewhere in the emulated file system.

If the application is neither clean neither portable the two ideas must be combined.

If the application does not write settings at all, skip the `if` and start it from `/usr/share`.

The task of preparing the environment may differ greatly between applications, but follow these rules of thumb: If the program:

*   just needs to read a file, symlink it.
*   needs to write in a file, copy it.
*   does not use a file, ignore it.

Of course the minimum is just starting `WINEDEBUG=-all wine /usr/share/programname "$@"`.

Usually the environment will be made by symlinking between the `"$HOME"/.*programname*` directory and the `/usr/share/*programname*` files. But since some Windows programs are very fickle about their paths, you may need to symlink directly in the `"$HOME"/.*programname*/wine/drive_c/Program\ Files/*programname*` directory.

Of course those are just ideas to integrate Win32 applications in the Linux environment, do not forget your intelligence and gumption.

As example, [μTorrent](https://en.wikipedia.org/wiki/%CE%BCTorrent "wikipedia:μTorrent") is by default a clean application, but with a easy step can be used as a portable one. Since it is a single file and it is pretty small creating its wine environment (about 5MB) it is probably an overkill. It is better to symlink the executable, create the empty **settings.dat** in order to use it portable in the `$HOME/.utorrent` directory. With the added advantage that just visiting `.utorrent` folder an user can see a copy of the `.torrent` files she downloaded.

### UnionFsFuse

You can consider using the [UnionFsFuse](http://podgorny.cz/moin/UnionFsFuse) program available in the [official repositories](/index.php/Official_repositories "Official repositories") as [unionfs-fuse](https://www.archlinux.org/packages/?name=unionfs-fuse)). UnionFsFuse allows to keep the base directory in `/usr/share` and put a copy of the files the application needed to write inside `$HOME/.programname` almost automatically.

Using UnionFsFuse means an additional dependency and it requires the fuse module that not all users might load. Yet, it might be worthwhile if the application would need lots of symlinking or if it is unclear exactly what it needs to be written. Just ensure to mount and unmount the UnionFs correctly. Among others, the [GeneRally](https://aur.archlinux.org/packages/GeneRally/) package uses this approach.

## One example

We will make a package for [eMule](http://www.emule-project.net/). According to [Portable Freeware](http://www.portablefreeware.com/?q=emule), eMule is not completely portable since it writes some (useless) keys in the registry.

On the other hand, it is not clean either since it writes its configuration files and puts its downloads in its installation folder.

Luckily there is an [installer-less version available](http://prdownloads.sourceforge.net/emule/eMule0.49b.zip).

So we make our [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"); the only dependency is [wine](https://www.archlinux.org/packages/?name=wine). The `md5sums` should be added.

```
# Maintainer: You <youremail>
pkgname=emule
pkgver=0.49b
pkgrel=1
pkgdesc="One of the biggest and most reliable peer-to-peer file sharing
clients around the world."
arch=(i686 x86_64)
url="http://www.emule-project.net"
license=('GPL')
depends=()
depends=(wine)
makedepends=(unzip)
source=(emule http://prdownloads.sourceforge.net/emule/eMule$pkgver.zip)
noextract=()
options=(!strip)

build() {
  rm -f src/eMule"$pkgver"/license* #It is GPL

  install -d -m755 pkg/usr/share/emule
  cp -ra src/eMule"$pkgver"/* pkg/usr/share/emule
  find pkg/usr/share/emule -type d -exec chmod 755 "{}" \;
  find pkg/usr/share/emule -type f -exec chmod 644 "{}" \;

  install -d -m755 pkg/usr/bin
  install -m755 emule pkg/usr/bin 
}

```

Now we make our **emule** file, which according to `build`, will be copied and made executable in `/usr/bin`.

```
#!/bin/bash
export WINEARCH=win32 WINEPREFIX="$HOME/.emule/wine"

if [ ! -d "$HOME"/.emule ] ; then
  mkdir -p "$HOME"/.emule/wine || exit 1
  #Each user will have its config, we copy the default file since emule
  #needs to write here.
  cp -r /usr/share/emule/config "$HOME"/.emule || exit 1
  #We symlink the files emule needs to read to work
  ln -s /usr/share/emule/emule.exe "$HOME"/.emule/emule || exit 1
  ln -s -T /usr/share/emule/lang "$HOME"/.emule/lang || exit 1
  ln -s -T /usr/share/emule/webserver "$HOME"/.emule/webserver || exit 1
fi

wine "$HOME"/.emule/emule "$@"

```

If you want to be more precise, you may add a message in the `.install` file telling the user that they should disable search history since wine messes up that menu. You may even provide a default config file with the best settings. And that's it... run `$ makepkg`, check the package folder to be sure, and install.

## Gecko and Mono

Unless you know for sure, that software require browser of .NET runtime (packages [wine_gecko](https://www.archlinux.org/packages/?name=wine_gecko) and [wine-mono](https://www.archlinux.org/packages/?name=wine-mono) in official repositories), default wine installation prompts for Gecko/Mono are undesirable.

To disable HTML rendering, bytecode support and the dialogs, you need to use a dlloverride in your script. For Gecko:

```
export WINEDLLOVERRIDES="mshtml="

```

For Mono:

```
export WINEDLLOVERRIDES="mscoree="

```

For both:

```
export WINEDLLOVERRIDES="mscoree,mshtml="

```

You can also disable them via `winecfg`: just set mscoree/mshtml to Disable.