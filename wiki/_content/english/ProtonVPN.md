Related articles

*   [OpenVPN](/index.php/OpenVPN "OpenVPN")

[ProtonVPN](https://www.protonvpn.com) is a VPN provider that utilizes the OpenVPN protocol.

In order to use this tutorial, one must have a ProtonVPN account.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Saving OpenVPN authentication](#Saving_OpenVPN_authentication)
    *   [3.2 Enable VPN on boot](#Enable_VPN_on_boot)
*   [4 protonvpn-cli](#protonvpn-cli)
    *   [4.1 Installation](#Installation_2)
    *   [4.2 Usage](#Usage_2)

## Installation

[Install](/index.php/Install "Install") the [openvpn](https://www.archlinux.org/packages/?name=openvpn) package.

## Usage

Log into ProtonVPN and download one or more OpenVPN configuration files.

Copy the *.ovpn client configuration files into `/etc/openvpn/client/` and make backup of original.

Follow [these steps](/index.php/OpenVPN#Update_systemd-resolved_script "OpenVPN") to make sure, that all your network traffic uses VPN. If you use systemd older than 229, follow [these steps](/index.php/OpenVPN#Update_resolv-conf_script "OpenVPN").

Connect to the VPN:

```
# openvpn /etc/openvpn/client/client_config_file.ovpn

```

Press `Ctrl+C` to close the VPN connection.

## Tips and tricks

### Saving OpenVPN authentication

If you get tired of punching in your username and password, you may save your OpenVPN credentials in a separate file and read them automatically.

 `/etc/openvpn/client/client_config_file.ovpn` 
```
auth-user-pass /etc/openvpn/client/login.conf

```
 `/etc/openvpn/client/login.conf` 
```
openvpn_username
openvpn_password

```

### Enable VPN on boot

For systemd service configuration, see [OpenVPN#systemd service configuration](/index.php/OpenVPN#systemd_service_configuration "OpenVPN").

## protonvpn-cli

ProtonVPN supplies a utility to access the VPN. Details can be found on the [official website](https://protonvpn.com/support/linux-vpn-tool/) and the [GitHub repository](https://github.com/ProtonVPN/protonvpn-cli).

### Installation

[Install](/index.php/Install "Install") the [protonvpn-cli](https://aur.archlinux.org/packages/protonvpn-cli/) package.

### Usage

Initialize the client:

```
# protonvpn-cli -init

```

Enter your OpenVPN username and password, which have to be configured on the [ProtonVPN Settings](https://account.protonvpn.com/settings) page. For example:

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

Now you can connect to the VPN:

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