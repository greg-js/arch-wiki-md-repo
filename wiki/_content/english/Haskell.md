[Haskell](http://www.haskell.org) is a general purpose, purely functional, programming language.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Compiler](#Compiler)
*   [2 Problems with linking](#Problems_with_linking)
    *   [2.1 Static linking](#Static_linking)
    *   [2.2 Building statically linked packages with Cabal (without using shared libraries)](#Building_statically_linked_packages_with_Cabal_.28without_using_shared_libraries.29)
    *   [2.3 Haskell development tools](#Haskell_development_tools)
*   [3 Managing Haskell packages](#Managing_Haskell_packages)
    *   [3.1 Pros/Cons of the different methods](#Pros.2FCons_of_the_different_methods)
    *   [3.2 ArchHaskell repository](#ArchHaskell_repository)
    *   [3.3 cabal-install](#cabal-install)
        *   [3.3.1 Preparation and $PATH](#Preparation_and_.24PATH)
        *   [3.3.2 Installing packages user-wide](#Installing_packages_user-wide)
        *   [3.3.3 Sandboxes](#Sandboxes)
        *   [3.3.4 Removing packages](#Removing_packages)
    *   [3.4 stack](#stack)
*   [4 See also](#See_also)

## Installation

Haskell generates machine code that can be run natively on Linux. There is nothing special required to run a binary (already compiled) software, like the ones provided in the [official repositories](/index.php/Official_repositories "Official repositories") or by the [#ArchHaskell repository](#ArchHaskell_repository). On the other side, [AUR](/index.php/AUR "AUR") packages or source codes requires a compiler to build the software.

Installing the compiler alone permits to build Haskell source code. A few additional tools are needed for development work.

### Compiler

To build a Haskell source code into native code, a compiler must be installed. There are several [implementations available](http://www.haskell.org/haskellwiki/Implementations), but the one used most (which is now *de facto* the reference) is the GHC (Glasgow Haskell Compiler). It is available in the official repositories as [ghc](https://www.archlinux.org/packages/?name=ghc).

You can try it with the following file:

 `Main.hs`  `main = putStrLn "Hello, World"` 

and by running:

```
$ ghc -dynamic Main.hs
$ ./Main 
```

```
Hello, World

```

## Problems with linking

Since version [8.0.2-1](https://git.archlinux.org/svntogit/community.git/commit/trunk?h=packages/ghc&id=7a948cdfb808afd3ce6f93047ae0dc1778e79f9f), the Arch [ghc](https://www.archlinux.org/packages/?name=ghc) package no longer installs static versions of the GHC boot libraries by default, nor do any of the [haskell-*](https://www.archlinux.org/packages/?q=haskell) packages in *community*. Therefore, to link successfully one must pass the `-dynamic` flag to GHC, as the default is to use static linking. For Cabal, this amounts to the following configuration:

```
cabal configure --disable-library-vanilla --enable-shared --enable-executable-dynamic

```

*   `--disable-library-vanilla` suppresses the creation of static libraries (if your project contains a library).
*   `--enable-shared` enables the creation of shared libraries (if your project contains a library).
*   `--enable-executable-dynamic` causes dynamic linking to be used for executables (if your project contains executables).

You can also set these flags in `~/.cabal/config` so that it applies to all projects by default:

 `~/.cabal/config` 
```
library-vanilla: False
shared: True
executable-dynamic: True

```

Dynamic linking is used for most Haskell modules packaged through [pacman](/index.php/Pacman "Pacman") and some packages in the [AUR](/index.php/AUR "AUR"). Since GHC provides no [ABI](https://en.wikipedia.org/wiki/Application_binary_interface "w:Application binary interface") compatibility between compiler releases, static linking is often the preferred option for local development outside of the package system.

**Note:** In the context of this article, static linking does not mean generating completely static ELF binaries. Only Haskell code will be linked statically into a single ELF binary, which may be dynamically linked to other system libraries such as *glibc*.

### Static linking

To use static linking, one must, at minimum, install the static boot libraries through the [ghc-static](https://www.archlinux.org/packages/?name=ghc-static) package. This would allow you to build projects that depend exclusively on the boot libraries as well as any library that is not installed through the `haskell-*` packages.

Unfortunately, if your project depends on any of the `haskell-*` packages that you have installed, Cabal does not take the absence of static libraries into account during dependency resolution. As a result, it will try to use the existing `haskell-*` package and then fail with [linker errors](https://bugs.archlinux.org/task/54563#comment158808) when it realizes the static libraries are missing. Unlike `ghc-static`, there are no “`haskell-*-static`” packages to fix this problem.

To work around this problem, you can install [ghc-pristine](https://aur.archlinux.org/packages/ghc-pristine/), which wraps over an existing GHC installation to create a separate GHC distribution in `/usr/share/ghc-pristine`, with a package database that contains only boot libraries. Then, to build software with static linking, one simply needs to invoke the wrapped compiler `/usr/share/ghc-pristine/bin/ghc`. For Cabal, this amounts to the following configuration:

 `cabal configure --with-compiler=/usr/share/ghc-pristine` 

This can be made permanent by editing `~/.cabal/config`. Be aware that you still need `ghc-static`.

Alternatives to `ghc-pristine`:

*   One could manually run `cabal install --force-reinstalls` to shadow the corresponding `haskell-*` packages. This can be tedious as you must explicitly enumerate all transitive dependencies that coincide with an existing `haskell-*` package.
*   Use a completely separate GHC distribution: download the official Linux binaries for [GHC](https://www.haskell.org/ghc/) and [cabal-install](https://www.haskell.org/cabal/download.html) and unpack them somewhere else. This is in effect what `ghc-pristine` does, but `ghc-pristine` uses less disk space.

### Building statically linked packages with Cabal (without using shared libraries)

This section explains how to install `cabal-install` but from [Hackage](https://hackage.haskell.org/package/cabal-install) instead of the official [cabal-install](https://www.archlinux.org/packages/?name=cabal-install) package from the repositories. This `cabal-install` will build Haskell packages without using [shared libraries](https://downloads.haskell.org/~ghc/latest/docs/html/users_guide/shared_libs.html) unlike the official [cabal-install](https://www.archlinux.org/packages/?name=cabal-install) which requires you to link dynamically.

In theory with any `cabal-install` you could choose between both methods, static and dynamic, for linking your Haskell code. In practice because in Arch some basic Haskell libraries (`haskell-*` packages) are provided as shared objects (`.so` files) and those libraries are globally registered in Cabal, it has trouble using the same libraries for static linking. To avoid linking [errors](https://bugs.archlinux.org/task/54563#comment158826), it's also especially important to not to mix statically and dynamically Haskell packages installed on the same system, as Cabal doesn't fetch a required package once it has been globally registered (check them with the command `ghc-pkg list`) in one of its forms and not the other (independently of the linking type of the package that it's needed).

For these reasons, **you have to make sure** that the only two related Haskell packages you have installed are [ghc](https://www.archlinux.org/packages/?name=ghc), the compiler, and [ghc-static](https://www.archlinux.org/packages/?name=ghc-static), the boot libraries on its static form, (not [stack](https://www.archlinux.org/packages/?name=stack), [cabal-helper](https://www.archlinux.org/packages/?name=cabal-helper), [cabal-install](https://www.archlinux.org/packages/?name=cabal-install) and none of the `haskell-*` dynamic libraries [available](https://www.archlinux.org/packages/?q=haskell-) in the official repositories).

You can also use [Stack](https://www.haskellstack.org/) as an alternative build tool for Haskell packages, which will link statically by default. But if you still want to use Cabal to build using static linking, follow the next steps of this section to install your own compiled `cabal-install` from Hackage. For this purpose we are going to use the tool [Stack](https://haskellstack.org/) that will help us fetching all the dependencies required and building your own `cabal-install`.

First you have to install [stack-bin](https://aur.archlinux.org/packages/stack-bin/) because you'll use it to bootstrap the compilation of your own Cabal and you don't want to pull as dependencies those packages from the official Arch repositories containing the `haskell-*` dynamic libraries.

Then prepare Stack downloading the package index. Stack will be used with the only purpose of bootstrapping the compilation of your own `cabal-install` but using the already installed [ghc](https://www.archlinux.org/packages/?name=ghc) compiler:

```
$ stack setup --system-ghc

```

Now install your own `cabal-install`:

```
$ stack install --system-ghc cabal-install

```

This newly installed `cabal-install` has been compiled without shared libraries and won't use them when building packages by default. Also, this `cabal-install` will use the installed [ghc](https://www.archlinux.org/packages/?name=ghc) compiler.

### Haskell development tools

To start developing in Haskell easily, one option is the [haskell-platform](http://www.haskell.org/platform/) bundle which is described as:

	*The easiest way to get started with programming Haskell. It comes with all you need to get up and running. Think of it as "Haskell: batteries included".*

The Haskell Platform can be advantageously replaced by [installing](/index.php/Installing "Installing") the [following packages](https://bbs.archlinux.org/viewtopic.php?pid=1151382#p1151382) from the [official repositories](/index.php/Official_repositories "Official repositories"):

*   ghc ([ghc](https://www.archlinux.org/packages/?name=ghc)) — Compiler, which only comes with dynamic [boot libraries](https://ghc.haskell.org/trac/ghc/wiki/Commentary/Libraries) ([ghc-libs](https://www.archlinux.org/packages/?name=ghc-libs)). Static boot libraries ([ghc-static](https://www.archlinux.org/packages/?name=ghc-static)) must be separately installed.
*   cabal-install ([cabal-install](https://www.archlinux.org/packages/?name=cabal-install)) — A build tool focused on dependency resolution and sources packages from Hackage
*   stack ([stack](https://www.archlinux.org/packages/?name=stack)) — A build tool focused on curated snapshots and sources packages from Stackage
*   haddock ([haskell-haddock-api](https://www.archlinux.org/packages/?name=haskell-haddock-api) and [haskell-haddock-library](https://www.archlinux.org/packages/?name=haskell-haddock-library)) — Tools for generating documentation
*   alex ([alex](https://www.archlinux.org/packages/?name=alex)) — Lexical analyzer generator
*   happy ([happy](https://www.archlinux.org/packages/?name=happy)) — Parser generator

Alternatively, you can use [stack](https://www.archlinux.org/packages/?name=stack) to manage your Haskell environment by following the [Arch Linux install instructions](https://docs.haskellstack.org/en/stable/install_and_upgrade/#arch-linux).

## Managing Haskell packages

Many Haskell libraries and executables are grouped in packages. They are all available on [Hackage](http://hackage.haskell.org), and a subset of them is curated on [Stackage](https://www.stackage.org). To install and manage these packages, several methods are available:

*   Either (but not both):
    *   [Official repositories](/index.php/Official_repositories "Official repositories"), or
    *   [ArchHaskell repository](#ArchHaskell_repository)
*   [cabal-install](#cabal-install)
*   [stack](#stack)
*   [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")

[cblrepo](https://github.com/magthe/cblrepo) is a tool used for maintaining Haskell packages for Linux distributions. A wrapper around this, [cabal2pkgbuild-git](https://aur.archlinux.org/packages/cabal2pkgbuild-git/), can create PKGBUILD files from Hackage packages. See [Haskell package guidelines](/index.php/Haskell_package_guidelines "Haskell package guidelines") for more information on *creating new* Haskell packages.

### Pros/Cons of the different methods

The following table documents the advantages and disadvantages of different package management styles.

| **Method** | **Pros** | **Cons** |
| [Official repositories](/index.php/Official_repositories "Official repositories") | Provided by ArchLinux developers, consistent versions of packages, already compiled | Only a few packages available, only dynamic libraries available |
| [ArchHaskell repository](#ArchHaskell_repository) | Provided by ArchHaskell group, consistent versions of packages, already compiled | Need manual intervention to get started with |
| [cabal-install](#cabal-install) | All packages available, root not required | Installed in home directory, [failures in dependency resolution](http://www.haskell.org/haskellwiki/Cabal/Survival#What_is_the_difficulty_caused_by_Cabal-install.3F), difficult to remove specific packages |
| [stack](#stack) | All packages available (favors Stackage), root not required | Installed in home directory, versions are pinned to snapshot, difficult to remove specific packages |
| [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") | Simple to get started | Risk of unmaintained or orphaned packages, incompatible versions of packages possible |

### ArchHaskell repository

See [Unofficial user repositories/ArchHaskell](/index.php/Unofficial_user_repositories/ArchHaskell "Unofficial user repositories/ArchHaskell") for details.

### cabal-install

[cabal-install](https://www.archlinux.org/packages/?name=cabal-install) is available from the [official repositories](/index.php/Official_repositories "Official repositories").

**Note:** `cabal-install` is the package that contains the "cabal" command-line utility, whereas `Cabal` is the package that provides the "Cabal" library, used by both cabal-install and stack.

#### Preparation and $PATH

To run user-wide executables installed by cabal-install, `~/.cabal/bin` must be added to the `$PATH` variable. That can be done by putting the following line in your shell configuration file, for instance `~/.bashrc` for [bash](https://www.archlinux.org/packages/?name=bash) or `~/.zshrc` for [zsh](https://www.archlinux.org/packages/?name=zsh):

 `PATH=$PATH:~/.cabal/bin` 

#### Installing packages user-wide

```
$ cabal update

$ # Dynamic linking
$ cabal install --disable-library-vanilla --enable-shared --enable-executable-dynamic *<pkg>*

$ # Static linking (requires ghc-static and ghc-pristine)
$ cabal install --with-compiler=/usr/share/ghc-pristine/bin/ghc *<pkg>*
```

It is possible to install a package system-wide with the `--global` flag, but this is **strongly discouraged**. With the user-wide install, all files are kept in `~/.cabal` and libraries are registered to `~/.ghc`, offering the possibility to do a clean-up easily by simply removing these folders. With system-wide install, the files will be dispersed in the file system and difficult to manage.

#### Sandboxes

Cabal sandboxes provide a *consistent* local package database and environment (similar to virtual-env in Python or rvm in Ruby). To create a sandbox in the current directory, run:

 `cabal sandbox init` It can be later removed using `cabal sandbox delete` 

By default, if the current directory contains a sandbox, cabal will take advantage of it for installation, so you can follow the same steps as [#Installing packages user-wide](#Installing_packages_user-wide). If you want to use a sandbox elsewhere, you can – while the current directory contains the sandbox – run `cabal exec "$SHELL"` to start a sandbox-aware shell. Then you can change the directory to wherever you want, and cabal will still use the sandbox. Alternatively, you can pass the `--sandbox-config-file=*/somewhere*/cabal.sandbox.config` flag to cabal.

To run executables within a cabal sandbox, you must also set `PATH=$PATH:$PWD/.cabal-sandbox/bin` or start a local shell with `cabal exec "$SHELL"`.

#### Removing packages

There is no easy way to do it. Cabal does not have support this functionality.

Consider installing to a sandbox instead, which can be deleted without affecting other sandboxes or your user-wide installation.

One thing to make your life easier is use zsh auto completion to find all the Haskell packages.

If you want/can fix/reinstall whole user-wide Haskell package system - remove `~/.cabal` and `~/.ghc` and start from scratch. This is often necessary when GHC is upgraded.

### stack

[Stack](https://haskellstack.org) is a build tool that focuses on automatically curated, consistent package sets rather than dependency resolution. This means it's easy to install a set of packages without concern of version conflicts as long as they coexist within a given Stackage snapshot. It can be installed through either [stack](https://www.archlinux.org/packages/?name=stack), [stack-static](https://aur.archlinux.org/packages/stack-static/) or [stack-bin](https://aur.archlinux.org/packages/stack-bin/). The latter provides statically linked binaries, thereby avoiding dozens of `haskell-*` dependencies. More information can be found at [§ Install/upgrade # Arch Linux](https://docs.haskellstack.org/en/stable/install_and_upgrade/#arch-linux).

## See also

*   [Learn You a Haskell for Great Good!](http://learnyouahaskell.com/)
*   [Real World Haskell](http://book.realworldhaskell.org/)