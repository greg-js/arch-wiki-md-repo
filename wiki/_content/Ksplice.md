# Ksplice

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Ksplice is an open source extension of the Linux kernel which allows system administrators to apply security patches to a running kernel without having to reboot the operating system.

## Installation

Install the [ksplice-git](https://aur.archlinux.org/packages/ksplice-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ksplice-git)]</sup> package from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

## Usage

First, you need the kernel source tree for the kernel you are currently running, and some files from the previous kernel build: `System.map` and `.config`.

If you don't have `System.map` from the previous build, you can copy `/proc/kallsyms` as an equivalent. If the `kernel.kptr_restrict` kernel parameter is enabled, remember to copy it as root.

This example makes use of the `--diffext` option which creates a patch based on the differences between the old and the new source files.

Make a `ksplice` directory in the kernel source tree, copy `System.map` over from the previous build, and copy `.config` into the tree if it is not already in the source tree:

```
# mkdir -p src/ksplice
# cp System.map src/ksplice
# cp .config src/

```

Create a ksplice patch and wait for the kernel to rebuild. All files that end with `new` will be compiled into the ksplice patch. C source files, for example, should end in `.cnew` as the diffext is appended directly.

```
# ksplice-create --diffext=new src/

```

Apply the newly generated patch to the running kernel:

```
# ksplice-apply ksplice-*.tar.gz

```

See man pages for `ksplice-apply`, `ksplice-create`, `ksplice-view`, and `ksplice-undo`.

## See also

*   [Ksplice GitHub](https://github.com/jirislaby/ksplice)
*   [Ksplice on Wikipedia](https://en.wikipedia.org/wiki/Ksplice)
*   [Offical website of Ksplice Uptrack](http://www.ksplice.com/) (proprietary, owned by Oracle)
*   [How to use the Ksplice raw utilities](http://cormander.com/2011/08/how-to-use-the-ksplice-raw-utilities/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Ksplice&oldid=392319](https://wiki.archlinux.org/index.php?title=Ksplice&oldid=392319)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Kernel](/index.php/Category:Kernel "Category:Kernel")
*   [Security](/index.php/Category:Security "Category:Security")