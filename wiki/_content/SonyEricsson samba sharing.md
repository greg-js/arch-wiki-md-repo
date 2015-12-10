# SonyEricsson samba sharing

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

You can have acess to Sony Ericsson phones and phone cards via samba sharing. It works even with old firmware and you have still full functional phone, not like USB mass storage mode.

## Contents

*   [1 Supported Phones](#Supported_Phones)
*   [2 Setting Up Phone](#Setting_Up_Phone)
*   [3 Setting Up Computer](#Setting_Up_Computer)
*   [4 External Links](#External_Links)

## Supported Phones

*   Se C702

## Setting Up Phone

*   Settings > Connectivity > USB > USB network > USB Network type > Via Computer
*   Settings > Connectivity > Network sharing > set up name and password
*   Settings > Connectivity > Sreaming settings > Connect using > USB Ethernet (set ip adress eg. 192.168.0.50, mask 255.255.255.0)
*   Settings > Connectivity > Sreaming settings > Connect using > USB Ethernet > Allow local connection > Yes

## Setting Up Computer

*   you must have installed samba:

```
# pacman -S samba smbclient

```

*   start samba:

```
# /etc/rc.d/samba start

```

*   plug in phone in **Phone Mode**
*   set IP for phone:

```
# ip link set dev usb0 address 192.168.0.50

```

*   now you should be able to ping your phone

```
$ ping 192.168.0.50

```

*   in eg. Konqueror you can browse phone by entering

```
smb://192.168.0.50 

```

enter name and password you choosed in phone

## External Links

[Czech-language wiki](http://www.abclinuxu.cz/poradna/hardware/show/250631)

Retrieved from "[https://wiki.archlinux.org/index.php?title=SonyEricsson_samba_sharing&oldid=250561](https://wiki.archlinux.org/index.php?title=SonyEricsson_samba_sharing&oldid=250561)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Mobile devices](/index.php/Category:Mobile_devices "Category:Mobile devices")