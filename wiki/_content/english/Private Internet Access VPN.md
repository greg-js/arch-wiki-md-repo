This article details the installation and usage of [private-internet-access-vpn](https://aur.archlinux.org/packages/private-internet-access-vpn/). For the general information on the service and additional packages, see [Private internet access](/index.php/Private_internet_access "Private internet access").

## Contents

*   [1 Installation](#Installation)
*   [2 After Installation](#After_Installation)
*   [3 Usage](#Usage)
    *   [3.1 Enabling auto-login](#Enabling_auto-login)
        *   [3.1.1 Manually Connecting to VPN](#Manually_Connecting_to_VPN)
        *   [3.1.2 Automatically connect to VPN](#Automatically_connect_to_VPN)
        *   [3.1.3 Advanced Options](#Advanced_Options)
    *   [3.2 Example Configuration](#Example_Configuration)
    *   [3.3 Troubleshooting](#Troubleshooting)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [private-internet-access-vpn](https://aur.archlinux.org/packages/private-internet-access-vpn/) or [private-internet-access-vpn-dev](https://aur.archlinux.org/packages/private-internet-access-vpn-dev/)package.

The package provides a tool that downloads the [OpenVPN configuration files](https://www.privateinternetaccess.com/openvpn/openvpn.zip) and stores them in `/etc/openvpn`. However, it updates the file names to better support using them on the command line.

Configuration for the package is stored in `/etc/private-internet-access`

## After Installation

If there are any issues with connectivity and you are running [connman](https://www.archlinux.org/packages/?name=connman), please [restart](/index.php/Restart "Restart") `connman-vpn.service`.

## Usage

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
    *   If you have [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) installed, it will create the configuration files for [networkmanager](https://www.archlinux.org/packages/?name=networkmanager). Make sure to [restart](/index.php/Restart "Restart") [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) to see them.
    *   If you have [connman](https://www.archlinux.org/packages/?name=connman) installed, it will create the configuration files for [connman](https://www.archlinux.org/packages/?name=connman). [Start](/index.php/Start "Start") `connman-vpn.service` if not running already. It will auto load the profiles.
    *   Regardless, it will create the OpenVPN `.conf` files in `/etc/openvpn`.

**Tip:** Disable auto-login in configurations by adding `openvpn_auto_login = False` to `/etc/private-internet-access/pia.conf` and running `pia -a`

#### Manually Connecting to VPN

Run `openvpn --config /etc/openvpn/client/{config_file_name}` as root. `{config_file_name}` will be listed in the /etc/openvpn directory or run `pia -l`.

#### Automatically connect to VPN

*   For [connman](https://www.archlinux.org/packages/?name=connman):

1.  [enable](/index.php/Enable "Enable") the `connman-vpn.service`.
2.  Run `pia -a` as root.

**Note:** These are unsupported configurations.

*   For [openvpn](https://www.archlinux.org/packages/?name=openvpn) you can look here: [OpenVPN#systemd service configuration](/index.php/OpenVPN#systemd_service_configuration "OpenVPN").

#### Advanced Options

**Warning:** Protocols and port combinations no longer work as of Version 3.1\. See [Github Issue #17](https://github.com/flamusdiu/python-pia/issues/17) or PIA's Support - [Which encryption/auth settings should I use for ports on your gateways?](https://helpdesk.privateinternetaccess.com/hc/en-us/articles/225274288-Which-encryption-auth-settings-should-I-use-for-ports-on-your-gateways-)

*   Create `/etc/private-internet-access/pia.conf`
*   For the `[pia]` section:

| option | option values | description |
| openvpn_auto_login | True,False | Default: True; Configures if OpenVPN configuration files should have auto-login enabled. See [#Enabling auto-login](#Enabling_auto-login) |

*   For the `[configure]` section:

| option | option values | description |
| apps | cm, nm | Default: all; This configures which applications are configured. The application will configure all applications installed; however, if a user only needed configurations for Conman, then setting this to 'cm' would generate only those configurations even if they had NetworkManager installed. OpenVPN configurations are always generated. cm = Conman; nm = NetworkManager |
| port | See for list: PIA's Support -
[Which encryption/auth settings should I use for ports on your gateways?](https://helpdesk.privateinternetaccess.com/hc/en-us/articles/225274288-Which-encryption-auth-settings-should-I-use-for-ports-on-your-gateways-) | Default: 1198 |

### Example Configuration

The configuration enables auto-login, configures only Connman and OpenVPN, uses port 8080 over UDP, and configures only US East, US West, Japan, UK London, and UK Southampton VPN endpoints. OpenVPN is always configured.

 `/etc/private-internet-access-vpn/pia.conf` 
```

[pia]
openvpn_auto_login = True

[configure]
apps = cm
port = 8080
hosts = US East, US West, Japan, UK London, UK Southampton

```

### Troubleshooting

In order to use the NetworkManager applet to connect:

```
   - Right click the Network Manager icon in the system tray
   - and click "Configure Network Connections..."
   - then click "Add"
   - choose "Import VPN..."
   - browse to "/etc/openvpn/client/CA_Toronto.conf" or whichever configuration you would like to use
   - then click "Open"
   - Remove only the ":1198" from the "Gateway:" ( if present ) as only the domain name should be in this box
   - for the "Username:" type in your "p1234567" username
   - for the "Password:" type in the password that goes with your "p-xxxxx" username
   - then click "Advanced..."
   - set "Custom gateway port:" and set it to "1198"
   - click on the "Security" tab
   - set the "Cipher:" to "AES-128-CBC"
   - set the "HMAC Authentication:" to "SHA-1"
   - click "OK"
   - click "OK" again

```

Concerning DNS Leaks (See: [python-pia/#13](https://github.com/flamusdiu/python-pia/issues/13)), Network Manager leak information due to how /etc/resolv.conf is setup. The script below is a work around posted by [@maximbaz](https://github.com/maximbaz) to work around the problem. You may need to [disable IPv6](/index.php/IPv6#Disable_IPv6 "IPv6") if you continue to get leaks.

 `/etc/NetworkManager/dispatcher.d/pia-vpn` 
```

#!/bin/bash
#/etc/NetworkManager/dispatcher.d/pia-vpn

interface="$1"
status=$2

case $status in
  vpn-up)
    if [[ $interface == "tun0" ]]; then
      chmod +w /etc/resolv.conf
      echo -e "nameserver 209.222.18.222
nameserver 209.222.18.218" > /etc/resolv.conf
      chmod -w /etc/resolv.conf
    fi
    ;;
  vpn-down)
    if [[ $interface == "tun0" ]]; then
      chmod +w /etc/resolv.conf
    fi
    ;;
esac

```

## See also

*   [OpenVPN](/index.php/OpenVPN "OpenVPN")
*   [NetworkManager](/index.php/NetworkManager "NetworkManager")
*   [connman](/index.php/Connman "Connman")
*   [python-pia GitHub](https://github.com/flamusdiu/python-pia/)
*   [PIA Client Support](https://www.privateinternetaccess.com/pages/client-support/)