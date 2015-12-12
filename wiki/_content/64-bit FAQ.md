# 64-bit FAQ

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Below is a list of frequently asked questions about Arch Linux on 64-bit.

## Contents

*   [1 How do I determine if my processor is x86_64 compatible?](#How_do_I_determine_if_my_processor_is_x86_64_compatible.3F)
    *   [1.1 Linux users](#Linux_users)
    *   [1.2 Windows users](#Windows_users)
*   [2 Should I use the 32 or 64 bit version of Arch?](#Should_I_use_the_32_or_64_bit_version_of_Arch.3F)
*   [3 How can I install Arch64?](#How_can_I_install_Arch64.3F)
*   [4 How complete is the port?](#How_complete_is_the_port.3F)
*   [5 Will I have all the packages from my 32-bit Arch I am used to?](#Will_I_have_all_the_packages_from_my_32-bit_Arch_I_am_used_to.3F)
*   [6 Why 64-bit?](#Why_64-bit.3F)
*   [7 What repositories should I set up for pacman to use?](#What_repositories_should_I_set_up_for_pacman_to_use.3F)
*   [8 What will I miss in Arch64?](#What_will_I_miss_in_Arch64.3F)
*   [9 Can I run 32-bit apps inside Arch64?](#Can_I_run_32-bit_apps_inside_Arch64.3F)
*   [10 Can I build 32-bit packages for i686 inside Arch64?](#Can_I_build_32-bit_packages_for_i686_inside_Arch64.3F)
    *   [10.1 Multilib repository](#Multilib_repository)
    *   [10.2 Chroot](#Chroot)
*   [11 Can I upgrade/switch my system from i686 to x86_64 without reinstalling?](#Can_I_upgrade.2Fswitch_my_system_from_i686_to_x86_64_without_reinstalling.3F)

## How do I determine if my processor is x86_64 compatible?

### Linux users

Run the following command:

```
$ less /proc/cpuinfo

```

Look for the `flags` entry. If you see the `lm` flag then your processor is x86_64 compatible.

Or you can run this command:

```
$ grep -q "^flags.*\blm\b" /proc/cpuinfo && echo "x86_64" || echo "not x86_64"

```

### Windows users

Using the freeware [CPU-Z](http://www.cpuid.com/cpuz.php) you can determine whether your CPU is 64-bit compatible. CPUs with AMD's instruction set "AMD64" or Intel's solution "EM64T" should be compatible with the x86_64 releases and binary packages.

## Should I use the 32 or 64 bit version of Arch?

If your processor is [x86_64](https://en.wikipedia.org/wiki/X86-64 "wikipedia:X86-64") compatible, you should use Arch64.

## How can I install Arch64?

Just use our [official installation ISO CD](https://www.archlinux.org/download/).

## How complete is the port?

The port is ready for daily use in a desktop or server environment.

## Will I have all the packages from my 32-bit Arch I am used to?

The repositories are ported and pretty much everything should work as expected.

Rarely, an old package in the [AUR](/index.php/AUR "AUR") will only have `'i686'` listed, but typically they work for 64-bit too. Just try adding `'x86_64'`.

## Why 64-bit?

It is faster under most circumstances and as an added bonus also inherently more secure due to the nature of [Address space layout randomization (ASLR)](https://en.wikipedia.org/wiki/Address_space_layout_randomization "wikipedia:Address space layout randomization") in combination with [Position-independent code (PIC)](https://en.wikipedia.org/wiki/Position-independent_code "wikipedia:Position-independent code") and the [NX Bit](https://en.wikipedia.org/wiki/NX_Bit "wikipedia:NX Bit") which is not available in the stock i686 kernel due to disabled PAE. If your computer is running 4 GB or more of usable RAM, 64-bit should be strongly considered as any additional RAM cannot be allocated by a 32-bit OS.

Programmers also increasingly tend to care less about 32-bit ("legacy") as "new" x86 CPUs typically support the 64-bit extensions.

There are many more reasons we could list here to tell you to avoid 32-bit, but between the kernel, userspace and individual programs it is simply not viable to list every last thing that 64-bit does much better these days.

For further details watch our [differences reports](https://www.archlinux.org/packages/differences/). There you will find a list comparing 32-/64-bit package versions.

## What repositories should I set up for pacman to use?

All repositories are supported for the port.

## What will I miss in Arch64?

Nothing, really. Almost all applications support 64-bit by now or are in the transition to become 64-bit compatible.

The biggest problem are packages that are either **closed source** or contain x86-specific assembly that is cumbersome to port to 64-bit (typical for emulators).

For a quick overview on which currently installed packages from aur may need fixing, run the following (requires cower):

```
pacman -Q|while read -r pkg pkgver; do curl -s "[https://aur.archlinux.org/cgit/aur.git/plain/PKGBUILD?h=${pkg}](https://aur.archlinux.org/cgit/aur.git/plain/PKGBUILD?h=${pkg})" | grep 'arch=(' | sed 's/any/x86_64/' | grep -qv 'x86_64' && echo "$pkg is missing x86_64 in @arch on aur (possible candidates: $(cower -s $pkg --format "%n\n" | grep -E '64$|^lib32|^bin32'| tr '\n' ' '))"; done

```

These applications were previously problematic but are now available in the [AUR](/index.php/AUR "AUR") and work fine:

*   Acrobat Reader is not available in 64-bit, but you can run the 32-bit version in compatibility mode. There are also many other open source alternatives that can be used to read PDF files.

Everything else should work perfectly fine. If you miss any Arch32 package in our port and you know that it will compile on x86_64 (perhaps you have found it as native packages in another 64-bit distribution), just contact the developers or request a new package in the forums.

## Can I run 32-bit apps inside Arch64?

Yes! You can install `lib32-*` packages from the [multilib](/index.php/Multilib "Multilib") repository.

An alternative method is to create a 32-bit chroot (refer to [Install bundled 32-bit system in Arch64](/index.php/Install_bundled_32-bit_system_in_Arch64 "Install bundled 32-bit system in Arch64"))

## Can I build 32-bit packages for i686 inside Arch64?

Yes. You can either use

*   the [Multilib](/index.php/Multilib "Multilib") versions of the relevant packages or
*   an [i686 chroot](/index.php/Install_bundled_32-bit_system_in_Arch64 "Install bundled 32-bit system in Arch64").

### Multilib repository

First, enable the Multilib repository as described in [Multilib](/index.php/Multilib "Multilib"). Then [install](/index.php/Install "Install") the [gcc-multilib](https://www.archlinux.org/packages/?name=gcc-multilib) package.

**Note:**

*   If the system has the [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) package group installed, users must replace the [extra] versions with the [multilib] versions as shown below.
*   [gcc-multilib](https://www.archlinux.org/packages/?name=gcc-multilib) is capable of building 32-bit and 64-bit code. You can safely install [multilib-devel](https://www.archlinux.org/groups/x86_64/multilib-devel/) to replace the packages shown below, but you still need [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) for the other packages it includes. See [https://bbs.archlinux.org/viewtopic.php?id=102828](https://bbs.archlinux.org/viewtopic.php?id=102828) for more information.

Compiling packages on x86_64 for i686 is as easy as adding the following lines to an alternate configuration file (e.g. `~/.makepkg.i686.conf`)

```
CARCH="i686"
CHOST="i686-pc-linux-gnu"
CFLAGS="-m32 -march=i686 -mtune=generic -O2 -pipe -fstack-protector-strong --param=ssp-buffer-size=4 -D_FORTIFY_SOURCE=2"
CXXFLAGS="${CFLAGS}"
LDFLAGS="-m32 -Wl,-O1,--sort-common,--as-needed,-z,relro"                                                                                                           

```

and invoking makepkg via the following

```
$ linux32 makepkg -src --config ~/.makepkg.i686.conf

```

### Chroot

See [Install bundled 32-bit system in Arch64](/index.php/Install_bundled_32-bit_system_in_Arch64 "Install bundled 32-bit system in Arch64")

## Can I upgrade/switch my system from i686 to x86_64 without reinstalling?

No. Strictly speaking any kind of migration implies that all packages or nearly all packages must be reinstalled for the newer architecture. However, it is possible to move your system without performing a fresh install, and even from within your current installation. A forum thread has been created [here](https://bbs.archlinux.org/viewtopic.php?id=64485) which outlines steps taken to successfully migrate an install from 32 to 64 bit without losing any configurations/settings/data. Note: A large external hard drive was used for the transfer.

However, you can also start the system with the Arch64 installation CD, mount the disk, backup anything you may want to keep that is not a 32-bit binary (e.g: `/home` & `/etc`), and install.

You may also want to read [Migrating Between Architectures Without Reinstalling](/index.php/Migrating_Between_Architectures_Without_Reinstalling "Migrating Between Architectures Without Reinstalling").

Retrieved from "[https://wiki.archlinux.org/index.php?title=64-bit_FAQ&oldid=411499](https://wiki.archlinux.org/index.php?title=64-bit_FAQ&oldid=411499)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [About Arch](/index.php/Category:About_Arch "Category:About Arch")