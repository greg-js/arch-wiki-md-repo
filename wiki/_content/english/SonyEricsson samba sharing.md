You can have acess to Sony Ericsson phones and phone cards via samba sharing. It works even with old firmware and you have still full functional phone, not like USB mass storage mode.

## Contents

*   [1 Supported phones](#Supported_phones)
*   [2 Set up phone](#Set_up_phone)
*   [3 Set up computer](#Set_up_computer)
*   [4 External links](#External_links)

## Supported phones

*   Se C702

## Set up phone

*   Settings > Connectivity > USB > USB network > USB Network type > Via Computer
*   Settings > Connectivity > Network sharing > set up name and password
*   Settings > Connectivity > Sreaming settings > Connect using > USB Ethernet (set ip adress eg. 192.168.0.50, mask 255.255.255.0)
*   Settings > Connectivity > Sreaming settings > Connect using > USB Ethernet > Allow local connection > Yes

## Set up computer

*   You must have installed [Samba](/index.php/Samba "Samba").

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

## External links

[Czech-language wiki](http://www.abclinuxu.cz/poradna/hardware/show/250631)