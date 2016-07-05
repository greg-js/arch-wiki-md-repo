[Rust](http://rust-lang.org/) is a general-purpose, multi-paradigm, compiled systems programming language that runs blazingly fast, prevents nearly all segfaults, and guarantees thread safety.

## Contents

*   [1 Background](#Background)
    *   [1.1 Design](#Design)
    *   [1.2 Rust Core Library](#Rust_Core_Library)
    *   [1.3 Rust Standard Library](#Rust_Standard_Library)
    *   [1.4 Release Cycle](#Release_Cycle)
*   [2 Features](#Features)
    *   [2.1 Immutable By Default](#Immutable_By_Default)
    *   [2.2 Borrowing and Ownership](#Borrowing_and_Ownership)
    *   [2.3 Trait-based Polymorphism](#Trait-based_Polymorphism)
        *   [2.3.1 Implementing Traits](#Implementing_Traits)
        *   [2.3.2 Trait-based Generics](#Trait-based_Generics)
    *   [2.4 Sum Types & Pattern Matching](#Sum_Types_.26_Pattern_Matching)
    *   [2.5 Concurrency](#Concurrency)
        *   [2.5.1 Channel Selection (Requires Nightly)](#Channel_Selection_.28Requires_Nightly.29)
        *   [2.5.2 Channel Selection (Stable)](#Channel_Selection_.28Stable.29)
        *   [2.5.3 Chan Crate Periodic Timer](#Chan_Crate_Periodic_Timer)
*   [3 Installation](#Installation)
    *   [3.1 Native Installation](#Native_Installation)
    *   [3.2 Official Rustup Installation](#Official_Rustup_Installation)
    *   [3.3 Test your installation](#Test_your_installation)
*   [4 Cross Compiling](#Cross_Compiling)
    *   [4.1 Using rustup](#Using_rustup)
    *   [4.2 Windows](#Windows)
    *   [4.3 unofficial packages](#unofficial_packages)
*   [5 Cargo](#Cargo)
    *   [5.1 Usage](#Usage)
*   [6 IDE Support](#IDE_Support)
    *   [6.1 Tools](#Tools)
        *   [6.1.1 Racer](#Racer)
        *   [6.1.2 Clippy](#Clippy)
    *   [6.2 Editors](#Editors)
        *   [6.2.1 Atom](#Atom)
        *   [6.2.2 Visual Studio Code](#Visual_Studio_Code)
*   [7 See also](#See_also)

## Background

Rust originally started as a personal project by Graydon Hoare, a Mozilla employee. Shortly thereafter, Mozilla began sponsoring the project in 2009 before announcing the project publicly in 2010\. However, although sponsored by Mozilla, it is largely an open community project. A significant portion of the commits are from community members. The initial rustc compiler was written in OCaml until it achieved self-compiling status with the port to Rust in 2011\. Over the next several years, the design of the language was refined as Rust was developed alongside the Servo web browser layout engine. Finally, on May 15th, 2015, the first stable release of Rust (1.0) was released.

### Design

The design and tooling of the language is heavily inspired by the myriad of programming languages that have come before. On the language aspect, Rust lifts a plethora of concepts from both functional programming languages such as Haskell and ML, as well as imperative programming languages such as C and C++. On the tooling side, Rust provides the Cargo package manager as the standard build tool which takes a page directly from Node's NPM and improves upon that concept.

### Rust Core Library

The [Rust Core Library](https://doc.rust-lang.org/core/) is the dependency-free foundation of the Rust Standard Library. It interfaces directly with LLVM primitives, which allows Rust to be platform and hardware-agnostic. It is this integration with LLVM allows Rust to obtain greater performance than equivalent C applications compiled with Clang, making Rust software designed with libcore lower level than C. Developers looking to target software for embedded platforms may forego the standard library with `#[nostd]` to exclusively use the no-batteries-included core library for smaller binary sizes and improved performance. However, using `#[nostd]` limits the amount of software support that you can get from the larger Rust community as a majority of libraries require the standard library.

### Rust Standard Library

The [Rust Standard Library](http://doc.rust-lang.org/std/index.html) provides the convenient high level abstractions by which a majority of portable Rust software is created with. It features convenient features such as the `Vec`, `Iterator`, `Option`, `Result`, and `String` types; a vast amount of methods for language primitives; a large number of standard macros; I/O and multithreading support; heap allocations with `Box`; and many more high level features not available in the core library.

### Release Cycle

Rust follows a regular six week release cycle, similar to the release cycle of Firefox, to enable Rust to become an agile language that can react quickly to advances in technology. With each new release, the core and standard libraries are improved to support more platforms, improve performance, and to stabilize new features for use with stable Rust. Some consider Rust to be an eternally unstable language due to the plan to continue perpetual development of Rust, but Rust's commitment to stability has proven otherwise.

## Features

### Immutable By Default

All variables are initialized using the `let` binding, but unlike other languages, variables are immutable by default. It is only when variables have been initialized with `let mut` that they can be later modified. An immutable `let` binding should not be confused with the `const` keyword, however, as `const` defines immutability at compile-time, versus immutability at run-time with `let`.

### Borrowing and Ownership

Another key feature of Rust is the borrowing and ownership model which is used by the compiler to detect and prevent a large number of errors at compile-time. Many newcomers to Rust from other programming languages often fight with the compiler because of the borrowing and ownership rules, as they do not necessarily understand how it works. When a variable is passed into a function by value (`String`), the ownership of the variable is given to that function, and the variable will be destroyed upon the return of the function. Typically, functions are written to take values by reference instead of by value so that they may live beyond the function call, but in cases where you cannot pass a value by reference, you must use the `clone` method on that variable to create a copy of itself to pass to the function.

```
let value = String::from("This is some text");
do_something_with(value); // <- `value` will be destroyed by the function after use
println!("{}", value);    // <- Causes an error because `value` was moved

```

```
let value = String::from("This is some text");
do_something_with(&value); // <- `value` will not be destroyed
println!("{}", value);     // <- Will print the value of `value`

```

```
let value = String::from("This is some text");
do_something_with(value.clone()); // <- Creates a copy of `value`
println!("{}", value);            // <- Will print the value of `value`

```

### Trait-based Polymorphism

Inspired by Haskell's type classes, the type system features traits which allow Rust to obtain ad-hoc polymorphism. Traits provide the ability to extend the feature set of types with additional methods beyond their initial implementations. They are not bound to any specific type, and thus they may be re-used. In addition, they are used in generics to define what types are supported as function inputs, and soon, what types are supported as function outputs. What makes them particularly potent is that trait implementations do not have to happen in the same crate that a type is defined, so they can be used to extend both Rust's primitive types as well as imported types from other crates.

#### Implementing Traits

```
trait Number {
    fn is_even(&self) -> bool;
}

impl Number for u64 {
    fn is_even(&self) -> bool {
        *self % 2 == 0
    }
}

impl Number for u32 {
    fn is_even(&self) -> bool {
        *self % 2 == 0
    }
}

fn main() {
    println!("{}", 6u64.is_even());
    println!("{}", 6u32.is_even());
}

```

#### Trait-based Generics

```
trait Number {
    fn is_even(&self) -> bool;
}

impl Number for u64 {
    fn is_even(&self) -> bool {
        *self % 2 == 0
    }
}

impl Number for u32 {
    fn is_even(&self) -> bool {
        *self % 2 == 0
    }
}

fn is_even<N: Number>(input: N) -> bool {
    input.is_even()
}

fn main() {
    println!("{}", is_even(6u64));
    println!("{}", is_even(6u32));
}

```

### Sum Types & Pattern Matching

Used throughout the language are sum types such as `Option` and `Result`. The purpose of these types are to denote that the value may or may not exist (`Option`), or that a value may or may not have encountered an error `Result`. By combining them with enums, it is possible to perform advanced pattern matching to cover a large number of possible scenarios, especially given that enums may also contain unique values

```
enum Attempt { Int(i64), String(String) }

enum AttemptError { NoResponse, InvalidResponse(String), Fatal(String) }

match attempt() {
    Ok(Attempt::Int(value)) if value > 5           => println!("returned integer, {}, is greater than five"),
    Ok(Attempt::Int(value))                        => println!("returned integer: {}", value),
    Ok(Attempt::String(value)) if value.is_empty() => println!("returned string is empty"),
    Ok(Attempt::String(value))                     => println!("returned string: {}", value),
    Err(AttemptError::NoResponse)                  => println!("no response given"),
    Err(AttemptError::InvalidResponse(cause))      => println!("invalid response received: {}", cause),
    Err(AttemptError::Fatal(cause))                => panic!("fatal error: {}", cause),
}

```

### Concurrency

Rust provides strong support for concurrency out of the box, which is made even better with additional crates such as [bus](https://jon.tsp.io/crates/bus/) and [chan](http://burntsushi.net/rustdoc/chan/). Rust supports the concept of channels that have been pioneered by previous languages, namely Newsqueak and Go, and combines them with the ownership and borrowing model to provide strong thread-safety guarantees.

#### Channel Selection (Requires Nightly)

```
#![feature(mpsc_select)]
use std::sync::mpsc::channel;
use std::thread;
use std::time::Duration;

fn main() {
    // Create channels for sending and receieving
    let (one_tx, one_rx) = channel();
    let (three_tx, three_rx) = channel();

    // Spawn one second timer
    thread::spawn(move || {
        loop {
            thread::sleep(Duration::from_secs(1));
            one_tx.send("tick").unwrap();
        }
    });

    // Spawn three second timer
    thread::spawn(move || {
        loop {
            thread::sleep(Duration::from_secs(3));
            three_tx.send("tock").unwrap();
        }
    });

    loop {
        select! {
            reply = one_rx.recv()   => println!("{}", reply.unwrap()),
            reply = three_rx.recv() => println!("{}", reply.unwrap())
        }
    }
}

```

#### Channel Selection (Stable)

```
use std::sync::mpsc::channel;
use std::thread;
use std::time::Duration;

fn main() {
    // Create channels for sending and receieving
    let (one_tx, one_rx) = channel();
    let (three_tx, three_rx) = channel();

    // Spawn one second timer
    thread::spawn(move || {
        loop {
            thread::sleep(Duration::from_secs(1));
            one_tx.send("tick").unwrap();
        }
    });

    // Spawn three second timer
    thread::spawn(move || {
        loop {
            thread::sleep(Duration::from_secs(3));
            three_tx.send("tock").unwrap();
        }
    });

    loop {
        thread::sleep(Duration::from_millis(50));
        let _ = one_rx.try_recv().map(|reply| println!("{}", reply));
        let _ = three_rx.try_recv().map(|reply| println!("{}", reply));
    }
}

```

#### Chan Crate Periodic Timer

```
#[macro_use]
extern crate chan;

fn main() {
    let tick = chan::tick_ms(1000);
    let tock = chan::tick_ms(3000);
    loop {
        chan_select! {
            tick.recv() => println!("tick"),
            tock.recv() => println!("tock"),
        }
    }
}

```

## Installation

### Native Installation

To [install](/index.php/Install "Install") the latest stable version of Rust from the official Arch Linux software repository, [install](/index.php/Install "Install") the [rust](https://www.archlinux.org/packages/?name=rust) package. This will only install the rustc compiler, so you will also have to install the [cargo](https://www.archlinux.org/packages/?name=cargo) package as well.

### Official Rustup Installation

The official and recommended method of installing Rust for the purpose of developing software is to use the [Rustup toolchain manager](https://www.rustup.rs/), written in Rust. After installing rustup, one only needs to run `rustup self update` to upgrade rustup in the future. `curl -sSf [https://static.rust-lang.org/rustup.sh](https://static.rust-lang.org/rustup.sh) ` 

The benefits to using the Rustup toolchain manager instead of the standalone prepackaged Rust in the software repository is the ability to install multiple toolchains (stable, beta, nightly) for multiple targets (windows, mac, android) and architectures (x86, x86_64, arm). It is also important to note that tools such as [Clippy](https://github.com/Manishearth/rust-clippy) require compiler plugin support, which is only supported in nightly builds of Rust.

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

## IDE Support

### Tools

#### Racer

The [Racer](https://github.com/phildawes/racer) autocomplete engine is the current best method of gaining autocomplete support. However, it requires that you also install a copy of the Rust source code, which you can obtain either directly or from the AUR ([rust-src](https://aur.archlinux.org/packages/rust-src/) or [rust-nightly-src](https://aur.archlinux.org/packages/rust-nightly-src/)). After installing the source code, you can either use `Cargo` to install racer or obtain it from the AUR ([racer](https://aur.archlinux.org/packages/racer/)).

 `cargo install racer` 

#### Clippy

[Clippy](https://github.com/Manishearth/rust-clippy) takes advantage of compiler plugin support in Nightly builds of Rust to provide a large number of additional lints for detecting and warning about a larger variety of errors and non-idiomatic Rust. Because it requires support for compiler plugins in order to operate, clippy will not work when compiling with the stable Rust compiler.

 `cargo install clippy` 

### Editors

#### Atom

Atom has the best support for Rust programming as of this moment with the available [Tokamak IDE](https://vertexclique.github.io/tokamak/) plugin.

#### Visual Studio Code

Visual Studio Code also provides support for Rust, although it is not as great as Atom's support. Support for Rust can be obtained by installing [RustyCode](https://marketplace.visualstudio.com/items?itemName=saviorisdead.RustyCode).

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