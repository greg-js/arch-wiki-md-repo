From [Wikipedia:D (programming language)](https://en.wikipedia.org/wiki/D_(programming_language) "wikipedia:D (programming language)"):

	"The D programming language, also known simply as D, is an object-oriented, imperative, multi-paradigm system programming language by Walter Bright of Digital Mars. It originated as a re-engineering of C++, but even though it is predominantly influenced by that language, it is not a variant of it. D has redesigned some C++ features and has been influenced by concepts used in other programming languages, such as Java, C#, and Eiffel".

## Contents

*   [1 Installation](#Installation)
*   [2 Testing the installation](#Testing_the_installation)
*   [3 Considerations](#Considerations)
*   [4 hardening-wrapper](#hardening-wrapper)
*   [5 Useful libraries and bindings](#Useful_libraries_and_bindings)
*   [6 See Also](#See_Also)

## Installation

To program in D you will need two things - a D compiler and a library. Easiest way to get started fast is to install [dlang-dmd](https://www.archlinux.org/groups/x86_64/dlang-dmd/) package group. It will provide the official compiler ([dmd](https://www.archlinux.org/packages/?name=dmd)), the standard lbrary [libphobos](https://www.archlinux.org/packages/?name=libphobos) and [dtools](https://www.archlinux.org/packages/?name=dtools), a collection of small development tools.

## Testing the installation

To make sure that everything is installed and set up correctly, a simple Hello World program should suffice.

```
import std.stdio;

void main() {
   string yourName = "archer";
   writefln("Hello %s!", yourName);
}

```

Paste the code into a file, name it hello.d, and run

```
$ dmd hello.d

```

in the same directory as the file. You should then be able to execute the program with:

```
$ ./hello

```

You can also execute

```
$ dmd -run hello.d

```

which will simply compile and run without leaving any object files in the directory.

## Considerations

There are however possible choices regarding the compiler you choose. The standard (reference one) is dmd, but [gdc](https://aur.archlinux.org/packages/gdc/) (GNU D Compiler) and [ldc](https://www.archlinux.org/packages/?name=ldc) (LLVM D Compiler) are also popular. Those are also in [community].

As of April 2017 [dmd's backend is now FOSS](https://github.com/dlang/dmd/pull/6680) (Boost-licensed). All 3 compilers share same front-end code and thus have almost identical support for language features (assuming same front-end version).

## hardening-wrapper

In Arch Linux [dmd](https://www.archlinux.org/packages/?name=dmd) and [libphobos](https://www.archlinux.org/packages/?name=libphobos) packages are built without PIC support. Using [hardening-wrapper](https://www.archlinux.org/packages/?name=hardening-wrapper) forces building executables with PIC support which results in:

```
dmd app.d
/usr/bin/ld: app.o: relocation R_X86_64_32 against  `__dmd_personality_v0' can not be used when making a shared object;  recompile with -fPIC
app.o: error adding symbols: Bad value
collect2: error: ld returned 1 exit status
--- errorlevel 1

```

There are few possible workarounds:

*   uninstall [hardening-wrapper](https://www.archlinux.org/packages/?name=hardening-wrapper)
*   use [gdc](https://aur.archlinux.org/packages/gdc/) compiler which is compiled with PIC support

```
gdc app.d 

```

or for [dub](https://aur.archlinux.org/packages/dub/)

```
dub --compiler=gdc

```

*   recompile [dmd](https://www.archlinux.org/packages/?name=dmd) and [libphobos](https://www.archlinux.org/packages/?name=libphobos) with -fPIC flags using [abs](/index.php/Abs "Abs") or manually
*   use clang linker

```
CC=/usr/bin/clang dmd app.d

```

if using dub

```
CC=/usr/bin/clang dub

```

more information

*   [https://issues.dlang.org/show_bug.cgi?id=15054](https://issues.dlang.org/show_bug.cgi?id=15054)
*   [FS#34983](https://bugs.archlinux.org/task/34983)
*   [FS#46260](https://bugs.archlinux.org/task/46260)
*   [http://wiki.dlang.org/Installing_LDC_on_Gentoo#Hardened_Gentoo](http://wiki.dlang.org/Installing_LDC_on_Gentoo#Hardened_Gentoo)

## Useful libraries and bindings

*   [DDT](https://code.google.com/p/ddt/) - Eclipse plugin for project and code management in D
*   [Mono-D](http://mono-d.alexanderbothe.com/) - [MonoDevelop](http://monodevelop.com/) addin for programming in D
*   [QtD](https://bitbucket.org/qtd/repo) - Qt bindings for D
*   [GtkD](http://gtkd.org/) - An object oriented GTK+ wrapper for D
*   [Derelict](https://github.com/aldacron/Derelict3) - Bindings for multimedia libraries, focused toward game development
*   [Deimos](https://github.com/D-Programming-Deimos) - A project that houses a lot of bindings to different C libraries

## See Also

*   [Phobos source on github](https://github.com/D-Programming-Language/phobos/) - The official Phobos repo
*   [The D Programming Language](http://dlang.org/) - The official home of D
*   [Planet D](http://planet.dsource.org/) - A collection of blogs about D