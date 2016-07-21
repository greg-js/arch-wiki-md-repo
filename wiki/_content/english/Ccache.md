[ccache](http://ccache.samba.org/) is a tool for the gcc compiler used to compile the same program over and over again with little downtime. While it may take a few seconds longer to compile a program the first time with `ccache`, subsequent compiles will be much, much faster.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Enable ccache for makepkg](#Enable_ccache_for_makepkg)
    *   [2.2 Enable for command line](#Enable_for_command_line)
    *   [2.3 Enable with colorgcc](#Enable_with_colorgcc)
*   [3 Misc](#Misc)
    *   [3.1 Change the cache directory](#Change_the_cache_directory)
    *   [3.2 Disable the cache via environment](#Disable_the_cache_via_environment)
    *   [3.3 CLI](#CLI)
    *   [3.4 makechrootpkg](#makechrootpkg)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [ccache](https://www.archlinux.org/packages/?name=ccache) package.

## Configuration

### Enable ccache for makepkg

To enable ccache when using [makepkg](/index.php/Makepkg "Makepkg") edit `/etc/makepkg.conf`. In `BUILDENV` uncomment `ccache` (remove the exclamation mark) to enable caching. For example:

 `/etc/makepkg.conf`  `BUILDENV=(fakeroot !distcc color **ccache** check !sign)` 

### Enable for command line

If you are compiling your code from the command line, and not building packages, then you will still want to use `ccache` to help speed things up.

For that, you need to change your `$PATH` to include `ccache`'s binaries before the path to your compiler:

```
$ export PATH="/usr/lib/ccache/bin/:$PATH"

```

You may want to add this line to your `~/.bashrc` file for regular usage.

### Enable with colorgcc

Since colorgcc is also a compiler wrapper, some care needs to be taken to ensure each wrapper is called in the correct sequence.

```
export PATH="/usr/lib/colorgcc/bin/:$PATH"    # As per usual colorgcc installation, leave unchanged (don't add ccache)
export CCACHE_PATH="/usr/bin"                 # Tell ccache to only use compilers here

```

Then colorgcc needs to be told to call ccache instead of the real compiler. Edit `/etc/colorgcc/colorgccrc` and change the `/usr/bin` paths to `/usr/lib/ccache/bin` for all the compilers in `/usr/lib/ccache/bin`:

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

## Misc

### Change the cache directory

You may want to move the cache directory to a faster location than the default `~/.ccache` directory, like an SSD or a [ramdisk](/index.php/Ramdisk "Ramdisk").

To change the cache location:

```
$ export CCACHE_DIR=/ramdisk/ccache

```

### Disable the cache via environment

If you wish to disable CCache only in the current shell you can set:

```
$ export CCACHE_DISABLE=1

```

### CLI

You can use the command-line utility `ccache` to show a statistics summary:

```
$ ccache -s

```

or clear the cache completely:

```
$ ccache -C

```

### makechrootpkg

It is also possible to use ccache with makechrootpkg. To retain the cache when the chroot is cleaned the makechrootpkg option `-d` can be used to bind the cache directory from the regular system into the chroot, eg.:

```
$ mkdir /path/of/chroot/ccache
$ makechrootpkg -d /path/to/cache/:/ccache -r /path/of/chroot -- CCACHE_DIR=/ccache

```

Then ccache can be configured for the chroot in the same way as explained above for the regular system.

## See also

*   [ccache manual](http://ccache.samba.org/manual.html)