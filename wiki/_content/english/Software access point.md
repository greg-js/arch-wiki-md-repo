A software access point is used when you want your computer to act as a Wi-Fi access point for the local network. It saves you the trouble of getting a separate wireless router.

## Contents

*   [1 Requirements](#Requirements)
    *   [1.1 Wi-Fi device must support AP mode](#Wi-Fi_device_must_support_AP_mode)
    *   [1.2 Wireless client and software AP with a single Wi-Fi device](#Wireless_client_and_software_AP_with_a_single_Wi-Fi_device)
*   [2 Overview](#Overview)
*   [3 Wi-Fi Link Layer](#Wi-Fi_Link_Layer)
*   [4 Network configuration](#Network_configuration)
    *   [4.1 Bridge Setup](#Bridge_Setup)
    *   [4.2 NAT Setup](#NAT_Setup)
*   [5 Tools](#Tools)
    *   [5.1 create_ap](#create_ap)
    *   [5.2 RADIUS](#RADIUS)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 WLAN is very slow](#WLAN_is_very_slow)
    *   [6.2 NetworkManager is interfering](#NetworkManager_is_interfering)
*   [7 See also](#See_also)

## Requirements

### Wi-Fi device must support AP mode

You need a [nl80211](http://wireless.kernel.org/en/developers/Documentation/nl80211) compatible wireless device, which supports the AP [operating mode](http://wireless.kernel.org/en/users/Documentation/modes). This can be verified by running `iw list` command, under the `Supported interface modes` block there should be `AP` listed:

 `$ iw list` 
```
Wiphy phy1
...
	Supported interface modes:
		 * IBSS
		 * managed
		 * **AP**
		 * AP/VLAN
		 * WDS
		 * monitor
		 * mesh point
...

```

### Wireless client and software AP with a single Wi-Fi device

Creating a software AP is independent from your own network connection (Ethernet, wireless, ...). Many wireless devices even support *simultaneous* operation both as AP and as wireless "client" at the same time. Using that capability you can create a software AP acting as a "wireless repeater" for an existing network, using a single wireless device. The capability is listed in the following section in the output of `iw list`:

 `$ iw list` 
```
Wiphy phy1
...
        valid interface combinations:
                 * #{ managed } <= 2048, #{ AP, mesh point } <= 8, #{ P2P-client, P2P-GO } <= 1,
                   total <= 2048, #channels <= 1, STA/AP BI must match
...
```

The constraint `#channels <= 1` means that your software AP must operate on the same channel as your Wi-Fi client connection; see the `channel` setting in `hostapd.conf` below.

If you want to use the capability/feature, perhaps because an Ethernet connection is not available, you need to create two separate *virtual interfaces* for using it. Virtual interfaces for a physical device `wlan0` can be created as follows: The *virtual interfaces* with unique MAC address are created for the network connection (`wlan0_sta`) itself and for the software AP/hostapd "wireless repeater":

```
# iw dev wlan0 interface add wlan0_sta type managed addr 12:34:56:78:ab:cd  
# iw dev wlan0 interface add wlan0_ap  type wds addr 12:34:56:78:ab:ce

```

Random MAC address can be generated using [macchanger](/index.php/Macchanger "Macchanger").

## Overview

Setting up an access point comprises two main parts:

*   Setting up the **Wi-Fi link layer**, so that wireless clients can associate to your computer's "software access point" and send/receive IP packets from/to your computer; this is what the hostapd package will do for you.
*   Setting up the **network configuration** on you computer, so that your computer will properly relay IP packets from/to its own Internet connection from/to wireless clients.

## Wi-Fi Link Layer

The actual Wi-Fi link is established via the [hostapd](https://www.archlinux.org/packages/?name=hostapd) package, which has WPA2 support.

Adjust the options in *hostapd* configuration file if necessary. Especially, change the `ssid` and the `wpa_passphrase`. See [hostapd Linux documentation page](http://wireless.kernel.org/en/users/Documentation/hostapd) for more information.

 `/etc/hostapd/hostapd.conf` 
```
ssid=YourWiFiName
wpa_passphrase=Somepassphrase
interface=wlan0_ap
bridge=br0
auth_algs=3
channel=7
driver=nl80211
hw_mode=g
logger_stdout=-1
logger_stdout_level=2
max_num_sta=5
rsn_pairwise=CCMP
wpa=2
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP CCMP

```

**Tip:** You can set up the SSID with UTF-8 characters, so international characters will show properly. The option to enable it is `utf8_ssid=1`. Some clients may have problems with recognizing the correct encoding (e.g. [wpa_supplicant](/index.php/Wpa_supplicant "Wpa supplicant") or Windows 7).

When starting hostapd, make sure the wireless network interface is brought up first:

```
# ip link set dev wlan0_ap up

```

Otherwise, it will fail with a nondescript error: "could not configure driver mode".

For automatically starting hostapd, [enable](/index.php/Daemon "Daemon") the `hostapd.service`.

**Warning:** The wireless channels allowed for access point operation differ according to geography. Depending on the wireless firmware, you may have to set the region correctly to use legal channels. **Do not** choose another region, as you may be illegally disturbing network traffic, affecting wireless functionality of your own device and others within its reach! To set the region see [Wireless network configuration#Respecting the regulatory domain](/index.php/Wireless_network_configuration#Respecting_the_regulatory_domain "Wireless network configuration").

**Note:** If you have a card based on RTL8192CU chipset, install [hostapd-8192cu](https://aur.archlinux.org/packages/hostapd-8192cu/) in the [AUR](/index.php/AUR "AUR") and replace `driver=nl80211` with `driver=rtl871xdrv` in the `hostapd.conf` file.

## Network configuration

There are two basic ways for implementing this:

1.  **bridge**: create a network *bridge* on your computer (wireless clients will appear to access the same network interface and the same subnet that's used by your computer)
2.  **NAT**: with IP forwarding/masquerading and DHCP service (wireless clients will use a dedicated subnet, data from/to that subnet is NAT-ted -- similar to a normal Wi-Fi router that's connected to your DSL or cable modem)

The bridge approach is simpler, but it requires that any service that's needed by your wireless clients (like, DHCP) is available on your computers external interface. That means it will not work if you have a dial-up connection (e.g., via PPPoE or a 3G modem) or if you're using a cable modem that will supply exactly one IP address to you via DHCP.

The NAT approach is more versatile, as it clearly separates Wi-Fi clients from your computer and it's completely transparent to the outside world. It will work with any kind of network connection, and (if needed) you can introduce traffic policies using the usual iptables approach.

Of course, it is possible to *combine both things*. For that, studying both articles would be necessary. Example: Like having a bridge that contains both an ethernet device and the wireless device with an static ip, offering DHCP and setting NAT configured to relay the traffic to an additional network device - that can be ppp or eth.

### Bridge Setup

You need to create a network *bridge* and add your network interface (e.g. `eth0`) to it. You **should not** add the wireless device (e.g. `wlan0`) to the bridge; hostapd will add it on its own.

See [Network bridge](/index.php/Network_bridge "Network bridge").

**Tip:** You may wish to reuse an existing bridge, if you have one (e.g. used by a virtual machine).

### NAT Setup

See [Internet sharing](/index.php/Internet_sharing "Internet sharing") for details.

On that article, the device connected to the LAN is `net0`. That device would be in this case your wireless device (e.g. `wlan0`).

## Tools

### create_ap

The [create_ap](https://bbs.archlinux.org/viewtopic.php?pid=1269258) script combines [hostapd](https://www.archlinux.org/packages/?name=hostapd), [dnsmasq](/index.php/Dnsmasq "Dnsmasq") and [iptables](/index.php/Iptables "Iptables") to create a Bridged/NATed Access Point (available in the [AUR](/index.php/AUR "AUR") [create_ap](https://aur.archlinux.org/packages/create_ap/)).

### RADIUS

See [[1]](https://me.m01.eu/blog/2012/05/wpa-2-enterprise-from-scratch-on-a-raspberry-pi/) for instructions to run a [FreeRADIUS](http://freeradius.org/) server for [WPA2 Enterprise](/index.php/WPA2_Enterprise "WPA2 Enterprise").

## Troubleshooting

### WLAN is very slow

This could be caused by low entropy. Consider installing [haveged](/index.php/Haveged "Haveged").

### NetworkManager is interfering

hostapd may not work, if the device is managed by NetworkManager. You can mask the device:

 `/etc/NetworkManager/NetworkManager.conf` 
```
[keyfile]
unmanaged-devices=mac:<hwaddr>

```

## See also

*   [Router](/index.php/Router "Router")
*   [Hostapd : The Linux Way to create Virtual Wi-Fi Access Point](http://nims11.wordpress.com/2012/04/27/hostapd-the-linux-way-to-create-virtual-wifi-access-point/)
*   [tutorial and script for configuring a subnet with DHCP and DNS](http://xyne.archlinux.ca/notes/network/dhcp_with_dns.html)