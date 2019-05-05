Related articles

*   [Network configuration](/index.php/Network_configuration "Network configuration")
*   [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")

[NetworkManager](https://wiki.gnome.org/Projects/NetworkManager/) is a program for providing detection and configuration for systems to automatically connect to network. NetworkManager's functionality can be useful for both wireless and wired networks. For wireless networks, NetworkManager prefers known wireless networks and has the ability to switch to the most reliable network. NetworkManager-aware applications can switch from online and offline mode. NetworkManager also prefers wired connections over wireless ones, has support for modem connections and certain types of VPN. NetworkManager was originally developed by Red Hat and now is hosted by the [GNOME](/index.php/GNOME "GNOME") project.

**Warning:** By default, Wi-Fi passwords are stored in clear text, see [#Encrypted Wi-Fi passwords](#Encrypted_Wi-Fi_passwords).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Mobile broadband support](#Mobile_broadband_support)
    *   [1.2 PPPoE / DSL support](#PPPoE_/_DSL_support)
    *   [1.3 VPN support](#VPN_support)
*   [2 Usage](#Usage)
    *   [2.1 nmcli examples](#nmcli_examples)
    *   [2.2 Edit a connection](#Edit_a_connection)
*   [3 Front-ends](#Front-ends)
    *   [3.1 GNOME](#GNOME)
    *   [3.2 KDE Plasma](#KDE_Plasma)
    *   [3.3 nm-applet](#nm-applet)
        *   [3.3.1 Appindicator](#Appindicator)
    *   [3.4 networkmanager-dmenu](#networkmanager-dmenu)
*   [4 Configuration](#Configuration)
    *   [4.1 Enable NetworkManager](#Enable_NetworkManager)
    *   [4.2 Enable NetworkManager Wait Online](#Enable_NetworkManager_Wait_Online)
    *   [4.3 Set up PolicyKit permissions](#Set_up_PolicyKit_permissions)
    *   [4.4 Proxy settings](#Proxy_settings)
    *   [4.5 Checking connectivity](#Checking_connectivity)
    *   [4.6 DHCP client](#DHCP_client)
    *   [4.7 DNS management](#DNS_management)
        *   [4.7.1 DNS caching and split DNS](#DNS_caching_and_split_DNS)
            *   [4.7.1.1 dnsmasq](#dnsmasq)
                *   [4.7.1.1.1 Custom configuration](#Custom_configuration)
                *   [4.7.1.1.2 IPv6](#IPv6)
                *   [4.7.1.1.3 DNSSEC](#DNSSEC)
            *   [4.7.1.2 systemd-resolved](#systemd-resolved)
            *   [4.7.1.3 DNS resolver with an openresolv subscriber](#DNS_resolver_with_an_openresolv_subscriber)
        *   [4.7.2 Setting custom DNS servers in a connection](#Setting_custom_DNS_servers_in_a_connection)
            *   [4.7.2.1 Setting custom DNS servers in a connection (GUI)](#Setting_custom_DNS_servers_in_a_connection_(GUI))
            *   [4.7.2.2 Setting custom DNS servers in a connection (nmcli / connection file)](#Setting_custom_DNS_servers_in_a_connection_(nmcli_/_connection_file))
        *   [4.7.3 /etc/resolv.conf](#/etc/resolv.conf)
            *   [4.7.3.1 Unmanaged /etc/resolv.conf](#Unmanaged_/etc/resolv.conf)
            *   [4.7.3.2 Use openresolv](#Use_openresolv)
*   [5 Network services with NetworkManager dispatcher](#Network_services_with_NetworkManager_dispatcher)
    *   [5.1 Avoiding the dispatcher timeout](#Avoiding_the_dispatcher_timeout)
    *   [5.2 Dispatcher examples](#Dispatcher_examples)
        *   [5.2.1 Mount remote folder with sshfs](#Mount_remote_folder_with_sshfs)
        *   [5.2.2 Mounting of SMB shares](#Mounting_of_SMB_shares)
        *   [5.2.3 Mounting of NFS shares](#Mounting_of_NFS_shares)
        *   [5.2.4 Use dispatcher to automatically toggle wireless depending on LAN cable being plugged in](#Use_dispatcher_to_automatically_toggle_wireless_depending_on_LAN_cable_being_plugged_in)
        *   [5.2.5 Use dispatcher to connect to a VPN after a network connection is established](#Use_dispatcher_to_connect_to_a_VPN_after_a_network_connection_is_established)
        *   [5.2.6 OpenNTPD](#OpenNTPD)
*   [6 Testing](#Testing)
*   [7 Tips and tricks](#Tips_and_tricks)
    *   [7.1 Encrypted Wi-Fi passwords](#Encrypted_Wi-Fi_passwords)
        *   [7.1.1 Using GNOME Keyring](#Using_GNOME_Keyring)
        *   [7.1.2 Using KDE Wallet](#Using_KDE_Wallet)
    *   [7.2 Sharing internet connection over Wi-Fi](#Sharing_internet_connection_over_Wi-Fi)
    *   [7.3 Sharing internet connection over Ethernet](#Sharing_internet_connection_over_Ethernet)
    *   [7.4 Checking if networking is up inside a cron job or script](#Checking_if_networking_is_up_inside_a_cron_job_or_script)
    *   [7.5 Connect to network with secret on boot](#Connect_to_network_with_secret_on_boot)
    *   [7.6 Automatically unlock keyring after login](#Automatically_unlock_keyring_after_login)
        *   [7.6.1 GNOME](#GNOME_2)
        *   [7.6.2 SLiM login manager](#SLiM_login_manager)
    *   [7.7 OpenConnect with password in KWallet](#OpenConnect_with_password_in_KWallet)
    *   [7.8 Ignore specific devices](#Ignore_specific_devices)
    *   [7.9 Configuring MAC address randomization](#Configuring_MAC_address_randomization)
    *   [7.10 Enable IPv6 Privacy Extensions](#Enable_IPv6_Privacy_Extensions)
    *   [7.11 Working with wired connections](#Working_with_wired_connections)
    *   [7.12 Using iwd as the Wi-Fi backend](#Using_iwd_as_the_Wi-Fi_backend)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 No prompt for password of secured Wi-Fi networks](#No_prompt_for_password_of_secured_Wi-Fi_networks)
    *   [8.2 No traffic via PPTP tunnel](#No_traffic_via_PPTP_tunnel)
    *   [8.3 Network management disabled](#Network_management_disabled)
    *   [8.4 Problems with internal DHCP client](#Problems_with_internal_DHCP_client)
    *   [8.5 DHCP problems with dhclient](#DHCP_problems_with_dhclient)
    *   [8.6 3G modem not detected](#3G_modem_not_detected)
    *   [8.7 Switching off WLAN on laptops](#Switching_off_WLAN_on_laptops)
    *   [8.8 Static IP address settings revert to DHCP](#Static_IP_address_settings_revert_to_DHCP)
    *   [8.9 Cannot edit connections as normal user](#Cannot_edit_connections_as_normal_user)
    *   [8.10 Forget hidden wireless network](#Forget_hidden_wireless_network)
    *   [8.11 VPN not working in GNOME](#VPN_not_working_in_GNOME)
    *   [8.12 Unable to connect to visible European wireless networks](#Unable_to_connect_to_visible_European_wireless_networks)
    *   [8.13 Automatic connect to VPN on boot is not working](#Automatic_connect_to_VPN_on_boot_is_not_working)
    *   [8.14 Systemd Bottleneck](#Systemd_Bottleneck)
    *   [8.15 Regular network disconnects, latency and lost packets (WiFi)](#Regular_network_disconnects,_latency_and_lost_packets_(WiFi))
    *   [8.16 Unable to turn on wi-fi with Lenovo laptop (IdeaPad, Legion, etc.)](#Unable_to_turn_on_wi-fi_with_Lenovo_laptop_(IdeaPad,_Legion,_etc.))
    *   [8.17 Turn off hostname sending](#Turn_off_hostname_sending)
    *   [8.18 nm-applet disappears in i3wm](#nm-applet_disappears_in_i3wm)
    *   [8.19 nm-applet tray icons display wrongly](#nm-applet_tray_icons_display_wrongly)
    *   [8.20 Unit dbus-org.freedesktop.resolve1.service not found](#Unit_dbus-org.freedesktop.resolve1.service_not_found)
*   [9 See also](#See_also)

## Installation

NetworkManager can be [installed](/index.php/Install "Install") with the package [networkmanager](https://www.archlinux.org/packages/?name=networkmanager), which contains a daemon, a command line interface (`nmcli`) and a curses‐based interface (`nmtui`). It has functionality for basic DHCP support. For full featured DHCP and if you require IPv6 support, [dhclient](https://www.archlinux.org/packages/?name=dhclient) integrates it. After installation, you should [enable the daemon](#Enable_NetworkManager).

Additional interfaces:

*   [nm-connection-editor](https://www.archlinux.org/packages/?name=nm-connection-editor) for a graphical user interface,
*   [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) for a system tray applet (`nm-applet`).

**Note:** You must ensure that no other service that wants to configure the network is running; in fact, multiple networking services will conflict. You can find a list of the currently running services with `systemctl --type=service` and then [stop](/index.php/Stop "Stop") them. See [#Configuration](#Configuration) to enable the NetworkManager service.

### Mobile broadband support

[Install](/index.php/Install "Install") [modemmanager](https://www.archlinux.org/packages/?name=modemmanager), [mobile-broadband-provider-info](https://www.archlinux.org/packages/?name=mobile-broadband-provider-info) and [usb_modeswitch](https://www.archlinux.org/packages/?name=usb_modeswitch) packages for mobile broadband connection support. See [USB 3G Modem#Network Manager](/index.php/USB_3G_Modem#Network_Manager "USB 3G Modem") for details.

### PPPoE / DSL support

[Install](/index.php/Install "Install") [rp-pppoe](https://www.archlinux.org/packages/?name=rp-pppoe) package for PPPoE / DSL connection support. To actually add PPPoE connection, use `nm-connection-editor` and add new DSL/PPPoE connection.

### VPN support

NetworkManager since version 1.16 has native support for [WireGuard](/index.php/WireGuard "WireGuard")[[1]](https://blogs.gnome.org/thaller/2019/03/15/wireguard-in-networkmanager/).

Support for other VPN types is based on a plug-in system. They are provided in the following packages:

*   [networkmanager-openconnect](https://www.archlinux.org/packages/?name=networkmanager-openconnect) for [OpenConnect](/index.php/OpenConnect "OpenConnect")
*   [networkmanager-openvpn](https://www.archlinux.org/packages/?name=networkmanager-openvpn) for [OpenVPN](/index.php/OpenVPN "OpenVPN")
*   [networkmanager-pptp](https://www.archlinux.org/packages/?name=networkmanager-pptp) for [PPTP Client](/index.php/PPTP_Client "PPTP Client")
*   [networkmanager-vpnc](https://www.archlinux.org/packages/?name=networkmanager-vpnc) for [Vpnc](/index.php/Vpnc "Vpnc")
*   [networkmanager-strongswan](https://www.archlinux.org/packages/?name=networkmanager-strongswan) for [strongSwan](/index.php/StrongSwan "StrongSwan")
*   [networkmanager-fortisslvpn-git](https://aur.archlinux.org/packages/networkmanager-fortisslvpn-git/)
*   [networkmanager-iodine-git](https://aur.archlinux.org/packages/networkmanager-iodine-git/)
*   [networkmanager-libreswan](https://aur.archlinux.org/packages/networkmanager-libreswan/)
*   [networkmanager-l2tp](https://aur.archlinux.org/packages/networkmanager-l2tp/)
*   [networkmanager-ssh-git](https://aur.archlinux.org/packages/networkmanager-ssh-git/)
*   [network-manager-sstp](https://www.archlinux.org/packages/?name=network-manager-sstp)

**Warning:** VPN support is [unstable](https://bugzilla.gnome.org/buglist.cgi?quicksearch=networkmanager%20vpn), check the daemon processes options set via the GUI correctly and double-check with each package release.[[2]](https://bugzilla.gnome.org/show_bug.cgi?id=755350)

**Note:** To have fully functioning DNS resolution when using VPN, you should set up [split DNS](#DNS_caching_and_split_DNS).

## Usage

NetworkManager comes with [nmcli(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nmcli.1) and [nmtui(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nmtui.1).

### nmcli examples

List nearby wifi networks:

```
$ nmcli device wifi list

```

Connect to a wifi network:

```
$ nmcli device wifi connect *SSID* password *password*

```

Connect to a hidden network:

```
$ nmcli device wifi connect *SSID* password *password* hidden yes

```

Connect to a wifi on the `wlan1` wifi interface:

```
$ nmcli device wifi connect *SSID* password *password* ifname wlan1 *profile_name*

```

Disconnect an interface:

```
$ nmcli device disconnect ifname eth0

```

Reconnect an interface marked as disconnected:

```
$ nmcli connection up uuid *UUID*

```

Get a list of UUIDs:

```
$ nmcli connection show

```

See a list of network devices and their state:

```
$ nmcli device

```

Turn off wifi:

```
$ nmcli radio wifi off

```

### Edit a connection

For a comprehensive list of settings, see [nm-settings(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nm-settings.5).

You have three methods to configure a connection after it has been created:

	nmcli interactive editor

	`nmcli connection edit *connection-id*`.
Usage is well documented from the editor.

	nmcli command line interface

	`nmcli connection modify *connection-id* *setting*.*property* *value*`. See [nmcli(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nmcli.1) for usage.

	Connection file

	In `/etc/NetworkManager/system-connections/`, modify the corresponding `*connection-id*.nmconnection` file .
Do not forget to reload the configuration file with `nmcli connection reload`

## Front-ends

To configure and have easy access to NetworkManager, most users will want to install an applet. This GUI front-end usually resides in the system tray (or notification area) and allows network selection and configuration of NetworkManager. Various desktop environments have their own applet. Otherwise you can use [#nm-applet](#nm-applet).

### GNOME

[GNOME](/index.php/GNOME "GNOME") has a built-in tool, accessible from the Network settings.

### KDE Plasma

[Install](/index.php/Install "Install") the [plasma-nm](https://www.archlinux.org/packages/?name=plasma-nm) package. After that, add it to the KDE taskbar via the *Panel options > Add widgets > Networks* menu.

### nm-applet

[network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) is a GTK+ 3 front-end which works under Xorg environments with a systray.

To store connection secrets install and configure [GNOME/Keyring](/index.php/GNOME/Keyring "GNOME/Keyring").

Be aware that after enabling the tick-box option `Make available to other users` for a connection, NetworkManager stores the password in plain-text, though the respective file is accessible only to root (or other users via `nm-applet`). See [#Encrypted Wi-Fi passwords](#Encrypted_Wi-Fi_passwords).

In order to run `nm-applet` without a systray, you can use [trayer](https://www.archlinux.org/packages/?name=trayer) or [stalonetray](https://www.archlinux.org/packages/?name=stalonetray). For example, you can add a script like this one in your path:

 `nmgui` 
```
#!/bin/sh
nm-applet    2>&1 > /dev/null &
stalonetray  2>&1 > /dev/null
killall nm-applet

```

When you close the *stalonetray* window, it closes `nm-applet` too, so no extra memory is used once you are done with network settings.

The applet can show notifications for events such as connecting to or disconnecting from a WiFi network. For these notifications to display, ensure that you have a notification server installed - see [Desktop notifications](/index.php/Desktop_notifications "Desktop notifications"). If you use the applet without a notification server, you might see some messages in stdout/stderr, and the app might hang. See [[3]](https://bugzilla.gnome.org/show_bug.cgi?id=788313).

In order to run `nm-applet` with such notifications disabled, start the applet with the following command:

```
$ nm-applet --no-agent

```

**Tip:** `nm-applet` might be started automatically with a [autostart desktop file](/index.php/XDG_Autostart "XDG Autostart"), to add the --no-agent option modify the Exec line there, i.e. `Exec=nm-applet --no-agent` 

#### Appindicator

Appindicator support is available in *nm-applet* however it is not compiled into the official package, see [FS#51740](https://bugs.archlinux.org/task/51740). To use nm-applet in an Appindicator environment, replace [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) with [network-manager-applet-indicator](https://aur.archlinux.org/packages/network-manager-applet-indicator/) and then start the applet with the following command:

```
$ nm-applet --indicator

```

### networkmanager-dmenu

Alternatively there is [networkmanager-dmenu-git](https://aur.archlinux.org/packages/networkmanager-dmenu-git/) which is a small script to manage NetworkManager connections with [dmenu](/index.php/Dmenu "Dmenu") or [rofi](/index.php/Rofi "Rofi") instead of `nm-applet`. It provides all essential features such as connection to existing NetworkManager wifi or wired connections, connect to new wifi connections, requests passphrase if required, connect to existing VPN connections, enable/disable networking, launch *nm-connection-editor* GUI, connect to Bluetooth networks.

## Configuration

NetworkManager will require some additional steps to be able run properly. Make sure you have configured `/etc/hosts` as described in [Network configuration#Set the hostname](/index.php/Network_configuration#Set_the_hostname "Network configuration") section.

### Enable NetworkManager

NetworkManager is [controlled](/index.php/Systemd#Using_units "Systemd") with the `NetworkManager.service` [systemd](/index.php/Systemd "Systemd") unit. Once the NetworkManager daemon is started, it will automatically connect to any available "system connections" that have already been configured. Any "user connections" or unconfigured connections will need *nmcli* or an applet to configure and connect.

NetworkManager has a global configuration file at `/etc/NetworkManager/NetworkManager.conf`. Addition configuration files can be placed in `/etc/NetworkManager/conf.d/`. Usually no configuration needs to be done to the global defaults.

### Enable NetworkManager Wait Online

If you have services which fail if they are started before the network is up, you may use `NetworkManager-wait-online.service` in addition to `NetworkManager.service`. This is, however, rarely necessary because most networked daemons start up okay, even if the network has not been configured yet.

In some cases, the service will still fail to start successfully on boot due to the timeout setting in `/usr/lib/systemd/system/NetworkManager-wait-online.service` being too short. Change the default timeout from 30 to a higher value.

### Set up PolicyKit permissions

See [General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") for setting up a working session.

With a working session, you have several options for granting the necessary privileges to NetworkManager:

*   *Option 1.* Run a [Polkit](/index.php/Polkit "Polkit") authentication agent when you log in, such as `/usr/lib/polkit-gnome/polkit-gnome-authentication-agent-1` (part of [polkit-gnome](https://www.archlinux.org/packages/?name=polkit-gnome)). You will be prompted for your password whenever you add or remove a network connection.
*   *Option 2.* [Add](/index.php/Users_and_groups#Group_management "Users and groups") yourself to the `wheel` group. You will not have to enter your password, but your user account may be granted other permissions as well, such as the ability to use [sudo](/index.php/Sudo "Sudo") without entering the root password.
*   *Option 3.* [Add](/index.php/Users_and_groups#Group_management "Users and groups") yourself to the `network` group and create the following file:

 `/etc/polkit-1/rules.d/50-org.freedesktop.NetworkManager.rules` 
```
polkit.addRule(function(action, subject) {
  if (action.id.indexOf("org.freedesktop.NetworkManager.") == 0 && subject.isInGroup("network")) {
    return polkit.Result.YES;
  }
});

```

	All users in the `network` group will be able to add and remove networks without a password. This will not work under [systemd](/index.php/Systemd "Systemd") if you do not have an active session with *systemd-logind*.

### Proxy settings

NetworkManager does not directly handle proxy settings, but if you are using [GNOME](/index.php/GNOME "GNOME") or [KDE](/index.php/KDE "KDE"), you could use [proxydriver](http://marin.jb.free.fr/proxydriver/) which handles proxy settings using NetworkManager's information. proxydriver is found in the package [proxydriver](https://aur.archlinux.org/packages/proxydriver/).

In order for *proxydriver* to be able to change the proxy settings, you would need to execute this command, as part of the GNOME startup process (see [GNOME#Autostart](/index.php/GNOME#Autostart "GNOME")).

```
xhost +si:localuser:*username*

```

See also [Proxy settings](/index.php/Proxy_settings "Proxy settings").

### Checking connectivity

NetworkManager can try to reach a page on Internet when connecting to a network. [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) is configured by default in `/usr/lib/NetworkManager/conf.d/20-connectivity.conf` to check connectivity to archlinux.org. To use a different webserver or disable connectivity checking create `/etc/NetworkManager/conf.d/20-connectivity.conf`, see [NetworkManager.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/NetworkManager.conf.5#CONNECTIVITY_SECTION).

For those behind a captive portal, the desktop manager can automatically open a window asking for credentials.

### DHCP client

By default NetworkManager will use its internal DHCP client, based on systemd-networkd. To use a different DHCP client [install](/index.php/Install "Install") one of the alternatives:

*   [dhclient](https://www.archlinux.org/packages/?name=dhclient) - ISC’s DHCP client.
*   [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) - [dhcpcd](/index.php/Dhcpcd "Dhcpcd").

**Warning:** NetworkManger does not support using dhcpcd for IPv6\. See [NetworkManager issue #5](https://gitlab.freedesktop.org/NetworkManager/NetworkManager/issues/5).

To change the DHCP client backend, set the option `main.dhcp=*dhcp_client_name*` with a configuration file in `/etc/NetworkManager/conf.d/`. E.g.:

 `/etc/NetworkManager/conf.d/dhcp-client.conf` 
```
[main]
dhcp=dhclient
```

### DNS management

NetworkManager's DNS management is described in the GNOME project's wiki page—[Projects/NetworkManager/DNS](https://wiki.gnome.org/Projects/NetworkManager/DNS).

#### DNS caching and split DNS

NetworkManager has a plugin to enable DNS caching and split DNS using [dnsmasq](/index.php/Dnsmasq "Dnsmasq") or [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved"), or Unbound via dnssec-trigger. The advantages of this setup is that DNS lookups will be cached, shortening resolve times, and DNS lookups of VPN hosts will be routed to the relevant VPN's DNS servers. This is especially useful if you are connected to more than one VPN.

##### dnsmasq

Make sure [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) has been installed. Then set `main.dns=dnsmasq` with a configuration file in `/etc/NetworkManager/conf.d/`:

 `/etc/NetworkManager/conf.d/dns.conf` 
```
[main]
dns=dnsmasq
```

Now [restart](/index.php/Restart "Restart") `NetworkManager.service`. NetworkManager will automatically start dnsmasq and add `127.0.0.1` to `/etc/resolv.conf`. The original DNS servers can be found in `/run/NetworkManager/no-stub-resolv.conf`. You can verify dnsmasq is being used by doing the same DNS lookup twice with `drill example.com` and verifying the server and query times.

**Note:** You do not need to start `dnsmasq.service` or edit `/etc/dnsmasq.conf`. NetworkManager will start dnsmasq without using the systemd service and without reading the dnsmasq's default configuration file(s).

###### Custom configuration

Custom configurations can be created for *dnsmasq* by creating configuration files in `/etc/NetworkManager/dnsmasq.d/`. For example, to change the size of the DNS cache (which is stored in RAM):

 `/etc/NetworkManager/dnsmasq.d/cache.conf`  `cache-size=1000` 
**Tip:** Check the configuration file syntax with `dnsmasq --test --conf-file=/dev/null --conf-dir=/etc/NetworkManager/dnsmasq.d`.

See [dnsmasq(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dnsmasq.8) for all available options.

###### IPv6

Enabling `dnsmasq` in NetworkManager may break IPv6-only DNS lookups (i.e. `drill -6 [hostname]`) which would otherwise work. In order to resolve this, creating the following file will configure *dnsmasq* to also listen to the IPv6 loopback:

 `/etc/NetworkManager/dnsmasq.d/ipv6_listen.conf`  `listen-address=::1` 

In addition, `dnsmasq` also does not prioritize upstream IPv6 DNS. Unfortunately NetworkManager does not do this ([Ubuntu Bug](https://bugs.launchpad.net/ubuntu/+source/network-manager/+bug/936712)). A workaround would be to disable IPv4 DNS in the NetworkManager config, assuming one exists

###### DNSSEC

The dnsmasq instance started by NetworkManager by default will not validate [DNSSEC](/index.php/DNSSEC "DNSSEC") since it is started with the `--proxy-dnssec` option. It will trust whatever DNSSEC information it gets from the upstream DNS server.

For dnsmasq to properly validate DNSSEC, thus breaking DNS resolution with name servers that do not support it, create the following configuration file:

 `/etc/NetworkManager/dnsmasq.d/dnssec.conf` 
```
conf-file=/usr/share/dnsmasq/trust-anchors.conf
dnssec
```

##### systemd-resolved

NetworkManager can use [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved") as a DNS resolver and cache. Make sure that *systemd-resolved* is properly configured and that `systemd-resolved.service` is [started](/index.php/Started "Started") before using it.

systemd-resolved will be used automatically if `/etc/resolv.conf` is a [symlink](/index.php/Systemd-resolved#DNS "Systemd-resolved") to `/run/systemd/resolve/stub-resolv.conf`, `/run/systemd/resolve/resolv.conf` or `/usr/lib/systemd/resolv.conf`.

You can enable it explicitly by setting `main.dns=systemd-resolved` with a configuration file in `/etc/NetworkManager/conf.d/`:

 `/etc/NetworkManager/conf.d/dns.conf` 
```
[main]
dns=systemd-resolved
```

##### DNS resolver with an openresolv subscriber

If [openresolv](/index.php/Openresolv "Openresolv") has a subscriber for your local [DNS resolver](/index.php/DNS_resolver "DNS resolver"), set up the subscriber and [configure NetworkManager to use openresolv](#Use_openresolv).

Because NetworkManager advertises a single "interface" to *resolvconf*, it is not possible to implement split DNS between to NetworkManager connections. See [NetworkManager issue 153](https://gitlab.freedesktop.org/NetworkManager/NetworkManager/issues/153).

This can be partially mitigated if you set `private="*"` in `/etc/resolvconf.conf`[[5]](https://roy.marples.name/projects/openresolv/config). Any queries for domains that are not in search domain list will not get forwarded. They will be handled according to the local resolver's configuration, for example, forwarded to another DNS server or resolved recursively from the DNS root.

#### Setting custom DNS servers in a connection

##### Setting custom DNS servers in a connection (GUI)

Setup will depend on the type of front-end used; the process usually involves right-clicking on the applet, editing (or creating) a profile, and then choosing DHCP type as *Automatic (specify addresses)*. The DNS addresses will need to be entered and are usually in this form: `127.0.0.1, *DNS-server-one*, ...`.

##### Setting custom DNS servers in a connection (nmcli / connection file)

To setup DNS Servers per connection, you can use the `dns` field (and the associated `dns-search` and `dns-options`) in the [connection settings](#Edit_a_connection).

If `method` is set to `auto` (when you use DHCP), you need to set `ignore-auto-dns` to `yes`.

#### /etc/resolv.conf

By default `/etc/resolv.conf` is managed by *NetworkManager* unless it is a symlink.

It can be configured to write it through [openresolv](#Use_openresolv) or to [not touch it at all](#Unmanaged_/etc/resolv.conf).

Using openresolv allows NetworkManager to coexists with other *resolvconf* supporting software or, for example, to run a local DNS caching and split-DNS resolver for which openresolv has a [subscriber](/index.php/Openresolv#Subscribers "Openresolv").

*NetworkManager* also offers hooks via so called dispatcher scripts that can be used to alter the `/etc/resolv.conf` after network changes. See [#Network services with NetworkManager dispatcher](#Network_services_with_NetworkManager_dispatcher) and [NetworkManager(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/NetworkManager.8) for more information.

**Note:**

*   If NetworkManager is configured to use either [dnsmasq](#dnsmasq) or [systemd-resolved](#systemd-resolved), then the appropriate loopback addresses will be written to `/etc/resolv.conf`.
*   The `resolv.conf` file NetworkManager writes or would write to `/etc/resolv.conf` can be found at `/run/NetworkManager/resolv.conf`.
*   A `resolv.conf` file with the acquired name servers and search domains can be found at `/run/NetworkManager/no-stub-resolv.conf`.

##### Unmanaged /etc/resolv.conf

To stop NetworkManager from touching `/etc/resolv.conf`, set `main.dns=none` with a configuration file in `/etc/NetworkManager/conf.d/`:

 `/etc/NetworkManager/conf.d/dns.conf` 
```
[main]
dns=none
```

**Note:** See [#DNS caching and split DNS](#DNS_caching_and_split_DNS), to configure NetworkManager using other DNS backends like [dnsmasq](/index.php/Dnsmasq "Dnsmasq") and [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved"), instead of using `main.dns=none`.

After that `/etc/resolv.conf` might be a broken symlink that you will need to remove. Then, just create a new `/etc/resolv.conf` file.

##### Use openresolv

To configure NetworkManager to use [openresolv](/index.php/Openresolv "Openresolv"), set `main.rc-manager=resolvconf` with a configuration file in `/etc/NetworkManager/conf.d/`:

 `/etc/NetworkManager/conf.d/rc-manager.conf` 
```
[main]
rc-manager=resolvconf
```

## Network services with NetworkManager dispatcher

There are quite a few network services that you will not want running until NetworkManager brings up an interface. NetworkManager has the ability to start services when you connect to a network and stop them when you disconnect (e.g. when using [NFS](/index.php/NFS "NFS"), [SMB](/index.php/SMB "SMB") and [NTPd](/index.php/NTPd "NTPd")).

To activate the feature you need to [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `NetworkManager-dispatcher.service`.

Once the service is active, scripts can be added to the `/etc/NetworkManager/dispatcher.d` directory.

Scripts must be owned by **root**, otherwise the dispatcher will not execute them. For added security, set group [ownership](/index.php/Ownership "Ownership") to root as well:

```
# chown root:root /etc/NetworkManager/dispatcher.d/*10-script.sh*

```

Make sure the file has correct permissions:

```
# chmod 755 /etc/NetworkManager/dispatcher.d/*10-script.sh*

```

The scripts will be run in alphabetical order at connection time, and in reverse alphabetical order at disconnect time. To ensure what order they come up in, it is common to use numerical characters prior to the name of the script (e.g. `10-portmap` or `30-netfs` (which ensures that the *portmapper* is up before NFS mounts are attempted).

Scripts will receive the following arguments:

*   **Interface name:** e.g. `eth0`
*   **Interface status:** *up* or *down*
*   **VPN status:** *vpn-up* or *vpn-down*

**Warning:** If you connect to foreign or public networks, be aware of what services you are starting and what servers you expect to be available for them to connect to. You could make a security hole by starting the wrong services while connected to a public network.

### Avoiding the dispatcher timeout

If the above is working, then this section is not relevant. However, there is a general problem related to running dispatcher scripts which take longer to be executed. Initially an internal timeout of three seconds only was used. If the called script did not complete in time, it was killed. Later the timeout was extended to about 20 seconds (see the [Bugtracker](https://bugzilla.redhat.com/show_bug.cgi?id=982734) for more information). If the timeout still creates the problem, a work around may be to modify the dispatcher service file `/usr/lib/systemd/system/NetworkManager-dispatcher.service` to remain active after exit:

 `/etc/systemd/system/NetworkManager-dispatcher.service.d/remain_after_exit.conf` 
```
[Service]
RemainAfterExit=yes
```

Now start and enable the modified `NetworkManager-dispatcher` service.

**Warning:** Adding the `RemainAfterExit` line to it will prevent the dispatcher from closing. Unfortunately, the dispatcher **has** to close before it can run your scripts again. With it the dispatcher will not time out but it also will not close, which means that the scripts will only run once per boot. Therefore, do not add the line unless the timeout is definitely causing a problem.

### Dispatcher examples

#### Mount remote folder with sshfs

As the script is run in a very restrictive environment, you have to export `SSH_AUTH_SOCK` in order to connect to your SSH agent. There are different ways to accomplish this, see [this message](https://bbs.archlinux.org/viewtopic.php?pid=1042030#p1042030) for more information. The example below works with [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring"), and will ask you for the password if not unlocked already. In case NetworkManager connects automatically on login, it is likely *gnome-keyring* has not yet started and the export will fail (hence the sleep). The `UUID` to match can be found with the command `nmcli connection status` or `nmcli connection list`.

```
#!/bin/sh
USER='username'
REMOTE='user@host:/remote/path'
LOCAL='/local/path'

interface=$1 status=$2
if [ "$CONNECTION_UUID" = "*uuid*" ]; then
  case $status in
    up)
      SSH_AUTH_SOCK=$(find /tmp -maxdepth 1 -type s -user "$USER" -name 'ssh')
      export SSH_AUTH_SOCK
      su "$USER" -c "sshfs $REMOTE $LOCAL"
      ;;
    down)
      fusermount -u "$LOCAL"
      ;;
  esac
fi

```

#### Mounting of SMB shares

Some [SMB](/index.php/SMB "SMB") shares are only available on certain networks or locations (e.g. at home). You can use the dispatcher to only mount SMB shares that are present at your current location.

The following script will check if we connected to a specific network and mount shares accordingly:

 `/etc/NetworkManager/dispatcher.d/30-mount-smb.sh` 
```
#!/bin/sh

# Find the connection UUID with "nmcli connection show" in terminal.
# All NetworkManager connection types are supported: wireless, VPN, wired...
if [ "$2" = "up" ]; then
  if [ "$CONNECTION_UUID" = "uuid" ]; then
    mount /your/mount/point & 
    # add more shares as needed
  fi
fi

```

The following script will unmount all shares before a disconnect from a specific network:

 `/etc/NetworkManager/dispatcher.d/pre-down.d/30-mount-smb.sh` 
```
#!/bin/sh
umount -a -l -t cifs

```

**Note:**

*   Make sure this script is located in the `pre-down.d` sub-directory as shown above, otherwise it will unmount all shares on any connection state change.
*   Since NetworkManager 0.9.8, the *pre-down* and *down* events are not executed on shutdown or restart, see [this bug report](https://bugzilla.gnome.org/show_bug.cgi?id=701242) for more info.

An alternative is to use the script as seen in [NFS#Using a NetworkManager dispatcher](/index.php/NFS#Using_a_NetworkManager_dispatcher "NFS"):

 `/etc/NetworkManager/dispatcher.d/30-smb.sh` 
```
#!/bin/bash

# Find the connection UUID with "nmcli con show" in terminal.
# All NetworkManager connection types are supported: wireless, VPN, wired...
WANTED_CON_UUID="CHANGE-ME-NOW-9c7eff15-010a-4b1c-a786-9b4efa218ba9"

if [[ "$CONNECTION_UUID" == "$WANTED_CON_UUID" ]]; then

    # Script parameter $1: NetworkManager connection name, not used
    # Script parameter $2: dispatched event

    case "$2" in
        "up")
            mount -a -t cifs
            ;;
        "pre-down");&
        "vpn-pre-down")
            umount -l -a -t cifs >/dev/null
            ;;
    esac
fi

```

**Note:** This script ignores mounts with the `noauto` option, remove this mount option or use `auto` to allow the dispatcher to manage these mounts.

Create a symlink inside `/etc/NetworkManager/dispatcher.d/pre-down` to catch the `pre-down` events:

```
# ln -s /etc/NetworkManager/dispatcher.d/30-smb.sh /etc/NetworkManager/dispatcher.d/pre-down.d/30-smb.sh

```

#### Mounting of NFS shares

See [NFS#Using a NetworkManager dispatcher](/index.php/NFS#Using_a_NetworkManager_dispatcher "NFS").

#### Use dispatcher to automatically toggle wireless depending on LAN cable being plugged in

The idea is to only turn Wi-Fi on when the LAN cable is unplugged (for example when detaching from a laptop dock), and for Wi-Fi to be automatically disabled, once a LAN cable is plugged in again.

Create the following dispatcher script ([Source](https://superuser.com/questions/233448/disable-wlan-if-wired-cable-network-is-available)), replacing `LAN_interface` with yours.

 `/etc/NetworkManager/dispatcher.d/wlan_auto_toggle.sh` 
```
#!/bin/sh

if [ "$1" = "LAN_interface" ]; then
    case "$2" in
        up)
            nmcli radio wifi off
            ;;
        down)
            nmcli radio wifi on
            ;;
    esac
fi

```

**Note:** You can get a list of interfaces using [nmcli](#nmcli_examples). The ethernet (LAN) interfaces start with `en`, e.g. `enp0s5`

#### Use dispatcher to connect to a VPN after a network connection is established

In this example we want to connect automatically to a previously defined VPN connection after connecting to a specific Wi-Fi network. First thing to do is to create the dispatcher script that defines what to do after we are connected to the network.

**Note:** This script will require [wireless_tools](https://www.archlinux.org/packages/?name=wireless_tools) in order to use `iwgetid`.
 `/etc/NetworkManager/dispatcher.d/vpn-up` 
```
#!/bin/sh
VPN_NAME="name of VPN connection defined in NetworkManager"
ESSID="Wi-Fi network ESSID (not connection name)"

interface=$1 status=$2
case $status in
  up|vpn-down)
    if iwgetid | grep -qs ":\"$ESSID\""; then
      nmcli connection up id "$VPN_NAME"
    fi
    ;;
  down)
    if iwgetid | grep -qs ":\"$ESSID\""; then
      if nmcli connection show --active | grep "$VPN_NAME"; then
        nmcli connection down id "$VPN_NAME"
      fi
    fi
    ;;
esac

```

If you would like to attempt to automatically connect to VPN for all Wi-Fi networks, you can use the following definition of the ESSID: `ESSID=$(iwgetid -r)`. Remember to set the script's permissions [accordingly](#Network_services_with_NetworkManager_dispatcher).

Trying to connect with the above script may still fail with `NetworkManager-dispatcher.service` complaining about 'no valid VPN secrets', because of [the way VPN secrets are stored](https://developer.gnome.org/NetworkManager/0.9/secrets-flags.html). Fortunately, there are different options to give the above script access to your VPN password.

1: One of them requires editing the VPN connection configuration file to make NetworkManager store the secrets by itself rather than inside a keyring [that will be inaccessible for root](https://bugzilla.redhat.com/show_bug.cgi?id=710552): open up `/etc/NetworkManager/system-connections/*name of your VPN connection*` and change the `password-flags` and `secret-flags` from `1` to `0`.

If that alone does not work, you may have to create a `passwd-file` in a safe location with the same permissions and ownership as the dispatcher script, containing the following:

 `/path/to/passwd-file` 
```
vpn.secrets.password:YOUR_PASSWORD

```

The script must be changed accordingly, so that it gets the password from the file:

 `/etc/NetworkManager/dispatcher.d/vpn-up` 
```
#!/bin/sh
VPN_NAME="name of VPN connection defined in NetworkManager"
ESSID="Wi-Fi network ESSID (not connection name)"

interface=$1 status=$2
case $status in
  up|vpn-down)
    if iwgetid | grep -qs ":\"$ESSID\""; then
      nmcli connection up id "$VPN_NAME" passwd-file /path/to/passwd-file
    fi
    ;;
  down)
    if iwgetid | grep -qs ":\"$ESSID\""; then
      if nmcli connection show --active | grep "$VPN_NAME"; then
        nmcli connection down id "$VPN_NAME"
      fi
    fi
    ;;
esac

```

2: Alternatively, change the `password-flags` and put the password directly in the configuration file adding the section `vpn-secrets`:

```
 [vpn]
 ....
 password-flags=0

 [vpn-secrets]
 password=*your_password*

```

**Note:** It may now be necessary to re-open the NetworkManager connection editor and save the VPN passwords/secrets again.

#### OpenNTPD

See [OpenNTPD#Using NetworkManager dispatcher](/index.php/OpenNTPD#Using_NetworkManager_dispatcher "OpenNTPD").

## Testing

NetworkManager applets are designed to load upon login so no further configuration should be necessary for most users. If you have already disabled your previous network settings and disconnected from your network, you can now test if NetworkManager will work. The first step is to [start](/index.php/Start "Start") `NetworkManager.service`.

Some applets will provide you with a `.desktop` file so that the NetworkManager applet can be loaded through the application menu. If it does not, you are going to either have to discover the command to use or logout and login again to start the applet. Once the applet is started, it will likely begin polling network connections with for auto-configuration with a DHCP server.

To start the GNOME applet in non-xdg-compliant window managers like [awesome](/index.php/Awesome "Awesome"):

```
nm-applet --sm-disable &

```

For static IP addresses, you will have to configure NetworkManager to understand them. The process usually involves right-clicking the applet and selecting something like 'Edit Connections'.

## Tips and tricks

### Encrypted Wi-Fi passwords

By default, NetworkManager stores passwords in clear text in the connection files at `/etc/NetworkManager/system-connections/`. To print the stored passwords, use the following command:

```
# grep -H '^psk=' /etc/NetworkManager/system-connections/*

```

The passwords are accessible to the root user in the filesystem and to users with access to settings via the GUI (e.g. `nm-applet`).

It is preferable to save the passwords in encrypted form in a keyring instead of clear text. The downside of using a keyring is that the connections have to be set up for each user.

#### Using GNOME Keyring

The keyring daemon has to be started and the keyring needs to be unlocked for the following to work.

Furthermore, NetworkManager needs to be configured not to store the password for all users. Using GNOME `nm-applet`, run `nm-connection-editor` from a terminal, select a network connection, click `Edit`, select the `Wifi-Security` tab and click on the right icon of password and check `Store the password only for this user`.

#### Using KDE Wallet

Using KDE's [plasma-nm](https://www.archlinux.org/packages/?name=plasma-nm), click the applet, click on the top right `Settings` icon, click on a network connection, in the `General settings` tab, untick `all users may connect to this network`. If the option is ticked, the passwords will still be stored in clear text, even if a keyring daemon is running.

If the option was selected previously and you un-tick it, you may have to use the `reset` option first to make the password disappear from the file. Alternatively, delete the connection first and set it up again.

### Sharing internet connection over Wi-Fi

You can share your internet connection (e.g. 3G or wired) with a few clicks. You will need a supported Wi-Fi card (Cards based on Atheros AR9xx or at least AR5xx are probably best choice). Please note that a [firewall](/index.php/Firewall "Firewall") may interfere with internet sharing.

[Install](/index.php/Install "Install") the [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) package to be able to actually share the connection.

Create the shared connection:

*   Click on applet and choose *Create new wireless network*.
*   Follow wizard (if using WEP, be sure to use 5 or 13 character long password, different lengths will fail).
    *   Choose either [Hotspot](https://fedoraproject.org/wiki/Features/RealHotspot "fedora:Features/RealHotspot") or Ad-hoc as Wi-Fi mode.

The connection will be saved and remain stored for the next time you need it.

**Note:** Android does not support connecting to Ad-hoc networks. To share a connection with Android use infrastructure mode (i.e. set Wi-Fi mode to "Hotspot").

### Sharing internet connection over Ethernet

Scenario: your device has internet connection over wi-fi and you want to share the internet connection to other devices over ethernet.

Requirements:

*   [Install](/index.php/Install "Install") the [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) package to be able to actually share the connection.
*   Your internet connected device and the other devices are connected over a suitable ethernet cable (this usually means a cross over cable or a switch in between).
*   Internet sharing is not blocked by a [firewall](/index.php/Firewall "Firewall").

Steps:

*   Run `nm-connection-editor` from terminal.
*   Add a new ethernet connection.
*   Give it some sensible name. For example "Shared Internet"
*   Go to "IPv4 Settings".
*   For "Method:" select "Shared to other computers".
*   Save

Now you should have a new option "Shared Internet" under the Wired connections in NetworkManager.

### Checking if networking is up inside a cron job or script

Some *cron* jobs require networking to be up to succeed. You may wish to avoid running these jobs when the network is down. To accomplish this, add an **if** test for networking that queries NetworkManager's *nm-tool* and checks the state of networking. The test shown here succeeds if any interface is up, and fails if they are all down. This is convenient for laptops that might be hardwired, might be on wireless, or might be off the network.

```
if [ $(nm-tool|grep State|cut -f2 -d' ') == "connected" ]; then
    #Whatever you want to do if the network is online
else
    #Whatever you want to do if the network is offline - note, this and the else above are optional
fi

```

This useful for a `cron.hourly` script that runs *fpupdate* for the F-Prot virus scanner signature update, as an example. Another way it might be useful, with a little modification, is to differentiate between networks using various parts of the output from *nm-tool*; for example, since the active wireless network is denoted with an asterisk, you could grep for the network name and then grep for a literal asterisk.

### Connect to network with secret on boot

By default, NetworkManager will not connect to networks requiring a secret automatically on boot. This is because it locks such connections to the user who makes it by default, only connecting after they have logged in. To change this, do the following:

1.  Right click on the `nm-applet` icon in your panel and select Edit Connections and open the Wireless tab
2.  Select the connection you want to work with and click the Edit button
3.  Check the boxes “Connect Automatically” and “Available to all users”

Log out and log back in to complete.

### Automatically unlock keyring after login

NetworkManager requires access to the login keyring to connect to networks requiring a secret. Under most circumstances, this keyring is unlocked automatically at login, but if it is not, and NetworkManager is not connecting on login, you can try the following.

#### GNOME

*   In `/etc/pam.d/gdm` (or your corresponding daemon in `/etc/pam.d`), add these lines at the end of the "auth" and "session" blocks if they do not exist already:

```
 auth            optional        pam_gnome_keyring.so
 session         optional        pam_gnome_keyring.so  auto_start

```

*   In `/etc/pam.d/passwd`, use this line for the 'password' block:

```
 password    optional    pam_gnome_keyring.so

```

	Next time you log in, you should be asked if you want the password to be unlocked automatically on login.

#### SLiM login manager

See [SLiM#Gnome Keyring](/index.php/SLiM#Gnome_Keyring "SLiM").

### OpenConnect with password in KWallet

While you may type both values at connection time, [plasma-nm](https://www.archlinux.org/packages/?name=plasma-nm) 0.9.3.2-1 and above are capable of retrieving OpenConnect username and password directly from [KWallet](/index.php/KWallet "KWallet").

Open "KDE Wallet Manager" and look up your OpenConnect VPN connection under "Network Management|Maps". Click "Show values" and enter your credentials in key "VpnSecrets" in this form (replace *username* and *password* accordingly):

```
form:main:username%SEP%*username*%SEP%form:main:password%SEP%*password*

```

Next time you connect, username and password should appear in the "VPN secrets" dialog box.

### Ignore specific devices

Sometimes it may be desired that NetworkManager ignores specific devices and does not try to configure addresses and routes for them. You can quickly and easily ignore devices by MAC or interface-name by using the following in `/etc/NetworkManager/conf.d/unmanaged.conf`:

```
[keyfile]
unmanaged-devices=mac:00:22:68:1c:59:b1;mac:00:1E:65:30:D1:C4;interface-name:eth0

```

After you have put this in, [restart](/index.php/Restart "Restart") `NetworkManager.service`, and you should be able to configure interfaces without NetworkManager altering what you have set.

### Configuring MAC address randomization

**Note:** Disabling MAC address randomization may be needed to get (stable) link connection [[7]](https://bbs.archlinux.org/viewtopic.php?id=220101) and/or networks that restrict devices based on their MAC Address or have a limit network capacity.

MAC randomization can be used for increased privacy by not disclosing your real MAC address to the network.

NetworkManager supports two types MAC Address Randomization: randomization during scanning, and for network connections. Both modes can be configured by modifying `/etc/NetworkManager/NetworkManager.conf` or by creating a separate configuration file in `/etc/NetworkManager/conf.d/` which is recommended since the aforementioned config file may be overwritten by NetworkManager.

Randomization during Wi-Fi scanning is enabled by default, but it may be disabled by adding the following lines to `/etc/NetworkManager/NetworkManager.conf` or a dedicated configuration file under `/etc/NetworkManager/conf.d`:

 `/etc/NetworkManager/conf.d/wifi_rand_mac.conf` 
```
[device]
wifi.scan-rand-mac-address=no
```

MAC randomization for network connections can be set to different modes for both wireless and ethernet interfaces. See the [GNOME blog post](https://blogs.gnome.org/thaller/2016/08/26/mac-address-spoofing-in-networkmanager-1-4-0/) for more details on the different modes.

In terms of MAC randomization the most important modes are `stable` and `random`. `stable` generates a random MAC address when you connect to a new network and associates the two permanently. This means that you will use the same MAC address every time you connect to that network. In contrast, `random` will generate a new MAC address every time you connect to a network, new or previously known. You can configure the MAC randomization by adding the desired configuration under `/etc/NetworkManager/conf.d`.

```
[device-mac-randomization]
# "yes" is already the default for scanning
wifi.scan-rand-mac-address=yes

[connection-mac-randomization]
# Randomize MAC for every ethernet connection
ethernet.cloned-mac-address=random
# Generate a random MAC for each WiFi and associate the two permanently.
wifi.cloned-mac-address=stable

```

See the following [GNOME blog post](https://blogs.gnome.org/thaller/2016/08/26/mac-address-spoofing-in-networkmanager-1-4-0/) for more details.

### Enable IPv6 Privacy Extensions

See [IPv6#NetworkManager](/index.php/IPv6#NetworkManager "IPv6").

### Working with wired connections

By default, NetworkManager generates a connection profile for each wired ethernet connection it finds. At the point when generating the connection, it does not know whether there will be more ethernet adapters available. Hence, it calls the first wired connection "Wired connection 1". You can avoid generating this connection, by configuring `no-auto-default` (see [NetworkManager.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/NetworkManager.conf.5)), or by simply deleting it. Then NetworkManager will remember not to generate a connection for this interface again.

You can also edit the connection (and persist it to disk) or delete it. NetworkManager will not re-generate a new connection. Then you can change the name to whatever you want. You can use something like nm-connection-editor for this task.

### Using iwd as the Wi-Fi backend

To enable the experimental [iwd](/index.php/Iwd "Iwd") backend create the following configuration file:

 `/etc/NetworkManager/conf.d/wifi_backend.conf` 
```
[device]
wifi.backend=iwd
```

## Troubleshooting

### No prompt for password of secured Wi-Fi networks

When trying to connect to a secured Wi-Fi network, no prompt for a password is shown and no connection is established. This happens when no keyring package is installed. An easy solution is to install [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring). If you want the passwords to be stored in encrypted form, follow [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring") to set up the *gnome-keyring-daemon*.

### No traffic via PPTP tunnel

PPTP connection logins successfully; you see a ppp0 interface with the correct VPN IP address, but you cannot even ping the remote IP address. It is due to lack of MPPE (Microsoft Point-to-Point Encryption) support in stock Arch pppd. It is recommended to first try with the stock Arch [ppp](https://www.archlinux.org/packages/?name=ppp) as it may work as intended.

To solve the problem it should be sufficient to install the [ppp-mppe](https://aur.archlinux.org/packages/ppp-mppe/) package.

See also [WPA2 Enterprise#MS-CHAPv2](/index.php/WPA2_Enterprise#MS-CHAPv2 "WPA2 Enterprise").

### Network management disabled

When NetworkManager shuts down but the pid (state) file is not removed, you will see a `Network management disabled` message. If this happens, remove the file manually:

```
# rm /var/lib/NetworkManager/NetworkManager.state

```

### Problems with internal DHCP client

If you have problems with getting an IP address using the internal DHCP client, consider using another DHCP client, see [#DHCP client](#DHCP_client) for instructions. This workaround might solve problems in big wireless networks like eduroam.

### DHCP problems with dhclient

If you have problems with getting an IP address via DHCP, try to add the following to your `/etc/dhclient.conf`:

```
 interface "eth0" {
   send dhcp-client-identifier 01:*aa:bb:cc:dd:ee:ff*;
 }

```

Where `*aa:bb:cc:dd:ee:ff*` is the MAC address of this NIC. The MAC address can be found using the `ip link show *interface*` command from the [iproute2](https://www.archlinux.org/packages/?name=iproute2) package.

### 3G modem not detected

See [USB 3G Modem#Network Manager](/index.php/USB_3G_Modem#Network_Manager "USB 3G Modem").

### Switching off WLAN on laptops

Sometimes NetworkManager will not work when you disable your Wi-Fi adapter with a switch on your laptop and try to enable it again afterwards. This is often a problem with *rfkill*. To check if the driver notifies *rfkill* about the wireless adapter's status, use:

```
$ watch -n1 rfkill list all

```

If one identifier stays blocked after you switch on the adapter you could try to manually unblock it with (where X is the number of the identifier provided by the above output):

```
# rfkill event unblock X

```

### Static IP address settings revert to DHCP

Due to an unresolved bug, when changing default connections to a static IP address, `nm-applet` may not properly store the configuration change, and will revert to automatic DHCP.

To work around this issue you have to edit the default connection (e.g. "Auto eth0") in `nm-applet`, change the connection name (e.g. "my eth0"), uncheck the "Available to all users" checkbox, change your static IP address settings as desired, and click **Apply**. This will save a new connection with the given name.

Next, you will want to make the default connection not connect automatically. To do so, run `nm-connection-editor` (**not** as root). In the connection editor, edit the default connection (e.g. "Auto eth0") and uncheck "Connect automatically". Click **Apply** and close the connection editor.

### Cannot edit connections as normal user

See [#Set up PolicyKit permissions](#Set_up_PolicyKit_permissions).

### Forget hidden wireless network

Since hidden networks are not displayed in the selection list of the Wireless view, they cannot be forgotten (removed) with the GUI. You can delete one with the following command:

```
# rm /etc/NetworkManager/system-connections/*SSID*

```

This works for any other connection.

### VPN not working in GNOME

When setting up OpenConnect or vpnc connections in NetworkManager while using GNOME, you will sometimes never see the dialog box pop up and the following error appears in `/var/log/errors.log`:

```
localhost NetworkManager[399]: <error> [1361719690.10506] [nm-vpn-connection.c:1405] get_secrets_cb(): Failed to request VPN secrets #3: (6) No agents were available for this request.

```

This is caused by the GNOME NM Applet expecting dialog scripts to be at `/usr/lib/gnome-shell`, when NetworkManager's packages put them in `/usr/lib/networkmanager`. As a "temporary" fix (this bug has been around for a while now), make the following symlink(s):

*   For OpenConnect: `ln -s /usr/lib/networkmanager/nm-openconnect-auth-dialog /usr/lib/gnome-shell/`
*   For VPNC (i.e. Cisco VPN): `ln -s /usr/lib/networkmanager/nm-vpnc-auth-dialog /usr/lib/gnome-shell/`

This may need to be done for any other NM VPN plugins as well, but these are the two most common.

### Unable to connect to visible European wireless networks

WLAN chips are shipped with a default [regulatory domain](/index.php/Wireless_network_configuration#Respecting_the_regulatory_domain "Wireless network configuration"). If your access point does not operate within these limitations, you will not be able to connect to the network. Fixing this is easy:

1.  [Install](/index.php/Install "Install") [crda](https://www.archlinux.org/packages/?name=crda)
2.  Uncomment the correct Country Code in `/etc/conf.d/wireless-regdom`
3.  Reboot the system, because the setting is only read on boot

### Automatic connect to VPN on boot is not working

The problem occurs when the system (i.e. NetworkManager running as the root user) tries to establish a VPN connection, but the password is not accessible because it is stored in the GNOME keyring of a particular user.

A solution is to keep the password to your VPN in plaintext, as described in step (2.) of [#Use dispatcher to connect to a VPN after a network connection is established](#Use_dispatcher_to_connect_to_a_VPN_after_a_network_connection_is_established).

You do not need to use the dispatcher described in step (1.) to auto-connect anymore, if you use the new "auto-connect VPN" option from the `nm-applet` GUI.

### Systemd Bottleneck

Over time the log files (`/var/log/journal`) can become very large. This can have a big impact on boot performance when using NetworkManager, see: [Systemd#Boot time increasing over time](/index.php/Systemd#Boot_time_increasing_over_time "Systemd").

### Regular network disconnects, latency and lost packets (WiFi)

NetworkManager does a scan every 2 minutes.

Some WiFi drivers have issues when scanning for base stations whilst connected/associated. Symptoms include VPN disconnects/reconnects and lost packets, web pages failing to load and then refresh fine.

Running `journalctl -f` will indicate that this is taking place, messages like the following will be contained in the logs at regular intervals.

```
NetworkManager[410]: <info>  (wlp3s0): roamed from BSSID 00:14:48:11:20:CF (my-wifi-name) to (none) ((none))

```

There is a patched version of NetworkManager which should prevent this type of scanning: [networkmanager-noscan](https://aur.archlinux.org/packages/networkmanager-noscan/).

Alternatively, if roaming is not important, the periodic scanning behavior can be disabled by locking the BSSID of the access point in the WiFi connection profile.

### Unable to turn on wi-fi with Lenovo laptop (IdeaPad, Legion, etc.)

There is an issue with the `ideapad_laptop` module on some Lenovo models due to the wi-fi driver incorrectly reporting a soft block. The card can still be manipulated with `netctl`, but managers like NetworkManager break. You can verify that this is the problem by checking the output of `rfkill list` after toggling your hardware switch and seeing that the soft block persists.

[Unloading](/index.php/Modprobe "Modprobe") the `ideapad_laptop` module should fix this. (**warning**: this may disable the laptop keyboard and touchpad also!).

### Turn off hostname sending

NetworkManager by default sends the hostname to the DHCP server. Hostname sending can only be disabled per connection not globally ([GNOME Bug 768076](https://bugzilla.gnome.org/show_bug.cgi?id=768076)).

To disable sending your hostname to the DHCP server for a specific connection, add the following to your network connection file:

 `/etc/NetworkManager/system-connections/*your_connection_file*` 
```
...
[ipv4]
dhcp-send-hostname=false
...
[ipv6]
dhcp-send-hostname=false
...
```

### nm-applet disappears in i3wm

If you use the `xfce4-notifyd.service` for notifications you must [edit](/index.php/Edit "Edit") the unit and add the following:

 `/etc/systemd/user/xfce4-notifyd.service.d/display_env.conf` 
```
[Service]
Environment="DISPLAY=:0.0"
```

After reloading the daemons [restart](/index.php/Restart "Restart") `xfce4-notifyd.service`. Exit i3 and start it back up again and the applet should show on the tray.

### nm-applet tray icons display wrongly

Currently the tray icons of nm-applet are drawn on top of one another, i.e. the icon displaying wireless strength might show on top of the icon indicating no wired connection. This is apparently a GTK3 bug/problem: [https://gitlab.gnome.org/GNOME/gtk/issues/1280](https://gitlab.gnome.org/GNOME/gtk/issues/1280) .

A patched version of GTK3 exists in AUR, which apparently fixes the tray icon bug: [gtk3-mushrooms](https://aur.archlinux.org/packages/gtk3-mushrooms/) .

### Unit dbus-org.freedesktop.resolve1.service not found

If `systemd-resolved.service` is not started, NetworkManager will try to start it using D-Bus and fail:

```
dbus-daemon[991]: [system] Activating via systemd: service name='org.freedesktop.resolve1' unit='dbus-org.freedesktop.resolve1.service' requested by ':1.23' (uid=0 pid=1012 comm="/usr/bin/NetworkManager --no-daemon ")
dbus-daemon[991]: [system] Activation via systemd failed for unit 'dbus-org.freedesktop.resolve1.service': Unit dbus-org.freedesktop.resolve1.service not found.
dbus-daemon[991]: [system] Activating via systemd: service name='org.freedesktop.resolve1' unit='dbus-org.freedesktop.resolve1.service' requested by ':1.23' (uid=0 pid=1012 comm="/usr/bin/NetworkManager --no-daemon ")

```

This is because NetworkManager will try to send DNS information to [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved") regardless of the `main.dns=` setting in [NetworkManager.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/NetworkManager.conf.5).[[8]](https://gitlab.freedesktop.org/NetworkManager/NetworkManager/commit/d4eb4cb45f41b1751cacf71da558bf8f0988f383)

This can be disabled with a configuration file in `/etc/NetworkManager/conf.d/`:

 `/etc/NetworkManager/conf.d/no-systemd-resolved.conf` 
```
[main]
systemd-resolved=false
```

See [FS#62138](https://bugs.archlinux.org/task/62138).

## See also

*   [NetworkManager for Administrators Part 1](https://blogs.gnome.org/dcbw/2015/02/16/networkmanager-for-administrators-part-1/)
*   [Wikipedia:NetworkManager](https://en.wikipedia.org/wiki/NetworkManager "wikipedia:NetworkManager")