[TunnelBear](https://www.tunnelbear.com) is a VPN provider that utilizes OpenVPN protocol.

In order to use this tutorial, one must have Giant or Grizzly subscription.

**Note:** There is an [easier](https://www.tunnelbear.com/updates/linux_support/) method to use TunnelBear service for Gnome users.

## Walkthrough

[Install](/index.php/Install "Install") [openvpn](https://www.archlinux.org/packages/?name=openvpn).

Download [TunnelBear OpenVPN config files](https://s3.amazonaws.com/tunnelbear/linux/openvpn.zip) (also you can install [tunnelbear](https://aur.archlinux.org/packages/tunnelbear/) package from AUR).

Unzip the folder, and copy all the files to

```
$ /etc/openvpn/client/

```

Do not forget to change the permission

```
# chmod 600 /etc/openvpn/client/*

```

Pick the corresponding **.ovpn** that will be used (TunnelBear Japan is used as an example)

Rename the extension & remove the space

```
# mv "/etc/openvpn/client/TunnelBear Japan.ovpn" /etc/openvpn/client/TunnelBearJapan.conf

```

Edit the **.conf** file

 `/etc/openvpn/client/TunnelBearJapan.conf` 
```
...
keepalive 10 30
auth-user-pass login.key
...

```

Create **login.key**

 `/etc/openvpn/client/login.key` 
```
yourtunnelbearusername
yourtunnelbearpassword

```

[Start/enable](/index.php/Start/enable "Start/enable") `openvpn-client@TunnelBearJapan.service`.

## References

*   [TunnelBear Helper](https://github.com/JenniferMack/TunnelBear-Helper)
*   [Arch Wiki OpenVPN](/index.php/OpenVPN "OpenVPN")