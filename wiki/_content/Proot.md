# Proot

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[proot](http://proot.me/) is program that implements functionality similar to GNU/Linux's [chroot](/index.php/Chroot "Chroot"), `mount --bind`, and binfmt_misc in user-space, allowing an unprivileged user to execute programs with an alternative root directory, much like a chroot "jail". This is useful in cases where a chroot is not possible due to a lack of root privileges.

## Installation

proot can be installed from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") under the package [proot](https://aur.archlinux.org/packages/proot/). [pacstrap](/index.php?title=Pacstrap&action=edit&redlink=1 "Pacstrap (page does not exist)") can be used to initialize the directory with an Arch environment before running proot.

## Usage

After installation, proot does not require root privileges. As with chroot, proot must be given a directory to act as the new root directory for the program to be run. If a program is not specified, proot will launch `/bin/sh` by default. Virtual filesystems do not need to be manually mounted, as proot handles this automatically.

```
proot -r ~/mychroot/

```

At this point a shell will start, with `/` corresponding to the `~/chroot/` directory on the host system.

Paths may be explicitly bound using the `-b` option:

```
proot -b /bin/bash:/bin/sh

```

This makes the host's /bin/bash available at the guest's /bin/sh

proot internally utilizes the qemu user-mode emulator to allow programs to be run inside the proot even when they are compiled for an architecture other than the host system's.

## Security

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Compare security of chroot and proot: Are /proc, /sys, and /dev accessible inside a proot? Is privilege escalation possible? (Discuss in [Talk:Proot#](https://wiki.archlinux.org/index.php/Talk:Proot))

Like chroot, proot provides only filesystem level isolation. Programs inside the proot "jail" share the same kernel, hardware, process space, and networking subsystem. chroot and proot are not designed to be substitutes for real [virtualization](/index.php?title=Virtualization&action=edit&redlink=1 "Virtualization (page does not exist)") applications, such as hypervisors and paravirtualizers.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Proot&oldid=408371](https://wiki.archlinux.org/index.php?title=Proot&oldid=408371)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Security](/index.php/Category:Security "Category:Security")