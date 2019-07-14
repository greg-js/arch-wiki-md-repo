NordVPN is a personal virtual private network service provider. NordVPN is based in Panama. The country has no mandatory data retention laws and does not participate in the Five Eyes or Fourteen Eyes alliances. The Linux Version only use Command-line.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Create Account](#Create_Account)
*   [2 Installation](#Installation)
*   [3 Systemd](#Systemd)
*   [4 Configuration](#Configuration)
    *   [4.1 Login/Logout](#Login/Logout)
    *   [4.2 Connect to VPN](#Connect_to_VPN)
    *   [4.3 Settings](#Settings)
    *   [4.4 Server List](#Server_List)
*   [5 Alternative Method : connecting to NordVPN using NetworkManager](#Alternative_Method_:_connecting_to_NordVPN_using_NetworkManager)

## Create Account

In order to use NordVPN, you must create your own account on the official NordVPN website. [http://nordvpn.com](http://nordvpn.com)

There are different payment options to choose.

## Installation

NordVPN can be installed with a package [nordvpn-bin](https://aur.archlinux.org/packages/nordvpn-bin/), available in the [AUR](/index.php/AUR "AUR").

## Systemd

In order to use NordVPN. You must [enable](/index.php/Enable "Enable") `nordvpnd` service.

```
$ sudo systemctl enable nordvpnd.service
$ sudo systemctl start nordvpnd.service

```

## Configuration

Here are many different commands to use NordVPN.

### Login/Logout

```
$ nordvpn login

```

Logs you in to your NordVPN Account.

```
$ nordvpn logout

```

Logs you out from your NordVPN Account.

### Connect to VPN

 `$ nordvpn connect [[country]/[server]/[country_code]/[city] or [country] [city]]` 
```
Provide a [country] argument to automatically connect to a specific country. For example: 'nordvpn set autoconnect on Australia'
Provide a [country_code] argument to automatically connect to a specific country. For example: 'nordvpn set autoconnect on us'
Provide a [city] argument to automatically connect to a specific city. For example: 'nordvpn set autoconnect on Hungary Budapest'
```

Connect you to VPN.

```
$ nordvpn disconnect

```

Disconnect you from VPN.

```
$ nordvpn status

```

Shows the connection status.

### Settings

 `$ nordvpn set protocol [protocol]` 
```
Supported values for [protocol]: TCP, UDP
Example: nordvpn set protocol TCP
```

Sets the protocol.

 `$ nordvpn set killswitch [enabled]/[disabled]` 
```
Supported values for [disabled]: 0, false, disable, off, disabled
Example: nordvpn set killswitch off

Supported values for [enabled]: 1, true, enable, on, enabled
Example: nordvpn set killswitch on
```

Enables or disables Kill Switch. This security feature blocks your device from accessing the Internet outside the secure VPN tunnel, in case connection with a VPN server is lost.

 `$ nordvpn set cybersec [enabled]/[disabled]` 
```
Supported values for [disabled]: 0, false, disable, off, disabled
Example: nordvpn set cybersec off

Supported values for [enabled]: 1, true, enable, on, enabled
Example: nordvpn set cybersec on
```

Enables or disables CyberSec. When enabled, the CyberSec feature will automatically block suspicious websites so that no malware or other cyber threats can infect your device. Additionally, no flashy ads will come into your sight. More information on how it works: [https://nordvpn.com/features/cybersec/](https://nordvpn.com/features/cybersec/).

 `$ nordvpn set autoconnect [enabled]/[disabled] [[country]/[server]/[country_code]/[city] or [country] [city]]` 
```
Supported values for [disabled]: 0, false, disable, off, disabled
Example: nordvpn set autoconnect off

Supported values for [enabled]: 1, true, enable, on, enabled
Example: nordvpn set autoconnect on

Provide a [country] argument to automatically connect to a specific country. For example: 'nordvpn set autoconnect on Australia'
Provide a [country_code] argument to automatically connect to a specific country. For example: 'nordvpn set autoconnect on us'
Provide a [city] argument to automatically connect to a specific city. For example: 'nordvpn set autoconnect on Hungary Budapest'
```

Enables or disables auto connect. When enabled, this feature will automatically try to connect to VPN on operating system startup.

 `$ nordvpn set obfuscate [enabled]/[disabled]` 
```
Supported values for [disabled]: 0, false, disable, off, disabled
Example: nordvpn set obfuscate off

Supported values for [enabled]: 1, true, enable, on, enabled
Example: nordvpn set obfuscate on
```

Enables or disables obfuscation. When enabled, this feature allows to bypass network traffic sensors which aim to detect usage of the protocol and log, throttle or block it.

 `$ nordvpn set dns [servers]/[disabled]` 
```
Supported values for [disabled]: 0, false, disable, off, disabled
Example: nordvpn set dns off

Arguments [servers] is a list of IP addresses separated by space
Example: nordvpn set dns 0.0.0.0 1.2.3.4
```

Sets DNS servers.

 `$ nordvpn whitelist command [command options] [arguments...]` 
```
Commands:
     add     Adds option to whitelist
     remove  Removes option from whitelist
```

Adds or removes option from whitelist.

```
$ nordvpn settings

```

Shows the current settings.

### Server List

```
$ nordvpn countries

```

Shows the country list.

 `$ nordvpn cities [country]` 
```
Use this command to show cities of specific country.
Example: nordvpn cities United_States
```

Shows the city list.

## Alternative Method : connecting to NordVPN using NetworkManager

1\. [Install](/index.php/Install "Install") [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) and [networkmanager-openvpn](https://www.archlinux.org/packages/?name=networkmanager-openvpn).

2\. Choose and download an appropriate server using the NordVPN servers page : [https://nordvpn.com/fr/servers/](https://nordvpn.com/fr/servers/) Download the corresponding configuration file on the NordVPN site : [https://nordvpn.com/ovpn/](https://nordvpn.com/ovpn/)

3\. Add the file to you vpn connections in NetworkManager. In the VPN tab, enter your NordVPN id and password.

4\. Optional : to avoid DNS leak, choose "automatic adresses only (VPN)" in the ipv4 settings, and write the NordVPN DNS adresses in "DNS servers" : 103.86.96.100, 103.86.99.100

5\. Optional : you can make the connection automatic by ticking "Automatically connect to VPN when using this connection" in every connection you want, and choosing the right configuration file.

6\. Optional : if you want to use a killswitch, you'll have to install and configure a firewall, like [Uncomplicated Firewall](/index.php/Uncomplicated_Firewall "Uncomplicated Firewall") or [Iptables](/index.php/Iptables "Iptables")