PIA is a subscription based service provided from [PIA](https://www.privateinternetaccess.com/). See its [How It Works](https://www.privateinternetaccess.com/pages/how-it-works/) page for more information.

## Contents

*   [1 Requirements](#Requirements)
*   [2 Installation](#Installation)
*   [3 Usage](#Usage)
    *   [3.1 Enabling auto-login](#Enabling_auto-login)
    *   [3.2 Manually Connecting to VPN](#Manually_Connecting_to_VPN)
    *   [3.3 Automatically connect to VPN](#Automatically_connect_to_VPN)
    *   [3.4 WIP: Advanced Options](#WIP:_Advanced_Options)
*   [4 Example Configuration](#Example_Configuration)
*   [5 See also](#See_also)

## Requirements

PIA supports nearly any operating system and solution any user would need. This guide automatically sets up the configurations for PIA which works for most Arch Linux users.

**Note:** Arch Linux users may set up PIA manually by reading information on [PIA Client Support](https://www.privateinternetaccess.com/pages/client-support/) page.

## Installation

[Install](/index.php/Install "Install") the [private-internet-access-vpn](https://aur.archlinux.org/packages/private-internet-access-vpn/) or [private-internet-access-vpn-dev](https://aur.archlinux.org/packages/private-internet-access-vpn-dev/)package.

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

*   Change permissions of the file to *0600* and owner to *root:root*:

```
# chmod 0600 /etc/private-internet-access/login.conf
# chown root:root /etc/private-internet-access/login.conf
```
This secures the access to the file from non-root users. Read more on [File permissions and attributes](/index.php/File_permissions_and_attributes "File permissions and attributes"). It is **required** when activating auto-login.

*   Run `pia -a` as root.
    *   If you have [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) installed, it will created the configuration files for [networkmanager](https://www.archlinux.org/packages/?name=networkmanager). Make sure to [restart](/index.php/Restart "Restart") [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) to see them.
    *   If you have [connman](https://www.archlinux.org/packages/?name=connman) installed, it will create the configuration files for [connman](https://www.archlinux.org/packages/?name=connman). [Start](/index.php/Start "Start") `connman-vpn.service` if not running already. It will auto load the profiles.

**Tip:** Disable auto-login in configurations by adding `openvpn_auto_login = False` to `/etc/private-internet-access/pia.conf` and running `pia -a`

### Manually Connecting to VPN

Run `openvpn --config /etc/openvpn/{config_file_name}` as root. {config_file_name} will be listed in the /etc/openvpn directory.

### Automatically connect to VPN

*   For [connman](https://www.archlinux.org/packages/?name=connman):

1.  [enable](/index.php/Enable "Enable") the `connman-vpn.service`.
2.  Run `pia -a` as root.

**Note:** These are unsupported configurations.

*   For [openvpn](https://www.archlinux.org/packages/?name=openvpn) you can look here: [OpenVPN#systemd service configuration](/index.php/OpenVPN#systemd_service_configuration "OpenVPN").

### WIP: Advanced Options

*   Create `/etc/private-internet-access/pia.conf`
*   For the `[pia]` section:

| option | option values | description |
| openvpn_auto_login | True,False | Default: True; Configures if OpenVPN configuration files should have auto-login enabled. See [#Enabling auto-login](#Enabling_auto-login) |
| strong_encryption | True,False | Default: False; Configures strong encryption. Uses port 1197, cipher aes-256-cbc, auth sha256\. Custom configurations for port, cipher, and auth are ignored when enabling this option. |

*   For the `[configure]` section:

| option | option values | description |
| port | 80, 443, 110, 53, 8080, 9201 | Default: 1194; This configures which port and protocol the VPN uses. 80,443,110=TCP; 53,8080,9201=UDP |
| cipher | aes-128-cbc, aes-256-cbc, bf-cbc, None | Default: aes-128-cbc; This configures the data encryption cipher. |
| auth | sha1, sha256, None | Default: sha1; This configures the data authentication. |

## Example Configuration

The configuration enables auto-login, configures only Connman and OpenVPN, uses port 8080 over UDP, and configures only US East, US West, Japan, UK London, and UK Southampton VPN endpoints. OpenVPN is always configured.

 `/etc/private-internet-access-vpn/pia.conf` 
```

[pia]
openvpn_auto_login = True

[configure]
apps = cm
port = UDP/8080
hosts = US East, US West, Japan, UK London, UK Southampton

```

## See also

*   [OpenVPN](/index.php/OpenVPN "OpenVPN")
*   [NetworkManager](/index.php/NetworkManager "NetworkManager")
*   [connman](/index.php/Connman "Connman")
*   [python-pia GitHub](https://github.com/flamusdiu/python-pia/)
*   [PIA Client Support](https://www.privateinternetaccess.com/pages/client-support/)