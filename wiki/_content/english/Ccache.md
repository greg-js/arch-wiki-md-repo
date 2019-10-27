Related articles

*   [Makepkg](/index.php/Makepkg "Makepkg")
*   [Distcc](/index.php/Distcc "Distcc")

[ccache](https://ccache.dev/) is a tool for the gcc compiler used to compile the same program over and over again with little downtime. While it may take a few seconds longer to compile a program the first time with *ccache*, subsequent compiles will be much, much faster.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Enable ccache for makepkg](#Enable_ccache_for_makepkg)
    *   [2.2 Enable for command line](#Enable_for_command_line)
    *   [2.3 Enable with colorgcc](#Enable_with_colorgcc)
*   [3 Misc](#Misc)
    *   [3.1 Sloppiness](#Sloppiness)
    *   [3.2 Change the cache directory](#Change_the_cache_directory)
    *   [3.3 Set maximum cache size](#Set_maximum_cache_size)
    *   [3.4 Disable the cache via environment](#Disable_the_cache_via_environment)
    *   [3.5 CLI](#CLI)
    *   [3.6 makechrootpkg](#makechrootpkg)
*   [4 Caveat](#Caveat)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [ccache](https://www.archlinux.org/packages/?name=ccache) package.

## Configuration

The default behavior can be overridden by configuration files. Priority of the configuration settings is as follows (where 1 is highest):

1.  Environment variables
2.  Cache-specific configuration file (`$HOME/.ccache/ccache.conf`)
3.  System-wide configuration file (`/etc/ccache.conf`)

See [ccache(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ccache.1) for details.

### Enable ccache for makepkg

To enable *ccache* when using [makepkg](/index.php/Makepkg "Makepkg") edit `/etc/makepkg.conf`. In `BUILDENV` uncomment `ccache` (remove the exclamation mark) to enable caching. For example:

 `/etc/makepkg.conf`  `BUILDENV=(!distcc color **ccache** check !sign)` 

### Enable for command line

If you are compiling your code from the command line, and not building packages, then you will still want to use *ccache* to help speed things up.

For that, you can prefix each compilation command with `ccache`.

```
$ ccache cc hello_world.c

```

Alternatively, change your `$PATH` to include *ccache'*s binaries before the path to your compiler:

```
$ export PATH="/usr/lib/ccache/bin/:$PATH"

```

You may want to set this line as an [environment variable](/index.php/Environment_variable "Environment variable") for regular usage.

**Note:** Such export will inevitably enable *ccache* for *makepkg* as well if invoked with this PATH.

### Enable with colorgcc

Since [colorgcc](https://www.archlinux.org/packages/?name=colorgcc) is also a compiler wrapper, some care needs to be taken to ensure each wrapper is called in the correct sequence.

```
export PATH="/usr/lib/colorgcc/bin/:$PATH"    # As per usual colorgcc installation, leave unchanged (don't add *ccache*)
export CCACHE_PATH="/usr/bin"                 # Tell *ccache* to only use compilers here

```

Then *colorgcc* needs to be told to call *ccache* instead of the real compiler. Edit `/etc/colorgcc/colorgccrc` and change the `/usr/bin` paths to `/usr/lib/ccache/bin` for all the compilers in `/usr/lib/ccache/bin`:

 `/etc/colorgcc/colorgccrc` 
```
g++: /usr/lib/ccache/bin/g++
gcc: /usr/lib/ccache/bin/gcc
c++: /usr/lib/ccache/bin/g++
cc: /usr/lib/ccache/bin/cc
g77:/usr/bin/g77
f77:/usr/bin/g77
gcj:/usr/bin/gcj

```

Newer versions of *ccache* will always enable color for GCC when `GCC_COLORS` is set. Color is enabled for Clang by default. If the output is not a TTY, *ccache* will ask the compiler to generate color, storing them in the cache, but stripping them from the output. There remains some issue in unifying [-fdiagnostics-color](https://github.com/ccache/ccache/issues/224).

## Misc

### Sloppiness

*ccache* by default use a very conservative comparison that minimizes both false positives and, for some projects, true positives. Some of the comparisions are deemed useless and can be changed:

```
 $ ccache --set-config=sloppiness=file_macro,locale,time_macros

```

This tells *ccache* to ignore the `__FILE__` and time-related macros, which usually invalidate the cache and are considered harmful in reproducible builds anyways. Locale differences are also ignored; *ccache* cares about it mainly because it determines the language of diagnostic messages.

The `CCACHE_SLOPPINESS` environment variable can be exported to override any pre-existing sloppiness settings.

*ccache* also by default caches the current directory being used for each build, which means cache misses for build pipelines that use a new, random temporary directory each time it's called. See the [Compiling in different directories](https://ccache.dev/manual/latest.html#_compiling_in_different_directories) section of the *ccache* manual.

### Change the cache directory

You may want to move the cache directory to a faster location than the default `~/.ccache` directory, like an SSD or a [ramdisk](/index.php/Ramdisk "Ramdisk").

To change the cache location only in the current shell:

```
$ export CCACHE_DIR=/ramdisk/ccache

```

Or to change the location by default:

 `/home/*user*/.ccache/ccache.conf`  `cache_dir = /ramdisk/ccache` 

### Set maximum cache size

The default value is 5 gigabyte, however it is possible to use a lower or even a higher value:

```
$ ccache --set-config=max_size=2.0G

```

### Disable the cache via environment

If you wish to disable *ccache* only in the current shell:

```
$ export CCACHE_DISABLE=1

```

### CLI

You can use the command-line utility *ccache* to show a statistics summary:

```
$ ccache -s

```

or clear the cache completely:

```
$ ccache -C

```

### makechrootpkg

It is also possible to use *ccache* with *makechrootpkg* from [devtools](https://www.archlinux.org/packages/?name=devtools) package. To retain the cache when the chroot is cleaned the *makechrootpkg* option `-d` can be used to bind the cache directory from the regular system into the chroot, eg.:

```
$ mkdir /path/of/chroot/ccache
$ makechrootpkg -d /path/to/cache/:/ccache -r /path/of/chroot -- CCACHE_DIR=/ccache

```

Then *ccache* can be configured for the chroot in the same way as explained above for the regular system.

## Caveat

*ccache* is effective **only** when compiling **exactly identical** sources. (More exactly, preprocessed sources.)

In the Gentoo Linux community, a source based distro, *ccache* has been notorious for its placebo effect, compilation failure (due to undesirable leftover objects), etc. Gentoo requires to turn off *ccache* before reporting compilation failure. See the [*ccache* section](https://wiki.gentoo.org/wiki/Handbook:Parts/Working/Features#Caching_compilation_objects) in Gentoo Linux Handbook, and [the blog post](https://flameeyes.blog/2008/06/21/debunking-ccache-myths/) titled "Debunking ccache myths" by Diego Pettenò, an ex-Gentoo developer.

## See also

*   [ccache manual](https://ccache.dev/manual/latest.html)