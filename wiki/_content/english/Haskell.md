[Haskell](http://www.haskell.org) is a general purpose, purely functional, programming language.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Compiler](#Compiler)
    *   [1.2 Problems with linking](#Problems_with_linking)
    *   [1.3 Building statically linked packages with Cabal (without using shared libraries)](#Building_statically_linked_packages_with_Cabal_.28without_using_shared_libraries.29)
    *   [1.4 Haskell development tools](#Haskell_development_tools)
*   [2 Managing Haskell packages](#Managing_Haskell_packages)
    *   [2.1 Pros/Cons of the different methods](#Pros.2FCons_of_the_different_methods)
    *   [2.2 ArchHaskell repository](#ArchHaskell_repository)
    *   [2.3 cabal-install](#cabal-install)
        *   [2.3.1 Preparation and $PATH](#Preparation_and_.24PATH)
        *   [2.3.2 Installing packages](#Installing_packages)
        *   [2.3.3 Removing packages](#Removing_packages)
*   [3 See also](#See_also)

## Installation

Haskell generates machine code that can be run natively on Linux. There is nothing special required to run a binary (already compiled) software, like the ones provided in the [official repositories](/index.php/Official_repositories "Official repositories") or by the [ArchHaskell](/index.php/ArchHaskell "ArchHaskell") group. On the other side, [AUR](/index.php/AUR "AUR") packages or source codes requires a compiler to build the software.

Installing the compiler alone permits to build Haskell source code. A few additional tools are needed for development work.

### Compiler

To build a Haskell source–code into native–code, a compiler must be installed. There are several [implementations available](http://www.haskell.org/haskellwiki/Implementations), but the one used most (which is now *de facto* the reference) is the GHC (Glasgow Haskell Compiler). It is available in the official repositories as [ghc](https://www.archlinux.org/packages/?name=ghc).

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

### Problems with linking

GHC uses static linking by default and the `-dynamic` flag is needed to select dynamic linking. Since version [8.0.2-1](https://git.archlinux.org/svntogit/community.git/commit/trunk?h=packages/ghc&id=7a948cdfb808afd3ce6f93047ae0dc1778e79f9f), the Arch [ghc](https://www.archlinux.org/packages/?name=ghc) package no longer contains static versions of the GHC boot libraries by default, nor do any of the `haskell-*` packages . Static versions of the GHC boot libraries may be installed separately through the [ghc-static](https://www.archlinux.org/packages/?name=ghc-static) package, but no such equivalent exists for the `haskell-*` packages. Therefore, without `-dynamic` Haskell code and packages will generally fail to link unless the program depends only on boot packages and locally installed packages and [ghc-static](https://www.archlinux.org/packages/?name=ghc-static) is installed.

This also causes issues with Cabal trying to use the default static linking. To force dynamic linking in Cabal, edit `~/.cabal/config` and add the line `executable-dynamic: True`.

Dynamic linking is used for most Haskell modules packaged through [pacman](/index.php/Pacman "Pacman") and is common for packages in the [AUR](/index.php/AUR "AUR"). Since GHC provides no [ABI](https://en.wikipedia.org/wiki/Application_binary_interface "w:Application binary interface") compatibility between compiler releases, static linking is often the preferred option for local development outside of the package system.

### Building statically linked packages with Cabal (without using shared libraries)

This section explains how to install `cabal-install` but from [Hackage](https://hackage.haskell.org/package/cabal-install) instead of the official [cabal-install](https://www.archlinux.org/packages/?name=cabal-install) package from the repositories. This `cabal-install` will build Haskell packages without using [shared libraries](https://downloads.haskell.org/~ghc/latest/docs/html/users_guide/shared_libs.html) unlike the official [cabal-install](https://www.archlinux.org/packages/?name=cabal-install) which requires you to link dynamically.

**Note:** In the context of this section, static linking does not mean generating completely static ELF binaries. Only Haskell code will be linked statically into a single ELF binary, which may be dynamically linked to other system libraries such as *glibc*.

In theory with any `cabal-install` you could choose between both methods, static and dynamic, for linking your Haskell code. In practice because in Arch some basic Haskell libraries (`haskell-*` packages) are provided as shared objects (`.so` files) and those libraries are globally registered in Cabal, it has trouble using the same libraries for static linking. To avoid linking [errors](https://bugs.archlinux.org/task/54563#comment158826), it's also especially important to not to mix statically and dynamically Haskell packages installed on the same system, as Cabal doesn't fetch a required package once it has been globally registered (check them with the command `ghc-pkg list`) in one of its forms and not the other (independently of the linking type of the package that it's needed).

For these reasons, **you have to make sure** that the only two related Haskell packages you have installed are [ghc](https://www.archlinux.org/packages/?name=ghc), the compiler, and [ghc-static](https://www.archlinux.org/packages/?name=ghc-static), the boot libraries on its static form, (not [stack](https://www.archlinux.org/packages/?name=stack), [cabal-helper](https://www.archlinux.org/packages/?name=cabal-helper), [cabal-install](https://www.archlinux.org/packages/?name=cabal-install) and none of the `haskell-*` dynamic libraries [available](https://www.archlinux.org/packages/?q=haskell-) in the official repositories).

You can also use [Stack](https://www.haskellstack.org/) as an alternative build tool for Haskell packages, which will link statically by default. But if you still want to use Cabal to build using static linking, follow the next steps of this section to install your own compiled `cabal-install` from Hackage. For this purpose we are going to use the tool [Stack](https://haskellstack.org/) that will help us fetching all the dependencies required and building your own `cabal-install`.

First you have to install [stack-static](https://aur.archlinux.org/packages/stack-static/) because you'll use it to bootstrap the compilation of your own Cabal and you don't want to pull as dependencies those packages from the official Arch repositories containing the `haskell-*` dynamic libraries.

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

Although an [AUR](/index.php/AUR "AUR") package exists ([haskell-platform](https://aur.archlinux.org/packages/haskell-platform/)), the Haskell Platform can be advantageously replaced by [installing](/index.php/Installing "Installing") the [following packages](https://bbs.archlinux.org/viewtopic.php?pid=1151382#p1151382) from the [official repositories](/index.php/Official_repositories "Official repositories"):

*   ghc ([ghc](https://www.archlinux.org/packages/?name=ghc) and [ghc-static](https://www.archlinux.org/packages/?name=ghc-static)) — Compiler with dynamic [boot libraries](https://ghc.haskell.org/trac/ghc/wiki/Commentary/Libraries), and supplementary static boot libraries
*   cabal-install ([cabal-install](https://www.archlinux.org/packages/?name=cabal-install)) — A command line interface for *Cabal* and *Hackage*
*   haddock ([haskell-haddock-api](https://www.archlinux.org/packages/?name=haskell-haddock-api) and [haskell-haddock-library](https://www.archlinux.org/packages/?name=haskell-haddock-library)) — Tools for generating documentation
*   happy ([happy](https://www.archlinux.org/packages/?name=happy)) — Parser generator
*   alex ([alex](https://www.archlinux.org/packages/?name=alex)) — Lexical analyzer generator

Alternatively, you can use [stack](https://www.archlinux.org/packages/?name=stack) to manage your Haskell environment by following the [Arch Linux install instructions](https://docs.haskellstack.org/en/stable/install_and_upgrade/#arch-linux).

## Managing Haskell packages

Many Haskell libraries and executables are grouped in packages. They are all available on [Hackage](http://hackage.haskell.org). To install and manage these packages, several methods are available and unusual ones are explained in the rest of this section.

The recommended workflow is the following:

*   [Official repositories](/index.php/Official_repositories "Official repositories") or [ArchHaskell repository](/index.php/ArchHaskell "ArchHaskell") as principal source of Haskell packages (the *or* is exclusive here)
*   [cabal-install](#cabal-install) (possibly with sandboxes) for Haskell development
*   [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") for packages that are not available elsewhere

[cblrepo](https://github.com/magthe/cblrepo) is a tool used for maintaining Haskell packages for Linux distributions. A wrapper around this, [cabal2pkgbuild-git](https://aur.archlinux.org/packages/cabal2pkgbuild-git/), can create PKGBUILD files from Hackage packages. See [Haskell package guidelines](/index.php/Haskell_package_guidelines "Haskell package guidelines") for more information on *creating new* Haskell packages.

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

**Note:** The only exception is for Haskell development, where [cabal-install](https://www.archlinux.org/packages/?name=cabal-install) is the recommended tool. Since version 1.18, cabal provides a *sandbox* system that permits to isolate different versions of libraries for different projects. There is an introduction to cabal sandbox [here](http://coldwa.st/e/blog/2013-08-20-Cabal-sandbox.html).

#### Preparation and $PATH

Install [cabal-install](https://www.archlinux.org/packages/?name=cabal-install) from the [official repositories](/index.php/Official_repositories "Official repositories").

To run installed executables without specifying the path, the cabal binary folder `~/.cabal/bin` must be added to the `$PATH` variable. That can be done by putting the following line in your shell configuration file, for instance `~/.bashrc` for [bash](https://www.archlinux.org/packages/?name=bash) or `~/.zshrc` for [zsh](https://www.archlinux.org/packages/?name=zsh):

 `PATH=$PATH:~/.cabal/bin` To run executables within a cabal sandbox, you must also add `PATH=$PATH:.cabal-sandbox/bin` 

#### Installing packages

```
$ cabal update

$ # When using ghc-static
$ cabal install <pkg>

$ # When using ghc
$ cabal install\
	--enable-shared
	--enable-executable-dynamic
	--ghc-options≈-dynamic
	<pkg>

```

It is possible to install a package system–wide with the `--global` flag, but this is **strongly discouraged**. With the user–wide install, all files are kept in `~/.cabal` and libraries are registered to `~/.ghc`, offering the possibility to do a clean-up easily by simply removing these folders. With system–wide install, the files will be dispersed in the file system and difficult to manage.

#### Removing packages

There is no easy way to do it. Cabal does not have removing process.

One thing to make your life easier is use zsh auto completion to find all the haskell packages.

If you want/can fix/reinstall whole Haskell package system - remove `~/.cabal` and `~/.ghc` and start from scratch.

## See also

*   [Learn You a Haskell for Great Good!](http://learnyouahaskell.com/)
*   [Real World Haskell](http://book.realworldhaskell.org/)