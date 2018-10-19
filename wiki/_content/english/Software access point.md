Related articles

*   [Network configuration](/index.php/Network_configuration "Network configuration")
*   [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")
*   [Ad-hoc networking](/index.php/Ad-hoc_networking "Ad-hoc networking")
*   [Internet sharing](/index.php/Internet_sharing "Internet sharing")

A software access point, also called virtual router or virtual Wi-Fi, enables a computer to turn its wireless interface into a Wi-Fi access point. It saves the trouble of getting a separate wireless router.

## Contents

*   [1 Requirements](#Requirements)
    *   [1.1 Wi-Fi device must support AP mode](#Wi-Fi_device_must_support_AP_mode)
    *   [1.2 Wireless client and software AP with a single Wi-Fi device](#Wireless_client_and_software_AP_with_a_single_Wi-Fi_device)
*   [2 Configuration](#Configuration)
    *   [2.1 Wi-Fi link layer](#Wi-Fi_link_layer)
    *   [2.2 Network configuration](#Network_configuration)
        *   [2.2.1 Bridge setup](#Bridge_setup)
        *   [2.2.2 NAT setup](#NAT_setup)
*   [3 Tools](#Tools)
    *   [3.1 create_ap](#create_ap)
    *   [3.2 RADIUS](#RADIUS)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 WLAN is very slow](#WLAN_is_very_slow)
    *   [4.2 NetworkManager is interfering](#NetworkManager_is_interfering)
    *   [4.3 Cannot start AP mode in 5Ghz band](#Cannot_start_AP_mode_in_5Ghz_band)
*   [5 See also](#See_also)

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
# iw dev wlan0 interface add wlan0_ap  type managed addr 12:34:56:78:ab:ce

```

Random MAC address can be generated using [macchanger](/index.php/Macchanger "Macchanger").

## Configuration

Setting up an access point comprises two main parts:

1.  Setting up the **Wi-Fi link layer**, so that wireless clients can associate to your computer's *software access point* and exchange IP packets with it.
2.  Setting up the **network configuration** on your computer, so that it properly relays IP packets between its own internet connection and the wireless clients.

### Wi-Fi link layer

The actual Wi-Fi link is established via the [hostapd](https://www.archlinux.org/packages/?name=hostapd) package, which has WPA2 support.

Adjust the options in *hostapd* configuration file if necessary. Especially, change the `ssid` and the `wpa_passphrase`. See [hostapd Linux documentation page](http://wireless.kernel.org/en/users/Documentation/hostapd) for more information.

 `/etc/hostapd/hostapd.conf` 
```
interface=wlan0_ap
bridge=br0

# SSID to be used in IEEE 802.11 management frames
ssid=YourWiFiName
# Driver interface type (hostap/wired/none/nl80211/bsd)
driver=nl80211
# Country code (ISO/IEC 3166-1)
country_code=US

# Operation mode (a = IEEE 802.11a (5 GHz), b = IEEE 802.11b (2.4 GHz)
hw_mode=g
# Channel number
channel=7
# Maximum number of stations allowed
max_num_sta=5

# Bit field: bit0 = WPA, bit1 = WPA2
wpa=2
# Bit field: 1=wpa, 2=wep, 3=both
auth_algs=1

# Set of accepted cipher suites
rsn_pairwise=CCMP
# Set of accepted key management algorithms
wpa_key_mgmt=WPA-PSK
wpa_passphrase=Somepassphrase

# hostapd event logger configuration
logger_stdout=-1
logger_stdout_level=2

```

**Tip:** You can set up the SSID with UTF-8 characters, so international characters will show properly. The option to enable it is `utf8_ssid=1`. Some clients may have problems with recognizing the correct encoding (e.g. [wpa_supplicant](/index.php/Wpa_supplicant "Wpa supplicant") or Windows 7).

When starting hostapd, make sure the wireless [network interface](/index.php/Network_interface "Network interface") is brought up first, otherwise it will fail with the message "could not configure driver mode". Also make sure that the interface is not managed by a network manager.

For automatically starting hostapd, [enable](/index.php/Daemon "Daemon") the `hostapd.service`.

**Warning:** The wireless channels allowed for access point operation differ according to geography. Depending on the wireless firmware, you may have to set the region correctly to use legal channels. **Do not** choose another region, as you may be illegally disturbing network traffic, affecting wireless functionality of your own device and others within its reach! To set the region see [Wireless network configuration#Respecting the regulatory domain](/index.php/Wireless_network_configuration#Respecting_the_regulatory_domain "Wireless network configuration").

**Note:** If you have a card based on RTL8192CU chipset, install [hostapd-rtl871xdrv](https://aur.archlinux.org/packages/hostapd-rtl871xdrv/) and replace `driver=nl80211` with `driver=rtl871xdrv` in the `hostapd.conf` file.

### Network configuration

There are two basic ways for implementing this:

1.  **bridge**: creates a network *bridge* on your computer, wireless clients will appear to access the same network interface and the same subnet that's used by your computer.
2.  **NAT**: with IP forwarding/masquerading and DHCP service, wireless clients will use a dedicated subnet, data from/to that subnet is NAT-ted. This is similar to a normal Wi-Fi router which is connected to the internet.

The bridge approach is simpler, but it requires that any service that is needed by the wireless clients, in particular DHCP, is available on the computer's external interface. This means it will not work if the external modem which assigns IP addresses, supplies the same one to different clients.

The NAT approach is more versatile, as it clearly separates Wi-Fi clients from your computer and it is completely transparent to the outside world. It will work with any kind of network connection, and (if needed) traffic policies can be introduced using the usual iptables approach.

It is possible to combine these two approaches: for example having a bridge that contains both an ethernet device and the wireless device with a static ip, offering DHCP and setting NAT configured to relay the traffic to an additional network device connected to the WAN.

#### Bridge setup

You need to create a network *bridge* and add your network interface (e.g. `eth0`) to it. You **should not** add the wireless device (e.g. `wlan0`) to the bridge; hostapd will add it on its own.

See [Network bridge](/index.php/Network_bridge "Network bridge").

**Tip:** You may wish to reuse an existing bridge, if you have one (e.g. used by a virtual machine).

#### NAT setup

See [Internet sharing#Configuration](/index.php/Internet_sharing#Configuration "Internet sharing") for configuration details.

In that article, the device connected to the LAN is `net0`. That device would be in this case your wireless device (e.g. `wlan0`).

## Tools

### create_ap

The [create_ap](https://www.archlinux.org/packages/?name=create_ap) package provides a script that can create either a bridged or a NATed access point for internet sharing. It combines *hostapd*, [dnsmasq](/index.php/Dnsmasq "Dnsmasq") and [iptables](/index.php/Iptables "Iptables") for the good functioning of the access point. The basic syntax to create a NATed virtual network is the following:

```
# create_ap *wlan0* *eth0* *MyAccessPoint* *MyPassPhrase*

```

Alternatively, the template configuration provided in `/etc/create_ap.conf` can be adapted to ones need and the script run with:

```
# create_ap --config /etc/create_ap.conf

```

[enable](/index.php/Enable "Enable")/[start](/index.php/Start "Start") the `create_ap.service` to run the script at boot time with the configuration specified in `/etc/create_ap.conf` .

For more information see [create_ap on GitHub](https://github.com/oblique/create_ap).

**Note:** In bridge mode, *create_ap* may conflict at boot time with the current network configuration. In this case, do not configure the IP address of the ethernet interface, neither DHCP nor a statip IP address, in order to facilitate the binding to the bridge.

### RADIUS

See [[1]](https://me.m01.eu/blog/2012/05/wpa-2-enterprise-from-scratch-on-a-raspberry-pi/) for instructions to run a [FreeRADIUS](http://freeradius.org/) server for [WPA2 Enterprise](/index.php/WPA2_Enterprise "WPA2 Enterprise").

## Troubleshooting

### WLAN is very slow

This could be caused by low entropy. Consider installing [haveged](/index.php/Haveged "Haveged").

### NetworkManager is interfering

hostapd may not work, if the device is managed by NetworkManager. You can mask the device using MAC:

 `/etc/NetworkManager/NetworkManager.conf` 
```
[keyfile]
unmanaged-devices=mac:<hwaddr>

```

Or interface name:

 `/etc/NetworkManager/NetworkManager.conf` 
```
[keyfile]
unmanaged-devices=interface-name:<ifname>

```

### Cannot start AP mode in 5Ghz band

Apparently with the special country code `00` (global), all usable frequencies in the 5Ghz band will have the [`no-ir` (*no-initiating-radiation*)](https://wireless.wiki.kernel.org/en/developers/regulatory/processing_rules#post_processing_mechanisms) flag set, which will prevent hostapd from using them. You will need to have [crda](https://www.archlinux.org/packages/?name=crda) installed and have your country code set to make frequencies allowed in your country available for hostapd.

## See also

*   [Router](/index.php/Router "Router")
*   [Hostapd : The Linux Way to create Virtual Wi-Fi Access Point](http://nims11.wordpress.com/2012/04/27/hostapd-the-linux-way-to-create-virtual-wifi-access-point/)
*   [tutorial and script for configuring a subnet with DHCP and DNS](http://xyne.archlinux.ca/notes/network/dhcp_with_dns.html)