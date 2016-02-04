# Atomic Bomberman

Atomic Bomberman is a PC game developed by Interplay and released in 1997\. It can be played on Arch using [Wine](/index.php/Wine "Wine").

## Contents

*   [1 Environment](#Environment)
*   [2 Installing Atomic bomberman](#Installing_Atomic_bomberman)
*   [3 Playing Atomic Bomberman](#Playing_Atomic_Bomberman)
*   [4 Troubleshooting](#Troubleshooting)
*   [5 References and Resources](#References_and_Resources)

## Environment

Tested with Wine 1.3.7 successfully

For network play, you need to install IPX. It can be found in aur: [ipx](https://aur.archlinux.org/packages/ipx/)

*   After this, ipx can be added to your network card like this:

```
# ipx_interface add -p eth0 802.2 0x12345678

```

*   Use `ip a` to check if network is working.

*   you can remove ipx like this (IPX is also removed when the PC is rebooted):

```
# ipx_interface del eth0 802.2

```

## Installing Atomic bomberman

Download from here: [[1]](http://www.dosgamesonline.com/index/game/650/Atomic_Bomberman.html)

Then extract the zip file, then extract the rar files. For example to c:\bomber:

```
$ unzip atomic_bomberman.zip 
$ wine bomber.part01.exe (and choose c:\ as destination )

```

## Playing Atomic Bomberman

```
$ cd ~/.wine/drive_c/bomber
$ wine BM.EXE

```

## Troubleshooting

IPX does not work on the following wireless cards:

*   Network controller: Broadcom Corporation BCM4328 802.11a/b/g/n (rev 03)
*   Network controller: Broadcom Corporation BCM4312 802.11b/g (rev 01)

IPX works fine on the following wireless card:

*   Network controller: Intel Corporation Wireless WiFi Link 5100

IPX works fine on the following wired cards:

*   Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168B PCI Express Gigabit Ethernet controller (rev 02
*   Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168B PCI Express Gigabit Ethernet controller (rev 03) )

See also this forum thread: [wine forum: IPX works via wired network, not via wireless](http://forum.winehq.org/viewtopic.php?t=10313)

## References and Resources

*   [AUR](/index.php/AUR "AUR") package: [ipx](https://aur.archlinux.org/packages/ipx/)
*   [WineHQ - Atomic Bomberman 1.0](http://appdb.winehq.org/objectManager.php?sClass=version&iId=4774&iTestingId=9967)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Atomic_Bomberman&oldid=277254](https://wiki.archlinux.org/index.php?title=Atomic_Bomberman&oldid=277254)"