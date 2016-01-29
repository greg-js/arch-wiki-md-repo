# Private Internet Access VPN

PIA is a subscription based service provided from the [PIA](https://www.privateinternetaccess.com/). From the PIA's [How It Works](https://www.privateinternetaccess.com/pages/how-it-works/) page:

NaN

## Contents

*   [1 Requirements](#Requirements)
*   [2 Installation](#Installation)
*   [3 Usage](#Usage)
    *   [3.1 Enabling auto-login](#Enabling_auto-login)
    *   [3.2 Manually Connecting to VPN](#Manually_Connecting_to_VPN)
    *   [3.3 Automatically connect to VPN](#Automatically_connect_to_VPN)
*   [4 See also](#See_also)

## Requirements

PIA supports nearly any operating system and solution any user would need. This guide automatically sets up the configurations for PIA which works for most Arch Linux users.

**Note:** Arch Linux users may setup PIA manually by reading information on [PIA Client Support](https://www.privateinternetaccess.com/pages/client-support/) page.

## Installation

[Install](/index.php/Install "Install") the [private-internet-access-vpn](https://aur.archlinux.org/packages/private-internet-access-vpn/)<sup><small>AUR</small></sup> package.

The package downloads the [OPENVPN CONFIGURATION FILES (DEFAULT)](https://www.privateinternetaccess.com/openvpn/openvpn.zip) and stores them in `/etc/openvpn`. However, it updates the file names to better support using them on the command line.

Configuration for the package is stored in `/etc/private-internet-access`

## Usage

**Note:** As of version 2.0, the command `pia` is provided by [python-pia](https://github.com/flamusdiu/python-pia).

**Note:** As of version 1.5, the command as changed from `pia-auto-login.py` to `pia`. Also, command line options have changed.

### Enabling auto-login

Enabling auto-login allows a user to connect to the VPN service without having type any passwords on the command line (needed when using [networkmanager](https://www.archlinux.org/packages/?name=networkmanager)). To set this up, you must do the following:

*   Create `/etc/private-internet-access/login.conf`
*   Add your username and password in the file. Make sure LINE 1 is your username and LINE 2 is your password. Do not add any other text to the file or it will not work (this is a limitation of [OpenVPN](/index.php/OpenVPN "OpenVPN")):

 `/etc/private-internet-access/login.conf` 

```
USERNAME
PASSWORD
```

*   Change permissions of the file to _0600_ and owner to _root:root_:

```
# chmod 0600 /etc/private-internet-access/login.conf
# chown root:root /etc/private-internet-access/login.conf
```

This secures the access to the file from non-root users. Read more on [File permissions and attributes](/index.php/File_permissions_and_attributes "File permissions and attributes"). It is **required** when activating auto-login.

*   Run `pia -a` as root.
    *   If you have [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) installed, it will created the configuration files for [networkmanager](https://www.archlinux.org/packages/?name=networkmanager). Make sure to [restart](/index.php/Restart "Restart") [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) to see them.
    *   If you have [connman](https://www.archlinux.org/packages/?name=connman) installed, it will create the configuration files for [connman](https://www.archlinux.org/packages/?name=connman). [Start](/index.php/Start "Start") `connman-vpn.service` if not running already. It will auto load the profiles.

### Manually Connecting to VPN

Run `openvpn --config /etc/openvpn/{config_file_name}` as root. {config_file_name} will be listed in the /etc/openvpn directory.

### Automatically connect to VPN

*   For [connman](https://www.archlinux.org/packages/?name=connman):

1.  [enable](/index.php/Enable "Enable") the `connman-vpn.service`.
2.  Run `pia -a` as root.

**Note:** These are unsupported configurations.

*   For [openvpn](https://www.archlinux.org/packages/?name=openvpn) you can look here: [OpenVPN#systemd service configuration](/index.php/OpenVPN#systemd_service_configuration "OpenVPN").

## See also

*   [OpenVPN](/index.php/OpenVPN "OpenVPN")
*   [NetworkManager](/index.php/NetworkManager "NetworkManager")
*   [connman](/index.php/Connman "Connman")
*   [python-pia GitHub](https://github.com/flamusdiu/python-pia/)
*   [PIA Client Support](https://www.privateinternetaccess.com/pages/client-support/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Private_Internet_Access_VPN&oldid=381414](https://wiki.archlinux.org/index.php?title=Private_Internet_Access_VPN&oldid=381414)"