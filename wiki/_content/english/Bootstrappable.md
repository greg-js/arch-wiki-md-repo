[Bootstrappable Builds](http://bootstrappable.org/) allows us to bootstrap Arch Linux easily from scratch using a minimal set of binaries. Allowing a minimal set of binaries to be audited and together with reproducible builds provide confidence that you are running the code which you expect to run.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Bootstrapping Arch Linux](#Bootstrapping_Arch_Linux)
*   [2 Bootstrapping Languages](#Bootstrapping_Languages)
    *   [2.1 Rust](#Rust)
    *   [2.2 Java (openjdk)](#Java_(openjdk))

## Bootstrapping Arch Linux

[Mes](https://www.gnu.org/software/mes/) is a project which can be utilised to bootstrap Arch Linux from a minimal set of (32bit) binaries having the rest of the system compiled from source code. For Arch Linux we can start bootstrapping a C compiler from mes and later reduce the initial bootstrap binaries to a minimal auditable amount.

The roadmap to bootstrapping GCC:

*   Bring Mes into the repository
*   Compile Mes with Mes (and compare it with other distributions Debian, Guix, NixOS)

```
 MES=mes AR=mesar CC=mescc ./configure.sh --host=i686-unknown-linux-gnu
 V=2 MES=mes AR=mesar GUILE_LOAD_PATH=/usr/share/mes/module/ ./bootstrap.sh

```

*   Compile a [patched tcc-boot0](https://gitlab.com/janneke/tinycc/tree/mes-0.21)
*   Compile a tcc-boot with a tiny [patch](http://git.savannah.gnu.org/cgit/guix.git/tree/gnu/packages/patches/tcc-boot-0.9.27.patch)
*   System utilities
*   GCC-2.95.3

More information: [http://git.savannah.gnu.org/cgit/guix.git/tree/gnu/packages/commencement.scm](http://git.savannah.gnu.org/cgit/guix.git/tree/gnu/packages/commencement.scm) [http://guix.gnu.org/blog/2019/guix-reduces-bootstrap-seed-by-50/](http://guix.gnu.org/blog/2019/guix-reduces-bootstrap-seed-by-50/)

## Bootstrapping Languages

For languages which are self-hoisting (require itself to build a new version) we want a path from a C compiler to for example Rust.

### Rust

There is a Rust C++ implementation which can compile Rust 1.19.0 called [mrustc](https://github.com/thepowersgang/mrustc). Guix has more information in this [blog post](http://guix.gnu.org/blog/2018/bootstrapping-rust/).

### Java (openjdk)

A path to bootstrapping JDK is described [here](http://bootstrappable.org/projects/java.html)