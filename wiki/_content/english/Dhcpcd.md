*dhcpcd* is a DHCP and DHCPv6 client. It is currently the most feature-rich open source DHCP client, see the [home page](http://roy.marples.name/projects/dhcpcd/) for the full list of features.

**Note:** *dhcpcd* (DHCP **client** daemon) is not the same as [dhcpd](/index.php/Dhcpd "Dhcpd") (DHCP **(server)** daemon).

## Contents

*   [1 Installation](#Installation)
*   [2 Running](#Running)
*   [3 Configuration](#Configuration)
    *   [3.1 DHCP static route(s)](#DHCP_static_route.28s.29)
    *   [3.2 DHCP Client Identifier](#DHCP_Client_Identifier)
    *   [3.3 Speed up DHCP by disabling ARP probing](#Speed_up_DHCP_by_disabling_ARP_probing)
    *   [3.4 Static profile](#Static_profile)
        *   [3.4.1 Fallback profile](#Fallback_profile)
*   [4 Hooks](#Hooks)
    *   [4.1 10-wpa_supplicant](#10-wpa_supplicant)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Remove old DHCP lease](#Remove_old_DHCP_lease)
    *   [5.2 Different IPs when multi-booting](#Different_IPs_when_multi-booting)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Client ID](#Client_ID)
    *   [6.2 Check DHCP problem by releasing IP first](#Check_DHCP_problem_by_releasing_IP_first)
    *   [6.3 Problems with noncompliant routers](#Problems_with_noncompliant_routers)
    *   [6.4 dhcpcd and systemd network interfaces](#dhcpcd_and_systemd_network_interfaces)
    *   [6.5 Timeout delay](#Timeout_delay)
*   [7 See also](#See_also)

## Installation

The [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) package is available to be [installed](/index.php/Install "Install"). It is part of the [base](https://www.archlinux.org/groups/x86_64/base/) group, so it is likely already installed on your system.

You might be interested in [dhcpcd-ui](https://aur.archlinux.org/packages/dhcpcd-ui/), which is a [GTK+](/index.php/GTK%2B "GTK+") frontend for the *dhcpcd* daemon (and optionally [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant")). It features a configuration dialogue and the ability to enter a pass phrase for wireless networks.

## Running

*dhcpcd* includes two unit files which can be used to [control](/index.php/Enable "Enable") the daemon:

*   `dhcpcd.service` starts the daemon for *all* [network interfaces](/index.php/Network_interfaces "Network interfaces");
*   the template unit `dhcpcd@.service` binds it to a particular interface, for example `dhcpcd@*interface*.service` where *interface* is an interface shown with `ip link`.

Using the template unit is recommended; see [#dhcpcd and systemd network interfaces](#dhcpcd_and_systemd_network_interfaces) for details.

To start *dhcpcd* manually, run the following command:

 `# dhcpcd *eth0*` 
```
dhcpcd: version 5.1.1 starting
dhcpcd: *eth0*: broadcasting for a lease
...
dhcpcd: *eth0*: leased 192.168.1.70 for 86400 seconds

```

## Configuration

The main configuration is done in `/etc/dhcpcd.conf`, see `dhcpcd.conf(5)` for details. Some of the frequently used options are highlighted below.

### DHCP static route(s)

If you need to add a static route client-side, create a new dhcpcd hook-script in `/usr/lib/dhcpcd/dhcpcd-hooks`. The example shows a new hook-script which adds a static route to a VPN subnet on `10.11.12.0/24` via a gateway machine at `192.168.192.5`:

 `/usr/lib/dhcpcd/dhcpcd-hooks/40-vpnroute` 
```
ip route add 10.11.12.0/24 via 192.168.192.5

```

The `40` prefix means that it is the final hook-script to run when dhcpcd starts.

### DHCP Client Identifier

The DHCP client may be uniquely identified in different ways by the server:

1.  hostname (or the hostname value sent by the client),
2.  MAC address of the network interface controller through which the connection is being made, linked to this is the third,
3.  Identity Association ID (IAID), which is an abstraction layer to differentiate different use-cases and/or interfaces on a single host,
4.  DHCP Unique Identifier (DUID).

For a further description, see [RFC 3315](https://tools.ietf.org/html/rfc3315#section-4.2).

It depends on the DHCP-server configuration which options are optional or required to request a DHCP IP lease.

**Note:** The *dhcpcd* default configuration should be sufficient usually. The listed identifiers are determined automatically and manual configuration changes only be required in case of problems.

If the *dhcpcd* default configuration fails to obtain an IP, the following options are available to use in `dhcpcd.conf`:

*   `hostname` sends the hostname set in `/etc/hostname`
*   `clientid` sends the MAC address as identifier
*   `iaid <interface>` derives the IAID to use for DHCP discovery. It has to be used in an interface block (started by `interface <interface>`, see [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1388376#p1388376)), but more frequently the next option is used:
*   `duid` triggers using a combination of DUID and IAID as identifier.

The DUID value is set in `/etc/dhcpcd.duid`. For efficient DHCP lease operation it is important that it is unique for the system and applies to all network interfaces alike, while the IAID represents an identifier for each of the systems' interfaces (see [RFC 4361](http://tools.ietf.org/html/rfc4361#section-6.1)).

Care must be taken on a network running [Dynamic DNS](https://en.wikipedia.org/wiki/Dynamic_DNS "wikipedia:Dynamic DNS") to ensure that all three IDs are unique. If duplicate DUID values are presented to the DNS server, e.g. in the case where a virtual machine has been cloned and the hostname and MAC have been made unique but the DUID has not been changed, then the result will be that as each client with the duplicated DUID requests a lease the server will remove the predecessor from the DNS record.

### Speed up DHCP by disabling ARP probing

*dhcpcd* contains an implementation of a recommendation of the DHCP standard ([RFC2131](http://www.ietf.org/rfc/rfc2131.txt) section 2.2) to check via ARP if the assigned IP address is really not taken. This seems mostly useless in home networks, so you can save about 5 seconds on every connect by adding the following line to `/etc/dhcpcd.conf`:

```
noarp

```

This is equivalent to passing `--noarp` to `dhcpcd`, and disables the described ARP probing, speeding up connections to networks with DHCP.

### Static profile

Required settings are explained in [Network configuration#Static IP address](/index.php/Network_configuration#Static_IP_address "Network configuration"). These typically include the [device name](/index.php/Network_configuration#Device_names "Network configuration"), *IP address*, *router address*, and *name server*.

Configure a static profile for *dhcpcd* in `/etc/dhcpcd.conf`, for example:

 `/etc/dhcpcd.conf` 
```
interface eth0
static ip_address=192.168.0.10/24	
static routers=192.168.0.1
static domain_name_servers=192.168.0.1 8.8.8.8
```

More complicated configurations are possible, for example combining with the `arping` option. See `dhcpcd.conf(5)` for details.

#### Fallback profile

It is possible to configure a static profile within *dhcpcd* and fall back to it when DHCP lease fails. This is useful particularly for [headless machines](https://en.wikipedia.org/wiki/Headless_computer "wikipedia:Headless computer") such as [Raspberry Pi](/index.php/Raspberry_Pi "Raspberry Pi"), where the static profile can be used as "recovery" profile to ensure that it is always possible to connect to the machine.

The following example configures a `static_eth0` profile with `192.168.1.23` as IP address, `192.168.1.1` as gateway and name server, and makes this profile fallback for interface `eth0`.

 `/etc/dhcpcd.conf` 
```
# define static profile
profile static_eth0
static ip_address=192.168.1.23/24
static routers=192.168.1.1
static domain_name_servers=192.168.1.1

# fallback to static profile on eth0
interface *eth0*
fallback static_eth0
```

## Hooks

*dhcpcd* executes all scripts found in `/usr/lib/dhcpcd/dhcpcd-hooks/` in a lexical order. See `dhcpcd(5)` and `dhcpcd-run-hooks(8)` for details.

**Note:**

*   Each script can be disabled using the `nohook` option in `dhcpcd.conf`.
*   The `env` option can be used to set an environment variable for **all** hooks. For example, you can force the hostname hook to always set the hostname with `env force_hostname=YES`.

### 10-wpa_supplicant

Enable this hook by creating a symbolic link (to ensure that always the current version is used, even after package updates):

```
# ln -s /usr/share/dhcpcd/hooks/10-wpa_supplicant /usr/lib/dhcpcd/dhcpcd-hooks/

```

**Note:** Behaviour changed in [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd)-6.10.0-1: The hook is not enabled by default anymore [[2]](http://roy.marples.name/projects/dhcpcd/info/5d7b3cbea2808602), [[3]](http://roy.marples.name/projects/dhcpcd/info/28fd82a29a6d54ad), [[4]](http://roy.marples.name/projects/dhcpcd/info/9b0662ecd9a8b839).

The `10-wpa_supplicant` hook, if enabled, automatically launches [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") on wireless interfaces. It is started only if:

*   no *wpa_supplicant* process is already listening on that interface.
*   a *wpa_supplicant* configuration file exists. *dhcpcd* checks

```
/etc/wpa_supplicant/wpa_supplicant-*interface*.conf
/etc/wpa_supplicant/wpa_supplicant.conf
/etc/wpa_supplicant-*interface*.conf
/etc/wpa_supplicant.conf

```

by default, in that order, but a custom path can be set by adding `env wpa_supplicant_conf=*configuration_file_path*` into `/etc/dhcpcd.conf`.

**Note:** The hook stops at the first configuration file found, thus you should take this into consideration if you have several *wpa_supplicant* configuration files, otherwise *dhcpcd* might end up using the wrong file.

If you manage wireless connections with *wpa_supplicant* itself, the hook may create unwanted connection events. For example, if you stop *wpa_supplicant* the hook may bring the interface up again. Also, if you use [netctl-auto](/index.php/Netctl#Automatic_switching_of_profiles "Netctl"), *wpa_supplicant* is started automatically with `/run/network/wpa_supplicant_*interface*.conf` for config, so starting it again from the hook is unnecessary and may result in boot-time parse errors of the `/etc/wpa_supplicant/wpa_supplicant.conf` file, which only contains dummy values in the default packaged version.

To disable the hook, add `nohook wpa_supplicant` to `dhcpcd.conf`.

## Tips and tricks

### Remove old DHCP lease

The file `/var/lib/dhcpcd/dhcpcd-*interface*.lease`, where `*interface*` is the name of the interface on which you have a lease, contains the actual DHCP lease reply sent by the DHCP server. It is used to determine the last lease from the server, and its `mtime` attribute is used to determine when it was issued. This last lease information is then used to request the same IP address previously held on a network, if it is available. If you do not want that, simply delete this file.

If the DHCP server still assigns the same IP address, this may happen because it is configured to keep the assignment stable and recognizes the requesting DHCP client id or DUID (see [#DHCP Client Identifier](#DHCP_Client_Identifier)). You can test it by stopping *dhcpcd* and removing or renaming `/etc/dhcpcd.duid`. *dhcpcd* will generate a new one on next run.

Keep in mind that the DUID is intended as persistent machine identifier across reboots and interfaces. If you are transferring the system to new computer, preserving this file should make it appear as old one.

### Different IPs when multi-booting

If you are dualbooting Arch and OS X or Windows and want each to receive different IP addresses, you can exert control about the IPs leased by specifying a different DUID in each operating system installation.

In Windows (post XP) the DUID should be stored in the

```
\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip6\Parameters\Dhcpv6DUID 

```

registry key.

On OS X it is directly accessible in `Network\adapter\dhcp preferences panel`.

If you are using a [dnsmasq](/index.php/Dnsmasq "Dnsmasq") DHCP server, the different DUIDs can be used in appropriate `dhcp-host=` rules in its configuration.

## Troubleshooting

### Client ID

If you are on a network with DHCPv4 that filters Client IDs based on MAC addresses, you may need to change the following line:

 `/etc/dhcpcd.conf` 
```
# Use the same DUID + IAID as set in DHCPv6 for DHCPv4 Client ID as per RFC4361\. 
duid

```

To:

 `/etc/dhcpcd.conf` 
```
# Use the hardware address of the interface for the Client ID (DHCPv4).
clientid

```

Else, you may not obtain a lease since the DHCP server may not read your [DHCPv6-style](http://en.wikipedia.org/wiki/DHCPv6) Client ID correctly. See [RFC 4361](http://tools.ietf.org/html/rfc4361) for more information.

### Check DHCP problem by releasing IP first

A problem may occur when DHCP gets a wrong IP assignment, such as when two routers are tied together through a VPN. The router that is connected through the VPN may be assigning IP address. To fix it, as root, release the IP address:

```
# dhcpcd -k

```

Then request a new one:

```
# dhcpcd

```

You may have to run those two commands many times.

### Problems with noncompliant routers

For some (noncompliant) routers, you will not be able to connect properly unless you comment the line

```
require dhcp_server_identifier

```

in `/etc/dhcpcd.conf`. This should not cause issues unless you have multiple DHCP servers on your network (not typical); see [this page](http://technet.microsoft.com/en-us/library/cc977442.aspx) for more information.

### dhcpcd and systemd network interfaces

`dhcpcd.service` can be [enabled](/index.php/Enabled "Enabled") without specifying an interface. This may, however, create a race condition at boot with *systemd-udevd* trying to apply a predictable network interface name:

```
error changing net interface name wlan0 to wlp4s0: Device or resource busy" 

```

To avoid it, enable *dhcpcd* per interface it should bind to as described in [#Running](#Running). The downside of the template unit is, however, that it does not support hot-plugging of a wired connection and will fail if the network cable is not connected. To work-around the failure, see [#Timeout delay](#Timeout_delay).

### Timeout delay

If *dhcpcd* operates on a single interface and fails to obtain a lease after 30 seconds (for example when the server is not ready or the cable not plugged), it will exit with an error.

To have *dhcpcd* wait indefinitely for one-time, set the `timeout` option to `0`:

 `/etc/systemd/system/dhcpcd@.service.d/timeout.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/dhcpcd -w -q **-t 0** %I
```

To have it wait indefinetely, let the unit restart after it exited:

 `/etc/systemd/system/dhcpcd@.service.d/dhcpcdrestart.conf` 
```
[Service]
Restart=always
```

After making changes, [reload the configuration](/index.php/Systemd#Editing_provided_units "Systemd").

## See also

*   [dhcpcd(8)](http://roy.marples.name/man/html8/dhcpcd.html)
*   [dhcpcd.conf(5)](http://roy.marples.name/man/html5/dhcpcd.conf.html)