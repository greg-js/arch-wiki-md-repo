[Mullvad](https://mullvad.net/en/) is a VPN service based in Sweden which uses [OpenVPN](/index.php/OpenVPN "OpenVPN") and [WireGuard](/index.php/WireGuard "WireGuard").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Manual configuration](#Manual_configuration)
*   [3 DNS leaks](#DNS_leaks)
*   [4 See also](#See_also)

## Installation

The new [official GUI client](https://mullvad.net/download/) is available as [mullvad-vpn](https://aur.archlinux.org/packages/mullvad-vpn/).

After installation you will need to enable and start the [systemd](/index.php/Systemd "Systemd") service `mullvad-daemon.service`.

Alternatively you can use the old client or [OpenVPN](/index.php/OpenVPN "OpenVPN") with a configuration file for Mullvad as explained in [#Manual configuration](#Manual_configuration).

## Manual configuration

First make sure the packages [openvpn](https://www.archlinux.org/packages/?name=openvpn) and [openresolv](https://www.archlinux.org/packages/?name=openresolv) are installed, then proceed to download Mullvad's OpenVPN configuration file package from [their website](https://www.mullvad.net/download/config/) (under the "other platforms" tab) and unzip the downloaded file to `/etc/openvpn/client/`.

Rename mullvad_linux.conf for a shorter name to be used with the [systemd](/index.php/Systemd "Systemd") service later:

```
# mv /etc/openvpn/client/mullvad_linux.conf /etc/openvpn/client/mullvad.conf

```

In order to use the nameservers supplied by Mullvad, [update-resolv-conf script](/index.php/OpenVPN#Update_resolv-conf_script "OpenVPN") is being called upon starting and stopping the connection with OpenVPN to modify [resolv.conf](/index.php/Resolv.conf "Resolv.conf") to include the correct IP addresses. This script is also included in the Mullvad configuration zipfile, but should be moved to `/etc/openvpn/` to match the path specified in the Mullvad configuration file:

```
# mv /etc/openvpn/client/update-resolv-conf /etc/openvpn/

```

The script can be kept updated with the [openvpn-update-resolv-conf](https://github.com/masterkorp/openvpn-update-resolv-conf) script, which also contains a fix for DNS leaks.

After configuration the VPN connection can be [managed](/index.php/Enabled "Enabled") with `openvpn-client@mullvad.service`. If the service fails to start with an error like `Cannot open TUN/TAP dev /dev/net/tun: No such device (errno=19)`, you might need to reboot the system to enable OpenVPN creating the correct network device for the task.

## DNS leaks

By default, the Mullvad openvpn configurations allow DNS leaks and for usual VPN use cases this is an unfavorable privacy defect. Mullvad's new GUI client automatically stops DNS leaks by removing every DNS server IP from the system configuration and replacing them with an IP pointing out to Mullvad's own non-logging DNS server, valid during the VPN connection. This fix can also be applied with the plain OpenVPN method by configuring [resolv.conf](/index.php/Resolv.conf "Resolv.conf") to use **only** the Mullvad DNS server IP specified on their [website](https://www.mullvad.net/guides/dns-leaks/).

The resolv.conf update script version in [openvpn-update-resolv-conf](https://github.com/masterkorp/openvpn-update-resolv-conf) implements a different fix for the leaks by using the exclusive interface switch `-x` when running the `resolvconf` command, but this might cause another form of DNS leakage by making even every local network address resolve via the DNS server provided by Mullvad, as noted in the [script's GitHub issue page](https://github.com/masterkorp/openvpn-update-resolv-conf/issues/18).

## See also

*   [Mullvad client source code](https://github.com/mullvad/mullvadvpn-app)
*   [Mullvad FAQ](https://mullvad.net/en/faq/)