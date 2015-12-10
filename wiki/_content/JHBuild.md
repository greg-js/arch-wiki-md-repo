# JHBuild

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

JHBuild is a tool that allows you to automatically download and compile "modules" (i.e. source code packages). It can pull modules from a variety of sources (CVS, Subversion, Git, Bazaar, tarballs, etc.) and handle dependencies. You can also choose which specific modules you want to build, instead of building the whole project.

JHBuild was originally written for building [GNOME](/index.php/GNOME "GNOME"), but has since been extended to be usable with other projects.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 Installing prerequisites](#Installing_prerequisites)
    *   [3.2 Building](#Building)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Python issues](#Python_issues)
        *   [4.1.1 Building from scratch without JHBuild, or in a JHBuild shell](#Building_from_scratch_without_JHBuild.2C_or_in_a_JHBuild_shell)
        *   [4.1.2 itstool missing Python modules](#itstool_missing_Python_modules)
    *   [4.2 pkg-config issues](#pkg-config_issues)
    *   [4.3 totem does not build](#totem_does_not_build)
    *   [4.4 evolution does not build](#evolution_does_not_build)
    *   [4.5 gnome-devel-docs does not build](#gnome-devel-docs_does_not_build)
    *   [4.6 devhelp does not build](#devhelp_does_not_build)
    *   [4.7 libosinfo does not build](#libosinfo_does_not_build)
    *   [4.8 ibus-pinyin does not build](#ibus-pinyin_does_not_build)
    *   [4.9 cairo does not build](#cairo_does_not_build)
    *   [4.10 pango does not build](#pango_does_not_build)
    *   [4.11 Other broken modules](#Other_broken_modules)
*   [5 Packages needed to build specific modules](#Packages_needed_to_build_specific_modules)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Pacman "Pacman") a JHBuild variant from the [AUR](/index.php/AUR "AUR"):

*   [jhbuild](https://aur.archlinux.org/packages/jhbuild/)<sup><small>AUR</small></sup> - Stable version.
*   [jhbuild-git](https://aur.archlinux.org/packages/jhbuild-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/jhbuild-git)]</sup> - Development version.

## Configuration

The configuration file for JHBuild is located at `~/.config/jhbuildrc`. It uses [Python](/index.php/Python "Python") syntax to set configuration variables. Here is the sample file provided for building GNOME:

```
# -*- mode: python -*-
# -*- coding: utf-8 -*-

# edit this file to match your settings and copy it to ~/.config/jhbuildrc

# if you have a GNOME git account, uncomment this line
# repos['git.gnome.org'] = 'ssh://user@git.gnome.org/git/'

# what module set should be used. The default can be found in
# jhbuild/defaults.jhbuildrc, but can be any file in the modulesets directory
# or a URL of a module set file on a web server.
# moduleset = 'gnome-apps-3.12'
#
# A list of the modules to build. Defaults to the GNOME core and tested apps.
# modules = [ 'meta-gnome-core', 'meta-gnome-apps-tested' ]

# Or to build the old GNOME 2.32:
# moduleset = 'gnome2/gnome-2.32'
# modules = ['meta-gnome-desktop']

# what directory should the source be checked out to?
checkoutroot = os.path.expanduser('~/checkout/gnome')

# the prefix to configure/install modules to (must have write access)
prefix = '/opt/gnome'

# custom CFLAGS / environment pieces for the build
# os.environ['CFLAGS'] = '-Wall -g -O0'

# extra arguments to pass to all autogen.sh scripts
# to speed up builds of GNOME, try '--disable-static --disable-gtk-doc'
#autogenargs=''

# On multiprocessor systems setting makeargs to '-j2' may improve compilation
# time. Be aware that not all modules compile correctly with '-j2'.
# Set makeargs to 'V=1' for verbose build output.
#makeargs = '-j2'

```

You should edit (at least) _modules_ to the desired modules to be built. A reference for most configuration variables is available at [GNOME JHBuild Manual](http://developer.gnome.org/jhbuild/unstable/config-reference.html.en).

## Usage

### Installing prerequisites

JHBuild can check if the required tools are installed by running _sanitycheck_:

```
$ jhbuild sanitycheck

```

If any errors are shown, missing packages may be installed from repositories or running the _bootstrap_ command, which tries to download, build and install the build prerequisites:

```
$ jhbuild bootstrap

```

### Building

To build all the modules selected in the configuration file, just run the _build_ command:

```
$ jhbuild build

```

JHBuild will download, configure, compile and install each of the modules. See

```
$ jhbuild help

```

for more details.

If an error occurs at any stage, JHBuild will present a menu asking what to do. The choices include dropping to a shell to fix the error, rerunning the build from various stages, giving up on the module, or ignore the error and continue. Often, dropping to a shell and checking makefiles and configuration files can be helpful. If you face a build error, for example, you can try to manually `make` and check errors on the shell.

Giving up on a module will cause any modules depending on it to fail.

To build as many packages as possible, skipping broken packages, run:

```
$ yes 3 | jhbuild --try-checkout build

```

## Troubleshooting

**Note:** If you encounter an issue that is not documented below, please report it in a comment on the [jhbuild](https://aur.archlinux.org/packages/jhbuild/)<sup><small>AUR</small></sup> package.

### Python issues

#### Building from scratch without JHBuild, or in a JHBuild shell

If you are building from scratch on your own, it may be necessary to run _autogen.sh_ with the following:

```
$ PYTHON=/usr/bin/python2 ./autogen.sh

```

And set the PYTHON environment variable in ~/.config/jhbuildrc

```
os.environ['PYTHON'] = '/usr/bin/python2'

```

**Note:** JHBuild uses its own python lib directory in /opt/gnome/lib/python2.7; if you are having problems with python imports check to see that the .py files are there.

#### itstool missing Python modules

Chose `[4] Start shell` and run:

```
$ sed -ir 's/| python /| python2 /' configure

```

Then, exit the shell and choose `[1] Rerun phase configure`. See [this merge request](https://gitorious.org/itstool/itstool/merge_requests/6) for more details.

### pkg-config issues

If you have a malformatted .pc file on your PKG_CONFIG_PATH, JHBuild will not be able to detect all the (valid) .pc files you have installed and will complain that the .pc files are missing. Look at the output of `jhbuild sysdeps`—there should be a message about the problematic .pc files.

### totem does not build

Choose `[4] Start shell` and run:

```
$ curl [https://git.gnome.org/browse/totem/patch/?id=198d7f251e7816f837378fb2081829188847b916](https://git.gnome.org/browse/totem/patch/?id=198d7f251e7816f837378fb2081829188847b916) | git apply

```

Then, exit the shell and choose `[1] Rerun phase build`.

### evolution does not build

Choose `[4] Start shell` and run:

```
$ curl [https://bug707112.bugzilla-attachments.gnome.org/attachment.cgi?id=253584](https://bug707112.bugzilla-attachments.gnome.org/attachment.cgi?id=253584) | git apply

```

Then, exit the shell and choose `[1] Rerun phase build`. See [this bug](https://bugzilla.gnome.org/show_bug.cgi?id=707112) for further details.

### gnome-devel-docs does not build

Choose `[4] Start shell` and run:

```
$ git revert --no-edit 9ba0d959

```

Then, exit the shell and choose `[1] Rerun phase build`. See [this bug](https://bugzilla.gnome.org/show_bug.cgi?id=707007) for further details.

### devhelp does not build

Choose `[4] Start shell` and run:

```
$ curl [https://bug707490.bugzilla-attachments.gnome.org/attachment.cgi?id=254113](https://bug707490.bugzilla-attachments.gnome.org/attachment.cgi?id=254113) | git apply

```

Then, exit the shell and choose `[1] Rerun phase build`. See [this bug](https://bugzilla.gnome.org/show_bug.cgi?id=707490) for further details.

### libosinfo does not build

Choose `[4] Start shell` and run:

```
$ curl [https://fedorahosted.org/libosinfo/raw-attachment/ticket/9/0001-Don-t-use-AM_GNU_GETTEXT.patch](https://fedorahosted.org/libosinfo/raw-attachment/ticket/9/0001-Don-t-use-AM_GNU_GETTEXT.patch) | git apply

```

Then, exit the shell and choose `[1] Rerun phase build`. See [this bug](https://fedorahosted.org/libosinfo/ticket/9) for further details.

### ibus-pinyin does not build

Choose `[4] Start shell` and run:

```
$ curl [https://github.com/ibus/ibus-pinyin/commit/3d0680c2b9533d0abff30258d0e772b8aa97af1c.patch](https://github.com/ibus/ibus-pinyin/commit/3d0680c2b9533d0abff30258d0e772b8aa97af1c.patch) | git apply

```

Then, exit the shell and choose `[8] Go to phase "clean"`. See [this bug](https://code.google.com/p/ibus/issues/detail?id=1581) for further details.

### cairo does not build

Add "-flto -ffat-lto-objects" to CFLAGS. See [FS#40313](https://bugs.archlinux.org/task/40313) for further details.

### pango does not build

If build failed due to cairo.h not found, do the following: Enter [4]shell, edit `pango/pangocairo.h` changing:

 ` #define <cairo.h>` 

to

 ` #define <cairo/cairo.h>` 

### Other broken modules

The following modules do not build, and there are no known/immediate fixes (feel free to jump in and investigate):

*   aisleriot—[bug report](https://bugzilla.gnome.org/show_bug.cgi?id=707106) (probably easy to fix if you poke around)
*   gegl
*   gnome-boxes—[bug report](https://bugzilla.gnome.org/show_bug.cgi?id=725520) (a fix is provided there)
*   gnome-photos
*   gtksourceviewmm
*   meta-gnome-apps-tested
*   nemiver
*   orca
*   rygel
*   valadoc

This list includes modules transitively depending on broken modules (i.e. some of the modules might be fine; I did not check).

## Packages needed to build specific modules

*   gitg requires [gtkspell3](https://www.archlinux.org/packages/?name=gtkspell3)
*   gtk-vnc requires [perl-text-csv](https://aur.archlinux.org/packages/perl-text-csv/)<sup><small>AUR</small></sup>
*   latexila requires [lcov](https://aur.archlinux.org/packages/lcov/)<sup><small>AUR</small></sup>
*   pango requires [libpthread-stubs](https://aur.archlinux.org/packages/libpthread-stubs/)<sup><small>AUR</small></sup>
*   totem-pl-parser requires [libgcrypt15](https://aur.archlinux.org/packages/libgcrypt15/)<sup><small>AUR</small></sup>
*   xf86-video-intel requires [xorg-server-devel](https://www.archlinux.org/packages/?name=xorg-server-devel)
*   xwayland requires [xtrans](https://www.archlinux.org/packages/?name=xtrans), [xcmiscproto](https://www.archlinux.org/packages/?name=xcmiscproto), and [bigreqsproto](https://www.archlinux.org/packages/?name=bigreqsproto)
*   zeitgeist requires [python2-rdflib](https://www.archlinux.org/packages/?name=python2-rdflib)
*   wireless-tools requires [wireless_tools](https://www.archlinux.org/packages/?name=wireless_tools)
*   xorg-macros requires [xorg-util-macros](https://www.archlinux.org/packages/?name=xorg-util-macros)

## See also

[GNOME JHBuild Manual](http://developer.gnome.org/jhbuild/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=JHBuild&oldid=392285](https://wiki.archlinux.org/index.php?title=JHBuild&oldid=392285)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Development](/index.php/Category:Development "Category:Development")