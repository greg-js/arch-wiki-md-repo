JHBuild is a tool that allows you to automatically download and compile "modules" (i.e. source code packages). It can pull modules from a variety of sources (CVS, Subversion, Git, Bazaar, tarballs, etc.) and handle dependencies. You can also choose which specific modules you want to build, instead of building the whole project.

JHBuild was originally written for building [GNOME](/index.php/GNOME "GNOME"), but has since been extended to be usable with other projects.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Default JHBuild configuration](#Default_JHBuild_configuration)
    *   [2.2 User configuration](#User_configuration)
*   [3 Usage](#Usage)
    *   [3.1 Checking and installing prerequisites](#Checking_and_installing_prerequisites)
    *   [3.2 Updating modules](#Updating_modules)
    *   [3.3 Building modules](#Building_modules)
    *   [3.4 Running modules](#Running_modules)
    *   [3.5 Creating dependency graph](#Creating_dependency_graph)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Python issues](#Python_issues)
        *   [4.1.1 Building from scratch without JHBuild, or in a JHBuild shell](#Building_from_scratch_without_JHBuild.2C_or_in_a_JHBuild_shell)
        *   [4.1.2 itstool missing Python modules](#itstool_missing_Python_modules)
    *   [4.2 pkg-config issues](#pkg-config_issues)
    *   [4.3 gnome-devel-docs does not build](#gnome-devel-docs_does_not_build)
    *   [4.4 pango does not build](#pango_does_not_build)
    *   [4.5 geary does not build](#geary_does_not_build)
    *   [4.6 Other broken modules](#Other_broken_modules)
*   [5 Packages needed to build specific modules](#Packages_needed_to_build_specific_modules)
*   [6 See also](#See_also)

## Installation

Install the [jhbuild](https://aur.archlinux.org/packages/jhbuild/) package, which usually provides the stable version.

Alternatively, you may want to install [jhbuild-git](https://aur.archlinux.org/packages/jhbuild-git/) for latest JHBuild version in GNOME repository.

## Configuration

JHBuild gets its configuration from a system-wide configuration file installed with the package, the `defaults.jhbuildrc`, and from an optional user configuration file jhbuildrc, in `~/.config/jhbuildrc` (if it exists).

These files use [Python](/index.php/Python "Python") syntax to set configuration variables.

The variables currently accepted can be found in [JHBuild Manual](https://developer.gnome.org/jhbuild/stable/).

### Default JHBuild configuration

It can be found at `/usr/lib/python2.7/site-packages/jhbuild/defaults.jhbuildrc`.

`defaults.jhbuildrc` provides default values for many configuration options, e.g. moduleset, modules, autoargs, module_autoargs, and others.

It is provided with the package, so please avoid modifying it.

The values set in `defaults.jhbuildrc` should be enough for JHBuild to work. Nevertheless, take a look at its value to decide what you want to use the default, and what you want to customize in a personal jhbuild configuration file.

### User configuration

`~/.config/jhbuildrc` is very useful for setting personal values in order to overlap what is currently set in `defaults.jhbuildrc` (e.g.: want to set a different moduleset), or to set values not already set in `defaults.jhbuildrc` (e.g.: your own module_autoargs for a specific module).

You may find a very extended sample of a configuration file in `/usr/share/jhbuild/examples/sample.jhbuildrc`

See below a few examples for `~/.config/jhbuildrc` contents:

*   Enable a wide-most moduleset, and also force GTK3 for modules that would use GTK2 by default

```
 moduleset = ['gnome-world']
 autogenargs = '--with-gtk3'

```

*   Or you may want to enable documentation build, even though it will slowdown module compilation

```
 autogenargs = '--enable-gtk-doc'

```

*   Or you want some debug output from make command

```
 makeargs = 'V=1'

```

*   Or you found out that a module needs a specific setting (this is just an example; itstool is already specified)

```
 module_autogenargs = {
      'itstool': autogenargs + ' PYTHON=/usr/bin/python2'
 }

```

## Usage

This topic provides some information and examples on how to use some JHBuild commands, but without intending to exhaust the subject. For a detailed information on each of JHBuild commands, please refer to [JHBuild Manual](https://developer.gnome.org/jhbuild/stable/), learn from each command's help output or even read JHBuild's [source code](https://git.gnome.org/browse/jhbuild/).

JHBuild provides a general `--help` which lists all the commands available, and also a help message for each sub-command, e.g. `jhbuild sysdeps --help`.

### Checking and installing prerequisites

*sysdeps* can be used to get a detailed list of which dependencies you have installed and which ones you should install. In order to get this information, just run:

```
$ jhbuild sysdeps

```

Alternatively, *sanitycheck* may also be used to report missing tools that are required (e.g. mozjs38). If nothing is reported (and exit code is 0), then you're good to go! Similiar to the above command, just run:

```
$ jhbuild sanitycheck

```

If some tools are reported to be missing, you can — besides installing correspondent packages with pacman, if available — run *bootstrap* command, which will download, build and install the named module inside your jhbuild tree:

```
$ jhbuild bootstrap

```

**Note:** All dependencies informed by *sysdeps* should be already listed as dependency [jhbuild](https://aur.archlinux.org/packages/jhbuild/) by now. If you run *sysdeps* and find out a dependency that is not be listed, please report it in the comments of [jhbuild](https://aur.archlinux.org/packages/jhbuild/)

### Updating modules

It is possible to simply update the source code of the modules without building them, making it possible build another time without having to wait fetching the source code. There are three ways of simply updating modules:

*update*, without any arguments, will update all modules available in the moduleset/modules set in configuration file

```
$ jhbuild update

```

*update*, with one or more modules as arguments, will update **all** modules that the named modules depends on. e.g.:

```
$ jhbuild update gedit

```

*updateone*, with one or more modules, will update **only** the named module(s). e.g.:

```
$ jhbuild updateonly gedit

```

### Building modules

This action will run the whole build process: it will update the source code (unless it is already up-to-date), configure & build, and install it in the proper directory.

Just like *update*, There are three ways of building modules in JHBuild:

*build*, without any arguments, will build all modules available in the moduleset/modules set in configuration file

```
$ jhbuild build

```

*build*, with one or more modules as arguments, will build **all** modules that the named modules depends on. e.g.:

```
$ jhbuild build gedit

```

*buildone*, with one or more modules, will build **only** the named module(s). e.g.:

```
$ jhbuild buildone gedit

```

**Note:** Please notice that since *buildone* don't also build the latest development version of a module's dependencies, it may fail due to dependency not being installed or being out-of-date; in this case, you should run *build* for the named module

### Running modules

After a successfully installed application in JHBuild, use *run* to start the module you just built. e.g.:

```
$ jhbuild run gedit

```

### Creating dependency graph

JHBuild can output graph contents which can by piped into [graphviz](https://www.archlinux.org/packages/?name=graphviz) in order to generate e.g. a PNG or PostScript file.

To generate a PNG file of e.g. gedit, run:

```
$ jhbuild dot gedit | dot -Tpng > dependencies.png

```

## Troubleshooting

**Note:** If you encounter an issue that is not documented below, please report it in a comment on the [jhbuild](https://aur.archlinux.org/packages/jhbuild/) package.

### Python issues

#### Building from scratch without JHBuild, or in a JHBuild shell

If you are building from scratch on your own, it may be necessary to run *autogen.sh* with the following:

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

### gnome-devel-docs does not build

Choose `[4] Start shell` and run:

```
$ git revert --no-edit 9ba0d959

```

Then, exit the shell and choose `[1] Rerun phase build`. See [this bug](https://bugzilla.gnome.org/show_bug.cgi?id=707007) for further details.

### pango does not build

If build failed due to cairo.h not found, do the following: Enter [4]shell, edit `pango/pangocairo.h` changing:

 ` #define <cairo.h>` 

to

 ` #define <cairo/cairo.h>` 

### geary does not build

If you are getting this error message...

```
[ 78%] Generating webkitgtk-3.0.vapi
error: /home/rffontenelle/jhbuild/install/share/gir-1.0/WebKit-3.0.gir not found
Generation failed: 1 error(s), 0 warning(s)
make[2]: *** [src/CMakeFiles/geary.dir/build.make:1277: src/webkitgtk-3.0.vapi] Error 1
make[1]: *** [CMakeFiles/Makefile2:798: src/CMakeFiles/geary.dir/all] Error 2
```

... then please notice that geary depends on WebKitGTK (<= 2.4), but JHBuild compiles WebKit2GTK (newer). This is a known issue ([#741866](https://bugzilla.gnome.org/show_bug.cgi?id=741866) and [mailing list](https://mail.gnome.org/archives/geary-list/2016-June/msg00022.html)) and there is a plan for porting Geary ([#728002](https://bugzilla.gnome.org/show_bug.cgi?id=728002))

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
*   gtk-vnc requires [perl-text-csv](https://www.archlinux.org/packages/?name=perl-text-csv)
*   latexila requires [lcov](https://aur.archlinux.org/packages/lcov/)
*   pango requires [libpthread-stubs](https://aur.archlinux.org/packages/libpthread-stubs/)
*   totem-pl-parser requires [libgcrypt15](https://www.archlinux.org/packages/?name=libgcrypt15)
*   xf86-video-intel requires [xorg-server-devel](https://www.archlinux.org/packages/?name=xorg-server-devel)
*   xwayland requires [xtrans](https://www.archlinux.org/packages/?name=xtrans), [xcmiscproto](https://www.archlinux.org/packages/?name=xcmiscproto), and [bigreqsproto](https://www.archlinux.org/packages/?name=bigreqsproto)
*   zeitgeist requires [python2-rdflib](https://www.archlinux.org/packages/?name=python2-rdflib)
*   wireless-tools requires [wireless_tools](https://www.archlinux.org/packages/?name=wireless_tools)
*   xorg-macros requires [xorg-util-macros](https://www.archlinux.org/packages/?name=xorg-util-macros)

## See also

*   [JHBuild homepage in GNOME Wiki](https://wiki.gnome.org/Projects/Jhbuild)
*   [JHBuild for GNOME newcomers](https://wiki.gnome.org/Newcomers/BuildGnome)
*   [JHBuild for experienced GNOME contributors](https://wiki.gnome.org/HowDoI/Jhbuild)
*   [JHBuild Manual](https://developer.gnome.org/jhbuild/stable/)
*   [JHBuild Source Code](https://git.gnome.org/browse/jhbuild/)