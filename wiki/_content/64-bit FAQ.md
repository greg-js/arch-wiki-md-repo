# 64-bit FAQ

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Below is a list of frequently asked questions about Arch Linux on 64-bit.

## Contents

*   [1 How do I determine if my processor is x86_64 compatible?](#How_do_I_determine_if_my_processor_is_x86_64_compatible.3F)
    *   [1.1 Linux users](#Linux_users)
    *   [1.2 Windows users](#Windows_users)
*   [2 Should I use the 32 or 64 bit version of Arch?](#Should_I_use_the_32_or_64_bit_version_of_Arch.3F)
*   [3 How can I install 64-bit Arch?](#How_can_I_install_64-bit_Arch.3F)
*   [4 Will I have all the packages from my 32-bit Arch?](#Will_I_have_all_the_packages_from_my_32-bit_Arch.3F)
*   [5 Why 64-bit?](#Why_64-bit.3F)
*   [6 Can I build 32-bit packages for i686 inside 64-bit Arch?](#Can_I_build_32-bit_packages_for_i686_inside_64-bit_Arch.3F)
*   [7 Can I switch from i686 to x86_64 without reinstalling?](#Can_I_switch_from_i686_to_x86_64_without_reinstalling.3F)

## How do I determine if my processor is x86_64 compatible?

### Linux users

If your processor is [x86_64](https://en.wikipedia.org/wiki/X86-64 "wikipedia:X86-64") compatible, you will have the `lm` flag in `/proc/cpuinfo`. For example,

```
$ grep -w lm /proc/cpuinfo

```

### Windows users

Using the freeware [CPU-Z](http://www.cpuid.com/cpuz.php) you can determine whether your CPU is 64-bit compatible. CPUs with AMD's instruction set "AMD64" or Intel's solution "EM64T" should be compatible with the x86_64 releases and binary packages.

## Should I use the 32 or 64 bit version of Arch?

If your processor is x86_64 compatible, you should use 64-bit Arch Linux.

## How can I install 64-bit Arch?

Just use our [official installation ISO](https://www.archlinux.org/download/).

## Will I have all the packages from my 32-bit Arch?

Most official packages have 64-bit versions, though you may need to enable the [multilib](/index.php/Multilib "Multilib") repository to run some 32-bit programs. [Package Differences](https://www.archlinux.org/packages/differences/) lists the few cases where the multilib packages differ from the native 32-bit versions.

The only exception is [AUR](/index.php/AUR "AUR") packages which only have `'i686'` listed, but even then they may work for 64-bit too. Just try adding `'x86_64'` to the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").

As a last resort, you can always [install a 32-bit system inside your 64-bit system](/index.php/Install_bundled_32-bit_system_in_64-bit_system "Install bundled 32-bit system in 64-bit system").

## Why 64-bit?

It is faster under most circumstances and as an added bonus also inherently more secure due to the nature of [Address space layout randomization (ASLR)](https://en.wikipedia.org/wiki/Address_space_layout_randomization "wikipedia:Address space layout randomization") in combination with [Position-independent code (PIC)](https://en.wikipedia.org/wiki/Position-independent_code "wikipedia:Position-independent code") and the [NX Bit](https://en.wikipedia.org/wiki/NX_Bit "wikipedia:NX Bit") which is not available in the stock i686 kernel due to disabled PAE. If your computer has more than 4GB of RAM, only a 64-bit OS will be able to fully utilize it.

Programmers also increasingly tend to care less about 32-bit ("legacy") as "new" x86 CPUs typically support the 64-bit extensions.

There are many more reasons we could list here to tell you to avoid 32-bit, but between the kernel, userspace and individual programs it is simply not viable to list every last thing that 64-bit does much better these days.

## Can I build 32-bit packages for i686 inside 64-bit Arch?

Yes. You can use the [multilib](/index.php/Multilib "Multilib") repository with a [makepkg config](/index.php/Makepkg#Build_32-bit_packages_on_a_64-bit_system "Makepkg") or [install a 32-bit system inside your 64-bit system](/index.php/Install_bundled_32-bit_system_in_64-bit_system "Install bundled 32-bit system in 64-bit system").

## Can I switch from i686 to x86_64 without reinstalling?

No. All packages need to be reinstalled for the new architecture and configuration changes may be necessary. However, you do not need to repartition or reformat your hard drives during installation, so it possible to migrate all of your old data. A forum thread has been created [here](https://bbs.archlinux.org/viewtopic.php?id=64485) which outlines steps taken to migrate an install from 32 to 64 bit without losing any configurations/settings/data using a large external hard drive.

However, you can also start the system with the 64-bit installation ISO, mount the disk, backup anything you may want to keep that is not a 32-bit binary (e.g: `/home` & `/etc`), and install.

You may also want to read [Migrating Between Architectures Without Reinstalling](/index.php/Migrating_Between_Architectures_Without_Reinstalling "Migrating Between Architectures Without Reinstalling").

Retrieved from "[https://wiki.archlinux.org/index.php?title=64-bit_FAQ&oldid=413636](https://wiki.archlinux.org/index.php?title=64-bit_FAQ&oldid=413636)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [About Arch](/index.php/Category:About_Arch "Category:About Arch")