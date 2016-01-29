# RetroShare

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Numerous [Help:Style](/index.php/Help:Style "Help:Style") violations. (Discuss in [Talk:RetroShare#](https://wiki.archlinux.org/index.php/Talk:RetroShare))

**RetroShare** – open source, cross-platform [Friend-to-Friend](https://en.wikipedia.org/wiki/Friend-to-friend) application that offers secure chat and file sharing features.

## Contents

*   [1 Installation from unofficial repository](#Installation_from_unofficial_repository)
*   [2 Installation from AUR](#Installation_from_AUR)
*   [3 Usage](#Usage)
*   [4 External Links](#External_Links)

## Installation from unofficial repository

1\. Add this repo:

```
/etc/pacman.conf
------------------------------

[home_AsamK_RetroShare_Arch_Extra]
SigLevel = Never
Server = [http://download.opensuse.org/repositories/home:/AsamK:/RetroShare/Arch_Extra/$arch](http://download.opensuse.org/repositories/home:/AsamK:/RetroShare/Arch_Extra/$arch)

```

2\. Install RetroShare:

```
# pacman -Syu
# pacman -S home_AsamK_RetroShare_Arch_Extra/retroshare06

```

## Installation from AUR

RetroShare is available in the [retroshare-git](https://aur.archlinux.org/packages/retroshare-git/)<sup><small>AUR</small></sup> package providing compilation from source.

Note: this is unstable package! This package may not work!

## Usage

First, you have to create new profile. Then you need to explicitly add friends to be able to connect to them. In order to connect to your friends you need to exchange your certificates.

## External Links

*   [RetroShare Homepage](http://retroshare.sourceforge.net/)
*   [RetroShare Wikipedia entry](http://en.wikipedia.org/wiki/RetroShare)

Retrieved from "[https://wiki.archlinux.org/index.php?title=RetroShare&oldid=397111](https://wiki.archlinux.org/index.php?title=RetroShare&oldid=397111)"