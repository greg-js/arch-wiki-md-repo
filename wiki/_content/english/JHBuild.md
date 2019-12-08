Related articles

*   [GNOME](/index.php/GNOME "GNOME")

From [JHBuild's wiki](https://wiki.gnome.org/Projects/Jhbuild/Introduction):

	*JHBuild allows you to build and run GNOME platform and applications building the required modules in a sandbox environment, isolating the installation; so there is no need to build and run GNOME inside a virtual machine.*

JHBuild is a tool that allows you to automatically download and compile "modules" (i.e. source code packages). It can pull modules from a variety of sources (CVS, Subversion, Git, Bazaar, tarballs, etc.) and handle dependencies. You can also choose which specific modules you want to build, instead of building the whole project.

JHBuild was originally written for building [GNOME](/index.php/GNOME "GNOME"), but has since been extended to be usable with other projects.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Default configuration file](#Default_configuration_file)
    *   [2.2 User-specific configuration file](#User-specific_configuration_file)
    *   [2.3 Sample configuration](#Sample_configuration)
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
    *   [4.4 Build failed due to GCC library or object not found](#Build_failed_due_to_GCC_library_or_object_not_found)
    *   [4.5 gst-plugin-bad fails on missing vulkan headers](#gst-plugin-bad_fails_on_missing_vulkan_headers)
    *   [4.6 Library missing and no known rule to make it](#Library_missing_and_no_known_rule_to_make_it)
*   [5 Building JHBuild from scratch](#Building_JHBuild_from_scratch)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [jhbuild](https://aur.archlinux.org/packages/jhbuild/) package.

## Configuration

There are two configuration files: the [#Default configuration file](#Default_configuration_file) installed by [jhbuild](https://aur.archlinux.org/packages/jhbuild/) package, and the [#User-specific configuration file](#User-specific_configuration_file) created by the user.

By default JHBuild uses the installed configuration file. Its configuration is overridden by the configuration in the user-specific configuration file if it exists.

These use [Python](/index.php/Python "Python") syntax. See [JHBuild Manual](https://developer.gnome.org/jhbuild/stable/) for more information.

### Default configuration file

The default configuration file is located at `/usr/lib/python2.7/site-packages/jhbuild/defaults.jhbuildrc`. It should have everything you need for start using JHBuild, as it sets the modulesets directory, the default moduleset, autogen/meson/cmake arguments for all modules that use it.

Some default values currently set:

*   moduleset = `gnome-apps-latest`
*   modules = `meta-gnome-core`
*   directory of downloaded tarball = `$XDG_CACHE_HOME/jhbuild/downloads`
*   buildroot = `$XDG_CACHE_HOME/jhbuild/build`

If believe you found a Arch-specific setting that should be set, feel free to suggest that in [jhbuild](https://aur.archlinux.org/packages/jhbuild/) comments. If not Arch-specific, consider filing an [issue in the upstream](https://gitlab.gnome.org/GNOME/jhbuild/issues).

### User-specific configuration file

This configuration file is located at `$XDG_CONFIG_HOME/jhbuildrc` (e.g. `~/.config/jhbuildrc`). It is optional, does not exist by default and overrides values set in the default JHBuild configuration file.

It is very useful for, e.g., set a different moduleset, or to add a compiler flag to debug and try to fix a build failure system.

See examples in `/usr/share/jhbuild/examples/`.

### Sample configuration

This section shows a non-exhaustive list of key/value pairs that can be set in any of the configuration files.

*   Use a local moduleset file instead of downloading it again, making it possible to change something in the file and test it

```
use_local_modulesets = True
modulesets_dir = "~/.cache/jhbuild/"
```

*   Enable a wide-most moduleset, and also force GTK3 for modules that would use GTK2 by default

```
moduleset = ['gnome-world']
autogenargs = '--with-gtk3'
```

*   Or you may want to enable documentation build for autotools, even though it will slowdown module compilation

 `autogenargs = '--enable-gtk-doc'` 

*   Or you want some debug output from make command

 `makeargs = 'V=1'` 

*   Or you found out that a module requires a specific automake option (WebKit is already patched, there is no real need for this one)

 `module_autogenargs['WebKit'] = 'PYTHON=/usr/bin/python2'` 

*   Or you want to disable documentation build for a module that use meson build system

 `module_mesonargs['gstreamer'] = '-Ddisable_gtkdoc=true` 
**Note:** *autotools* and *meson* are different build systems, so make sure to add the desired flags for the correct option name

## Usage

This topic provides some information and examples on how to use some JHBuild commands, but without intending to exhaust the subject. For a detailed information on each of JHBuild commands, please refer to [JHBuild Manual](https://developer.gnome.org/jhbuild/stable/), learn from each command's help output or even read JHBuild's [source code](https://gitlab.gnome.org/GNOME/jhbuild/).

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

A module that depends on [python2](https://www.archlinux.org/packages/?name=python2) may fail to build as software usually expect the binary filename of python 2.x to be `/usr/bin/python` and python 3.x to be `/usr/bin/python3`, which is not the case in Arch Linux: python 2.x is `/usr/bin/python2` and python 3.x is `/usr/bin/python`.

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

You may come across with a message similar to one of these below.

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

### Build failed due to GCC library or object not found

You may come across with a message similar to the one below.

 `cc: error: /usr/lib/gcc/x86_64-pc-linux-gnu/*gcc_version*/../../../../lib/*name*.so: No such file or directory` 

or

 `g++: error: /usr/lib/gcc/x86_64-pc-linux-gnu/*gcc_version*/../../../../lib/*name*.o: No such file or directory` 

where *gcc_version* is a GCC version older than the current one, and *name* is the name of the library (.so) or object (.o) that failed to be found.

This may happen if [gcc](https://www.archlinux.org/packages/?name=gcc) was updated and the software was previously configured and built with the previous version of gcc.

**Solution:** Run *Configure* phase again, in order to have this module configured with newer GCC version

### gst-plugin-bad fails on missing vulkan headers

When building the *gst-plugins-bad* module, You may come across with a number of messages similar to the one below:

```
In file included from ext/vulkan/gstvulkan-plugins-enumtypes.c:8:
../../../../jhbuild/checkout/gst-plugins-bad/ext/vulkan/vkviewconvert.h:26:10: fatal error: gst/vulkan/vulkan.h: No such file or directory
   26 
```

It means *gst-plugin-bad* was automatically set to build its *vulkan* extension, but did not find all the dependecies it needs. As of the writing this subsection, [ext/vulkan/meson.build](https://github.com/GStreamer/gst-plugins-bad/blob/master/ext/vulkan/meson.build) looks for the binary *glslc* provided by [shaderc](https://www.archlinux.org/packages/?name=shaderc), which several packages depend on directly or indirectly. Removing [shaderc](https://www.archlinux.org/packages/?name=shaderc) would solve this error, but this might not be an option if you want to keep one those packages the depends on it.

**Solution:** edit your jhbuild user configuration file to disable the *vulkan* extension:

 `~/.config/jhbuildrc`  `module_mesonargs['gst-plugins-bad'] = '-D vulkan=disabled'` 

and run Configure phase again, in order to have the *gst-plugins-bad* module successfully built.

### Library missing and no known rule to make it

When building a module that uses meson build system you might come across an issue like this:

```
*** Checking out *module_name* *** [67/218]
*some omitted checkout output*
*** Building *module_name* *** [67/218]
ninja
**ninja: error: '*path/to/missing_library.so*', needed by '*path/to/module_file*', missing and no known rule to make it**
*** Error during the phase build of *module_name*: ########## Error running ninja   *** [67/218]

```

This happens because the module was previously configured and built in another commit of this module, and in that occasion it was configured to a previous version of the dependency `*path/to/missing_library.so*`. Since the file `*path/to/module_file*` was configured to and expects that missing library to be available, it fails.

**Solution**: Just run option 7 for the configure phase to reconfigure the module and build it again.

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
*   [JHBuild Source Code](https://gitlab.gnome.org/GNOME/jhbuild/)