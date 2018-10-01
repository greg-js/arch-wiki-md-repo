# Description

Brief description of the installation and possible problems of the version 13.2.13582-9.

# Installation

Installation from [AUR](https://wiki.archlinux.org/index.php/Arch_User_Repository):

```
$ yaourt -S teamviewer

```

# Possible problems

I encountered only one problem, the login and password windows were not active and there was no connection with the server of Teamviewer itself. The solution turned out to be simple, for this you need to start the service:

```
# systemctl start teamviewerd

```