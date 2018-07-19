**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – <a class="mw-selflink selflink">Perl</a> – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [R](/index.php/R_package_guidelines "R package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

This document covers the creation of [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") for perl modules distributed over CPAN, the Comprehensive Perl Authors Network. The target audience of this document is intended to be packagers of perl modules.

## Contents

*   [1 Arch Linux Packaging Conventions](#Arch_Linux_Packaging_Conventions)
    *   [1.1 Package names](#Package_names)
    *   [1.2 Package file placement](#Package_file_placement)
    *   [1.3 Architecture](#Architecture)
    *   [1.4 Automation](#Automation)
*   [2 PKGBUILD Examples](#PKGBUILD_Examples)
*   [3 CPAN Module Mechanics](#CPAN_Module_Mechanics)
    *   [3.1 Modules](#Modules)
    *   [3.2 Distributions](#Distributions)
    *   [3.3 CPAN](#CPAN)
    *   [3.4 Module dependencies](#Module_dependencies)
    *   [3.5 Dependency definition](#Dependency_definition)
    *   [3.6 Meta information](#Meta_information)
*   [4 Installation modules](#Installation_modules)
    *   [4.1 ExtUtils::MakeMaker](#ExtUtils::MakeMaker)
    *   [4.2 Module::Build](#Module::Build)
    *   [4.3 Module::Build::Tiny](#Module::Build::Tiny)
    *   [4.4 Module::Install](#Module::Install)
    *   [4.5 Environment variables](#Environment_variables)
        *   [4.5.1 PERL_MM_USE_DEFAULT](#PERL_MM_USE_DEFAULT)
        *   [4.5.2 PERL_AUTOINSTALL](#PERL_AUTOINSTALL)
        *   [4.5.3 PERL_MM_OPT](#PERL_MM_OPT)
        *   [4.5.4 PERL_MB_OPT](#PERL_MB_OPT)
        *   [4.5.5 MODULEBUILDRC](#MODULEBUILDRC)
        *   [4.5.6 PERL5LIB](#PERL5LIB)
        *   [4.5.7 PERL_LOCAL_LIB_ROOT](#PERL_LOCAL_LIB_ROOT)
*   [5 Problems with user-installed perl](#Problems_with_user-installed_perl)

## Arch Linux Packaging Conventions

The following conventions should be used to keep perl module packages consistent. This section serves as an introduction to the concept of perl packaging, from the point of view of Arch Linux; that is, package management and system administration. In an effort to please the casual TL;DR reader, the easiest and/or most popular material is at the top.

### Package names

For modules the package name should begin with `perl-` and the rest of the name should be constructed from the module name by converting it to lowercase and then replacing colons with hyphens. For example the package name corresponding to `HTML::Parser` will be `perl-html-parser`. Perl applications should have the same name as that of the application but in lowercase.

### Package file placement

Perl packages should install module files into `/usr/lib/perl5/$version/vendor_perl/` (use `perl -V:vendorarch` in scripts), or `/usr/share/perl5/vendor_perl/`. This is done by setting the `INSTALLDIRS` command line parameter to `vendor` as shown below. No files should be stored in `/usr/lib/perl5/$version/site_perl/` as that directory is reserved for use by the system administrator to install Perl packages outside the package management system. When a user installs modules system-wide by using the *cpan* shell, modules end up in the site-perl sub-directories.

The files `perllocal.pod` and `.packlist` also should not be present; this is taken care of by the example PKGBUILD described below.

### Architecture

In most cases, the `arch` array should contain `'any'` because most Perl packages are architecture independent. XS modules are compiled into dynamically loaded libraries (.so files) and should explicitly set their architecture to `('x86_64')` in order to indicate that they are architecture dependent when built. An XS module usually contains one or more .xs files which dynamically generate .c files.

### Automation

A plugin for the second-generation CPAN shell, CPANPLUS, is available in the perl-cpanplus-dist-arch package from the community repo. This plugin packages distributions on the fly as they are installed by CPANPLUS. Online documentation is available at [https://metacpan.org/release/CPANPLUS-Dist-Arch](https://metacpan.org/release/CPANPLUS-Dist-Arch)

## PKGBUILD Examples

An example PKGBUILD can be found at [[1]](https://git.archlinux.org/abs.git/tree/prototypes/PKGBUILD-perl.proto).

The following two PKGBUILD examples use techniques, introduced in this page, that are intended to make a PKGBUILD more resilient to more sophisticated problems. Because there are two styles of build scripts, there are two example PKGBUILDS. The first PKGBUILD is an example of how to package a distribution that uses `Makefile.PL`. The second PKGBUILD can be used as a starting point for a distribution which uses `Build.PL`.

 `PKGBUILD` 
```
# Contributor: Your Name <youremail@domain.com>
pkgname=perl-foo-bar
pkgver=1.0
pkgrel=1
pkgdesc='This packages the Foo-Bar distribution, containing the Foo::Bar module!'
_dist=Foo-Bar
arch=('any')
url="https://metacpan.org/release/$_dist"
license=('GPL' 'PerlArtistic')
depends=(perl)
options=('!emptydirs' purge)
source=("http://search.cpan.org/CPAN/authors/id/BAZ/$_dist-$pkgver.tar.gz")
md5sums=(...)

build() {
  cd "$srcdir/$_dist-$pkgver"
  unset PERL5LIB PERL_MM_OPT PERL_LOCAL_LIB_ROOT
  export PERL_MM_USE_DEFAULT=1 PERL_AUTOINSTALL=--skipdeps
  /usr/bin/perl Makefile.PL
  make
}

check() {
  cd "$srcdir/$_dist-$pkgver"
  unset PERL5LIB PERL_MM_OPT PERL_LOCAL_LIB_ROOT
  export PERL_MM_USE_DEFAULT=1
  make test
}

package() {
  cd "$srcdir/$_dist-$pkgver"
  unset PERL5LIB PERL_MM_OPT PERL_LOCAL_LIB_ROOT
  make install INSTALLDIRS=vendor DESTDIR="$pkgdir"
}

```
 `PKGBUILD` 
```
# Contributor: Your Name <youremail@domain.com>
pkgname=perl-foo-bar
pkgver=1.0
pkgrel=1
pkgdesc='This packages the Foo-Bar distribution, containing the Foo::Bar module!'
_dist=Foo-Bar
arch=('any')
url="https://metacpan.org/release/$_dist"
license=('GPL' 'PerlArtistic')
depends=(perl)
options=('!emptydirs' purge)
source=("http://search.cpan.org/CPAN/authors/id/BAZ/$_dist-$pkgver.tar.gz")
md5sums=(...)

build() {
  cd "$srcdir/$_dist-$pkgver"
  unset PERL5LIB PERL_MM_OPT PERL_MB_OPT PERL_LOCAL_LIB_ROOT
  export PERL_MM_USE_DEFAULT=1 MODULEBUILDRC=/dev/null
  /usr/bin/perl Build.PL
  ./Build
}

check() {
  cd "$srcdir/$_dist-$pkgver"
  unset PERL5LIB PERL_MM_OPT PERL_MB_OPT PERL_LOCAL_LIB_ROOT
  export PERL_MM_USE_DEFAULT=1
  ./Build test
}

package() {
  cd "$srcdir/$_dist-$pkgver"
  unset PERL5LIB PERL_MM_OPT PERL_MB_OPT PERL_LOCAL_LIB_ROOT
  ./Build install --installdirs=vendor --destdir="$pkgdir"
}

```

Justification for the added complexity of these PKGBUILDs is attempted in the latter sections.

## CPAN Module Mechanics

There are a number of carefully, and not so carefully, designed mechanics that work together to create the module system. When making use of the CPAN, procedures must be followed to fetch the source code of a module, build that fetched module, and insert it into the system software for later execution. In order to understand how modules should be packaged, it helps immensely if one understands how modules work without any involvement from pacman and Arch Linux packages. Our goal in the end is to try to be unobtrusive as possible, while improving organization and consistency in the end product.

### Modules

Modules are declared with the `package` keyword in perl. Modules are contained inside a `.pm` ("dot-pee-em") file. Though it's possible more than one module (`package`) is in the file. Modules have namespaces separated with `::` (double colons), like: `Archlinux::Module`. When loading a module, the `::`s are replaced with directory separators. For example: `Archlinux/Module.pm` will be loaded for the module `Archlinux::Module`.

Core modules are included with an installation of perl. Some core modules are *only* available bundled with perl. Other modules can still be downloaded and installed separately from CPAN.

### Distributions

(aka dist, package) This is the equivalent of an Arch Linux package in CPAN-lingo. Distributions are `.tar.gz` archives full of files. These archives contain primarily .pm module files, tests for the included modules, documentation for the modules, and whatever else is deemed necessary.

Usually a distribution contains a primary module with the same name. Sometimes this is not true, like with the Template-Toolkit distribution. The latest package, `Template-Toolkit-2.22.tar.gz`, for the `Template-Toolkit` dist, contains no `Template::Toolkit` module!

Sometimes because distributions are named after a main module, their names are used interchangeably and they get muddled together. However it is sometimes useful to consider them a separate entity (like in Template-Toolkit's case).

### CPAN

Each CPAN mirror contains indices that list the distributions on CPAN, the modules in the dists, and the name of the author who uploaded the dist. These are simply text files. The most useful index is in the `/modules/02packages.details.txt.gz` file available from each CPAN mirror. The term "packages" here refers to the `package` keyword in the perl language itself, not something similar to pacman packages. The CPAN shell, referred to as lowercased, italicized *cpan*, is simply the venerable perl script which navigates indices to find the module you want to install.

Modules are found in the `02packages.details.txt.gz` list. On the same line as the module/package name is the path to the distribution tarball that contains the module. When you ask *cpan* to install a module, it will look up the module and install the relevant distribution. As the distribution is installing it will generate a list of module dependencies. *Cpan* will try to load each module dependency into the perl interpreter. If a module of the given version cannot be loaded the process is repeated.

The *cpan* shell does not have to worry about what version of the required module it is installing. *cpan* can rely on the fact that the latest version of the module must satisfy the requirements of the original module that it began installing in the first place. Only the latest versions of modules are listed in the packages details file. Unfortunately for the perl package author, we cannot always rely on the fact that our packages offer the most recent version of a perl distribution and the modules contained within. Pacman dependency checking is much more static and strongly enforced.

### Module dependencies

Perl has a unique way of defining dependencies compared to similar systems like python eggs and ruby gems. Eggs define dependencies on other eggs. Gems depend on gems. Perl dists depend on modules. Modules are only available from CPAN distributions so in a way perl distributions depend on distributions only indirectly. Modules can define their own versions independent from distributions inside the module source code. This is done by defining a *package* variable called `$VERSION`. When using strict and warnings, this is defined with the our keyword. For example:

```
package Foo::Module;
use warnings;
use strict;
our $VERSION = '1.00';
```

Modules can change their versions however they like and even have a version distinct from the distribution version. The utility of this is questionable but it is important to keep in mind. Module versions are more difficult to determine from outside of the perl interpreter and require parsing the perl code itself and maybe even loading the module into perl. The advantage is that from inside the perl interpreter module versions are easy to determine. For example:

```
use Foo::Module;
print $Foo::Module::VERSION, "
";

```

### Dependency definition

Where are dependencies defined in perl distributions? They are "defined" inside of the `Makefile.PL` or `Build.PL` script. For example, inside of the `Makefile.PL` script the `WriteMakeFile` function is called to generate the `Makefile` like this:

```
use ExtUtils::MakeMaker;
WriteMakeFile(
    'NAME' => 'ArchLinux::Module',
    'VERSION' => '0.01',
    'PREREQ_PM' => { 'POSIX' => '0.01' },
);

```

This is a contrived example but it is important to understand the dependencies aren't final until after the `Makefile.PL` or `Build.PL` script is run. Dependencies are specified at runtime, which means they can be changed or modified using the full power of perl. This means the module author can add, remove, or change versions of dependencies right before the distribution is installed. Some modules authors use this to do overly clever things like depend on modules only if they are installed. Some multi-platform dists also depend on system-specific modules when installed on different operating systems.

As an example, the CPANPLUS distribution looks for CPANPLUS::Dist plugins that are currently installed. If any plugins are installed for the currently installed version of CPANPLUS it adds them to the new CPANPLUS's prerequisites. I'm not quite sure why. Luckily for the perl packager most dependencies are static like in the above example that requires the POSIX module with a minimum version of 0.01.

### Meta information

Meta files are included in recent distributions which contain meta-information about distributions such as the name, author, abstract description, and module requirements. Previously there were `META.yml` files in the YAML format but more recently the switch has been made to `META.json` files in the JSON format. These files can be edited by hand but more often they are generated automatically by `Makefile.PL` or `Build.PL` scripts when packaging a distribution for release. The latest specification is described in [CPAN::Meta::Spec's online docs](http://search.cpan.org/perldoc?CPAN::Meta::Spec).

Remember that dependencies can be changed at runtime! For this reason another meta file is generated after running the build script. This second meta file is called `MYMETA.json` and reflects changes the script made at runtime and may be different from the meta file generated when the distribution was packaged for CPAN.

Elderly distributions on the CPAN have no meta file at all. These old releases predate the idea of the META.yml file and only describe their prerequisites in their `Makefile.PL`.

## Installation modules

One of perl's greatest strengths is the sheer number of modules available on CPAN. Not too surprisingly, there are also several different modules used for installing... well... modules! TMTOWTDI! I am not aware of a standard name for these types of modules, so I just called them "Installation Modules".

These modules are concerned with building the distribution and installing module files wherever the user prefers. This seems straightforward, but considering the number of different systems perl runs on, this can get complex. Installation modules all place a perl code file inside the dist tarball. Running this perl script will initiate the build and install process. The script always ends with the `.PL` suffix and is termed the "Build script" in the below list.

### ExtUtils::MakeMaker

	Build script

	`Makefile.PL`

	CPAN link

	[http://search.cpan.org/dist/ExtUtils-MakeMaker](http://search.cpan.org/dist/ExtUtils-MakeMaker)

The original, oldest module for installing modules is `ExtUtils::MakeMaker`. The major downside to this module is that it requires the `make` program to build and install everything. This may not seem like a big deal to linux users but is a real hassle for Windows people!

### Module::Build

	Build script

	`Build.PL`

	CPAN link

	[http://search.cpan.org/dist/Module-Build](http://search.cpan.org/dist/Module-Build)

The main advantage of Module::Build is that it is pure-perl. This means it does not require a `make` program to be installed for you to build/install modules. Its adoption was rocky because if `Module::Build` was not already installed, you could not run the bundled `Build.PL` script! This is not a problem with recent versions of perl because `Module::Build` is a core module. (**NOTE** As of perl 5.22, Module::Build will no longer be a core module)

### Module::Build::Tiny

	Build script

	`Build.PL`

	CPAN link

	[http://search.cpan.org/dist/Module-Build-Tiny](http://search.cpan.org/dist/Module-Build-Tiny)

This is another pure-perl build tool. As an interface it implements a subset of Module::Build's interface, in particular it requires dashes before its arguments (Module::Build accepts with and without) and doesn't support `.modulebuildrc`.

### Module::Install

	Build script

	`Makefile.PL`

	CPAN link

	[http://search.cpan.org/dist/Module-Install](http://search.cpan.org/dist/Module-Install)

Another modern build/installation module, `Module::Install` still requires the `make` program be installed to function. `MI` was designed as a drop-in replacement for `MakeMaker`, to address some of `MakeMaker`'s shortcomings. Ironically, it depends on `MakeMaker` in order to operate. The `Makefile.PL` files that are generated by `MI` look much different and are implemented using a simple domain specific language.

One very interesting feature is that `Module::Install` bundles a *complete* *copy* of itself into the distribution file. Because of this, unlike `MakeMaker` or `M::B`, you do not need `Module::Install` to be installed on your system.

Another very unique feature is auto-install. *Though not recommended by `Module::Install`'s authors this feature is used quite often.* When the module author enables auto-install for his distribution, `Module::Install` will search for and install any pre-requisite modules that are not installed when `Makefile.PL` is executed. This feature is skipped when `Module::Install` detects it is being run by `CPAN` or `CPANPLUS`. However, this feature is not skipped when run inside... oh I don't know... a **PKGBUILD**! I hope you can see how a rogue perl program downloading and installing modules willy-nilly *inside a PKGBUILD* can be a problem. See the [#PERL_AUTOINSTALL](#PERL_AUTOINSTALL) environment variable to see how to fix this.

### Environment variables

A number of environment variables can affect the way the modules are built or installed. Some have a very dramatic effect and can cause problems if misunderstood. An advanced user could be using these environment variables. Some of these will break an unsuspecting PKGBUILD or cause unexpected behavior.

#### PERL_MM_USE_DEFAULT

When this variable is set to a true value, the installation module will pretend the default answer was given to any question it would normally ask. This does not *always* work, but all of the installation modules honour it. *That doesn't mean the module author will!*

#### PERL_AUTOINSTALL

You can pass additional command-line arguments to `Module::Install`'s `Makefile.PL` with this variable. In order to turn off auto-install (*highly recommended*), assign `--skipdeps` to this.

 `export PERL_AUTOINSTALL='--skipdeps'` 

#### PERL_MM_OPT

You can pass additional command-line arguments to `Makefile.PL` and/or `Build.PL` with this variable. For example, you can install modules into your home-dir by using:

 `export PERL_MM_OPT=INSTALLBASE=~/perl5` 

#### PERL_MB_OPT

This is the same thing as `PERL_MM_OPT` except it is only for `Module::Build`. For example, you could install modules into your home-dir by using:

 `export PERL_MB_OPT=--install_base=~/perl5` 

#### MODULEBUILDRC

`Module::Build` allows you to override its command-line-arguments with an rcfile. This defaults to `~/.modulebuildrc`. This is considered deprecated within the perl toolchain. You can override which file it uses by setting the path to the rcfile in `MODULEBUILDRC`. The paranoid might set `MODULEBUILDRC` to `/dev/null`... just in case.

#### PERL5LIB

The directories searched for libraries can be set by the user (particularly if they are using `Local::Lib`) by setting `PERL5LIB`. That should be cleared before building.

#### PERL_LOCAL_LIB_ROOT

If the user is using `Local::Lib` it will set `PERL_LOCAL_LIB_ROOT`. That should be cleared before building.

## Problems with user-installed perl

A subtle problem is that advanced perl programmers may like to have multiple versions of perl installed. This is useful for testing backwards-compatibility in created programs. There are also speed benefits to compiling your own custom perl interpreter (i.e. without threads). Another reason for a custom *perl* is simply because the official perl Arch Linux package sometimes lags behind perl releases. The user may be trying out the latest perl... who knows?

If the user has the custom perl executable in their `$PATH`, the custom perl will be run when the user types the *perl* command on the shell. In fact the custom perl will run inside the `PKGBUILD` as well! This can lead to insidious problems that are difficult to understand.

The problem lies in compiled XS modules. These modules bridge perl and C. As such they must use perl's internal C API to accomplish this bridge. Perl's C API changes slightly with different versions of perl. If the user has a different version of perl than the system perl (`/usr/bin/perl`) then any XS module compiled with the user's perl will be incompatible with the system-wide perl. When trying to use the compiled XS module with the system perl, the module will fail to load with a link error.

A simple solution is to always use the absolute path of the system-wide perl interpreter (`/usr/bin/perl`) when running perl in the `PKGBUILD`.