# Ad-hoc networking

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Network configuration](/index.php/Network_configuration "Network configuration")
*   [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")
*   [Software access point](/index.php/Software_access_point "Software access point")
*   [Internet sharing](/index.php/Internet_sharing "Internet sharing")

An IBSS (Independent Basic Service Set) network, often called an ad-hoc network, is a way to have a group of devices talk to each other wirelessly, without a central controller. It is an example of a peer-to-peer network, in which all devices talk directly to each other, with no inherent relaying.

For example, ad-hoc networking may be used to [share an internet connection](/index.php/Internet_sharing "Internet sharing").

## Contents

*   [1 Requirements](#Requirements)
*   [2 Wifi link layer](#Wifi_link_layer)
    *   [2.1 Manual method](#Manual_method)
    *   [2.2 WPA supplicant](#WPA_supplicant)
*   [3 Network configuration](#Network_configuration)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Using NetworkManager](#Using_NetworkManager)
    *   [4.2 Custom systemd service (with wpa_supplicant and static IP)](#Custom_systemd_service_.28with_wpa_supplicant_and_static_IP.29)
*   [5 See also](#See_also)

## Requirements

*   A [nl80211 compatible](https://wireless.wiki.kernel.org/en/users/drivers%7C) wireless device (e.g. ath9k) on all devices which will connect to the network

## Wifi link layer

Since IBSS network is a peer-to-peer network, the steps necessary to set up the wifi link layer should be the same on all devices.

**Tip:** It is possible to create complex network topologies, see [Linux Wireless documentation](http://wireless.kernel.org/en/users/Documentation/iw/vif) for advanced examples.

### Manual method

**Warning:** This method creates **unencrypted** ad-hoc network. See [#WPA supplicant](#WPA_supplicant) for method using WPA encryption.

See [Wireless network configuration#Manual setup](/index.php/Wireless_network_configuration#Manual_setup "Wireless network configuration") for a better explanation of the following commands. Make sure that [iw](https://www.archlinux.org/packages/?name=iw) is [installed](/index.php/Pacman "Pacman").

Set the operation mode to ibss:

```
# iw _interface_ set type ibss

```

Bring the interface up (an additional step like `rfkill unblock wifi` might be needed):

```
# ip link set _interface_ up

```

Now you can create an ad-hoc network. Replace _your_ssid_ with the name of the network and _frequency_ with the frequency in MHz, depending on which channel you want to use. See the Wikipedia page [List of WLAN channels](https://en.wikipedia.org/wiki/List_of_WLAN_channels#Interference_Concerns "wikipedia:List of WLAN channels") for a table showing frequencies of individual channels.

```
# iw _interface_ ibss join _your_ssid_ _frequency_

```

### WPA supplicant

**Note:** This method creates ad-hoc network using WPA encryption. WPA2 is currently not supported (August 2013).

Ensure that [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) is [installed](/index.php/Pacman "Pacman"), and create a configuration file for it (see [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") for details).

 `/etc/wpa_supplicant-adhoc.conf` 

```
ctrl_interface=DIR=/run/wpa_supplicant GROUP=wheel

# use 'ap_scan=2' on all devices connected to the network
ap_scan=2

network={
    ssid="MySSID"
    mode=1
    frequency=2432
    proto=WPA
    key_mgmt=WPA-NONE
    pairwise=NONE
    group=TKIP
    psk="secret passphrase"
}

```

Run _wpa_supplicant_ on all devices connected to the network with the following command:

```
# wpa_supplicant -B -i _interface_ -c /etc/wpa_supplicant-adhoc.conf -D nl80211,wext

```

## Network configuration

The final step is to assign an IP address to all devices in the network. There are multiple ways to do this:

*   Assign static IP addresses. See [Network configuration#Static IP address](/index.php/Network_configuration#Static_IP_address "Network configuration") for details.
*   Running DHCP server on one device. See [dhcpd](/index.php/Dhcpd "Dhcpd") or [dnsmasq](/index.php/Dnsmasq "Dnsmasq") for details.
*   Running _avahi-autoipd_. See [Avahi#Obtaining IPv4LL IP address](/index.php/Avahi#Obtaining_IPv4LL_IP_address "Avahi") for details.

If you want to share an internet connection to the ad-hoc network, see [Internet sharing](/index.php/Internet_sharing "Internet sharing").

## Tips and tricks

### Using NetworkManager

If you use [NetworkManager](/index.php/NetworkManager "NetworkManager"), you can use _nm-applet_ for ad-hoc network configuration instead of the manual method described above. See [NetworkManager#Ad-hoc](/index.php/NetworkManager#Ad-hoc "NetworkManager") for details.

**Note:** NetworkManager does not support WPA encryption in ad-hoc mode.

### Custom systemd service (with wpa_supplicant and static IP)

You can use the following templates to enable wireless ad-hoc networking:

 `/etc/conf.d/network-wireless-adhoc@<interface>` 

```
addr=192.168.0.2
mask=24

```

 `/etc/systemd/system/network-wireless-adhoc@.service` 

```
[Unit]
Description=Ad-hoc wireless network connectivity (%i)
Wants=network.target
Before=network.target
BindsTo=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device

[Service]
Type=oneshot
RemainAfterExit=yes
EnvironmentFile=/etc/conf.d/network-wireless-adhoc@%i

# perhaps rfkill is not needed for you
ExecStart=/usr/bin/rfkill unblock wifi
ExecStart=/usr/bin/ip link set %i up
ExecStart=/usr/bin/wpa_supplicant -B -i %i -D nl80211,wext -c /etc/wpa_supplicant-adhoc.conf
ExecStart=/usr/bin/ip addr add ${addr}/${mask} dev %i

ExecStop=/usr/bin/ip addr flush dev %i
ExecStop=/usr/bin/ip link set %i down

[Install]
WantedBy=multi-user.target

```

## See also

*   [Ubuntu community wiki WifiDocs/Adhoc](https://help.ubuntu.com/community/WifiDocs/Adhoc)
*   [Manual about creating an Ad-Hoc network on UbuntuGeek](http://www.ubuntugeek.com/creating-an-adhoc-host-with-ubuntu.html)
*   [Share your 3G Internet connection over wifi](http://go2linux.garron.me/linux/2011/03/share-your-3g-internet-connection-over-wifi-linux-ipod-touch-925)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Ad-hoc_networking&oldid=409555](https://wiki.archlinux.org/index.php?title=Ad-hoc_networking&oldid=409555)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Wireless networking](/index.php/Category:Wireless_networking "Category:Wireless networking")