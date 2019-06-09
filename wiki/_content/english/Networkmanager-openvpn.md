networkmanager-openvpn is a plugin to support [OpenVPN](/index.php/OpenVPN "OpenVPN") connections in [NetworkManager](/index.php/NetworkManager "NetworkManager")

#### Adding a connection

Although you could manually configure a connection to an OpenVPN server, you will most likely have a `.ovpn` file.

### Use .ovpn file through GUI

If you are using [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet), you can do `VPN Connections -> Configure VPN -> + -> Import a saved VPN connection...`

### Use .ovpn file through CLI

```
nmcli connection import type openvpn file <file.ovpn>

```