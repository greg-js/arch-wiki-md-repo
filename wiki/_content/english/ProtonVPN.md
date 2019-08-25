Related articles

*   [OpenVPN](/index.php/OpenVPN "OpenVPN")

[ProtonVPN](https://www.protonvpn.com) is a VPN provider that utilizes the OpenVPN protocol.

Every solution requires a ProtonVPN account and the [openvpn](https://www.archlinux.org/packages/?name=openvpn) package.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 OpenVPN command-line interface](#OpenVPN_command-line_interface)
    *   [1.1 Setup](#Setup)
    *   [1.2 Usage](#Usage)
    *   [1.3 Tips and tricks](#Tips_and_tricks)
        *   [1.3.1 Saving OpenVPN authentication](#Saving_OpenVPN_authentication)
        *   [1.3.2 Enable VPN on boot](#Enable_VPN_on_boot)
*   [2 protonvpn-cli](#protonvpn-cli)
    *   [2.1 Setup](#Setup_2)
    *   [2.2 Usage](#Usage_2)
*   [3 Graphical interface](#Graphical_interface)

## OpenVPN command-line interface

VPN connection can be run manually with interface provided by the [openvpn](https://www.archlinux.org/packages/?name=openvpn) package.

### Setup

Download one or more OpenVPN configuration files from [ProtonVPN Downloads page](https://account.protonvpn.com/downloads).

Copy the *.ovpn client configuration files into `/etc/openvpn/client/` and make backup of original.

Follow [these steps](/index.php/OpenVPN#Update_systemd-resolved_script "OpenVPN") to make sure, that all your network traffic uses VPN. If you use systemd older than 229, follow [these steps](/index.php/OpenVPN#Update_resolv-conf_script "OpenVPN").

### Usage

Connect to the VPN:

```
# openvpn /etc/openvpn/client/client_config_file.ovpn

```

Provide **OpenVPN / IKEv2 Username** from the [ProtonVPN Account page](https://account.protonvpn.com/settings).

Press `Ctrl+C` to close the VPN connection.

### Tips and tricks

#### Saving OpenVPN authentication

OpenVPN credentials can be saved in a separate file and read automatically:

 `/etc/openvpn/client/client_config_file.ovpn` 
```
auth-user-pass /etc/openvpn/client/login.conf

```
 `/etc/openvpn/client/login.conf` 
```
openvpn_username
openvpn_password

```

#### Enable VPN on boot

For systemd service configuration, see [OpenVPN#systemd service configuration](/index.php/OpenVPN#systemd_service_configuration "OpenVPN").

## protonvpn-cli

ProtonVPN supplies a utility to access the VPN. Details can be found on the [official website](https://protonvpn.com/support/linux-vpn-tool/) and the [GitHub repository](https://github.com/ProtonVPN/protonvpn-cli).

### Setup

[Install](/index.php/Install "Install") the [protonvpn-cli](https://aur.archlinux.org/packages/protonvpn-cli/) package.

Initialize the client:

```
# protonvpn-cli -init

```

Enter your **ProtonVPN Login** username and password, which have to be configured on the [ProtonVPN Settings](https://account.protonvpn.com/settings) page. For example:

```
Enter OpenVPN username: ProtonVPN.user
Enter OpenVPN password:

```

After entering the credentials, you have to select your subscription plan. For example, select the Free plan:

```
[.]ProtonVPN Plans:
1) Free
2) Basic
3) Plus
4) Visionary
Enter Your ProtonVPN plan ID: 1

```

### Usage

Connect to the VPN:

```
# protonvpn-cli -connect

```

You should see detailed country list with all available servers. Select preferred server and click OK.

Then select UDP or TCP protocol and click OK again.

If connection was successful, you will see following output:

```
Connecting...
Connected!
New IP: X.X.X.X

```

## Graphical interface

Graphical interface for setting up OpenVPN connection may be provided by your [desktop environment](/index.php/Desktop_environment "Desktop environment"). Search in connection settings. Otherwise, [NetworkManager#Installation](/index.php/NetworkManager#Installation "NetworkManager"), [NetworkManager#VPN support](/index.php/NetworkManager#VPN_support "NetworkManager") and [NetworkManager#Front-ends](/index.php/NetworkManager#Front-ends "NetworkManager") provide useful information.

**Note:** You still need to follow [#Setup](#Setup).