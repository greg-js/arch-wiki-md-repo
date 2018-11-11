Related articles

*   [General troubleshooting](/index.php/General_troubleshooting "General troubleshooting")
*   [Reporting bug guidelines](/index.php/Reporting_bug_guidelines "Reporting bug guidelines")
*   [Debug - Getting Traces](/index.php/Debug_-_Getting_Traces "Debug - Getting Traces")
*   [Boot debugging](/index.php/Boot_debugging "Boot debugging")

This page is mainly about how to gather more information in connection with bug reports. Even though the word "debug" is used, it's not intended as a guide for how to debug programs while developing.

## Contents

*   [1 When an application fails](#When_an_application_fails)
    *   [1.1 Run it from the commandline](#Run_it_from_the_commandline)
    *   [1.2 Check availability of a core dump](#Check_availability_of_a_core_dump)
*   [2 Segmentation faults](#Segmentation_faults)
    *   [2.1 Gdb](#Gdb)
    *   [2.2 Improved gdb output](#Improved_gdb_output)
    *   [2.3 Valgrind](#Valgrind)
*   [3 Missing files or libraries](#Missing_files_or_libraries)
    *   [3.1 Strace](#Strace)
    *   [3.2 LD_DEBUG](#LD_DEBUG)
    *   [3.3 Readelf](#Readelf)
*   [4 If it is not written in C or C++, but perhaps in Python](#If_it_is_not_written_in_C_or_C.2B.2B.2C_but_perhaps_in_Python)
*   [5 Report the bug](#Report_the_bug)
*   [6 See also](#See_also)

## When an application fails

### Run it from the commandline

If an application suddenly crashes, try running it from a [terminal emulator](/index.php/Terminal_emulator "Terminal emulator"). Type in the name of the application in lowercase letters. If you do not know the name of the executable, only the name of the package, the following command can find the name of the executable. Replace *packagename* with the name of the package:

```
for f in $(pacman -Ql *packagename* | grep /bin/ | cut -d' ' -f2); do file $f 2>/dev/null | grep -q executable && basename $f; done

```

### Check availability of a core dump

A core dump is a file containing a process's address space (memory) when the process terminates unexpectedly. If the application is compiled in a debug-friendly way, the "core" file can be used to find out where things went wrong.

The location of core dumps may vary depending on the operating system configuration. See [core dump](/index.php/Core_dump "Core dump") to find whether generation of core dump files is enabled on your system and where do they go.

## Segmentation faults

There are several techniques that can be used to figure out what went wrong. Put your detective hat on.

### Gdb

[gdb](https://www.archlinux.org/packages/?name=gdb) is an ancient and well tested application for debugging applications. Replace *appname* with the name of your executable:

```
$ gdb appname
r
(wait for segfault)
bt full

```

Now post the output to a [Pastebin client](/index.php/List_of_applications#Pastebin_clients "List of applications") and include the URL in your bug report.

### Improved gdb output

First [recompile](/index.php/Arch_Build_System "Arch Build System") the application in question with the **-g**, **-O0** and **-fbuiltin** flags. Make sure "!strip" is in the options array in the PKGBUILD, then install the package and run it again with gdb, as above.

This is what the options line can look like:

```
 options=('!strip')

```

One way of enabling **-g**, **-O0** and **-fbuiltin** is to put these two lines at the very beginning of the build() function in the relevant PKGBUILD:

```
export CFLAGS="$CFLAGS -O0 -fbuiltin -g"
export CXXFLAGS="$CXXFLAGS -O0 -fbuiltin -g"

```

The meaning of the flags is the following: **-g** enables debug symbols and **-O0** turns off optimizations. (**-O2** is the most common optimization level. ([**-O3** is usually overkill](http://funroll-loops.info/) and [**-O4** and above behaves exactly like **-O3**](http://stackoverflow.com/questions/1778538/how-many-gcc-optimization-levels-are-there)).

If you have a "core" file, it can be used together with gdb to get a backtrace:

```
$ gdb appname core
bt full

```

### Valgrind

Assuming you have an unstripped binary without inlined functions, it is usually a good idea to also run that program through [valgrind](https://www.archlinux.org/packages/?name=valgrind). *valgrind* is a tool that emulates a CPU and usually shows where things go wrong or provide additional info in addition to gdb.

```
$ valgrind appname

```

it will provide a lot of helpful debug output if there is a crash. Consider `-v` and `--leak-check=full` to get even more info.

Alternatively, use:

```
$ valgrind --tool=callgrind appname

```

and run the output through [kcachegrind](https://www.archlinux.org/packages/?name=kcachegrind) to graphically explore the functions the program uses. If a program hangs, this makes it easier to pinpoint the location of the error.

## Missing files or libraries

### Strace

[strace](https://www.archlinux.org/packages/?name=strace) finds out in detail what an application is actually doing. If an application tries to open a file that is not there, it can be discovered by strace.

For finding which files a program named *appname* tries to open:

```
$ strace -eopen appname

```

Save the output, post it to a [Pastebin client](/index.php/List_of_applications#Pastebin_clients "List of applications") and keep the URL in handy.

**Tip:** If you wish to grep the output from strace, you can try:

`strace -o /dev/stdout appname | grep *string*`

### LD_DEBUG

Setting `LD_DEBUG=files` gives another overview of what files an application is looking for. For an application named *appname*:

```
LD_DEBUG=files appname > appname.log 2>&1

```

The output will end up in `appname.log`.

For more information, see [ld-linux(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ld-linux.8).

### Readelf

If you get "no such file or directory" when running an application, try the following command:

```
$ readelf -a /usr/bin/appname | grep interp

```

(replace /usr/bin/appname with the location of your executable)

Make sure the interpreter in question (like /lib/ld-linux-x86-64.so.2) actually exists. Install [ld-lsb](https://www.archlinux.org/packages/?name=ld-lsb) from the [AUR](/index.php/AUR "AUR") if need be.

## If it is not written in C or C++, but perhaps in Python

Use [file](https://www.archlinux.org/packages/?name=file) on the executable to get more information (replace "appname" with your executable):

```
$ file /usr/bin/*appname*

```

If it says "ELF" it is a binary executable and is usually written in C or C++. If it says "Python script" you know you are dealing with an application written in Python.

If it is a shell script, open up the shell script in a text editor and see (usually at the bottom of the file) if you can find the name of the real application (ELF file). You can then temporarily put "gdb" right in the shellscript, before the name of the executable, for debugging purposes. See the sections about gdb further up. Prefix the command with `gdb --args` if the executable in question needs arguments as well.

For pure shell scripts, you can also use `bash -x *script_name*` or `bash -xv *script_name*`.

For Python applications, the output will often say which file and line number the crash occured at. If you are proficient with Python, you can try to fix this and include the fix in the bug report.

## Report the bug

Please report a bug at [https://bugs.archlinux.org](https://bugs.archlinux.org) and possibly also directly to the developers of the application in question, then include a link in the Arch Linux bug report. This helps us all.

However, if you think there is something wrong with the application itself, and not with how it is packaged, report the bug directly to upstream (which means the developers of the application). Normally, software streams from developers, through packagers/maintainers and down to users. Upstream means the other way, so for this case: directly to the developers of an application.

## See also

*   [Gentoo guide for getting useful backtraces](https://wiki.gentoo.org/wiki/Project:Quality_Assurance/Backtraces)