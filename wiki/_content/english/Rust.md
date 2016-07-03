[Rust](http://rust-lang.org/) is a systems programming language that runs blazingly fast, prevents nearly all segfaults, and guarantees thread and memory safety.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Vanilla Installation](#Vanilla_Installation)
    *   [1.2 Rustup Installation](#Rustup_Installation)
    *   [1.3 Test your installation](#Test_your_installation)
*   [2 Cross Compiling](#Cross_Compiling)
    *   [2.1 Using rustup](#Using_rustup)
    *   [2.2 Windows](#Windows)
    *   [2.3 unofficial packages](#unofficial_packages)
*   [3 Cargo](#Cargo)
    *   [3.1 Usage](#Usage)
*   [4 See also](#See_also)

## Installation

### Vanilla Installation

To [install](/index.php/Install "Install") the latest stable version of Rust, [install](/index.php/Install "Install") the [rust](https://www.archlinux.org/packages/?name=rust) package.

If you would like to build the stable or Beta from source, visit [Rust Downloads](http://www.rust-lang.org/install.html). You may also obtain [rust-nightly-bin](https://aur.archlinux.org/packages/rust-nightly-bin/) via the [AUR](/index.php/AUR "AUR") for the latest development snapshot (provides Cargo).

### Rustup Installation

An alternative is to use [rustup](https://aur.archlinux.org/packages/rustup/), a tool that allows you to install and manage multiple rust installations (stable, beta, nightly) without conflicts, and easily switch between them. It also supports installations of rust for cross-compiling. You either either install rustup via AUR or via [the source](https://doc.rust-lang.org/book/nightly-rust.html). rustup provides cargo.

You may need to add another gpg key to allow Rust installations :

```
$ gpg --recv-keys 108F66205EAEB0AAA8DD5E1C85AB96E6FA1BE5FE

```

**Note:** If you don't install rust via AUR, you can update it by running `rustup self update`. If you do install rustup via AUR, you will not be able to update rustup this way

By default, only the stable channel from your architecture will be installed. It will however not be usable right away, you need to specify the installed stable channel as default for it to work.

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
3.  If you are using rustup, you can run `rustup install $ARCH-pc-windows-gnu` to install rust for your architecture. If you are not using rustup, install a copy of rust's standard library for windows in your rustlib directory (`/usr/local/lib/rustlib` if you're using [rust-nightly-bin](https://aur.archlinux.org/packages/rust-nightly-bin/) and `/usr/lib/rustlib` if you're using the official [rust](https://www.archlinux.org/packages/?name=rust) package). The easiest way to do this is to download the rust installer for windows for your target architecture, install it under wine (`wine start my-rust-installer.msi`) and copy `$INSTALL_DIR/lib/rustlib/$ARCH-pc-windows-gnu` into your rustlib directory.
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

[Cargo](https://crates.io/), Rust's package manager, can be [installed](/index.php/Installed "Installed") as [cargo](https://www.archlinux.org/packages/?name=cargo). The nightly version is available in the AUR as [cargo-bin](https://aur.archlinux.org/packages/cargo-bin/). If you use [rustup](https://aur.archlinux.org/packages/rustup/), it already includes cargo.

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

## See also

*   [Official website of the Rust Programming Language](http://rust-lang.org/)
*   [Wikipedia article](https://en.wikipedia.org/wiki/Rust_(programming_language) "wikipedia:Rust (programming language)")
*   [Examples with small descriptions](http://rustbyexample.com/)
*   [Official starting guide](http://doc.rust-lang.org/stable/book/)
*   [Page listing of Rust tutorials](https://github.com/ctjhoa/rust-learning)
*   [Libraries(crates) available through Cargo](https://crates.io/)