NordVPN is a personal virtual private network service provider. NordVPN is based in Panama. The country has no mandatory data retention laws and does not participate in the Five Eyes or Fourteen Eyes alliances. On Linux, Nordvpn operates through a command-line tool.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Create Account](#Create_Account)
*   [2 Installation](#Installation)
*   [3 Systemd](#Systemd)
*   [4 Configuration](#Configuration)
    *   [4.1 Login/Logout](#Login/Logout)
    *   [4.2 Enable NordLynx](#Enable_NordLynx)
    *   [4.3 Connect to VPN](#Connect_to_VPN)
    *   [4.4 Settings](#Settings)
    *   [4.5 Server List](#Server_List)
*   [5 Alternative Method : connecting to NordVPN using NetworkManager](#Alternative_Method_:_connecting_to_NordVPN_using_NetworkManager)
    *   [5.1 Installation](#Installation_2)
    *   [5.2 Configuration](#Configuration_2)
    *   [5.3 Avoid DNS leak](#Avoid_DNS_leak)
    *   [5.4 Automatic connection to the VPN](#Automatic_connection_to_the_VPN)
    *   [5.5 Disable ipv6](#Disable_ipv6)
    *   [5.6 Use a killswitch](#Use_a_killswitch)
    *   [5.7 Test your configuration](#Test_your_configuration)

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

### Enable NordLynx

NordVPN has [introduced](https://nordvpn.com/blog/nordlynx-protocol-wireguard/) NordLynx technology which is based on [WireGuard](/index.php/WireGuard "WireGuard") protocol. Compared to default [OpenVPN](/index.php/OpenVPN "OpenVPN") technology, NordLynx provides lower latency, higher speeds and better connection stability.

Enable it with the below command:

```
$ nordvpn set technology nordlynx

```

To see all available technologies:

```
$ nordvpn set technology --help

```

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

### Installation

1\. [Install](/index.php/Install "Install") [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) and [networkmanager-openvpn](https://www.archlinux.org/packages/?name=networkmanager-openvpn).

2\. Choose an appropriate server using the NordVPN servers page : [https://nordvpn.com/servers/](https://nordvpn.com/servers/) Download the corresponding openvpn configuration file on the NordVPN site : [https://nordvpn.com/ovpn/](https://nordvpn.com/ovpn/) Save the file to a place in your user home directory or elsewhere that is memorable for future access.

### Configuration

1\. Right click on the NetworkManager applet from your desktop environment, and click Edit Connections. Click the Plus sign in the bottom left corner of the Network Connections window that appears.

2\. When you choose a connection type, click the drop down menu and scroll all the way down until you reach "Import a saved VPN configuration". Select that option. Now, click Create.

3\. Navigate to the directory you extracted all of the openvpn files to earlier, then open one of the files from that folder. Generally speaking, you will want to open the file that is associated with the connection you specifically want.

4\. After you have opened one of the openvpn files, the window that appears should be "Editing <connection type>". Type in your NordVPN Username and Password. There is an icon in the password box indicating user permission of the credentials; change the settings as you wish ("Save for all users" if you don't want to enter your password every time you connect).

### Avoid DNS leak

To prevent DNS leak you must :

1\. click on the "ipv4 settings"

2\. On method : choose "automatic adresses only (VPN)" and manually enter the NordVPN DNS adresses in "DNS servers" : "103.86.96.100, 103.86.99.100" (Separated by a coma)

3\. Click Save at the bottom left of the "Editing <connection type>" window.

### Automatic connection to the VPN

1\. Right click on the NetworkManager applet from your desktop environment, and click Edit Connections.

2\. Double click on the ethernet or Wifi connection for whom you want to automatically connect to the VPN

3\. On the "General" tab, click on "Automatically connect to VPN when using this connection" in every connection you want, and choosing the right configuration file.

4\. Repeat the operation for the other connections you'll use with the VPN.

### Disable ipv6

NordVPN is not ipv6 compatible. You may want to [completely disable it](/index.php/IPv6#Disable_IPv6 "IPv6").

Or you can also :

1\. Right click on the NetworkManager applet from your desktop environment, and click Edit Connections.

2\. Double click on the ethernet or Wifi connection for whom you want to automatically connect to the VPN

3\. On the "ipv6" tab, choose "ignore" in the method box.

### Use a killswitch

The NordVPN killswitch won't work with this method, you'll have to create your own using [ufw](/index.php/Ufw "Ufw") or [iptables](/index.php/Iptables "Iptables").

Here is an [example with UFW](https://www.smarthomebeginner.com/vpn-kill-switch-with-ufw/#Gather_information_about_your_IP_addresses).

### Test your configuration

You can use these site :

[https://ipleak.net/](https://ipleak.net/)

[https://www.dnsleaktest.com/](https://www.dnsleaktest.com/)

[http://ipv6leak.com/](http://ipv6leak.com/)