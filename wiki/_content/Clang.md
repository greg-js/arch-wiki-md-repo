# Clang

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[Clang](http://clang.llvm.org/) is a C/C++/Objective C compiler based on LLVM. It is distributed under the BSD Licence.

## Contents

*   [1 Installation](#Installation)
*   [2 Build packages with Clang](#Build_packages_with_Clang)
*   [3 Using the Static Analyzer](#Using_the_Static_Analyzer)
*   [4 References](#References)

## Installation

Install [clang](https://www.archlinux.org/packages/?name=clang) from the [Official repositories](/index.php/Official_repositories "Official repositories").

## Build packages with Clang

Add `export CC=clang` and (for C++) `export CXX=clang++` to your `/etc/makepkg.conf`.

NB: For packages that specify GCC-specific build options, there may be build errors that require either editing the source package, the pkgbuild or commenting out the clang lines in makepkg.conf.

## Using the Static Analyzer

First install the [clang-analyzer](https://www.archlinux.org/packages/?name=clang-analyzer) package. To analyze a project, simply place the word `scan-build` in front of your build command. For example:

```
$ scan-build make

```

**Tip:** If your project is already compiled, `scan-build` won't rebuild and won't analyse it. To force recompilation and analysis, use `-B` switch: `$ scan-build make -B` 

It is also possible to analyze specific files:

```
$ scan-build gcc -c t1.c t2.c

```

## References

*   [scan-build: running the analyzer from the command line](http://clang-analyzer.llvm.org/scan-build.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Clang&oldid=361634](https://wiki.archlinux.org/index.php?title=Clang&oldid=361634)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Package development](/index.php/Category:Package_development "Category:Package development")