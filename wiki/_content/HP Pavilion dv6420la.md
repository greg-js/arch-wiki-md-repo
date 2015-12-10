# HP Pavilion dv6420la

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [HCL/Laptops/HP](/index.php?title=HCL/Laptops/HP&action=edit&redlink=1 "HCL/Laptops/HP (page does not exist)").**

**Notes:** If information is still applicable, that is (Discuss in [Talk:HP Pavilion dv6420la#](https://wiki.archlinux.org/index.php/Talk:HP_Pavilion_dv6420la))

## Input devices

[HP Pavilion dv6018](/index.php/HP_Pavilion_dv6018 "HP Pavilion dv6018") also worked here. This is a laptop for Latin America, so their keyboard layout is "la-latin1" on rc.conf and "latam" on xorg.conf.

To use sensor keys and remote control you need to set keyboard model in /etc/X11/xorg.conf

```
   Option "XkbModel" "hpzt11xx"

```

Add this command to some startup script, /etc/rc.local in Arch Linux:

```
   setkeycodes e008 221 e00e 226 e00c 213

```

And finally add these commands to startup of your windowmanager or desktop environment. I put them to ~/.xinitrc

```
   xmodmap -e "keycode 197 = XF86Pictures"
   xmodmap -e "keycode 237 = XF86Video"
   xmodmap -e "keycode 118 = XF86Music"

```

TODO: Add Fn+fx keys Remote control mimics keyboard, no additional software needed. Range is about 4 meters.

## Networking

Only tried it with ndiswrapper, took the driver from the Windows Vista partition, works perfectly. Ethernet works too with the forcedeth driver and I think I'll never have the need to use the internal modem, but I think it's one of those that are only supported by linuxant, so it uses a propietary driver. (too much work for something that I'll never use)

Wireless card also works flawlessly with broadcom-wl module from the AUR.

Retrieved from "[https://wiki.archlinux.org/index.php?title=HP_Pavilion_dv6420la&oldid=376808](https://wiki.archlinux.org/index.php?title=HP_Pavilion_dv6420la&oldid=376808)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [HP](/index.php/Category:HP "Category:HP")