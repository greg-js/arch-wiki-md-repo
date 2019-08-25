The [Linux](/index.php/Linux "Linux") kernel and the [GNU](/index.php/GNU "GNU") userland are written primarily in [C](https://en.wikipedia.org/wiki/C_(programming_language) "wikipedia:C (programming language)").

Arch Linux uses the [GNU C Library](https://en.wikipedia.org/wiki/GNU_C_Library "wikipedia:GNU C Library") ([glibc](https://www.archlinux.org/packages/?name=glibc)) as the C standard library; it is part of the [base group](/index.php/Base_group "Base group").

You can use the [GNU toolchain](/index.php/GNU_toolchain "GNU toolchain") or the [LLVM toolchain](/index.php/LLVM_toolchain "LLVM toolchain") to develop software in C, [C++](https://en.wikipedia.org/wiki/C%2B%2B "wikipedia:C++") or [Objective-C](https://en.wikipedia.org/wiki/Objective-C "wikipedia:Objective-C").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Useful tools](#Useful_tools)
    *   [1.1 Static code analyzers](#Static_code_analyzers)
*   [2 Alternative compilers](#Alternative_compilers)
*   [3 Alternative libc implementations](#Alternative_libc_implementations)
*   [4 Libraries](#Libraries)
*   [5 See also](#See_also)

## Useful tools

*   **[Valgrind](https://en.wikipedia.org/wiki/Valgrind "wikipedia:Valgrind")** — Tool to help find memory-management problems in programs.

	[http://valgrind.org/](http://valgrind.org/) || [valgrind](https://www.archlinux.org/packages/?name=valgrind)

*   **[distcc](/index.php/Distcc "Distcc")** — Distributed compiling GCC front-end.

	[https://github.com/distcc/distcc](https://github.com/distcc/distcc) || [distcc](https://www.archlinux.org/packages/?name=distcc)

*   **rr** — Lightweight recording and deterministic debugging tool for C/C++, uses [GDB](/index.php/GDB "GDB").

	[https://rr-project.org/](https://rr-project.org/) || [rr](https://aur.archlinux.org/packages/rr/)

### Static code analyzers

*   **[Cppcheck](https://en.wikipedia.org/wiki/Cppcheck "wikipedia:Cppcheck")** — A tool for static C/C++ code analysis.

	[http://cppcheck.sourceforge.net/](http://cppcheck.sourceforge.net/) || [cppcheck](https://www.archlinux.org/packages/?name=cppcheck)

*   **[Splint](https://en.wikipedia.org/wiki/Splint_(programming_tool) "wikipedia:Splint (programming tool)")** — A tool for statically checking C programs for security vulnerabilities and coding mistakes.

	[http://repo.or.cz/splint-patched.git](http://repo.or.cz/splint-patched.git) || [splint](https://www.archlinux.org/packages/?name=splint)

*   [Clang](/index.php/Clang "Clang") has the *scan-build* static analyzer.

## Alternative compilers

*   **[TCC](https://en.wikipedia.org/wiki/Tiny_C_Compiler "wikipedia:Tiny C Compiler")** — Tiny C Compiler, claims to be faster than GCC.

	[https://bellard.org/tcc/](https://bellard.org/tcc/) || [tcc](https://www.archlinux.org/packages/?name=tcc)

*   **[ACK](https://en.wikipedia.org/wiki/Amsterdam_Compiler_Kit "wikipedia:Amsterdam Compiler Kit")** — Amsterdam Compiler Kit.

	[http://tack.sourceforge.net/](http://tack.sourceforge.net/) || [ack-git](https://aur.archlinux.org/packages/ack-git/)

*   **[PCC](https://en.wikipedia.org/wiki/Portable_C_Compiler "wikipedia:Portable C Compiler")** — Portable C Compiler.

	[http://pcc.ludd.ltu.se/](http://pcc.ludd.ltu.se/) || [pcc](https://aur.archlinux.org/packages/pcc/)

*   **[SDCC](https://en.wikipedia.org/wiki/Small_Device_C_Compiler "wikipedia:Small Device C Compiler")** — Retargettable ANSI C compiler.

	[http://sdcc.sourceforge.net/](http://sdcc.sourceforge.net/) || [sdcc](https://www.archlinux.org/packages/?name=sdcc)

See also [Wikipedia:List of compilers#C compilers](https://en.wikipedia.org/wiki/List_of_compilers#C_compilers "wikipedia:List of compilers").

## Alternative libc implementations

*   **[dietlibc](https://en.wikipedia.org/wiki/dietlibc "wikipedia:dietlibc")** — a libc optimized for small size

	[https://www.fefe.de/dietlibc/](https://www.fefe.de/dietlibc/) || [dietlibc](https://www.archlinux.org/packages/?name=dietlibc)

*   **[musl](https://en.wikipedia.org/wiki/musl "wikipedia:musl")** — Lightweight implementation of C standard library.

	[http://www.musl-libc.org/](http://www.musl-libc.org/) || [musl](https://www.archlinux.org/packages/?name=musl)

## Libraries

*   [FFmpeg](/index.php/FFmpeg "FFmpeg") - includes libav, the audio and video library (not to be confused with the FFmpeg fork of the same name).
*   **[GLib](https://en.wikipedia.org/wiki/GLib "wikipedia:GLib")** — Low-level system library by [GNOME](/index.php/GNOME "GNOME"), includes [GObject](https://en.wikipedia.org/wiki/GObject "wikipedia:GObject") and [GIO](https://en.wikipedia.org/wiki/GIO "wikipedia:GIO").

	[https://wiki.gnome.org/Projects/GLib](https://wiki.gnome.org/Projects/GLib) || [glib2](https://www.archlinux.org/packages/?name=glib2)

*   [GStreamer](/index.php/GStreamer "GStreamer") – pipeline-based multimedia framework

See also:

*   [GTK/Development#C](/index.php/GTK/Development#C "GTK/Development")
*   [Desktop notifications#C](/index.php/Desktop_notifications#C "Desktop notifications")
*   [Libcanberra#C](/index.php/Libcanberra#C "Libcanberra")
*   [Archiving and compression#Compression libraries](/index.php/Archiving_and_compression#Compression_libraries "Archiving and compression")
*   [Wikipedia:Category:C libraries](https://en.wikipedia.org/wiki/Category:C_libraries "wikipedia:Category:C libraries")
*   [A list of open source C libraries](https://en.cppreference.com/w/c/links/libs)

## See also

*   [man pages](/index.php/Man_page "Man page") in section 2 for system calls
*   [man pages](/index.php/Man_page "Man page") in section 3 for library functions
*   [GCC and Make – Compiling, Linking and Building C/C++ Applications](https://www3.ntu.edu.sg/home/ehchua/programming/cpp/gcc_make.html)
*   [SEI CERT C Coding Standard](https://wiki.sei.cmu.edu/confluence/display/c/SEI+CERT+C+Coding+Standard)
*   [##C IRC channel on Freenode](http://iso-9899.info/)