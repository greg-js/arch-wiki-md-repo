[Citadel](http://www.citadel.org/) is a groupware and collaboration suit that offers some of the following features (among many more)

*   full email server
*   calendar/scheduling
*   address books
*   bulletin boards (forums)
*   mailing list server
*   instant messaging
*   wiki and blog engines
*   multiple domain support
*   a powerful web interface
*   rss aggregation
*   instant messaging,
*   SSL support

This guide will help you install and configure Citadel groupware server and web interface.

## Installing

[Install](/index.php/Install "Install") the [libcitadel](https://aur.archlinux.org/packages/libcitadel/), [citadel](https://aur.archlinux.org/packages/citadel/) and [webcit](https://aur.archlinux.org/packages/webcit/) packages.

or manually install following dependences:

```
   pacman -S curl expat libical libsieve perl-berkeleydb

```

Then run the easy install script with curl:

```
  curl http://easyinstall.citadel.org/install | sh

```