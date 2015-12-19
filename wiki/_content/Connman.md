# Connman

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Network configuration](/index.php/Network_configuration "Network configuration")
*   [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")
*   [Category:Network managers](/index.php/Category:Network_managers "Category:Network managers")

[ConnMan](https://01.org/connman) is a command-line network manager designed for use with embedded devices and fast resolve times. It is modular through a [plugin architecture](http://git.kernel.org/cgit/network/connman/connman.git/tree/plugins), but has native [dhcp](http://git.kernel.org/cgit/network/connman/connman.git/tree/src/dhcp.c) and [ntp](http://git.kernel.org/cgit/network/connman/connman.git/tree/src/ntp.c) support.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Desktop clients](#Desktop_clients)
*   [2 Usage](#Usage)
    *   [2.1 Wired](#Wired)
    *   [2.2 Wi-Fi](#Wi-Fi)
        *   [2.2.1 Connecting to an open access point](#Connecting_to_an_open_access_point)
        *   [2.2.2 Connecting to a protected access point](#Connecting_to_a_protected_access_point)
    *   [2.3 Settings](#Settings)
    *   [2.4 Technologies](#Technologies)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Avoid changing the hostname](#Avoid_changing_the_hostname)
    *   [3.2 Prefer ethernet to wireless](#Prefer_ethernet_to_wireless)
    *   [3.3 Exclusive connection](#Exclusive_connection)
    *   [3.4 Connecting to eduroam](#Connecting_to_eduroam)
    *   [3.5 Avoiding conflicts with local DNS server](#Avoiding_conflicts_with_local_DNS_server)
    *   [3.6 Blacklist interfaces](#Blacklist_interfaces)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [connman](https://www.archlinux.org/packages/?name=connman) package. [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) and [bluez](https://www.archlinux.org/packages/?name=bluez) are optional dependencies required for Wi-Fi and Bluetooth functionality respectively.

Before [enabling](/index.php/Enabling "Enabling") `connman.service`, ensure any existing [network configuration](/index.php/Network_configuration "Network configuration") is disabled.

### Desktop clients

*   **cmst** — Qt GUI for ConnMan.

[https://github.com/andrew-bibb/cmst](https://github.com/andrew-bibb/cmst) || [cmst](https://aur.archlinux.org/packages/cmst/)<sup><small>AUR</small></sup>

*   **connman-ncurses** — Simple ncurses UI for ConnMan

[https://github.com/eurogiciel-oss/connman-json-client](https://github.com/eurogiciel-oss/connman-json-client) || [connman-ncurses-git](https://aur.archlinux.org/packages/connman-ncurses-git/)<sup><small>AUR</small></sup>

*   **connman-notify** — Connman event notification client

[https://github.com/wavexx/connman-notify](https://github.com/wavexx/connman-notify) || [connman-notify](https://aur.archlinux.org/packages/connman-notify/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/connman-notify)]</sup>

*   **ConnMan-UI** — GTK3 client applet.

[https://github.com/tbursztyka/connman-ui](https://github.com/tbursztyka/connman-ui) || [connman-ui-git](https://aur.archlinux.org/packages/connman-ui-git/)<sup><small>AUR</small></sup>

*   **connman_dmenu** — Client/frontend for dmenu.

[https://github.com/taylorchu/connman_dmenu](https://github.com/taylorchu/connman_dmenu) || [connman_dmenu-git](https://aur.archlinux.org/packages/connman_dmenu-git/)<sup><small>AUR</small></sup>

*   **EConnman** — Enlightenment desktop panel applet.

[http://www.enlightenment.org](http://www.enlightenment.org) || [econnman](https://aur.archlinux.org/packages/econnman/)<sup><small>AUR</small></sup>

*   **LXQt-Connman-Applet** — LXQt desktop panel applet.

[https://github.com/surlykke/lxqt-connman-applet](https://github.com/surlykke/lxqt-connman-applet) || [lxqt-connman-applet-git](https://aur.archlinux.org/packages/lxqt-connman-applet-git/)<sup><small>AUR</small></sup>

*   **qconnman-ui** — Qt management interface used on O.S. Systems products

[https://github.com/OSSystems/qconnman-ui](https://github.com/OSSystems/qconnman-ui) || [qconnman-ui-git](https://aur.archlinux.org/packages/qconnman-ui-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/qconnman-ui-git)]</sup>

*   **connman-gtk** — GTK client.

[https://github.com/jgke/connman-gtk](https://github.com/jgke/connman-gtk) || [connman-gtk](https://aur.archlinux.org/packages/connman-gtk/)<sup><small>AUR</small></sup>

*   **gnome-extension-connman** — Gnome3 extension for connman.

[https://github.com/jgke/gnome-extension-connman](https://github.com/jgke/gnome-extension-connman) || [https://extensions.gnome.org/extension/981/connman-extension/](https://extensions.gnome.org/extension/981/connman-extension/)

gnome-extension-connman: contains only some of the functionality without installing connman-gtk.

connman-ncurses: not all of connman functionality is implemented; but usable (with X or from terminal without X). See [wiki](https://github.com/eurogiciel-oss/connman-json-client/wiki).

## Usage

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Only Wired and Wi-Fi plugins are described. (Discuss in [Talk:Connman#](https://wiki.archlinux.org/index.php/Talk:Connman))

ConnMan has a standard command line client `connmanctl`. It can run in 2 modes:

*   In **command mode** commands are entered as arguments to `connmanctl` command, just like [systemctl](/index.php/Systemctl "Systemctl").
*   **Interactive mode** is started by typing `connmanctl` without arguments. Prompt will change to `connmanctl>` to indicate it is waiting for user commands, just like [python](/index.php/Python "Python") interactive mode.

### Wired

ConnMan will automatically handle wired connections.

### Wi-Fi

**Note:** Make sure the Wi-Fi device is listed in the output of `ip link show up`. If it is not listed that means it is not powered on. Use `Fn` keys on the laptop to turn it on. You may need to run `connmanctl enable wifi`.

#### Connecting to an open access point

The commands in this section show how to run `connmanctl` in command mode.

To scan the network `connmanctl` accepts simple names called _technologies_. To scan for nearby Wi-Fi networks:

```
$ connmanctl scan wifi

```

To list the available networks found after a scan run (example output):

 `$ connmanctl services` 

```
*AO MyNetwork               wifi_dc85de828967_68756773616d_managed_psk
    OtherNET                wifi_dc85de828967_38303944616e69656c73_managed_psk 
    AnotherOne              wifi_dc85de828967_3257495245363836_managed_wep
    FourthNetwork           wifi_dc85de828967_4d7572706879_managed_wep
    AnOpenNetwork           wifi_dc85de828967_4d6568657272696e_managed_none

```

To connect to an open network, use the second field beginning with **wifi_**:

```
$ connmanctl connect wifi_dc85de828967_4d6568657272696e_managed_none

```

You should now be connected to the network. Check using `ip addr` or `connmanctl state`.

#### Connecting to a protected access point

For protected access points you will need to provide some information to the ConnMan daemon, at the very least a password or a passphrase.

The commands in this section show how to run `connmanctl` in interactive mode, it is required for running the `agent` command. To start interactive mode simply type:

```
$ connmanctl

```

You then proceed almost as above, first scan for any Wi-Fi _technologies_:

```
connmanctl> scan wifi

```

To list services:

```
connmanctl> services

```

Now you need to register the agent to handle user requests. The command is:

```
connmanctl> agent on

```

You now need to connect to one of the protected services. To do this it is very handy to have a terminal that allows cut and paste. If you were connecting to OtherNET in the example above you would type:

```
connmanctl> connect wifi_dc85de828967_38303944616e69656c73_managed_psk

```

The agent will then ask you to provide any information the daemon needs to complete the connection. The information requested will vary depending on the type of network you are connecting to. The agent will also print additional data about the information it needs as shown in the example below.

```
Agent RequestInput wifi_dc85de828967_38303944616e69656c73_managed_psk
  Passphrase = [ Type=psk, Requirement=mandatory ]
  Passphrase?  

```

Provide the information requested, in this example the passphrase, and then type:

```
connmanctl> quit

```

If the information you provided is correct you should now be connected to the protected access point.

### Settings

Settings and profiles are automatically created for networks the user connects to often. They contain fields for the passphrase, essid and other information. Profile settings are stored in directories under `/var/lib/connman/` by their service name. To view all network profiles run this command from [root shell](/index.php/Help:Reading#Regular_user_or_root "Help:Reading"):

```
# cat /var/lib/connman/*/settings

```

**Note:** VPN settings can be found in `/var/lib/connman-vpn/`.

### Technologies

Various hardware interfaces are referred to as _Technologies_ by ConnMan.

To list available _technologies_ run:

```
$ connmanctl technologies

```

To get just the types by their name one can use this one liner:

```
$ connmanctl technologies | awk '/Type/ { print $NF }'

```

**Note:** The field `Type = tech_name` provides the technology type used with `connmanctl` commands

To interact with them one must refer to the technology by type. _Technologies_ can be toggled on/off with:

```
$ connmanctl enable _technology_type_

```

and:

```
$ connmanctl disable _technology_type_

```

For example to toggle off wifi:

```
$ connmanctl disable wifi

```

**Warning:** connman grabs all rfkill events. It is most likely impossible to use `rfkill` or `bluetoothctl` to (un)block devices. Always use `connmanctl enable|disable`

## Tips and tricks

### Avoid changing the hostname

By default, ConnMan changes the [transient hostname](http://www.freedesktop.org/software/systemd/man/hostnamectl.html) on a per network basis. This can create problems with X authority: If ConnMan changes your hostname to something else than the one used to generate the xauth magic cookie, then it will become impossible to create new windows. Symptoms are error messages like "No protocol specified" and "Can't open display: :0.0". Manually resetting the host name fixes this, but a permanent solution is to prevent ConnMan from changing your host name in the first place. This can be accomplished by adding the following to `/etc/connman/main.conf`:

```
[General]
AllowHostnameUpdates=false

```

Make sure to [restart](/index.php/Restart "Restart") the `connman.service` after changing this file.

For testing purposes it is recommended to watch the [journal](/index.php/Systemd#Journal "Systemd") and plug the network cable a few times to see the action.

### Prefer ethernet to wireless

By default ConnMan does not prefer ethernet over wireless, which can lead to it deciding to stick with a slow wireless network even when ethernet is available. You can tell connman to prefer ethernet adding the following to `/etc/connman/main.conf`:

```
[General]
PreferredTechnologies=ethernet,wifi

```

### Exclusive connection

ConnMan allows you to be connected to both ethernet and wireless at the same time. This can be useful as it allows programs that established a connection over wifi to stay connected even after you connect to ethernet. But some peope prefer to have only a single unambiguous connection active at a time. That behavior can be activated by adding the following to `/etc/connman/main.conf`:

```
[General]
SingleConnectedTechnology=true

```

### Connecting to eduroam

See [WPA2 Enterprise#connman](/index.php/WPA2_Enterprise#connman "WPA2 Enterprise").

### Avoiding conflicts with local DNS server

If you are running a local DNS server, it will likely have problems binding to port 53 (TCP and/or UDP) after installing Connman. This is because Connman includes its own DNS proxy which also tries to bind to those ports. If you see log messages from [BIND](/index.php/BIND "BIND") or [dnsmasq](/index.php/Dnsmasq "Dnsmasq") like `"named[529]: could not listen on UDP socket: address in use"`, this could be the problem. (Verify connmand is listening on that port with `netstat -tulpn`.)

To fix this connmand can be started with the `-r` or `--nodnsproxy` by [overriding](/index.php/Systemd#Editing_provided_units "Systemd") the systemd service file. Create the folder `/etc/systemd/system/connman.service.d/` and add the file `disable_dns_proxy.conf`:

```
[Service]
ExecStart=
ExecStart=/usr/bin/connmand -n --nodnsproxy

```

Make sure to [reload](/index.php/Reload "Reload") the systemd daemon and [restart](/index.php/Restart "Restart") the `connman.service`, and your DNS proxy, after adding this file.

### Blacklist interfaces

If something like [Docker](/index.php/Docker "Docker") is creating virtual interfaces Connman may attempt to connect to one of these instead of your physical adapter if the connection drops. A simple way of avoiding this is to blacklist the interfaces you do not want to use. Connman will by default blacklist interfaces starting with "vmnet", "vboxnet", "virbr" and "ifb" so those need to be included as well.

Blacklisting interface names is also useful to avoid a race condition where connman may access `eth#` or `wlan#` before systemd/udev can change it to use a [predictable interface name](/index.php/Network_configuration#Device_names "Network configuration") like `enp4s0`. Blacklisting the conventional (and unpredictable) interface prefixes makes connman wait until they are renamed.

If it does not already exist, create `/etc/connman/main.conf`:

```
[General]
NetworkInterfaceBlacklist=vmnet,vboxnet,virbr,ifb,docker,veth,eth,wlan

```

Once `connman.service` has been [restarted](/index.php/Systemd#Using_units "Systemd") this will also hide all the "veth#######" interfaces from GUI tools like Econnman.

## See also

For further detailed information on ConnMan you may refer to the documentation in its git repo at [[1]](https://git.kernel.org/cgit/network/connman/connman.git/tree/doc).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Connman&oldid=412739](https://wiki.archlinux.org/index.php?title=Connman&oldid=412739)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Network configuration](/index.php/Category:Network_configuration "Category:Network configuration")