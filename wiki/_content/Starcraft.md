# Starcraft

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This page is about the 1998 Starcraft, if you are looking for Starcraft 2, go [here](/index.php/Starcraft2 "Starcraft2").

## Installation

Simple steps to install and run StarCraft on Linux:

1.  Install and configure [Wine](/index.php/Wine "Wine")
2.  Run winecfg
3.  On the drives tab, click Autodetect
4.  Click "Show Advanced"
5.  Select the drive letter representing your optical drive
6.  Change type to CD-ROM
7.  On the Audio tab, I had to click OSS Driver (instead of Alsa) and check "Driver Emulation"

Install StarCraft:

1.  mount starcraft disc ($ mount /media/dvd)
2.  cd /media/dvd
3.  wine install.exe (install as you normally would)

At this point, the game should run fine. My StarCraft disc installs an older version which only supports IPX networking. I downloaded the latest patch from blizzard and ran it using Wine. It patched StarCraft to allow TCP networking, which worked flawlessly.

## Troubleshooting

If game works slow try downloading cnc-ddraw from [this page](http://hifi.iki.fi/cnc-ddraw/#download), placing in the game directory and overwriting library in winecfg for starcraft.

If the Audio tab could not detect OSS, even if you manually try to select this in regedit, you could try to use wine-staging from [this page](https://aur.archlinux.org/packages/wine-staging/). Then, select the "Staging" tab and check "Enable Environmental Audio Extensions (EAX)".

## See Also

*   [WineHQ's AppDB entry for StarCraft](http://appdb.winehq.org/objectManager.php?sClass=application&iId=72)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Starcraft&oldid=400630](https://wiki.archlinux.org/index.php?title=Starcraft&oldid=400630)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Gaming](/index.php/Category:Gaming "Category:Gaming")
*   [Wine](/index.php/Category:Wine "Category:Wine")