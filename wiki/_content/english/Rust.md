[Rust](http://rust-lang.org/) is a systems programming language that runs blazingly fast, prevents nearly all segfaults, and guarantees thread and memory safety.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Test your installation](#Test_your_installation)
*   [2 Cross Compiling](#Cross_Compiling)
    *   [2.1 Windows](#Windows)
    *   [2.2 unofficial packages](#unofficial_packages)
*   [3 Cargo](#Cargo)
    *   [3.1 Usage](#Usage)
*   [4 See also](#See_also)

## Installation

To [install](/index.php/Install "Install") the latest stable version of Rust, [install](/index.php/Install "Install") the [rust](https://www.archlinux.org/packages/?name=rust) package.

If you would like to build the stable or Beta from source, visit [Rust Downloads](http://www.rust-lang.org/install.html). You may also obtain [rust-nightly-bin](https://aur.archlinux.org/packages/rust-nightly-bin/) via the [AUR](/index.php/AUR "AUR") for the latest development snapshot (provides Cargo).

An alternative is to use [rustup](https://aur.archlinux.org/packages/rustup/), a tool that allows you to install and manage multiple rust installations (stable, beta, nightly), and easily switch between them.

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

### Windows

In this section, `$ARCH` is the target architecture (either `x86_64` or `i686`).

1.  [Install](/index.php/Install "Install") [mingw-w64-gcc](https://www.archlinux.org/packages/?name=mingw-w64-gcc) and [wine](https://www.archlinux.org/packages/?name=wine)
2.  Add a binfmt definition for windows executables either manually or by installing [binfmt-wine](https://aur.archlinux.org/packages/binfmt-wine/).
3.  Install a copy of rust's standard library for windows in your rustlib directory (`/usr/local/lib/rustlib` if you're using [rust-nightly-bin](https://aur.archlinux.org/packages/rust-nightly-bin/) and `/usr/lib/rustlib` if you're using the official [rust](https://www.archlinux.org/packages/?name=rust) package). The easiest way to do this is to download the rust installer for windows for your target architecture, install it under wine (`wine start my-rust-installer.msi`) and copy `$INSTALL_DIR/lib/rustlib/$ARCH-pc-windows-gnu` into your rustlib directory.
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