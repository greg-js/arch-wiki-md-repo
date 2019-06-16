networkmanager-openvpn is a plugin to support [OpenVPN](/index.php/OpenVPN "OpenVPN") connections in [NetworkManager](/index.php/NetworkManager "NetworkManager")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Adding a connection](#Adding_a_connection)
*   [2 Use .ovpn file through GUI](#Use_.ovpn_file_through_GUI)
*   [3 Use .ovpn file through CLI](#Use_.ovpn_file_through_CLI)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 No Certificate password](#No_Certificate_password)

#### Adding a connection

Although you could manually configure a connection to an OpenVPN server, you will most likely have a `.ovpn` file.

### Use .ovpn file through GUI

If you are using [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet), you can do `VPN Connections -> Configure VPN -> + -> Import a saved VPN connection...`

### Use .ovpn file through CLI

```
nmcli connection import type openvpn file <file.ovpn>

```

## Troubleshooting

### No Certificate password

If you get:

```
Warning: password for 'vpn.secrets.password' not given in 'passwd-file' and nmcli cannot ask without '--ask' option.
Error: Connection activation failed: No valid secrets

```

Even with

```
[vpn]
cert-pass-flags=0
```

You can add:

```
[vpn-secrets]
cert-pass=<anything you want>
```