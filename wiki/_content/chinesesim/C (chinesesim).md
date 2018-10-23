**翻译状态：** 本文是英文页面 [C](/index.php/C "C") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-10-22，点击[这里](https://wiki.archlinux.org/index.php?title=C&diff=0&oldid=549459)可以查看翻译后英文页面的改动。

[Kernels (简体中文)](/index.php/Kernels_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernels (简体中文)") 内核和 [GNU (简体中文)](/index.php/GNU_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNU (简体中文)") 用户空间主要由 [C](https://en.wikipedia.org/wiki/C_(programming_language) "wikipedia:C (programming language)")写成.

Arch Linux使用[GNU C Library](https://en.wikipedia.org/wiki/GNU_C_Library "wikipedia:GNU C Library") ([glibc](https://www.archlinux.org/packages/?name=glibc)) 作为C标准库; 它是 [base group](/index.php/Base_group "Base group")的一部分.

你可以使用 [GNU toolchain](/index.php/GNU_toolchain "GNU toolchain") 或者 [LLVM toolchain](/index.php/LLVM_toolchain "LLVM toolchain") 来用 C/[C++](https://en.wikipedia.org/wiki/C%2B%2B "wikipedia:C++")/[Objective-C](https://en.wikipedia.org/wiki/Objective-C "wikipedia:Objective-C")开发软件.

## Contents

*   [1 有用的工具](#.E6.9C.89.E7.94.A8.E7.9A.84.E5.B7.A5.E5.85.B7)
    *   [1.1 静态代码分析](#.E9.9D.99.E6.80.81.E4.BB.A3.E7.A0.81.E5.88.86.E6.9E.90)
*   [2 可选编译器](#.E5.8F.AF.E9.80.89.E7.BC.96.E8.AF.91.E5.99.A8)
*   [3 libc实现的替代品](#libc.E5.AE.9E.E7.8E.B0.E7.9A.84.E6.9B.BF.E4.BB.A3.E5.93.81)
*   [4 库](#.E5.BA.93)
*   [5 参阅](#.E5.8F.82.E9.98.85)

## 有用的工具

*   **[Valgrind](https://en.wikipedia.org/wiki/Valgrind "wikipedia:Valgrind")** — 用来找到程序里内存管理问题的工具.

	[http://valgrind.org/](http://valgrind.org/) || [valgrind](https://www.archlinux.org/packages/?name=valgrind)

*   **[Distcc (简体中文)](/index.php/Distcc_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Distcc (简体中文)")** — 分布式编译的GCC前端.

	[https://github.com/distcc/distcc](https://github.com/distcc/distcc) || [distcc](https://www.archlinux.org/packages/?name=distcc)

*   **rr** — 针对C/C++的轻量的记录和定性调试工具，用的是[GDB](/index.php/GDB "GDB").

	[https://rr-project.org/](https://rr-project.org/) || [rr](https://aur.archlinux.org/packages/rr/)

### 静态代码分析

*   **[Cppcheck](https://en.wikipedia.org/wiki/Cppcheck "wikipedia:Cppcheck")** — 静态C/C++代码分析工具.

	[http://cppcheck.sourceforge.net/](http://cppcheck.sourceforge.net/) || [cppcheck](https://www.archlinux.org/packages/?name=cppcheck)

*   **[Splint](https://en.wikipedia.org/wiki/Splint_(programming_tool) "wikipedia:Splint (programming tool)")** — 静态检查C程序安全问题和代码错误的工具.

	[http://repo.or.cz/splint-patched.git](http://repo.or.cz/splint-patched.git) || [splint](https://www.archlinux.org/packages/?name=splint)

*   [Clang (简体中文)](/index.php/Clang_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Clang (简体中文)") 有 *扫描-构建* 的静态分析器.

## 可选编译器

*   **[TCC](https://en.wikipedia.org/wiki/Tiny_C_Compiler "wikipedia:Tiny C Compiler")** — 微型的C编译器，声称比GCC快.

	[https://bellard.org/tcc/](https://bellard.org/tcc/) || [tcc](https://www.archlinux.org/packages/?name=tcc)

*   **[ACK](https://en.wikipedia.org/wiki/Amsterdam_Compiler_Kit "wikipedia:Amsterdam Compiler Kit")** — 阿姆斯特丹编译包.

	[http://tack.sourceforge.net/](http://tack.sourceforge.net/) || [ack-git](https://aur.archlinux.org/packages/ack-git/)

*   **[PCC](https://en.wikipedia.org/wiki/Portable_C_Compiler "wikipedia:Portable C Compiler")** — 可移植的C编译器.

	[http://pcc.ludd.ltu.se/](http://pcc.ludd.ltu.se/) || [pcc](https://aur.archlinux.org/packages/pcc/)

*   **[SDCC](https://en.wikipedia.org/wiki/Small_Device_C_Compiler "wikipedia:Small Device C Compiler")** — 可重定向的 ANSI C 编译器.

	[http://sdcc.sourceforge.net/](http://sdcc.sourceforge.net/) || [sdcc](https://www.archlinux.org/packages/?name=sdcc)

查阅 [Wikipedia:List of compilers#C compilers](https://en.wikipedia.org/wiki/List_of_compilers#C_compilers "wikipedia:List of compilers").

## libc实现的替代品

*   **[musl](https://en.wikipedia.org/wiki/musl "wikipedia:musl")** — C标准库的轻量实现.

	[http://www.musl-libc.org/](http://www.musl-libc.org/) || [musl](https://www.archlinux.org/packages/?name=musl)

## 库

*   **[GLib](https://en.wikipedia.org/wiki/GLib "wikipedia:GLib")** — [GNOME](/index.php/GNOME "GNOME")的底层库, 包括 [GObject](https://en.wikipedia.org/wiki/GObject "wikipedia:GObject") 和[GIO](https://en.wikipedia.org/wiki/GIO "wikipedia:GIO").

	[https://wiki.gnome.org/Projects/GLib](https://wiki.gnome.org/Projects/GLib) || [glib](https://aur.archlinux.org/packages/glib/)

*   [GStreamer (简体中文)](/index.php/GStreamer_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GStreamer (简体中文)") – 基于管道线的多媒体框架

参阅:

*   [GTK+/Development#C](/index.php/GTK%2B/Development#C "GTK+/Development")
*   [Desktop notifications#C](/index.php/Desktop_notifications#C "Desktop notifications")
*   [Libcanberra#C](/index.php/Libcanberra#C "Libcanberra")
*   [Archiving and compression#Compression libraries](/index.php/Archiving_and_compression#Compression_libraries "Archiving and compression")
*   [Wikipedia:Category:C libraries](https://en.wikipedia.org/wiki/Category:C_libraries "wikipedia:Category:C libraries")

## 参阅

*   [Man page (简体中文)](/index.php/Man_page_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Man page (简体中文)") 在第二区的系统调用
*   [Man page (简体中文)](/index.php/Man_page_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Man page (简体中文)") 在第三区的库函数
*   [GCC and Make – Compiling, Linking and Building C/C++ Applications](https://www3.ntu.edu.sg/home/ehchua/programming/cpp/gcc_make.html)
*   [SEI CERT C Coding Standard](https://wiki.sei.cmu.edu/confluence/display/c/SEI+CERT+C+Coding+Standard)
*   [##C IRC channel on Freenode](http://iso-9899.info/)