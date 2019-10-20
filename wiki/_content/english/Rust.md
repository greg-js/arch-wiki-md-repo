Related articles

*   [Rust package guidelines](/index.php/Rust_package_guidelines "Rust package guidelines")

From [Wikipedia](https://en.wikipedia.org/wiki/Rust_(programming_language) "wikipedia:Rust (programming language)"):

	[Rust](http://rust-lang.org/) is a general-purpose, multi-paradigm, compiled programming language sponsored by Mozilla Research. It is designed to be a "safe, concurrent, practical language", supporting pure-functional, imperative-procedural, and object-oriented styles. The goal of Rust is to be a good language for creating highly concurrent and highly safe systems, and programming in the large. This has led to a feature set with an emphasis on safety, control of memory layout, and concurrency. Performance of idiomatic Rust is comparable to the performance of idiomatic C++.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Core language](#Core_language)
    *   [1.1 Rust Core Library](#Rust_Core_Library)
    *   [1.2 Rust Standard Library](#Rust_Standard_Library)
    *   [1.3 Release cycle](#Release_cycle)
*   [2 Installation](#Installation)
    *   [2.1 Native installation](#Native_installation)
    *   [2.2 Rustup](#Rustup)
        *   [2.2.1 Upstream installation script](#Upstream_installation_script)
        *   [2.2.2 Arch Linux package](#Arch_Linux_package)
        *   [2.2.3 Usage](#Usage)
    *   [2.3 Test your installation](#Test_your_installation)
*   [3 Cross compiling](#Cross_compiling)
    *   [3.1 Using rustup](#Using_rustup)
    *   [3.2 Windows](#Windows)
    *   [3.3 Unofficial packages](#Unofficial_packages)
*   [4 Cargo](#Cargo)
    *   [4.1 Usage](#Usage_2)
*   [5 IDE support](#IDE_support)
    *   [5.1 Tools](#Tools)
        *   [5.1.1 RLS](#RLS)
        *   [5.1.2 Racer](#Racer)
        *   [5.1.3 Clippy](#Clippy)
        *   [5.1.4 Rustfmt](#Rustfmt)
    *   [5.2 Editors](#Editors)
        *   [5.2.1 Atom](#Atom)
        *   [5.2.2 IntelliJ IDEA](#IntelliJ_IDEA)
        *   [5.2.3 Visual Studio Code](#Visual_Studio_Code)
        *   [5.2.4 Vim](#Vim)
        *   [5.2.5 Emacs](#Emacs)
        *   [5.2.6 Kate](#Kate)
*   [6 See also](#See_also)

## Core language

### Rust Core Library

The [Rust Core Library](https://doc.rust-lang.org/core/) is the dependency-free foundation of the Rust Standard Library. It interfaces directly with LLVM primitives, which allows Rust to be platform and hardware-agnostic. It is this integration with LLVM that allows Rust to obtain greater performance than equivalent C applications compiled with Clang, making Rust software designed with libcore lower level than C. Developers looking to target software for embedded platforms may forego the standard library with `#![no_std]` to exclusively use the no-batteries-included core library for smaller binary sizes and improved performance. However, using `#![no_std]` limits the amount of software support that you can get from the larger Rust community as a majority of libraries require the standard library.

### Rust Standard Library

The [Rust Standard Library](http://doc.rust-lang.org/std/index.html) provides the convenient high level abstractions by which a majority of portable Rust software is created with. It features convenient features such as the `Vec`, `Iterator`, `Option`, `Result`, and `String` types; a vast amount of methods for language primitives; a large number of standard macros; I/O and multithreading support; heap allocations with `Box`; and many more high level features not available in the core library.

### Release cycle

Rust follows a regular six week release cycle, similar to the release cycle of Firefox. With each new release, the core and standard libraries are improved to support more platforms, improve performance, and to stabilize new features for use with stable Rust.

## Installation

There are two choices for a rust installation, one is supported by Arch Linux, while the other is officially supported by Rust.

### Native installation

To [install](/index.php/Install "Install") the latest stable version of Rust from the official Arch Linux software repository, [install](/index.php/Install "Install") the [rust](https://www.archlinux.org/packages/?name=rust) package. This will install the `rustc` compiler and [Cargo](#Cargo).

There's also development version of the Rust compiler available from [AUR](/index.php/AUR "AUR"). Use [rust-nightly-bin](https://aur.archlinux.org/packages/rust-nightly-bin/) for prebuilt generic binaries or [rust-git](https://aur.archlinux.org/packages/rust-git/) to build the compiler with system libraries.

### Rustup

The official and recommended method of installing Rust for the purpose of developing software is to use the [Rustup toolchain manager](https://www.rustup.rs/), written in Rust.

The benefits to using the Rustup toolchain manager instead of the standalone prepackaged Rust in the software repository is the ability to install multiple toolchains (stable, beta, nightly) for multiple targets (windows, mac, android) and architectures (x86, x86_64, arm).

#### Upstream installation script

Download the file with `curl -f https://sh.rustup.rs > rust.sh`, view it: `less ./rust.sh`, and run the script `./rust.sh` to start rustup installation. The script makes PATH changes only to login shell [configuration files](/index.php/Bash#Invocation "Bash"). You need to `source ~/.cargo/env` until you logout and login back into the system. To update rustup afterwards, run `rustup self update`.

The script installs and activates the default toolchain by default (the one used by the [rust](https://www.archlinux.org/packages/?name=rust) package, so there is no need to manually install it to start using Rust.

**Warning:** Running `curl *some-url* | sh`, as the Rust documentation suggests, is considered as a security risk, because it executes unknown code, that might even be corrupted during the download. Therefore it is recommended to manually download the script and check it, before executing it.

**Note:** Please make sure that `~/.cargo/bin` is in your `PATH` when you run `rustup`.

#### Arch Linux package

[rustup](https://www.archlinux.org/packages/?name=rustup) is also available on the Arch Linux software repository. Note that `rustup self update` will **not** work when installed this way, the package needs to be updated by pacman.

This package has the advantage that the various Rust executables live in `/usr/bin`, instead of `~/.cargo/bin`, removing the need to add another directory to your `PATH`.

**Note:** The [rustup](https://www.archlinux.org/packages/?name=rustup) package does **not** install a toolchain by default. It provides instead symlinks between `/usr/bin/rustup` to the common binaries such as `/usr/bin/rustc` and `/usr/bin/cargo`. As stated above, The user still needs to install a toolchain manually, for these Rust commands to do anything.

In order to install the toolchain, you need to tell rustup which version to use: `stable` or `nightly`.

Example:

 `$ rustup default stable` 

#### Usage

You might need to manually install a toolchain, e.g. `stable`, `beta`, `nightly` or `1.23.0`. You also need to do this if you want to use/test another toolchain.

```
$ rustup toolchain install *toolchain*

```

You can now run the Rust commands by running, `rustup run *toolchain* *command*`. However, to use these commands directly, you need to activate the toolchain:

```
$ rustup default *toolchain*

```

Check the installed Rust version using `rustc -V`:

 `$ rustc -V ` 
```
rustc 1.26.0 (a77568041 2018-05-07)

```

**Note:** Rustup does not install some Rust commands that the [rust](https://www.archlinux.org/packages/?name=rust) package does include, such as `rustfmt` and `rls`. They are not included because this allows the Rust maintainers to ship a nightly of Rust with a broken `rustfmt`/`rls`. To install them, run `rustup component add rls` and `rustup component add rustfmt` respectively. This will also suspend updates of the nightly channel, if they break `rustfmt`/`rls`.

**Note:** Rust does not do its own linking, and so you’ll need to have a linker installed. You can use [gcc](https://www.archlinux.org/packages/?name=gcc), otherwise Rust will generate the following `error: linker `cc` not found.`

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

## Cross compiling

### Using rustup

You can easily cross-compile using rustup. rustup supports many crosscompile targets. A full list can be found running `rustup target list`.

For instance, if you want to install rust using the stable channel for windows, using the gnu compiler, you will need to do :

```
$ rustup install stable-x86_64-pc-windows-gnu

```

This will only installs rust and its tools for your target architecture, but some additional tools might be needed for cross compiling.

### Windows

In this section, `$ARCH` is the target architecture (either `x86_64` or `i686`). It will explain how to cross compile using rustup.

1.  [Install](/index.php/Install "Install") [mingw-w64-gcc](https://aur.archlinux.org/packages/mingw-w64-gcc/) and [wine](https://www.archlinux.org/packages/?name=wine)
2.  If you are using rustup, you can run `rustup install stable-$ARCH-pc-windows-gnu` and `rustup target add $ARCH-pc-windows-gnu` to install rust and rust standard library for your architecture. If you are not using rustup, install a copy of rust's standard library for windows in your rustlib directory (`/usr/local/lib/rustlib` if you're using [rust-nightly-bin](https://aur.archlinux.org/packages/rust-nightly-bin/) and `/usr/lib/rustlib` if you're using the official [rust](https://www.archlinux.org/packages/?name=rust) package). The easiest way to do this is to download the rust installer for windows for your target architecture, install it under wine (`wine start my-rust-installer.msi`) and copy `$INSTALL_DIR/lib/rustlib/$ARCH-pc-windows-gnu` into your rustlib directory.
3.  Finally, tell cargo where to find the MinGW-w64 gcc/ar by adding the following to your `~/.cargo/config`:

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

Currently building executables using MinGW 6 and the toolchains installed by rustup is broken. To fix it, execute

```
for lib in crt2.o dllcrt2.o libmsvcrt.a; do cp -v /usr/x86_64-w64-mingw32/lib/$lib $HOME/.rustup/toolchains/$CHANNEL-x86_64-unknown-linux-gnu/lib/rustlib/x86_64-pc-windows-gnu/lib/; done

```

where `CHANNEL` is the update channel (`stable`, `beta` or `nightly`)

### Unofficial packages

The [unofficial repository archlinuxcn](/index.php/Unofficial_user_repositories#archlinuxcn "Unofficial user repositories") has rust-nightly and Rust std library for i686, ARM, ARMv7, Windows 32 and 64 so you can just install the one you want then enjoy cross compiling. However, you have to find an ARM toolchain by yourself. For Windows 32bit targets, you'll need to get a libgcc_s_dw2-1.dll to build and run.

## Cargo

[Cargo](https://crates.io/), Rust's package manager, is part of the [rust](https://www.archlinux.org/packages/?name=rust) package. The nightly version is available in the AUR as [cargo-nightly-bin](https://aur.archlinux.org/packages/cargo-nightly-bin/). If you use [rustup](https://www.archlinux.org/packages/?name=rustup), it already includes cargo.

Cargo is a tool that allows Rust projects to declare their various dependencies, and ensure that you'll always get a repeatable build. You're encouraged to read the [official guide](http://doc.crates.io/guide.html).

### Usage

To create a new project using Cargo:

```
$ cargo new hello_world 

```

This creates a directory with a default `Cargo.toml` file, set to build an executable.

**Note:** Cargo uses this `Cargo.toml` as a manifest containing all of the metadata required to compile your project. `Cargo.toml` 
```
[package]
name = "hello_world"
version = "0.1.0"
authors = ["Your Name <you@example.com>"]
edition = "2018"

[dependencies]
```

## IDE support

### Tools

#### RLS

[RLS](https://github.com/rust-lang/rls) provides a [Language Server Protocol](https://microsoft.github.io/language-server-protocol/) implementation for Rust, providing IDEs, editors, and other tools with information about Rust programs. It supports functionality such as 'goto definition', symbol search, reformatting, and code completion, and enables renaming and refactorings.

RLS is included in the [rust](https://www.archlinux.org/packages/?name=rust) package. To install RLS using rustup:

```
$ rustup component add rls rust-analysis rust-src

```

#### Racer

[Racer](https://github.com/phildawes/racer) provides code completion support for editors and IDEs. It has been superseded by RLS (which uses Racer as a fallback).

It requires that you also install a copy of the Rust source code, which you can obtain in one of several ways:

*   With rustup: `rustup component add rust-src`
*   From the AUR: [rust-src](https://aur.archlinux.org/packages/rust-src/) or [rust-nightly-src](https://aur.archlinux.org/packages/rust-nightly-src/), in this case you must set the `RUST_SRC_PATH` environment var.

After installing the source code, you can either use `Cargo` to install racer or obtain it from the repos ([rust-racer](https://www.archlinux.org/packages/?name=rust-racer)).

```
$ cargo +nightly install racer

```

#### Clippy

[Clippy](https://github.com/rust-lang/rust-clippy) takes advantage of compiler plugin support to provide a large number of additional lints for detecting and warning about a larger variety of errors and non-idiomatic Rust.

Clippy is included in the [rust](https://www.archlinux.org/packages/?name=rust) package. To install it with rustup use:

```
$ rustup component add clippy

```

#### Rustfmt

[Rustfmt](https://github.com/rust-lang/rustfmt) is a tool to format Rust code according to the official style guidelines.

Rustup is included in the [rust](https://www.archlinux.org/packages/?name=rust) package. To install it with rustup use:

```
$ rustup component add rustfmt

```

### Editors

#### Atom

[Atom](/index.php/Atom "Atom") support for Rust programming is provided by the [ide-rust](https://atom.io/packages/ide-rust) plugin (requires rustup).

#### IntelliJ IDEA

[IntelliJ IDEA](https://www.jetbrains.com/idea/) has a [Rust plugin](https://github.com/intellij-rust/intellij-rust). The same plugin also works with CLion. When configuring the toolchain, use rustup to download the source (`rustup component add rust-src`), and then select `~/.rustup/toolchains/<your toolchain>/bin` as the toolchain location.

#### Visual Studio Code

[Visual Studio Code](/index.php/Visual_Studio_Code "Visual Studio Code") support for Rust can be obtained via [rust-lang.rls](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust) extension (requires rustup) or the [kalitaalexey.vscode-rust](https://marketplace.visualstudio.com/items?itemName=kalitaalexey.vscode-rust) extension.

#### Vim

[Vim](/index.php/Vim "Vim") support for Rust can be obtained via the official [rust.vim](https://github.com/rust-lang/rust.vim) plugin, which provides file detection, syntax highlighting, formatting and support for the [Syntastic](https://github.com/vim-syntastic/syntastic) syntax checking plugin. Many completion engines have Rust support, like [coc](https://github.com/neoclide/coc.nvim) (via the [coc.rls](https://github.com/neoclide/coc-rls) plugin) and [YouCompleteMe](https://github.com/ycm-core/YouCompleteMe).

#### Emacs

[Emacs](/index.php/Emacs "Emacs") support for Rust can be obtained via the official [rust-mode](https://github.com/rust-lang/rust-mode) plugin or the [emacs-rust-mode](https://aur.archlinux.org/packages/emacs-rust-mode/) package.

#### Kate

Kate support for Rust is installed by default by the [kate](https://www.archlinux.org/packages/?name=kate) package, but also requires extra configurations. First, install the package [rust-racer](https://www.archlinux.org/packages/?name=rust-racer) Second, get the Rust source:

*   With rustup: `rustup component add rust-src`
*   or From the AUR: [rust-src](https://aur.archlinux.org/packages/rust-src/) or [rust-nightly-src](https://aur.archlinux.org/packages/rust-nightly-src/), in this case you must set the `RUST_SRC_PATH` environment var.

Third, configure Kate by clicking Settings -> Configure Kate, then navigate to Application -> Plugins, then tick the 'Rust code completion', then you will see Application -> Rust code completion in the left sidebar, navigation to it, and assign 'Rust source tree location' to `$HOME/.rustup/toolchains/stable-x86_64-unknown-linux-gnu/lib/rustlib/src/rust/src` if you install the Rust source with rustup.

## See also

*   [Official website of the Rust Programming Language](http://rust-lang.org/)
*   [Rust Documentation](https://www.rust-lang.org/documentation.html)
*   [Official Rust Book](http://doc.rust-lang.org/stable/book/)
*   [Standard Library API Lookup](https://doc.rust-lang.org/std/)
*   [Examples with small descriptions](https://doc.rust-lang.org/stable/rust-by-example/)
*   [Page listing of Rust tutorials](https://github.com/ctjhoa/rust-learning)
*   [Libraries(crates) available through Cargo](https://crates.io/)
*   [This Week in Rust](https://this-week-in-rust.org/)
*   [The Rust Programming Language Blog](http://blog.rust-lang.org/)
*   [The Rust Users Forum](https://users.rust-lang.org/)
*   [The Rust Internals Forum](https://internals.rust-lang.org/)
*   [Awesome Rust: A curated list of Rust libraries and resources](https://rust.libhunt.com/)
*   [Wikipedia article](https://en.wikipedia.org/wiki/Rust_(programming_language) "wikipedia:Rust (programming language)")