# Citadel groupware

Related articles

*   [Simple Virtual User Mail System](/index.php/Simple_Virtual_User_Mail_System "Simple Virtual User Mail System")
*   [Postfix](/index.php/Postfix "Postfix")

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

First [Install](/index.php/Install "Install") the following dependences:

```
   pacman -S curl expat libical libsieve perl-berkeleydb

```

Then run the easy install script with curl:

```
  curl http://easyinstall.citadel.org/install | sh

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Citadel_groupware&oldid=412053](https://wiki.archlinux.org/index.php?title=Citadel_groupware&oldid=412053)"