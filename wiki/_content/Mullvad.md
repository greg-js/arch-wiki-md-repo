# Mullvad

Mullvad is a VPN service based in Sweden which operates [OpenVPN](/index.php/OpenVPN "OpenVPN") and PPTP servers. This article explains how to set up an OpenVPN connection to Mullvad.

## Configuring OpenVPN

Mullvad supply their own client but it can also be used with a manual configuration of Openvpn. Install [openvpn](https://www.archlinux.org/packages/?name=openvpn) and [openresolv](https://www.archlinux.org/packages/?name=openresolv). Download the Mullvad OpenVPN configuration files from [Mullvad](http://mullvad.net/en/openvpn_conf.php) and unzip into /etc/openvpn. Rename mullvad_linux.conf:

```
# mv /etc/openvpn/mullvad_linux.conf /etc/openvpn/mullvad.conf

```

In order to use the nameservers supplied by the VPN, a script needs to be called when starting and stopping OpenVPN to update resolvconf with the correct servers.

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
# 07/2013 colin@daedrum.net Fixed intet name
# 05/2006 chlauber@bnc.ch
#
# Example envs set from openvpn:
# foreign_option_1='dhcp-option DNS 193.43.27.132'
# foreign_option_2='dhcp-option DNS 193.43.27.133'
# foreign_option_3='dhcp-option DOMAIN be.bnc.ch'
# foreign_option_4='dhcp-option DOMAIN-SEARCH bnc.local'

RESOLVCONF=/usr/bin/resolvconf

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
      if [[ "$part2" == "DOMAIN" || "$part2" == "DOMAIN-SEARCH" ]] ; then
        IF_DNS_SEARCH="$IF_DNS_SEARCH $part3"
      fi
    fi
  done
  R=""
  if [ "$IF_DNS_SEARCH" ]; then
    R="search "
    for DS in $IF_DNS_SEARCH ; do
      R="${R} $DS"
    done
  R="${R}
"
  fi

  for NS in $IF_DNS_NAMESERVERS ; do
    R="${R}nameserver $NS
"
  done
  #echo -n "$R" | $RESOLVCONF -x -p -a "${dev}"
  echo -n "$R" | $RESOLVCONF -x -a "${dev}.inet"
  ;;
down)
  $RESOLVCONF -d "${dev}.inet"
  ;;
esac

```

Make it executable:

```
# chmod +x /etc/openvpn/update-resolv-conf

```

The VPN can then be [controlled](/index.php/Enabled "Enabled") through `openvpn@mullvad.service`.

## Mullvad Client

Mullvad also supply their own [graphical client](https://mullvad.net/en/download/), packaged as [mullvad](https://aur.archlinux.org/packages/mullvad/)<sup><small>AUR</small></sup>.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Mullvad&oldid=415851](https://wiki.archlinux.org/index.php?title=Mullvad&oldid=415851)"