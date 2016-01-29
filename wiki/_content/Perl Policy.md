# Perl Policy

This page covers the policy for how perl itself is configured and packaged. For Perl module packaging guidelines, see [Perl package guidelines](/index.php/Perl_package_guidelines "Perl package guidelines").

## Contents

*   [1 Introduction](#Introduction)
    *   [1.1 5.10 caveats](#5.10_caveats)
    *   [1.2 Reasoning](#Reasoning)
    *   [1.3 Pitfalls](#Pitfalls)
*   [2 Perl versions](#Perl_versions)
*   [3 Module paths](#Module_paths)
*   [4 Documents](#Documents)
*   [5 Binaries and scripts](#Binaries_and_scripts)
*   [6 Core](#Core)
    *   [6.1 Core directories](#Core_directories)
    *   [6.2 Core perl packages](#Core_perl_packages)
*   [7 Site](#Site)
    *   [7.1 Site directories](#Site_directories)
    *   [7.2 Site installation](#Site_installation)
*   [8 Vendor](#Vendor)
    *   [8.1 Package naming](#Package_naming)
    *   [8.2 Vendor directories](#Vendor_directories)
    *   [8.3 Vendor installation](#Vendor_installation)
    *   [8.4 Sample vendor PKGBUILD](#Sample_vendor_PKGBUILD)
    *   [8.5 Dependencies](#Dependencies)
        *   [8.5.1 Binary modules](#Binary_modules)
        *   [8.5.2 Architecture-independent modules](#Architecture-independent_modules)
*   [9 Perl6](#Perl6)

## Introduction

This policy document was proposed, accepted, and implemented in version 5.10.0 of the [perl](https://www.archlinux.org/packages/?name=perl) package. It is the standard regarding to the _perl_ package, related Perl packages, and creating Perl module packages (both in binary form and in the form of PKGBUILDs). Portions are derived from the [Debian Perl Policy](http://www.debian.org/doc/packaging-manuals/perl-policy/index.html) document and from various portions of the Perl man pages.

### 5.10 caveats

NOT TRUE: The directories for scripts do not conform to the Filesystem Hierarchy Standard (FHS).

**Note:** The FHS describes what directories must be in `/usr/bin` and does not prohibit adding other directories.

### Reasoning

Apparent problems with pre-5.10.0 perl packaging conventions included:

1.  The current Arch Linux default perl installation installs _site_ and _vendor_ packages into the same directory tree, which frequently causes conflicts if the end user installs and upgrades Arch Linux perl (_vendor_) packages on top of _site_ packages.
2.  The current Arch Linux default perl installation installs updates to _core_ modules into the perl _core_ directories, creating file conflicts. Examples include modules such as `Data::Dumper` and `version`.
3.  A symlink-farm is created in `/usr/lib/perl5/` and `/usr/lib/perl5/site_perl` which is un-necessary and confusing.
4.  A number of standard modules seem to be missing, or were neglected to be added as _provides_ in the perl package itself, causing confusion and redundant entries in AUR and Community as users try and _fix_ the apparent problem of missing modules, which are provided by perl. This is probably a matter of education.
5.  Current perl-module PKGBUILD's could be simplified and standardized quite a bit.

This policy would eliminate all these problems.

### Pitfalls

Current (apparent) downsides to adopting a policy such as this one:

1.  An update of every perl module PKGBUILD so that it installs into the correct (_vendor_) directory tree. It remains somewhat backwards-compatible with the old structure, in that old PKGBUILD's would technically **work**.
2.  Introduces changes into the `perl` package, which lives in the _core_ repository, and proposes a new `perl-modules` package, which would live in the _extra_ repository.
3.  Non-perl packages which compile static copies of the perl interpreter will not operate correctly until recompiled on an Arch Linux PC which adheres to this document. Examples of such packages include `vim`, `subversion`, and `irssi`. Many such examples exist.

## Perl versions

At any given time, the package `perl` should represent the current stable upstream version of Perl revision 5\. (see Perl 6).

Only one package may contain the `/usr/bin/perl` binary and that package must either be perl or a dependency of that package. In order to provide a minimal installation of Perl for use by applications without requiring the whole of Perl to be installed, the `perl` package contains the binary and a basic set of modules. The perl package should declare provide statements for every module provided by the base perl package.

## Module paths

Perl searches three different locations for modules, referred to in this document as _core_ in which modules distributed with Perl are installed, _vendor_ for packaged modules, and _site_ for modules installed by the local administrator.

The module search path (`@INC`) in the Arch Linux packages has been ordered to include these locations in the following order:

*   _**site**_

Modules installed by the local administrator for the current version of Perl. Typically, these modules are installed using the _cpan_ or _cpanp_ tool, or are downloaded in source form and installed via make.

NaN

*   _**vendor**_

Packaged modules, installed via the pacman tool from the _core_, _extra_, or _community_ repositories, or built into proper Arch Linux packages from ABS/AUR PKGBUILDs.

NaN

*   _**core**_

Modules included in the core Perl distribution.

NaN

*   _**obsolete**_

Obsolete is the path name to modules installed prior to the establishment of this document. These paths have been removed from @INC in perl 5.12.2.

NaN

In each of the directory pairs above, the `lib` component is for binary, architecture dependent (XS) modules, and `share` for architecture-independent (pure-perl) modules. Under no circumstances should `current` be used as a replacement for `version`. Core and Vendor modules _should_ be matched to the current installation of perl.

## Documents

The POD files and manual pages and HTML documentation which do not refer to programs may be stripped from the package, which is normal for most Arch Linux packages in general. This is optional.

Manual pages distributed with Perl packages must be installed into the standard directories:

NaN

NaN

## Binaries and scripts

In order to prevent file collisions, it is important to keep binaries generated by _core_, _vendor_, and _site_ installs separate. It is also important that the default `PATH` environment variable set in each users profile to search for binaries in the same order as perl's `@INC` path. In order to accomplish this, binaries should be installed into the following directories:

NaN

The `perl` package should include a mechanism to adjust end-users `PATH` entries accordingly so that perl binaries are searched for in the following order: _site_, _vendor_, _core_.

## Core

Core modules are Perl modules "typically" included in the core Perl distribution.

### Core directories

*   Modules included in the core Perl distribution should be installed into `/usr/lib/perl5` and `/usr/share/perl5`.
*   Only modules contained in the `perl` package should be installed into this directory tree.
*   No version subdirectory exists in these paths as the dependencies for packaged modules should ensure that all work with the current `perl` package.

### Core perl packages

The `perl` package should contain the `/usr/bin/perl` binary, and a minimal set of modules needed in order for simple perl scripts to run and for a base system to operate. It should be maintained in the _core_ repository.

The following is a list of a few modules (for example), which are provided in the perl package. (See the PKGBUILD for the official list).

`'perl-checktree' 'perl-collate' 'perl-config' 'perl-cwd' 'perl-dynaloader' 'perl-english' 'perl-env' 'perl-exporter' 'perl-fnctl' 'perl-filehandle' 'perl-find' 'perl-finddepth' 'perl-getopt' 'perl-makemaker' 'perl-socket' 'perl-sys-syslog' 'perl-db-file' 'perl-storable' 'perl-data-dumper' 'perl-digest-md5'`.

Every module supplied in the perl package shall be added into the `provides` array in the PKGBUILD. Modules in this array should NOT appear in the perl packages `conflicts` or `replaces` arrays. End users should be able to install newer versions of core modules, either in _vendor_ or _site_ directories without file collisions.

## Site

Site modules are perl modules installed by the local administrator for the current version of Perl. Typically, these modules are installed using the cpan tool, or are downloaded in source form and installed via make (or MakeMaker).

### Site directories

The Perl packages must provide a mechanism for the local administrator to install modules under `/usr/lib/perl5/site_perl` but must not create or remove those directories.

Modules should be installed to the directories described above in Module Path `site`, programs to `/usr/bin/site_perl` and manual pages under `/usr/man`.

### Site installation

The following commands should be sufficient in the majority of cases for the local administrator to install modules and must create directories as required:

```
perl Makefile.PL
make install

```

or

```
cpan Foo::Bar

```

## Vendor

Vendor modules are packaged modules, installed via the pacman tool, or modules which have been built into proper Arch Linux packages from a PKGBUILD and makepkg.

### Package naming

Perl module packages should be named for the primary module provided. The naming convention for module Foo::Bar is perl-foo-bar. Packages which include multiple modules may additionally include provides for those modules using the same convention.

### Vendor directories

The installation directory for Arch Linux modules must be different from that for `site` modules. Some guidelines include:

*   The current Perl packaging uses the _vendor_ directories for this purpose, which are at present as described in above as `vendor`.
*   No version subdirectory exists on these directories as the dependencies for packaged modules should ensure that all work with the current `perl` package.
*   The Perl distribution includes many modules available separately from CPAN, which may have a newer version. The intent of the `@INC` ordering (described above) is to allow such modules to be packaged to _vendor_ which take precedence over the version in _core_. A packaged module which shadows a _core_ module in this way must be a newer version.
*   Module packages must install manual pages into the standard directories using the extensions `.1p` and `.3pm` to ensure that no conflict arises where a packaged module duplicates a _core_ module.
*   `.packlist` (used for module uninstalls) and `perllocal.pod` (used to record local/site installations) files should not be installed, and should be removed from the package if found.
*   Empty directories should be pruned.

### Vendor installation

A module should use the following lines in the PKGBUILD build target.

```
perl Makefile.PL INSTALLDIRS=vendor

```

and this one to install the results into the temporary tree...

```
make install DESTDIR="${pkgdir}" install

```

A depends on perl (>= 5.10.0) is required in order ensure that the module is correctly installed into the new `@INC` path.

### Sample vendor PKGBUILD

```
# $Id$
# Contributor: Barry User <barry@user.com>
# Maintainer: Harry Hacker <harry@hacker.com>

pkgname=perl-html-template
_realname=HTML-Template
pkgver=2.9
pkgrel=2
pkgdesc="Perl/CPAN Module HTML::Template : a simple HTML templating system"
arch=('any')
url="http://search.cpan.org/dist/${_realname}/"
license=('GPL' 'Artistic')
depends=('perl>=5.10.0')
source=("http://www.cpan.org/authors/id/S/SA/SAMTREGAR/${_realname}-${pkgver}.tar.gz")
md5sums=("cbf88a486b36284be55765ac7357c187")
options=('!emptydirs')

build() {
  cd "${_realname}-${pkgver}"

 # Setting these env variables overwrites any command-line options we don't want...
 export PERL_MM_USE_DEFAULT=1 PERL_AUTOINSTALL=--skipdeps \
   PERL_MM_OPT="INSTALLDIRS=vendor DESTDIR='$pkgdir'" \
   PERL_MB_OPT="--installdirs vendor --destdir '$pkgdir'" \
   PERL5LIB="" PERL_LOCAL_LIB_ROOT="" \
   MODULEBUILDRC=/dev/null

 # If using Makefile.PL
 { /usr/bin/perl Makefile.PL &&
   make &&
   make test &&
   make install; } || return 1

 # If using Build.PL
 { /usr/bin/perl Build.PL &&
   ./Build &&
   ./Build test &&
   ./Build install; } || return 1

 # remove perllocal.pod and .packlist
 find "$pkgdir" -name .packlist -o -name perllocal.pod -delete 
}

```

### Dependencies

#### Binary modules

Binary modules must specify a dependency on either `perl` with a minimum version of the `perl` package used to build the module, and must additionally depend on the expansion of `perlapi-$Config{version`}using the `Config` module.

#### Architecture-independent modules

Architecture-independent modules which require _core_ modules from the `perl` package must specify a dependency on that package.

Modules which contain explicit `require _version_` or `use _version_` statements must specify a dependency on `perl` with the minimum required version, or more simply the current version.

In the absence of an explicit requirement, architecture-independent modules must depend on a minimum `perl` version of `5.10.0` due to the changes in `@INC` introduced by that version.

## Perl6

There is currently work in progress on the next major revision, although the specifications have yet to be finalised.

It is anticipated that when Perl 6 is released it will initially be packaged as perl6, install the binary as `/usr/bin/perl6`, and use different directories for packaged modules to perl:

NaN

This will allow Perl 5 and 6 packages and modules (which should be packaged as perl6-foo-bar), to coexist for as long as required.

At some stage in the future when Perl 6 is sufficiently mature, the package naming may be reversed such that the `perl` package contains Perl 6 and the current package becomes `perl5`.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Perl_Policy&oldid=409211](https://wiki.archlinux.org/index.php?title=Perl_Policy&oldid=409211)"