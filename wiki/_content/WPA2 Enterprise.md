# WPA2 Enterprise

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Wireless configuration](/index.php/Wireless_configuration "Wireless configuration")
*   [Network configuration](/index.php/Network_configuration "Network configuration")
*   [Software access point](/index.php/Software_access_point "Software access point")
*   [Ad-hoc networking](/index.php/Ad-hoc_networking "Ad-hoc networking")

**WPA2 Enterprise** is a mode of [Wi-Fi Protected Access](https://en.wikipedia.org/wiki/Wi-Fi_Protected_Access "wikipedia:Wi-Fi Protected Access"). It provides better security and key management than _WPA2 Personal_, and supports other enterprise-type functionality, such as VLANs and [NAP](https://en.wikipedia.org/wiki/Network_Access_Protection "wikipedia:Network Access Protection"). However, it requires an external authentication server, called [RADIUS](https://en.wikipedia.org/wiki/RADIUS "wikipedia:RADIUS") server to handle the authentication of users. This is in contrast to Personal mode which does not require anything beyond the wireless router or access points (APs), and uses a single passphrase or password for all users.

The Enterprise mode enables users to log onto the Wi-Fi network with a username and password and/or a digital certificate. Since each user has a dynamic and unique encryption key, it also helps to prevent user-to-user snooping on the wireless network, and improves encryption strength.

## Contents

*   [1 Supported clients](#Supported_clients)
    *   [1.1 wpa_supplicant](#wpa_supplicant)
*   [2 Usage](#Usage)
    *   [2.1 eduroam](#eduroam)
        *   [2.1.1 connman](#connman)
        *   [2.1.2 Wicd](#Wicd)
        *   [2.1.3 netctl](#netctl)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 MS-CHAPv2](#MS-CHAPv2)

## Supported clients

**Note:** [NetworkManager](/index.php/NetworkManager "NetworkManager") can generate WPA2 Enterprise profiles with [graphical front ends](/index.php/NetworkManager#Graphical_front-ends "NetworkManager"). _nmcli_ and _nmtui_ do not support this, but may use existing profiles.

See [List of applications#Network managers](/index.php/List_of_applications#Network_managers "List of applications") for an overview.

### wpa_supplicant

[WPA supplicant](/index.php/WPA_supplicant#Advanced_usage "WPA supplicant") can be configured directly and used in combination with a dhcp client or with systemd, e.g. for a [dynamic address](/index.php/Wireless_network_configuration#Manual_wireless_connection_at_boot_using_systemd_and_dhcpcd "Wireless network configuration"). See the examples in `/etc/wpa_supplicant/wpa_supplicant.conf` for configuring the connection details.

Once the connection configuration is complete, you can use the dhcp client to test them. For example:

```
# dhcpcd _interface_

```

will automatically invoke WPA supplicant to establish the connection before proceeding to acquire an IP address.

## Usage

This section describes the configuration of the alternative available network clients to connect to a wireless access point with WPA2 Enterprise mode. See [Software access point#RADIUS](/index.php/Software_access_point#RADIUS "Software access point") for information on setting up an access point itself.

Enterprise mode requires a more complex client configuration, whereas Personal mode only requires entering a passphrase when prompted. Clients likely need to install the server’s CA certificate (plus per-user certificates if using EAP-TLS), and then manually configure the wireless security and 802.1X authentication settings.

For a comparison of protocols see the following [table](http://deployingradius.com/documents/protocols/compatibility.html).

**Warning:** It is possible to use WPA2 Enterprise without the client checking the server CA certificate. However, you should always seek to do so, because without authenticating the access point the connection can be subject to a man-in-the-middle attack. This may happen because while the connection handshake itself may be encrypted, the most widely used setups transmit the password itself either in plain text or the easily breakable [#MS-CHAPv2](#MS-CHAPv2). Hence, the client might send the password to a malicious access point which then proxies the connection.

### eduroam

[eduroam](https://en.wikipedia.org/wiki/eduroam "wikipedia:eduroam") (education roaming) is an international roaming service for users in research, higher education and further education, based on WPA2 Enterprise.

**Warning:**

*   Check connection details **first** with your institution before applying any profiles listed in this section. Example profiles are not guaranteed to work or match any security requirements.
*   When storing connection profiles unencrypted, restrict read access to the root account by specifying `chmod 600 _profile_` as root.

#### connman

[connman](/index.php/Connman "Connman") needs a separate configuration file before [connecting](/index.php/Connman#Wi-Fi "Connman"). While the connman git repository contains an [example eduroam config](https://git.kernel.org/cgit/network/connman/connman.git/tree/src/eduroam.config), see below for a more extensive configuration:

**Note:**

*   Create the `/var/lib/connman` directory if it does not exist.
*   Options are case-sensitive. [[1]](https://together.jolla.com/question/55969/connman-fails-due-to-case-sensitive-settings/)

 `/var/lib/connman/wifi_eduroam.config` 

```
[service_eduroam]
Type=wifi
Name=eduroam
EAP=ttls
CACertFile=/etc/ssl/certs/ca-certificates.crt
Phase2=PAP
Identity=_username_@_domain.edu_
Passphrase=_password_
```

[Restart](/index.php/Restart "Restart") `wpa_supplicant.service` and `connman.service` to connect to the new network.

#### Wicd

The [wicd-eduroam](https://aur.archlinux.org/packages/wicd-eduroam/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/wicd-eduroam)]</sup> package contains configuration templates which will appear to wicd as _eduroam_.

Alternatively, see [[2]](https://gist.githubusercontent.com/anonymous/0fa3b2c2b2a34c68a6f1/raw/9b8fdb7301182d18b6cd5068a7dbdfc57e5ba430/gistfile1.txt) for an example of a **TTLS** profile. To activate the profile, run:

```
# echo ttls-80211 >> /etc/wicd/encryption/templates/active

```

Open _wicd_, choose _TTLS for Wireless_ and enter the appropriate settings. The format of the subject match should be similar to `/CN=server.example.com`.

#### netctl

The [netctl-eduroam](https://aur.archlinux.org/packages/netctl-eduroam/)<sup><small>AUR</small></sup> package provides a template for easy configuration. Once installed, copy the template from `/etc/netctl/examples/eduroam` to `/etc/netctl/eduroam` and modify it according to your credentials.

Alternatively, adapt an example configuration from [[3]](https://gist.githubusercontent.com/anonymous/ed16e3b191cf627814b3/raw/d476e0dddbc8920b855702737ff69c287e620c7b/eduroam-netctl) (plain) or [[4]](https://gist.githubusercontent.com/anonymous/3fd8f8808a22b3a96feb/raw/d9537016a8c9852561630e676c4cbf98553a1a48/eduroam-ttls-netctl) (TTLS and certified universities).

**Tip:**

*   To prevent storing your password as plaintext, you can generate a password hash with `$ tr -d '\n' | iconv -t utf16le | openssl md4`. Type your password, press `Enter` and then `Ctrl+d`. Store the hashed password as `'password=hash:<hash>'`. This password hash is only available for MSCHAPV2 or MSCHAP, when using PAP use a plaintext password.
*   Custom certificates can be specified by adding the line `'ca_cert="/path/to/special/certificate.cer"'` in `WPAConfigSection`.

## Troubleshooting

### MS-CHAPv2

WPA2-Enterprise wireless networks demanding MSCHAPv2 type-2 authentication with PEAP sometimes require [pptpclient](https://www.archlinux.org/packages/?name=pptpclient) in addition to the stock [ppp](https://www.archlinux.org/packages/?name=ppp) package. [netctl](/index.php/Netctl "Netctl") seems to work out of the box without ppp-mppe, however. In either case, usage of MSCHAPv2 is discouraged as it is highly vulnerable, although using another method is usually not an option. See also [[5]](https://www.cloudcracker.com/blog/2012/07/29/cracking-ms-chap-v2/) and [[6]](http://research.edm.uhasselt.be/~bbonne/docs/robyns14wpa2enterprise.pdf).

Retrieved from "[https://wiki.archlinux.org/index.php?title=WPA2_Enterprise&oldid=412733](https://wiki.archlinux.org/index.php?title=WPA2_Enterprise&oldid=412733)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Wireless networking](/index.php/Category:Wireless_networking "Category:Wireless networking")
*   [Network configuration](/index.php/Category:Network_configuration "Category:Network configuration")

Hidden category:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")