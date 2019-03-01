From [Wikipedia:D (programming language)](https://en.wikipedia.org/wiki/D_(programming_language) "wikipedia:D (programming language)"):

	"The D programming language, also known simply as D, is an object-oriented, imperative, multi-paradigm system programming language by Walter Bright of Digital Mars. It originated as a re-engineering of C++, but even though it is predominantly influenced by that language, it is not a variant of it. D has redesigned some C++ features and has been influenced by concepts used in other programming languages, such as Java, C#, and Eiffel".

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Testing the installation](#Testing_the_installation)
*   [3 Considerations](#Considerations)
*   [4 Useful libraries and bindings](#Useful_libraries_and_bindings)
*   [5 See also](#See_also)

## Installation

To program in D you will need two things - a D compiler and a library. Easiest way to get started fast is to install [dlang-dmd](https://www.archlinux.org/groups/x86_64/dlang-dmd/) package group. It will provide the official compiler ([dmd](https://www.archlinux.org/packages/?name=dmd)), the standard library [libphobos](https://www.archlinux.org/packages/?name=libphobos) and [dtools](https://www.archlinux.org/packages/?name=dtools), a collection of small development tools.

## Testing the installation

To make sure that everything is installed and set up correctly, a simple Hello World program should suffice.

```
import std.stdio;

void main() {
   string yourName = "archer";
   writefln("Hello %s!", yourName);
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

There are however possible choices regarding the compiler you choose. The standard (reference one) is dmd, but [gdc](https://www.archlinux.org/packages/?name=gdc) (GNU D Compiler) and [ldc](https://www.archlinux.org/packages/?name=ldc) (LLVM D Compiler) are also popular. Those are also in [community].

As of April 2017 [dmd's backend is now FOSS](https://github.com/dlang/dmd/pull/6680) (Boost-licensed). All 3 compilers share same front-end code and thus have almost identical support for language features (assuming same front-end version).

## Useful libraries and bindings

*   [DDT](https://code.google.com/p/ddt/) - Eclipse plugin for project and code management in D
*   [Mono-D](http://mono-d.alexanderbothe.com/) - [MonoDevelop](http://monodevelop.com/) addin for programming in D
*   [QtD](https://bitbucket.org/qtd/repo) - Qt bindings for D
*   [GtkD](http://gtkd.org/) - An object oriented GTK+ wrapper for D
*   [Derelict](https://github.com/aldacron/Derelict3) - Bindings for multimedia libraries, focused toward game development
*   [Deimos](https://github.com/D-Programming-Deimos) - A project that houses a lot of bindings to different C libraries

## See also

*   [Phobos GitHub repository](https://github.com/D-Programming-Language/phobos/)
*   [The D Programming Language](http://dlang.org/) - The official home of D
*   [Planet D](http://planet.dsource.org/) - A collection of blogs about D