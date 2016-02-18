**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – **Python** – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

This document covers standards and guidelines on writing [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") for [Python](/index.php/Python "Python") software.

## Contents

*   [1 Package naming](#Package_naming)
    *   [1.1 Versioned packages](#Versioned_packages)
*   [2 File placement](#File_placement)
*   [3 Notes](#Notes)
*   [4 Example](#Example)

## Package naming

For Python 3 libraries, use `python-*modulename*`. For applications, use the program name. In either case, the package name should be entirely lowercase.

Python 2 libraries should instead be named `python2-*modulename*`.

### Versioned packages

If you need to add a versioned package then use `python-*modulename*-*version*`, e.g. `python-colorama-0.2.5`. So python dependency `colorama==0.2.5` will turn into `python-colorama-0.2.5` Arch package.

## File placement

Most Python packages are installed with the [distutils](http://docs.python.org/library/distutils.html) system using **setup.py**, which installs files under `/usr/lib/python*<python version>*/site-packages/*pkgname*` directory.

## Notes

The `--optimize=1` parameter compiles `.pyo` files so they can be tracked by [pacman](/index.php/Pacman "Pacman").

In most cases, you should put `any` in the `arch` array since most Python packages are architecture independent.

Please do not install a directory named just `tests`, as it easily conflicts with other Python packages (for example, `/usr/lib/python2.7/site-packages/tests/`).

## Example

An example PKGBUILD can be found [here](https://projects.archlinux.org/abs.git/tree/prototypes/PKGBUILD-python.proto) or at `/usr/share/pacman/PKGBUILD-python.proto`, which is in the [abs](https://www.archlinux.org/packages/?name=abs) package.