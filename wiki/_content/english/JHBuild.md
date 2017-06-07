From [JHBuild's wiki](https://wiki.gnome.org/Projects/Jhbuild/Introduction):

	*JHBuild allows you to build and run GNOME platform and applications building the required modules in a sandbox environment, isolating the installation; so there is no need to build and run GNOME inside a virtual machine.*

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
        *   [4.1.1 Modules known to require python2 exclusively](#Modules_known_to_require_python2_exclusively)
    *   [4.2 pkg-config issues](#pkg-config_issues)
    *   [4.3 Build failed due to incompatible meson versions](#Build_failed_due_to_incompatible_meson_versions)
*   [5 Building JHBuild from scratch](#Building_JHBuild_from_scratch)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [jhbuild](https://aur.archlinux.org/packages/jhbuild/) package.

## Configuration

JHBuild gets its configuration from a system-wide configuration file installed with the package, the `defaults.jhbuildrc`, and from an optional user configuration file jhbuildrc, in `~/.config/jhbuildrc` (if it exists).

These files use [Python](/index.php/Python "Python") syntax to set configuration variables.

The variables currently accepted can be found in [JHBuild Manual](https://developer.gnome.org/jhbuild/stable/).

### Default JHBuild configuration

JHBuild default configuration is provided by [jhbuild](https://aur.archlinux.org/packages/jhbuild/) and can be found at `/usr/lib/python2.7/site-packages/jhbuild/defaults.jhbuildrc`.

`defaults.jhbuildrc` should contain all values for options (e.g. moduleset, module_autoargs) needed to run JHBuild smoothly.

Even though the default values in `defaults.jhbuildrc` should be all you need for running JHBuild, you might want to take a look at it to decide if and what you want to customize in a personal configuration file.

**Note:** If you think you found a setting that should be default, feel free to suggestion that in [jhbuild](https://aur.archlinux.org/packages/jhbuild/) comments

### User configuration

The file `~/.config/jhbuildrc` is optional. You can create it with your personal JHBuild configurations, in order to overlap the default values (see above topic).

A very extended sample of a configuration file can be found in `/usr/share/jhbuild/examples/sample.jhbuildrc`

User configuration is particularly useful to, e.g., set a different moduleset, to add a flag to a build system to debug or to disable something.

See below a few examples for `~/.config/jhbuildrc` contents:

*   Enable a wide-most moduleset, and also force GTK3 for modules that would use GTK2 by default

```
 moduleset = ['gnome-world']
 autogenargs = '--with-gtk3'

```

*   Or you may want to enable documentation build for autotools, even though it will slowdown module compilation

```
 autogenargs = '--enable-gtk-doc'

```

*   Or you want some debug output from make command

```
 makeargs = 'V=1'

```

*   Or you found out that a module requires a specific automake option (WebKit is already patched, there is no real need for this one)

```
 module_autogenargs['WebKit'] = 'PYTHON=/usr/bin/python2'

```

*   Or you want to disable documentation build for a module that use meson build system

```
 module_mesonargs['gstreamer'] = '-Ddisable_gtkdoc=true

```

**Note:** **autotools** and **meson** are different build systems, so make sure to add the desired flags for the correct option name

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

A module that depends on [python2](https://www.archlinux.org/packages/?name=python2) may fail to build as softwares usually expect the binary filename of python 2.x to be `/usr/bin/python` and python 3.x to be `/usr/bin/python3`, which is not the case in Arch Linux: python 2.x is `/usr/bin/python2` and python 3.x is `/usr/bin/python`.

For cases like that, force the modules to run `/usr/bin/python2` using the one or more methods below:

*   set *module_autoargs* with *PYTHON=/usr/bin/python2* for this specific module in `~/.config/jhbuildrc`, as mentioned in the above Configuration section — this will run autogen.sh or configure with this value for variable PYTHON

*   if the *configure* or *Makefile* doesn't parse PYTHON variable, one approach is to manually find all lines in *configure*/*Makefile* that run python binary and rename python -> python2 — this will hard code python2 in the module's source code.

*   if only the above workarounds still don't work for you, consider editing module's .py files in order to replace *python* with *python2* when the first line matches *#!/usr/bin/env python* or *#!/usr/bin/python*

**Note:** All edits and patches that are manually applied to the source code will be lost when you wipe the directory and checkout (download) it again, so it is not exactly a permanent solution

**Note:** If a module's configure/build process misuse PYTHON variable, or doesn't use at all, consider reporting it to the module's upstream and/or providing patch for JHBuild upstream

#### Modules known to require python2 exclusively

[jhbuild](https://aur.archlinux.org/packages/jhbuild/) is already patched to use *python2* for modules that exclusively require this Python version, and therefore no action is required if you're using packaged JHBuild.

They are:

*   telepathy-mission-control
*   WebKit

### pkg-config issues

If you have a malformatted .pc file on your PKG_CONFIG_PATH, JHBuild will not be able to detect all the (valid) .pc files you have installed and will complain that the .pc files are missing. Look at the output of `jhbuild sysdeps`—there should be a message about the problematic .pc files.

### Build failed due to incompatible meson versions

You may come across with a message similar to the one below.

```
Meson encountered an error:
Build directory has been generated with Meson version 0.40.0, which is incompatible with current version 0.40.1.
Please delete this build directory AND create a new one.
FAILED: build.ninja 
'/usr/bin/python3' '/home/foobar/jhbuild/install/bin/meson' --internal regenerate '/home/foobar/jhbuild/checkout/gst-plugins-base' '/home/foobar/.cache/jhbuild/build/gst-plugins-base' --backend ninja
ninja: error: rebuilding 'build.ninja': subcommand failed
```

In the above example, the module was configured with meson 0.40.0 at on time, but a newer version (0.40.1, in the example) is now installed and is not compatible with the old one.

**Solution:** Run Configure phase again, in order to have this module configured with newer Meson version

## Building JHBuild from scratch

If you do not want to use the [jhbuild](https://aur.archlinux.org/packages/jhbuild/) package, and instead you want build JHBuild from scratch on your own, there are a few things you should pay attention too.

*   Make sure to install all the dependencies required by JHBuild and its target modules. Refer to [list of dependencies for Arch Linux](https://wiki.gnome.org/Projects/Jhbuild/Dependencies/ArchLinux);

*   JHBuild itself depends on [Python](/index.php/Python "Python") version 2, so make sure to run JHBuild's *autogen.sh* with the following command line:

```
$ PYTHON=/usr/bin/python2 ./autogen.sh

```

*   Likewise, some modules may still depend on python2\. Make sure to read the above topic 'Python issues'.

*   For detailed information downloading and building the source code of JHBuild, check ["How Do I" at GNOME wiki](https://wiki.gnome.org/HowDoI/JhbuildJHBuild's).

## See also

*   [JHBuild homepage in GNOME Wiki](https://wiki.gnome.org/Projects/Jhbuild)
*   [JHBuild for GNOME newcomers](https://wiki.gnome.org/Newcomers/BuildGnome)
*   [JHBuild for experienced GNOME contributors](https://wiki.gnome.org/HowDoI/Jhbuild)
*   [JHBuild Manual](https://developer.gnome.org/jhbuild/stable/)
*   [JHBuild Source Code](https://git.gnome.org/browse/jhbuild/)