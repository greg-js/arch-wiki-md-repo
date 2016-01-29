# UWMWiFi

UWMWiFi is the wireless network used by the University of Wisconsin-Milwaukee.

## Contents

*   [1 Netctl setup](#Netctl_setup)
*   [2 Manual setup](#Manual_setup)
*   [3 About identity](#About_identity)
*   [4 See also](#See_also)

## Netctl setup

Still a work in progress, but this seems to function

 `/etc/netctl/UWMWiFi` 

```
Description='UWM WiFi Network'
Interface=wlp3s0
Connection=wireless
Security=wpa-configsection
IP=dhcp
WPAConfigSection=(
    'ssid="UWMWiFi"'
    'key_mgmt=WPA-EAP'
    'eap=PEAP'
    'identity="user@uwm.edu"'
    'password="password"'
    'priority=1'
)

```

Then to connect

```
# netctl stop-all
# netctl enable UWMWiFi
# netctl start UWMWiFi

```

## Manual setup

If netctl does not work properly, try connecting manually using the iw tool and [wpa_supplicant](/index.php/Wpa_supplicant "Wpa supplicant") as directed in [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration"). Do not forget that most of these commands need to be run with elevated permissions.

 `/etc/wpa_supplicant/uwm.conf` 

```

network={
 ssid="UWMWiFi"
 key_mgmt=WPA-EAP
 eap=PEAP
 identity="user@uwm.edu"
 password="password"

}

ctrl_interface=DIR=/run/wpa_supplicant

```

Get card name

```
# ip link

```

Assuming your card is _wlan0_

```
# ip link set wlan0 up
# wpa_supplicant -B -i wlan0 -c /etc/wpa_supplicant/uwm.conf
# dhcpcd wlan0

```

After resuming from sleep or similar

```
# dhcpcd wlan0 -k
# dhcpcd wlan0

```

So far, this method seems more reliable.

## About identity

On some parts of campus the identity field requires "@uwm.edu" and on some parts it requires only the username. For example, the in the Union connecting will fail if you include @uwm.edu, but in the EMS it will fail without it.

This will be tested and validated in the future.

## See also

*   [Netctl](/index.php/Netctl "Netctl")
*   [Wireless Setup](/index.php/Wireless_Setup "Wireless Setup")
*   [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant")
*   [http://www4.uwm.edu/technology/authenticated/wifi/uwm/](http://www4.uwm.edu/technology/authenticated/wifi/uwm/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=UWMWiFi&oldid=388098](https://wiki.archlinux.org/index.php?title=UWMWiFi&oldid=388098)"