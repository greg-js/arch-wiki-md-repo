The [Common Desktop Environment](https://en.wikipedia.org/wiki/Common_Desktop_Environment "wikipedia:Common Desktop Environment") is a desktop environment for Unix and OpenVMS, based on the Motif widget toolkit. It was part of the UNIX98 Workstation Product Standard, and was long the "classic" Unix desktop associated with commercial Unix workstations. Despite being a legacy environment, it is still kept alive with support for Linux systems as well.

**Warning:** Running CDE on Linux is extremely experimental, has several known security issues, and requires some system modifications which are insecure. It is advisable to run CDE only under controlled settings (e.g. inside a VM) and never for real-life usage.

**Note:** CDE is only supported on 32-bit systems, 64-bit support is still experimental.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Modifications](#Modifications)
*   [2 Usage](#Usage)
    *   [2.1 dtlogin](#dtlogin)
    *   [2.2 xinit](#xinit)
*   [3 References](#References)

## Installation

The base CDE system is installed through the [cdesktopenv](https://aur.archlinux.org/packages/cdesktopenv/) AUR package. After package installation, some modifications are required.

### Modifications

The `rpcbind` service must be set to insecure mode:

 `/etc/conf.d/rpcbind`  `RPCBIND_ARGS="-i"` 

This change requires a [restart](/index.php/Restart "Restart") of `rpcbind.service`.

## Usage

### dtlogin

The [cdesktopenv](https://aur.archlinux.org/packages/cdesktopenv/) package supplies the `dtlogin` systemd service which upon starting will launch the CDE login manager.

### xinit

CDE can be directly launched with `startx` (install [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit)):

```
$ export PATH=$PATH:/usr/dt/bin
$ export LANG=C
$ startx /usr/dt/bin/Xsession

```

## References

*   [Common Desktop Environment Wiki](http://sourceforge.net/p/cdesktopenv/wiki/Home/)