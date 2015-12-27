# Haskell package guidelines

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Please help improve this article by creating reasonable [package creation guidelines](/index.php/Creating_packages "Creating packages") for [Haskell](/index.php/Haskell "Haskell") packages. The previous content on this page, which was unrelated to packaging guidelines, has been moved to [ArchHaskell](/index.php/ArchHaskell "ArchHaskell"). (Discuss in [Talk:Haskell package guidelines#](https://wiki.archlinux.org/index.php/Talk:Haskell_package_guidelines))

**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – **Haskell** – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

This document aims to cover standards and guidelines for producing good [Haskell](/index.php/Haskell "Haskell") [packages](/index.php/Creating_packages "Creating packages") on Arch.

## cabal2pkgbuild

[cabal2pkgbuild-git](https://aur.archlinux.org/packages/cabal2pkgbuild-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/cabal2pkgbuild-git)]</sup>, available in the [AUR](/index.php/AUR "AUR"), may be used to automatically generate Arch packages from [cabal](/index.php/Haskell#cabal-install "Haskell") build files. It is a wrapper around [cblrepo](https://github.com/magthe/cblrepo). Generally there should be one package (i.e., one [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")) per `.cabal` file for a package.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Haskell_package_guidelines&oldid=413553](https://wiki.archlinux.org/index.php?title=Haskell_package_guidelines&oldid=413553)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Package development](/index.php/Category:Package_development "Category:Package development")