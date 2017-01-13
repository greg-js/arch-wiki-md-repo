From [Wikipedia](https://en.wikipedia.org/wiki/Rust_(programming_language) "wikipedia:Rust (programming language)"):

	*[Rust](http://rust-lang.org/) is a general-purpose, multi-paradigm, compiled programming language sponsored by Mozilla Research. It is designed to be a "safe, concurrent, practical language", supporting pure-functional, imperative-procedural, and object-oriented styles.*

	*The goal of Rust is to be a good language for creating highly concurrent and highly safe systems, and programming in the large. This has led to a feature set with an emphasis on safety, control of memory layout, and concurrency. Performance of idiomatic Rust is comparable to the performance of idiomatic C++.*

## Contents

*   [1 Rust Core Library](#Rust_Core_Library)
*   [2 Rust Standard Library](#Rust_Standard_Library)
*   [3 Release Cycle](#Release_Cycle)
*   [4 Installation](#Installation)
    *   [4.1 Native Installation](#Native_Installation)
    *   [4.2 Official Rustup Installation](#Official_Rustup_Installation)
    *   [4.3 Test your installation](#Test_your_installation)
*   [5 Cross Compiling](#Cross_Compiling)
    *   [5.1 Using rustup](#Using_rustup)
    *   [5.2 Windows](#Windows)
    *   [5.3 unofficial packages](#unofficial_packages)
*   [6 Cargo](#Cargo)
    *   [6.1 Usage](#Usage)
*   [7 IDE Support](#IDE_Support)
    *   [7.1 Tools](#Tools)
        *   [7.1.1 Racer](#Racer)
        *   [7.1.2 Clippy](#Clippy)
    *   [7.2 Editors](#Editors)
        *   [7.2.1 Atom](#Atom)
        *   [7.2.2 Visual Studio Code](#Visual_Studio_Code)
        *   [7.2.3 Vim](#Vim)
*   [8 See also](#See_also)

### Rust Core Library

The [Rust Core Library](https://doc.rust-lang.org/core/) is the dependency-free foundation of the Rust Standard Library. It interfaces directly with LLVM primitives, which allows Rust to be platform and hardware-agnostic. It is this integration with LLVM allows Rust to obtain greater performance than equivalent C applications compiled with Clang, making Rust software designed with libcore lower level than C. Developers looking to target software for embedded platforms may forego the standard library with `#[nostd]` to exclusively use the no-batteries-included core library for smaller binary sizes and improved performance. However, using `#[nostd]` limits the amount of software support that you can get from the larger Rust community as a majority of libraries require the standard library.

### Rust Standard Library

The [Rust Standard Library](http://doc.rust-lang.org/std/index.html) provides the convenient high level abstractions by which a majority of portable Rust software is created with. It features convenient features such as the `Vec`, `Iterator`, `Option`, `Result`, and `String` types; a vast amount of methods for language primitives; a large number of standard macros; I/O and multithreading support; heap allocations with `Box`; and many more high level features not available in the core library.

### Release Cycle

Rust follows a regular six week release cycle, similar to the release cycle of Firefox. With each new release, the core and standard libraries are improved to support more platforms, improve performance, and to stabilize new features for use with stable Rust.

## Installation

### Native Installation

To [install](/index.php/Install "Install") the latest stable version of Rust from the official Arch Linux software repository, [install](/index.php/Install "Install") the [rust](https://www.archlinux.org/packages/?name=rust) package. This will install the rustc compiler. You can choose to install the [cargo](https://www.archlinux.org/packages/?name=cargo) package as well.

### Official Rustup Installation

The official and recommended method of installing Rust for the purpose of developing software is to use the [Rustup toolchain manager](https://www.rustup.rs/), written in Rust.

The benefits to using the Rustup toolchain manager instead of the standalone prepackaged Rust in the software repository is the ability to install multiple toolchains (stable, beta, nightly) for multiple targets (windows, mac, android) and architectures (x86, x86_64, arm). It is also important to note that tools such as [Clippy](https://github.com/Manishearth/rust-clippy) require compiler plugin support, which is only supported in nightly builds of Rust.

One has 2 choices for a rustup installation, one is officially supported by Rust, while the other is supported by archlinux wiki

1.  Download the file with `curl -f https://sh.rustup.rs > rust.sh`, view it: `vim ./rust.sh`, and run the script `./rust.sh` to start rustup installation. To update rustup afterwards, run `rustup self update`.
2.  [rustup](https://www.archlinux.org/packages/?name=rustup) is also available on the Arch Linux software repository. Note that `rustup self update` will **not** work when installed this way, the package needs to be updated by pacman.

By default, only the stable channel from your architecture will be installed. It will however not be usable right away, you need to specify the installed stable channel as default for it to work.

**Note:** Please make sure that you have added the $HOME/.cargo/bin to your PATH before you run the rustup command.

```
$ rustup default stable

```

Then checking rust's version using `rustc -V` :

 `$ rustc -V ` 
```
rustc 1.9.0 (e4e8b6668 2016-05-18)

```

If you wish to install and use nightly, you can do like so :

```
$ rustup install nightly
$ rustup default nightly

```
 `$ rustc -V ` 
```
rustc 1.11.0-nightly (01411937f 2016-07-01)

```

Rust is now fired up for nightly !

### Test your installation

Check that Rust is installed correctly by building a simple program, as follows:

 `~/hello.rs` 
```
 fn main() {
     println!("Hello, World!");
 }

```

You can compile it with `rustc`, then run it:

 `$ rustc hello.rs && ./hello` 
```
Hello, World!

```

## Cross Compiling

### Using rustup

You can easily cross-compile using rustup. rustup supports many crosscompile targets. A full list can be found running `rustup target list`.

For instance, if you want to install rust using the stable channel for windows, using the gnu compiler, you will need to do :

```
$ rustup install stable-x86_64-pc-windows-gnu

```

This will only installs rust and its tools for your target architecture, but some additional tools might be needed for cross compiling.

### Windows

In this section, `$ARCH` is the target architecture (either `x86_64` or `i686`). It will explain how to cross compile using rustup.

1.  [Install](/index.php/Install "Install") [mingw-w64-gcc](https://www.archlinux.org/packages/?name=mingw-w64-gcc) and [wine](https://www.archlinux.org/packages/?name=wine)
2.  Add a binfmt definition for windows executables either manually or by installing [binfmt-wine](https://aur.archlinux.org/packages/binfmt-wine/).
3.  If you are using rustup, you can run `rustup install stable-$ARCH-pc-windows-gnu` and `rustup target add $ARCH-pc-windows-gnu` to install rust and rust standard library for your architecture. If you are not using rustup, install a copy of rust's standard library for windows in your rustlib directory (`/usr/local/lib/rustlib` if you're using [rust-nightly-bin](https://aur.archlinux.org/packages/rust-nightly-bin/) and `/usr/lib/rustlib` if you're using the official [rust](https://www.archlinux.org/packages/?name=rust) package). The easiest way to do this is to download the rust installer for windows for your target architecture, install it under wine (`wine start my-rust-installer.msi`) and copy `$INSTALL_DIR/lib/rustlib/$ARCH-pc-windows-gnu` into your rustlib directory.
4.  Finally, tell cargo where to find the MinGW-w64 gcc/ar by adding the following to your `~/.cargo/config`:

 `~/.cargo/config` 
```
[target.$ARCH-pc-windows-gnu]
linker = "/usr/bin/$ARCH-w64-mingw32-gcc"
ar = "/usr/$ARCH-w64-mingw32/bin/ar"

```

Finally, you can cross compile for windows by passing the `--target $ARCH-pc-windows-gnu` to cargo:

```
$ # Build
$ cargo build --release --target "$ARCH-pc-windows-gnu"
$ # Run unit tests under wine
$ cargo test --target "$ARCH-pc-windows-gnu"

```

### unofficial packages

The [unofficial repo archlinuxcn](/index.php/Unofficial_user_repositories#archlinuxcn "Unofficial user repositories") has rust-nightly and Rust std library for i686, ARM, ARMv7, Windows 32 and 64 so you can just install the one you want then enjoy cross compiling. However, you have to find an ARM toolchain by yourself. For Windows 32bit targets, you'll need to get a libgcc_s_dw2-1.dll to build and run.

## Cargo

[Cargo](https://crates.io/), Rust's package manager, can be [installed](/index.php/Installed "Installed") as [cargo](https://www.archlinux.org/packages/?name=cargo). The nightly version is available in the AUR as [cargo-bin](https://aur.archlinux.org/packages/cargo-bin/). If you use [rustup](https://www.archlinux.org/packages/?name=rustup), it already includes cargo.

Cargo is a tool that allows Rust projects to declare their various dependencies, and ensure that you'll always get a repeatable build. You're encouraged to read the [official guide](http://doc.crates.io/guide.html).

### Usage

To create a new project using Cargo:

 `$ cargo new hello_world --bin` 

This creates a directory with a default `Cargo.toml` file, set to build an executable (because we included `--bin`, otherwise it would build a library).

**Note:** Cargo uses this `Cargo.toml` as a manifest containing all of the metadata required to compile your project. `Cargo.toml` 
```
[package]
name = "hello_world"
version = "0.1.0"
authors = ["Your Name <you@example.com>"]
```

## IDE Support

### Tools

#### Racer

The [Racer](https://github.com/phildawes/racer) autocomplete engine is the current best method of gaining autocomplete support. However, it requires that you also install a copy of the Rust source code, which you can obtain in one of several ways:

*   With rustup: `rustup component add rust-src`
*   From the AUR: [rust-src](https://aur.archlinux.org/packages/rust-src/) or [rust-nightly-src](https://aur.archlinux.org/packages/rust-nightly-src/), in this case you must set the `RUST_SRC_PATH` environment var.

After installing the source code, you can either use `Cargo` to install racer or obtain it from the repos ([rust-racer](https://www.archlinux.org/packages/?name=rust-racer)).

```
$ cargo install racer

```

#### Clippy

[Clippy](https://github.com/Manishearth/rust-clippy) takes advantage of compiler plugin support in Nightly builds of Rust to provide a large number of additional lints for detecting and warning about a larger variety of errors and non-idiomatic Rust. Because it requires support for compiler plugins in order to operate, clippy will not work when compiling with the stable Rust compiler.

```
$ cargo install clippy

```

### Editors

#### Atom

Atom supports Rust programming with the available [Tokamak IDE](https://vertexclique.github.io/tokamak/) plugin.

#### Visual Studio Code

Support for Rust can be obtained by installing [RustyCode](https://marketplace.visualstudio.com/items?itemName=saviorisdead.RustyCode).

#### Vim

Vim support for Rust is enabled via [vim-racer](https://github.com/racer-rust/vim-racer) plugin.

## See also

*   [Official website of the Rust Programming Language](http://rust-lang.org/)
*   [Rust Documentation](https://www.rust-lang.org/documentation.html)
*   [Official Rust Book](http://doc.rust-lang.org/stable/book/)
*   [Standard Library API Lookup](https://doc.rust-lang.org/std/)
*   [Examples with small descriptions](http://rustbyexample.com/)
*   [Page listing of Rust tutorials](https://github.com/ctjhoa/rust-learning)
*   [Libraries(crates) available through Cargo](https://crates.io/)
*   [This Week in Rust](https://this-week-in-rust.org/)
*   [The Rust Programming Language Blog](http://blog.rust-lang.org/)
*   [The Rust Users Forum](https://users.rust-lang.org/)
*   [The Rust Internals Forum](https://internals.rust-lang.org/)
*   [Awesome Rust: A curated list of Rust libraries and resources](https://rust.libhunt.com/)
*   [Wikipedia article](https://en.wikipedia.org/wiki/Rust_(programming_language) "wikipedia:Rust (programming language)")