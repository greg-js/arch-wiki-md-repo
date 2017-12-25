[PRoot](https://proot-me.github.io) is program that implements functionality similar to GNU/Linux's [chroot](/index.php/Chroot "Chroot"), `mount --bind`, and binfmt_misc in user-space, allowing an unprivileged user to execute programs with an alternative root directory, much like a chroot "jail". This is useful in cases where a chroot is not possible due to a lack of root privileges.

## Installation

PRoot can be installed from the [proot](https://aur.archlinux.org/packages/proot/) package. *pacstrap* can be used to initialize the directory with an Arch environment before running *proot*.

## Usage

After installation, PRoot does not require root privileges. As with chroot, PRoot must be given a directory to act as the new root directory for the program to be run. If a program is not specified, PRoot will launch `/bin/sh` by default. Virtual filesystems do not need to be manually mounted, as PRoot handles this automatically.

```
proot -r ~/mychroot/

```

At this point a shell will start, with `/` corresponding to the `~/chroot/` directory on the host system.

Paths may be explicitly bound using the `-b` option:

```
proot -b /bin/bash:/bin/sh

```

This makes the host's /bin/bash available at the guest's /bin/sh

PRoot internally utilizes the qemu user-mode emulator to allow programs to be run inside the PRoot even when they are compiled for an architecture other than the host system's.

## Security

Like chroot, PRoot provides only filesystem level isolation. Programs inside the PRoot "jail" share the same kernel, hardware, process space, and networking subsystem. chroot and PRoot are not designed to be substitutes for real [virtualization](/index.php/Virtualization "Virtualization") applications, such as hypervisors and paravirtualizers.