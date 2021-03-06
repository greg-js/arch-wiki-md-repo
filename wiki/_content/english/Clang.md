[Clang](http://clang.llvm.org/) is a [C](/index.php/C "C")/C++/Objective C/[CUDA](/index.php/CUDA "CUDA") compiler based on [LLVM](/index.php/LLVM "LLVM"). The most recent iteration is distributed under the "Apache 2.0 License with LLVM exceptions".

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Build packages with Clang](#Build_packages_with_Clang)
*   [3 Using the Static Analyzer](#Using_the_Static_Analyzer)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [clang](https://www.archlinux.org/packages/?name=clang) package.

## Build packages with Clang

Add `export CC=clang` and (for C++) `export CXX=clang++` to your `/etc/makepkg.conf`. If you are building with `debug` also remove `-fvar-tracking-assignments` from `DEBUG_CFLAGS` and `DEBUG_CXXFLAGS` as clang does not support it.

NB: For packages that specify GCC-specific build options, there may be build errors that require either editing the source package, the pkgbuild or commenting out the clang lines in makepkg.conf.

## Using the Static Analyzer

To analyze a project, simply place the word `scan-build` in front of your build command. For example:

```
$ scan-build make

```

**Tip:** If your project is already compiled, `scan-build` won't rebuild and won't analyse it. To force recompilation and analysis, use `-B` switch: `$ scan-build make -B` 

It is also possible to analyze specific files:

```
$ scan-build gcc -c t1.c t2.c

```

## See also

*   [Wikipedia:Clang](https://en.wikipedia.org/wiki/Clang "wikipedia:Clang")
*   [scan-build: running the analyzer from the command line](http://clang-analyzer.llvm.org/scan-build.html)
*   [Compiling CUDA with clang](http://llvm.org/docs/CompileCudaWithLLVM.html)