# Haskell

[Haskell](http://www.haskell.org) is a general purpose, purely functional, programming language.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Compiler](#Compiler)
    *   [1.2 Haskell development tools](#Haskell_development_tools)
*   [2 Managing Haskell packages](#Managing_Haskell_packages)
    *   [2.1 Pros/Cons of the different methods](#Pros.2FCons_of_the_different_methods)
    *   [2.2 ArchHaskell repository](#ArchHaskell_repository)
    *   [2.3 cabal-install](#cabal-install)
        *   [2.3.1 Preparation and $PATH](#Preparation_and_.24PATH)
        *   [2.3.2 Installing packages](#Installing_packages)
        *   [2.3.3 Removing packages](#Removing_packages)

## Installation

Haskell generates machine code that can be run natively on Linux. There is nothing special required to run a binary (already compiled) software, like the ones provided in the [official repositories](/index.php/Official_repositories "Official repositories") or by the [ArchHaskell](/index.php/ArchHaskell "ArchHaskell") group. On the other side, [AUR](/index.php/AUR "AUR") packages or source codes requires a compiler to build the software.

Installing the compiler alone permits to build Haskell source code. A few additional tools are needed for development work.

### Compiler

To build a Haskell source–code into native–code, a compiler must be installed. There are several [implementations available](http://www.haskell.org/haskellwiki/Implementations), but the one used most (which is now _de facto_ the reference) is the GHC (Glasgow Haskell Compiler). It is available in the official repositories as [ghc](https://www.archlinux.org/packages/?name=ghc).

You can try it with the following file:

 `Main.hs`  `main = putStrLn "Hello, World"` 

and by running:

```
$ ghc Main.hs
$ ./Main 
```

```
Hello, World

```

### Haskell development tools

To start developing in Haskell easily, one option is the [haskell-platform](http://www.haskell.org/platform/) bundle which is described as:

	_The easiest way to get started with programming Haskell. It comes with all you need to get up and running. Think of it as "Haskell: batteries included"._

Although an [AUR](/index.php/AUR "AUR") package exists ([haskell-platform](https://aur.archlinux.org/packages/haskell-platform/)), the Haskell Platform can be advantageously replaced by [installing](/index.php/Installing "Installing") the [following packages](https://bbs.archlinux.org/viewtopic.php?pid=1151382#p1151382) from the [official repositories](/index.php/Official_repositories "Official repositories"):

*   ghc ([ghc](https://www.archlinux.org/packages/?name=ghc)) — The compiler
*   cabal-install ([cabal-install](https://www.archlinux.org/packages/?name=cabal-install)) — A command line interface for _Cabal_ and _Hackage_
*   haddock ([haddock](https://www.archlinux.org/packages/?name=haddock)) — Tools for generating documentation
*   happy ([happy](https://www.archlinux.org/packages/?name=happy)) — Parser generator
*   alex ([alex](https://www.archlinux.org/packages/?name=alex)) — Lexical analyzer generator

## Managing Haskell packages

Many Haskell libraries and executables are grouped in packages. They are all available on [Hackage](http://hackage.haskell.org). To install and manage these packages, several methods are available and unusual ones are explained in the rest of this section.

The recommended workflow is the following:

*   [Official repositories](/index.php/Official_repositories "Official repositories") or [ArchHaskell repository](/index.php/ArchHaskell "ArchHaskell") as principal source of Haskell packages (the _or_ is exclusive here)
*   [cabal-install](#cabal-install) (possibly with sandboxes) for Haskell development
*   [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") for packages that are not available elsewhere

[cblrepo](https://github.com/magthe/cblrepo) is a tool used for maintaining Haskell packages for Linux distributions. A wrapper around this, [cabal2pkgbuild-git](https://aur.archlinux.org/packages/cabal2pkgbuild-git/), can create PKGBUILD files from Hackage packages. See [Haskell package guidelines](/index.php/Haskell_package_guidelines "Haskell package guidelines") for more information on _creating new_ Haskell packages.

### Pros/Cons of the different methods

The following table documents the advantages and disadvantages of different package management styles.

| **Method** | **Pros** | **Cons** |
| [Official repositories](/index.php/Official_repositories "Official repositories") | Provided by ArchLinux developers, consistent versions of packages, already compiled | Only a few packages available |
| [ArchHaskell repository](#ArchHaskell_repository) | Provided by ArchHaskell group, consistent versions of packages, already compiled | Need manual intervention to get started with |
| [cabal-install](#cabal-install) | All packages available | Installed in home folder, [cabal-install](https://www.archlinux.org/packages/?name=cabal-install) [is not a package manager](https://ivanmiljenovic.wordpress.com/2010/03/15/repeat-after-me-cabal-is-not-a-package-manager), incompatible versions of packages possible (aka. [cabal hell](http://www.haskell.org/haskellwiki/Cabal/Survival#What_is_the_difficulty_caused_by_Cabal-install.3F)) |
| [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") | Simple to get started | Risk of unmaintained or orphaned packages, incompatible versions of packages possible |

### ArchHaskell repository

See [ArchHaskell](/index.php/ArchHaskell "ArchHaskell") for details.

### cabal-install

**Warning:** Discouraged method, keep in mind that [cabal-install](https://www.archlinux.org/packages/?name=cabal-install) [is not a package manager](https://ivanmiljenovic.wordpress.com/2010/03/15/repeat-after-me-cabal-is-not-a-package-manager).

**Note:** The only exception is for Haskell development, where [cabal-install](https://www.archlinux.org/packages/?name=cabal-install) is the recommended tool. Since version 1.18, cabal provides a _sandbox_ system that permits to isolate different versions of libraries for different projects. There is an introduction to cabal sandbox [here](http://coldwa.st/e/blog/2013-08-20-Cabal-sandbox.html).

#### Preparation and $PATH

Install [cabal-install](https://www.archlinux.org/packages/?name=cabal-install) from the [official repositories](/index.php/Official_repositories "Official repositories").

To run installed executables without specifying the path, the cabal binary folder `~/.cabal/bin` must be added to the `$PATH` variable. That can be done by putting the following line in your shell configuration file, for instance `~/.bashrc` for [bash](https://www.archlinux.org/packages/?name=bash) or `~/.zshrc` for [zsh](https://www.archlinux.org/packages/?name=zsh):

 `PATH=$PATH:~/.cabal/bin` To run executables within a cabal sandbox, you must also add `PATH=$PATH:.cabal-sandbox/bin` 

#### Installing packages

```
$ cabal update
$ cabal install <pkg>
```

It is possible to install a package system–wide with the `--global` flag, but this is **strongly discouraged**. With the user–wide install, all files are kept in `~/.cabal` and libraries are registered to `~/.ghc`, offering the possibility to do a clean-up easily by simply removing these folders. With system–wide install, the files will be dispersed in the file system and difficult to manage.

#### Removing packages

There is no easy way to do it.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Haskell&oldid=412095](https://wiki.archlinux.org/index.php?title=Haskell&oldid=412095)"