[arch-bootstrap.sh](https://raw.githubusercontent.com/tokland/arch-bootstrap/master/arch-bootstrap.sh) is a Bash script that creates a minimum Arch Linux system where you can chroot to. Bootstrapping for other architectures than the host architecture requires static compiled [QEMU](http://www.qemu.org) binaries registered in Linux [binfmt_misc](https://en.wikipedia.org/wiki/Binfmt_misc "wikipedia:Binfmt misc"). More info about arm on x86_64 [here](http://tinkering-is-fun.blogspot.de/2009/12/running-arm-linux-on-your-desktop-pc_12.html). Report bugs [here](https://github.com/tokland/arch-bootstrap/issues).

## Installing Arch

Some examples:

*   Using default architecture (i686) and repository:

```
# bash arch-bootstrap.sh target

```

*   Bootstrap a *x86_64* system using a specific repository:

```
# bash arch-bootstrap.sh -a x86_64 -r "[ftp://ftp.archlinux.org](ftp://ftp.archlinux.org)" target

```

## See also

*   Port for sh4 CPU: [http://code.google.com/p/sh4twbox](http://code.google.com/p/sh4twbox).