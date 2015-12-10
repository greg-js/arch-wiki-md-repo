# Mullvad

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

## Using Mullvad as plain OpenVPN

To use the VPN service Mullvad on Arch Linux a few small adjustments need to be done. First, install [OpenVPN](/index.php/OpenVPN "OpenVPN") and resolvconf. Download the plain [OpenVPN](/index.php/OpenVPN "OpenVPN") version of Mullvad ["here"](http://mullvad.net/en/openvpn_conf.php). Next, copy the content of the zip file to /etc/openvpn. Move mullvad_linux.conf into mullvad.conf `sudo mv /etc/openvpn/mullvad_linux.conf /etc/openvpn/mullvad.conf` then open it and change the end of the file from

 `mullvad.conf` 

```
ping 10

ca ca.crt
cert mullvad.crt
key mullvad.key

crl-verify crl.pem

```

to

 `mullvad.conf` 

```
ping 10

ca /etc/openvpn/ca.crt
cert /etc/openvpn/mullvad.crt
key /etc/openvpn/mullvad.key

crl-verify /etc/openvpn/crl.pem

```

and make it executable by running `sudo chmod +x /etc/openvpn/mullvad.conf`.

If `lsmod | grep tun` returns a blank line, the tun module isn't getting loaded by default and you'll need to load it manually and tell the system to load it during startup by running `sudo modprobe tun` and `sudo echo "tun" > /etc/modules-load.d/tun.conf`

then create

 `/etc/openvpn/update-resolv-conf` 

```
#!/bin/bash
#
# Parses DHCP options from openvpn to update resolv.conf
# To use set as 'up' and 'down' script in your openvpn *.conf:
# up /etc/openvpn/update-resolv-conf
# down /etc/openvpn/update-resolv-conf
#
# Used snippets of resolvconf script by Thomas Hood <jdthood@yahoo.co.uk>
# and Chris Hanson
# Licensed under the GNU GPL.  See /usr/share/common-licenses/GPL.
#
# 05/2006 chlauber@bnc.ch
#
# Example envs set from openvpn:
# foreign_option_1='dhcp-option DNS 193.43.27.132'
# foreign_option_2='dhcp-option DNS 193.43.27.133'
# foreign_option_3='dhcp-option DOMAIN be.bnc.ch'

[ -x /usr/sbin/resolvconf ] || exit 0

case $script_type in

up)
   for optionname in ${!foreign_option_*} ; do
      option="${!optionname}"
      echo $option
      part1=$(echo "$option" | cut -d " " -f 1)
      if [ "$part1" == "dhcp-option" ] ; then
         part2=$(echo "$option" | cut -d " " -f 2)
         part3=$(echo "$option" | cut -d " " -f 3)
         if [ "$part2" == "DNS" ] ; then
            IF_DNS_NAMESERVERS="$IF_DNS_NAMESERVERS $part3"
         fi
         if [ "$part2" == "DOMAIN" ] ; then
            IF_DNS_SEARCH="$part3"
         fi
      fi
   done
   R=""
   if [ "$IF_DNS_SEARCH" ] ; then
           R="${R}search $IF_DNS_SEARCH
"
   fi
   for NS in $IF_DNS_NAMESERVERS ; do
           R="${R}nameserver $NS
"
   done
   echo -n "$R" | /usr/sbin/resolvconf -a "${dev}.inet"
   ;;
down)
   /usr/sbin/resolvconf -d "${dev}.inet"
   ;;
esac

```

and don't forget to make it executable by running `sudo chmod +x /etc/openvpn/update-resolv-conf`

Now create the launch script:

 `/usr/local/bin/mullvad` 

```
#!/usr/bin/env bash

if [ ! "$UID" = 0 ]; then
    if [ `type -P gksu` ]; then
        SUDOAPP="gksu"
    elif [ `type -P kdesu` ]; then
        SUDOAPP="kdesu"
    else
        SUDOAPP="sudo"
    fi
fi

if [ -n "$1" ]; then
    if [ "$1" = "start" ]; then
        $SUDOAPP systemctl start openvpn@mullvad
    elif [ "$1" = "stop" ]; then
        $SUDOAPP systemctl stop openvpn@mullvad
    elif [ "$1" = "restart" ]; then
        $SUDOAPP systemctl restart openvpn@mullvad
    else
        echo "Invalid command"
        exit 1
    fi
else
    echo "Run 'start', 'stop' or 'restart' as an argument to start, stop or restart the Mullvad VPN"
    exit 1
fi

```

Then make the launch script executable by running `sudo chmod a+x /usr/local/bin/mullvad`

You can then start Mullvad in the terminal by running `mullvad start`. Stop it with `mullvad stop`, and restart with `mullvad restart`.

To create a menu item we need the logo run: `wget https://mullvad.net/static/images/mullvad-circle.svg -O ~/.local/share/icons/mullvad.svg`

Then create the .desktop file by running `echo -e "[Desktop Entry]\nType=Application\nName=Mullvad\nComment=Start Mullvad VPN service\nIcon=mullvad\nExec=mullvad start\nCategories=Network" > ~/.local/share/applications/mullvad.desktop`

If `mullvad start` is successful from the command line, the desktop file should appear in your menu and start the service the same way by selecting it.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Mullvad&oldid=358935](https://wiki.archlinux.org/index.php?title=Mullvad&oldid=358935)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Virtual Private Network](/index.php/Category:Virtual_Private_Network "Category:Virtual Private Network")