# HP Mini 311c

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:HP Mini 311c#](https://wiki.archlinux.org/index.php/Talk:HP_Mini_311c))

## Contents

*   [1 Before installation](#Before_installation)
*   [2 Installation](#Installation)
*   [3 FIRST BOOT](#FIRST_BOOT)
*   [4 Another device](#Another_device)

#### Before installation

Before installation of archlinux you need to activate Wake On Lan on your BIOS , if you not make it, your ethernet controller not work on Linux if your ethernet cable is not connected on Windows

#### Installation

Installation on this computer is very similar to a standard archlinux installation, but you need to blacklist the b43 module, if you not make it, udev crash at reboot in your new OS, edit the /etc/rc.conf file with

```
  …
  MOD BLACKLIST=(b43)
  …

```

#### FIRST BOOT

Now you boot on your new archlinux, install wireless with the [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/)<sup><small>AUR</small></sup> package.

(WARNING : This module is not a free module but propietary) After installation edit your rc.conf, remove blacklisted module and add at MODULES line :

```
  MODULES=(lib80211 wl !b43 !ssb)

```

And restart If problem : If after restart your wirless don’t work, verify if wireless is activate (the orange led need to be blue)

#### Another device

Sound work out of box but i recommand install and use of PulseAudio ION is supported by nvidia drivers For get hardward acceleration working with mplayer, you need to get ffmpeg-vdpau and mplayer-svn from AUR

Retrieved from "[https://wiki.archlinux.org/index.php?title=HP_Mini_311c&oldid=390558](https://wiki.archlinux.org/index.php?title=HP_Mini_311c&oldid=390558)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [HP](/index.php/Category:HP "Category:HP")