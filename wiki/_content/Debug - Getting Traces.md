# Debug - Getting Traces

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [General troubleshooting](/index.php/General_troubleshooting "General troubleshooting")
*   [Reporting bug guidelines](/index.php/Reporting_bug_guidelines "Reporting bug guidelines")
*   [Step-by-step debugging guide](/index.php/Step-by-step_debugging_guide "Step-by-step debugging guide")

This article aims to help in creating a debugging Arch package and using it to provide trace and debug information for reporting software bugs to developers.

## Contents

*   [1 Package names](#Package_names)
*   [2 PKGBUILD](#PKGBUILD)
*   [3 Compilation settings](#Compilation_settings)
    *   [3.1 General](#General)
    *   [3.2 Qt4](#Qt4)
    *   [3.3 Qt5](#Qt5)
    *   [3.4 CMAKE (KDE) applications](#CMAKE_.28KDE.29_applications)
*   [4 Building and installing the package](#Building_and_installing_the_package)
*   [5 Getting the trace](#Getting_the_trace)
*   [6 Conclusion](#Conclusion)
*   [7 See also](#See_also)

## Package names

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** "call the function", "stack trace", gdb is only mentioned later in the article -> unclear introduction (Discuss in [Talk:Debug - Getting Traces#](https://wiki.archlinux.org/index.php/Talk:Debug_-_Getting_Traces))

When looking at debug messages, such as:

```
[...]
Backtrace was generated from '/usr/bin/epiphany'

**(no debugging symbols found)**
Using host libthread_db library "/lib/libthread_db.so.1".
**(no debugging symbols found)**
[Thread debugging using libthread_db enabled]
[New Thread -1241265952 (LWP 12630)]
(no debugging symbols found)
0xb7f25410 in __kernel_vsyscall ()
#0  0xb7f25410 in __kernel_vsyscall ()
#1  0xb741b45b in **??** () from /lib/libpthread.so.0
[...]

```

`??` shows where debugging info is missing, as well as the name of library or executable which called the function. Similarly, when `(no debugging symbols found)` appears, you should look for the stated file names. For example, with [pacman](/index.php/Pacman "Pacman"):

```
# pacman -Qo /lib/libthread_db.so.1
/lib/libthread_db.so.1 is owned by _glibc_ 2.5-8

```

The package is called [glibc](https://www.archlinux.org/packages/?name=glibc) in version 2.5-8\. Repeat this step for every package that needs debugging.

## PKGBUILD

In order to build a package from source, the PKGBUILD file is required. See [ABS](/index.php/ABS "ABS") for packages in the [official repositories](/index.php/Official_repositories "Official repositories"), and [AUR#Acquire build files](/index.php/AUR#Acquire_build_files "AUR") for packages in the [AUR](/index.php/AUR "AUR").

## Compilation settings

At this stage, you can modify the global configuration file of `makepkg` if you will be using it only for debug purposes. In other cases, you should modify package's PKGBUILD file only for each package you would like to rebuild.

### General

As of pacman 4.1, `/etc/makepkg.conf` has debug compilation flags in `DEBUG_CFLAGS` and `DEBUG_CXXFLAGS`. To use them, enable the `debug` makepkg option, and disable `strip`.

```
OPTIONS+=(debug !strip)

```

These settings will force compilation with debugging information and will disable the stripping of debug symbols from executables. To apply this setting to a single package, modify the PKGBUILD:

```
options=(debug !strip)

```

Alternatively you can put the debug information in a separate package by enabling both `debug` and `strip`, debugging information will then be stripped from the main package and placed in a separate `_foo_-debug` package.

**Note:** It is insufficient to simply install the newly compiled debug package, because the debugger will check that the file containing the debug symbols is from the same build as the associated library and executable. You must install both of the recompiled packages. In Arch, the debug symbols files are installed under `/usr/lib/debug`. See the [GDB documentation](https://sourceware.org/gdb/onlinedocs/gdb/Separate-Debug-Files.html) for more information about debug packages.

Note that certain packages such as _glibc_ are stripped regardless. Check the PKGBUILD for sections such as:

```
strip $STRIP_BINARIES usr/bin/{gencat,getconf,getent,iconv,iconvconfig} \
                      usr/bin/{ldconfig,locale,localedef,nscd,makedb} \
                      usr/bin/{pcprofiledump,pldd,rpcgen,sln,sprof} \
                      usr/lib/getconf/*
[[ $CARCH = "i686" ]] && strip $STRIP_BINARIES usr/bin/lddlibc4

strip $STRIP_STATIC usr/lib/*.a

strip $STRIP_SHARED usr/lib/{libanl,libBrokenLocale,libcidn,libcrypt}-*.so \
                    usr/lib/libnss_{compat,db,dns,files,hesiod,nis,nisplus}-*.so \
                    usr/lib/{libdl,libm,libnsl,libresolv,librt,libutil}-*.so \
                    usr/lib/{libmemusage,libpcprofile,libSegFault}.so \
                    usr/lib/{audit,gconv}/*.so

```

And remove them where appropriate.

### Qt4

In addition to the previous general settings, pass `-developer-build` option to the `configure` script in the `PKGBUILD`. By default, `-developer-build` passes `-Werror` to the compiler, which may cause the compilation to fail. To avoid compilation errors, you may need pass `-no-warnings-are-errors`, too.

### Qt5

The [qt-debug](/index.php/Unofficial_user_repositories#qt-debug "Unofficial user repositories") repository contains pre-built Qt/PyQt packages with debug symbols. See also [upstream](http://doc.qt.io/qt-5/debug.html) instructions.

### CMAKE (KDE) applications

[KDE](/index.php/KDE "KDE") and related programs typically use [cmake](https://www.archlinux.org/packages/?name=cmake). To enable debug information and disable optimisations, change `-DCMAKE_BUILD_TYPE` to `Debug`. To enable debug information while keeping optimisations enabled, change `-DCMAKE_BUILD_TYPE` to `RelWithDebInfo`.

## Building and installing the package

Build the package from source using `makepkg` while in the PKGBUILD's directory. This could take some time:

```
# makepkg

```

Then install the built package:

```
# pacman -U glibc-2.5-8-i686.pkg.tar.gz

```

## Getting the trace

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Mention core dumps (Discuss in [Talk:Debug - Getting Traces#](https://wiki.archlinux.org/index.php/Talk:Debug_-_Getting_Traces))

The actual backtrace (or stack trace) can now be obtained via e.g. [gdb](https://www.archlinux.org/packages/?name=gdb), the GNU Debugger. Run it either via:

```
# gdb /path/to/file

```

or:

```
# gdb
(gdb) exec /path/to/file

```

The path is optional, if already set in the `$PATH` variable.

Then, within `gdb`, type `run` followed by any arguments you wish the program to start with, e.g.:

```
(gdb) run --no-daemon --verbose

```

to start execution of the file. Do whatever necessary to evoke the bug. For the actual log, type the lines:

```
(gdb) set logging file trace.log
(gdb) set logging on

```

and then:

```
(gdb) thread apply all bt full

```

to output the trace to `trace.log` into the directory `gdb` was started in. To exit, enter:

```
(gdb) set logging off
(gdb) quit

```

**Tip:** To debug an application written in python:

```
# gdb /usr/bin/python
(gdb) run <python application>

```

You can also debug an already running application, e.g.:

```
 # gdb --pid=$(pidof firefox)
 (gdb) continue

```

## Conclusion

Use the complete stack trace to inform developers of a bug you have discovered before. This will be highly appreciated by them and will help to improve your favorite program.

## See also

*   [Gentoo Wiki - Backtraces with Gentoo](https://wiki.gentoo.org/wiki/Project:Quality_Assurance/Backtraces)
*   [Fedora - StackTraces](http://fedoraproject.org/wiki/StackTraces)
*   [GNOME - Getting Stack Traces](https://wiki.gnome.org/Community/GettingInTouch/Bugzilla/GettingTraces/Details#obtain-a-stacktrace)
*   [gdb mini intro](http://linux.bytesex.org/gdb.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Debug_-_Getting_Traces&oldid=410383](https://wiki.archlinux.org/index.php?title=Debug_-_Getting_Traces&oldid=410383)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Package development](/index.php/Category:Package_development "Category:Package development")

Hidden categories:

*   [Pages or sections flagged with Template:Style](/index.php/Category:Pages_or_sections_flagged_with_Template:Style "Category:Pages or sections flagged with Template:Style")
*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")