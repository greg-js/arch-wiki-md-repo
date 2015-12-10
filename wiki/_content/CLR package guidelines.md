# CLR package guidelines

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

**CLR** – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

This document defines the standard for packaging Common Language Runtime (.NET) projects under Arch Linux. Currently only [Mono](/index.php/Mono "Mono") is capable of providing a usable, efficient CLR runtime for multiple systems and this standard will reflect its use. Be aware that a lot of CLR programs were developed with Microsoft .NET in mind and, as such, may or may not run under Mono because of .NET-exclusive factors such as P/Invoke calls and Microsoft digital rights management (DRM) APIs and are thus will not yield a usable package for Arch Linux. However, if combined with [Wine](/index.php/Wine "Wine") as of version 1.5.6 (?), your package may have a chance to run under it. Please see the [Wine PKGBUILD Guidelines](/index.php/Wine_PKGBUILD_Guidelines "Wine PKGBUILD Guidelines") for more information if such is the case.

## Contents

*   [1 Packaging gotchas](#Packaging_gotchas)
    *   [1.1 Signed assemblies](#Signed_assemblies)
*   [2 Sample PKGBUILDs](#Sample_PKGBUILDs)
    *   [2.1 xbuild](#xbuild)
        *   [2.1.1 Unsigned DLL](#Unsigned_DLL)
    *   [2.2 NAnt](#NAnt)
    *   [2.3 Prebuild](#Prebuild)

## Packaging gotchas

*   Always add [mono](https://www.archlinux.org/packages/?name=mono) to `depends`
*   Always set `arch` to `any`. Mono does not yet support compiling (running?) 64-bit assemblies.
*   Always add `!strip` to `options`
*   If the package is a library (DLL), consider installing it to Mono's global assembly cache (GAC) if it is to be used as a dependency.
*   If the assembly is precompiled and comes with a program debug database file (Foo.dll.pdb), consider converting it as such: `pdb2mdb Foo.dll`
*   If the package is meant to be executed (EXE), be sure to install to `/usr/bin` a shell script to run it, similar to this one:

```
#!/bin/sh
mono foo.exe $@

```

### Signed assemblies

If the package is to be installed into the GAC, be sure it has a signed key file. If not, you can generate one like this: `sn -k 1024 Foo.snk`. Following that, the easiest way to embed the key file into the assembly is to disassemble it like this: `monodis Foo.dll --output=Foo.il`. Afterwards, reassemble it like so: `ilasm /dll /key:Foo.snk Foo.il`

## Sample PKGBUILDs

The following examples will try to cover some of the most common conventions and build systems.

### xbuild

#### Unsigned DLL

```
# Maintainer: yourname <yourmail>
pkgname=foo
pkgver=1.0
pkgrel=1
pkgdesc="Fantabulous library for .Net"
arch=('any')
url="http://www.foo.bar"
license=('GPL')
depends=('mono')
options=('!strip')
source=("http://www.foo.bar/foobar.tar.gz")
md5sums=('4736ac4f34fd9a41fa0197eac23bbc24')

build() {
  cd "${srcdir}/foobar"

  xbuild Foo.sln

  # if the package is unsigned, do the following:
  cd "/bin/x86/Debug"
  monodis Foo.dll --output=Foo.il
  sn -k 1024 Foo.snk
  ilasm /dll /key:Foo.snk Foo.il
}

package() {
  cd "${srcdir}/foobar/bin/x86/Debug"

  install -Dm644 Foo.dll "$pkgdir/usr/lib/foobar/Foo.dll"
  install -Dm644 Foo.dll.mdb "$pkgdir/usr/lib/foobar/Foo.dll.mdb"

  # Register assembly into Mono's GAC
  gacutil -i Foo.dll -root "$pkgdir/usr/lib"
}

```

### NAnt

### Prebuild

Retrieved from "[https://wiki.archlinux.org/index.php?title=CLR_package_guidelines&oldid=365629](https://wiki.archlinux.org/index.php?title=CLR_package_guidelines&oldid=365629)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Package development](/index.php/Category:Package_development "Category:Package development")