Configuring wireless is a two-part process; the first part is to identify and ensure the correct driver for your wireless device is installed (they are available on the installation media, but often have to be installed explicitly), and to configure the interface. The second is choosing a method of managing wireless connections. This article covers both parts, and provides additional links to wireless management tools.

## Contents

*   [1 Device driver](#Device_driver)
    *   [1.1 Check the driver status](#Check_the_driver_status)
    *   [1.2 Installing driver/firmware](#Installing_driver.2Ffirmware)
*   [2 Wireless management](#Wireless_management)
    *   [2.1 Manual setup](#Manual_setup)
        *   [2.1.1 Getting some useful information](#Getting_some_useful_information)
        *   [2.1.2 Interface activation](#Interface_activation)
        *   [2.1.3 Access point discovery](#Access_point_discovery)
        *   [2.1.4 Operating mode](#Operating_mode)
        *   [2.1.5 Association](#Association)
        *   [2.1.6 Getting an IP address](#Getting_an_IP_address)
        *   [2.1.7 Example](#Example)
    *   [2.2 Automatic setup](#Automatic_setup)
        *   [2.2.1 Connman](#Connman)
        *   [2.2.2 netctl](#netctl)
        *   [2.2.3 Wicd](#Wicd)
        *   [2.2.4 NetworkManager](#NetworkManager)
        *   [2.2.5 WiFi Radar](#WiFi_Radar)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Temporary internet access](#Temporary_internet_access)
    *   [3.2 Rfkill caveat](#Rfkill_caveat)
    *   [3.3 Respecting the regulatory domain](#Respecting_the_regulatory_domain)
    *   [3.4 Observing Logs](#Observing_Logs)
    *   [3.5 Power saving](#Power_saving)
    *   [3.6 Failed to get IP address](#Failed_to_get_IP_address)
    *   [3.7 Valid IP address but cannot resolve host](#Valid_IP_address_but_cannot_resolve_host)
    *   [3.8 Connection always times out](#Connection_always_times_out)
        *   [3.8.1 Lowering the rate](#Lowering_the_rate)
        *   [3.8.2 Lowering the txpower](#Lowering_the_txpower)
        *   [3.8.3 Setting rts and fragmentation thresholds](#Setting_rts_and_fragmentation_thresholds)
    *   [3.9 Random disconnections](#Random_disconnections)
        *   [3.9.1 Cause #1](#Cause_.231)
        *   [3.9.2 Cause #2](#Cause_.232)
        *   [3.9.3 Cause #3](#Cause_.233)
        *   [3.9.4 Cause #4](#Cause_.234)
*   [4 Troubleshooting drivers and firmware](#Troubleshooting_drivers_and_firmware)
    *   [4.1 Ralink](#Ralink)
        *   [4.1.1 rt2x00](#rt2x00)
        *   [4.1.2 rt3090](#rt3090)
        *   [4.1.3 rt3290](#rt3290)
        *   [4.1.4 rt3573](#rt3573)
        *   [4.1.5 rt5572](#rt5572)
    *   [4.2 Realtek](#Realtek)
        *   [4.2.1 rtl8192cu](#rtl8192cu)
        *   [4.2.2 rtl8192e](#rtl8192e)
        *   [4.2.3 rtl8188eu](#rtl8188eu)
        *   [4.2.4 rtl8723ae/rtl8723be](#rtl8723ae.2Frtl8723be)
    *   [4.3 Atheros](#Atheros)
        *   [4.3.1 ath5k](#ath5k)
        *   [4.3.2 ath9k](#ath9k)
            *   [4.3.2.1 Power saving](#Power_saving_2)
            *   [4.3.2.2 ASUS](#ASUS)
    *   [4.4 Intel](#Intel)
        *   [4.4.1 ipw2100 and ipw2200](#ipw2100_and_ipw2200)
        *   [4.4.2 iwlegacy](#iwlegacy)
        *   [4.4.3 iwlwifi](#iwlwifi)
        *   [4.4.4 Disabling LED blink](#Disabling_LED_blink)
    *   [4.5 Broadcom](#Broadcom)
    *   [4.6 Other drivers/devices](#Other_drivers.2Fdevices)
        *   [4.6.1 Tenda w322u](#Tenda_w322u)
        *   [4.6.2 orinoco](#orinoco)
        *   [4.6.3 prism54](#prism54)
        *   [4.6.4 ACX100/111](#ACX100.2F111)
        *   [4.6.5 zd1211rw](#zd1211rw)
        *   [4.6.6 hostap_cs](#hostap_cs)
    *   [4.7 ndiswrapper](#ndiswrapper)
    *   [4.8 compat-drivers-patched](#compat-drivers-patched)
*   [5 See also](#See_also)

## Device driver

The default Arch Linux kernel is *modular*, meaning many of the drivers for machine hardware reside on the hard drive and are available as [modules](/index.php/Kernel_modules "Kernel modules"). At boot, [udev](/index.php/Udev "Udev") takes an inventory of your hardware and loads appropriate modules (drivers) for your corresponding hardware, which will in turn allow creation of a network *interface*.

Some wireless chipsets also require firmware, in addition to a corresponding driver. Many firmware images are provided by the [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) package which is installed by default, however, proprietary firmware images are not included and have to be installed separately. This is described in [#Installing driver/firmware](#Installing_driver.2Ffirmware).

**Note:** Udev is not perfect. If the proper module is not loaded by udev on boot, simply [load it manually](/index.php/Kernel_modules#Loading "Kernel modules"). Note also that udev may occasionally load more than one driver for a device, and the resulting conflict will prevent successful configuration. Make sure to [blacklist](/index.php/Kernel_modules#Blacklisting "Kernel modules") the unwanted module.

**Tip:** Though not strictly required, it's a good idea to first install user-space tools mentioned in [#Manual setup](#Manual_setup), especially when some problem should appear.

### Check the driver status

To check if the driver for your card has been loaded, check the output of the `lspci -k` or `lsusb -v` command, depending on if the card is connected by PCI(e) or USB. You should see that some kernel driver is in use, for example:

 `$ lspci -k` 
```
06:00.0 Network controller: Intel Corporation WiFi Link 5100
	Subsystem: Intel Corporation WiFi Link 5100 AGN
	Kernel driver in use: iwlwifi
	Kernel modules: iwlwifi

```

**Note:** If the card is a USB device, running `dmesg | grep usbcore` should give something like `usbcore: registered new interface driver rtl8187` as output.

Also check the output of `ip link` command to see if a wireless interface ([usually](/index.php/Network_configuration#Device_names "Network configuration") it starts with the letter "w", e.g. `wlp2s1`) was created. Then bring the interface up with `ip link set *interface* up`. For example, assuming the interface is `wlan0`:

```
# ip link set wlan0 up

```

If you get this error message: `SIOCSIFFLAGS: No such file or directory`, it most certainly means that your wireless chipset requires a firmware to function.

Check kernel messages for firmware being loaded:

 `$ dmesg | grep firmware` 
```
[   7.148259] iwlwifi 0000:02:00.0: loaded firmware version 39.30.4.1 build 35138 op_mode iwldvm

```

If there is no relevant output, check the messages for the full output for the module you identified earlier (`iwlwifi` in this example) to identify the relevant message or further issues:

 `$ dmesg | grep iwlwifi` 
```
[   12.342694] iwlwifi 0000:02:00.0: irq 44 for MSI/MSI-X
[   12.353466] iwlwifi 0000:02:00.0: loaded firmware version 39.31.5.1 build 35138 op_mode iwldvm
[   12.430317] iwlwifi 0000:02:00.0: CONFIG_IWLWIFI_DEBUG disabled
...
[   12.430341] iwlwifi 0000:02:00.0: Detected Intel(R) Corporation WiFi Link 5100 AGN, REV=0x6B

```

If the kernel module is successfully loaded and the interface is up, you can skip the next section.

### Installing driver/firmware

Check the following lists to discover if your card is supported:

*   See the table of [existing Linux wireless drivers](https://wireless.wiki.kernel.org/en/users/drivers) and follow to the specific driver's page, which contains a list of supported devices. There is also a [List of Wi-Fi Device IDs in Linux](https://wikidevi.com/wiki/List_of_Wi-Fi_Device_IDs_in_Linux).
*   The [Ubuntu Wiki](https://help.ubuntu.com/community/WifiDocs/WirelessCardsSupported) has a good list of wireless cards and whether or not they are supported either in the Linux kernel or by a user-space driver (includes driver name).
*   [Linux Wireless Support](http://linux-wless.passys.nl/) and The Linux Questions' [Hardware Compatibility List](http://www.linuxquestions.org/hcl/index.php?cat=10) (HCL) also have a good database of kernel-friendly hardware.

Note that some vendors ship products that may contain different chip sets, even if the product identifier is the same. Only the usb-id (for USB devices) or pci-id (for PCI devices) is authoritative.

If your wireless card is listed above, follow the [#Troubleshooting drivers and firmware](#Troubleshooting_drivers_and_firmware) subsection of this page, which contains information about installing drivers and firmware of some specific wireless cards. Then [check the driver status](#Check_the_driver_status) again.

If your wireless card is not listed above, it is likely supported only under Windows (some Broadcom, 3com, etc). For these, you can try to use [#ndiswrapper](#ndiswrapper).

## Wireless management

Assuming that your drivers are installed and working properly, you will need to choose a method of managing your wireless connections. The following subsections will help you decide.

Procedure and tools required will depend on several factors:

*   The desired nature of configuration management; from a completely manual command line procedure to an automated solution with graphical front-ends.
*   The encryption type (or lack thereof) which protects the wireless network.
*   The need for network profiles, if the computer will frequently change networks (such as a laptop).

**Tip:**

*   Whatever is your choice, **you should try to connect using the manual method first**. This will help you understand the different steps that are required and troubleshoot possible problems.
*   If possible (e.g. if you manage your Wi-Fi access point), try connecting with no encryption, to check that everything works. Then try using encryption, either WEP (simple to configure, but crackable in a matter of seconds), WPA or WPA2.
*   If you anticipate to connect the machine to different wireless networks over time, a tool which provides its own connection management may be easier to handle.

The following table shows the different methods that can be used to activate and manage a wireless connection, depending on the encryption and management types, and the various tools that are required. Although there may be other possibilities, these are the most frequently used:

| Management method | Interface activation | Wireless connection management
(/=alternatives) | Assigning IP address
(/=alternatives) |
| [Manually managed](#Manual_setup),
with no or WEP encryption | [ip](/index.php/Core_utilities#ip "Core utilities") | [iw](https://www.archlinux.org/packages/?name=iw) / [iwconfig](https://www.archlinux.org/packages/?name=wireless_tools) | [ip](/index.php/Core_utilities#ip "Core utilities") / [dhcpcd](/index.php/Dhcpcd "Dhcpcd") / [dhclient](https://www.archlinux.org/packages/?name=dhclient) / [networkd](/index.php/Networkd "Networkd") |
| [Manually managed](#Manual_setup),
with WPA or WPA2 PSK encryption | [ip](/index.php/Core_utilities#ip "Core utilities") | [iw](https://www.archlinux.org/packages/?name=iw) / [iwconfig](https://www.archlinux.org/packages/?name=wireless_tools) + [wpa_supplicant](/index.php/Wpa_supplicant "Wpa supplicant") | [ip](/index.php/Core_utilities#ip "Core utilities") / [dhcpcd](/index.php/Dhcpcd "Dhcpcd") / [dhclient](https://www.archlinux.org/packages/?name=dhclient) / [networkd](/index.php/Networkd "Networkd") |
| [Automatically managed](#Automatic_setup),
with network profiles support | [netctl](/index.php/Netctl "Netctl"), [Wicd](/index.php/Wicd "Wicd"), [NetworkManager](/index.php/NetworkManager "NetworkManager"), etc.

These tools pull in the required dependencies from the list of packages in the manual method.

 |

### Manual setup

Just like other network interfaces, the wireless ones are controlled with *ip* from the [iproute2](https://www.archlinux.org/packages/?name=iproute2) package.

You will need to install a basic set of tools for managing the wireless connection. Either:

*   [iw](https://www.archlinux.org/packages/?name=iw) - only supports the nl80211 (netlink) standard. It does not support the older WEXT (Wireless EXTentions) standard. If *iw* does not see your card, this may be the reason.

	or

*   [wireless_tools](https://www.archlinux.org/packages/?name=wireless_tools) - currently deprecated, but still widely supported. Use this for modules using the WEXT standard.

For WPA/WPA2 encryption, you will also need:

*   [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) - works with both WEXT and nl80211.

The table below gives an overview of comparable commands for *iw* and *wireless_tools* (see [iw replaces iwconfig](http://wireless.kernel.org/en/users/Documentation/iw/replace-iwconfig) for more examples). These user-space tools work extremely well and allow complete manual control of wireless connection.

**Note:**

*   [iw](https://www.archlinux.org/packages/?name=iw) and [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) are provided on the installation medium.
*   Examples in this section assume that your wireless device interface is `wlan0` and that you are connecting to `*your_essid*` wifi access point. Replace both accordingly. To find your wireless device interface, see [#Getting some useful information](#Getting_some_useful_information).
*   Note that most of the commands have to be executed with [root permissions](/index.php/Users_and_groups "Users and groups"). Executed with normal user rights, some of the commands (e.g. *iwlist*), will exit without error but not produce the correct output either, which can be confusing.

| *iw* command | *wireless_tools* command | Description |
| iw dev wlan0 link | iwconfig wlan0 | Getting link status. |
| iw dev wlan0 scan | iwlist wlan0 scan | Scanning for available access points. |
| iw dev wlan0 set type ibss | iwconfig wlan0 mode ad-hoc | Setting the operation mode to *ad-hoc*. |
| iw dev wlan0 connect *your_essid* | iwconfig wlan0 essid *your_essid* | Connecting to open network. |
| iw dev wlan0 connect *your_essid* 2432 | iwconfig wlan0 essid *your_essid* freq 2432M | Connecting to open network specifying channel. |
| iw dev wlan0 connect *your_essid* key 0:*your_key* | iwconfig wlan0 essid *your_essid* key *your_key* | Connecting to WEP encrypted network using hexadecimal key. |
| iw dev wlan0 connect *your_essid* key 0:*your_key* | iwconfig wlan0 essid *your_essid* key s:*your_key* | Connecting to WEP encrypted network using ASCII key. |
| iw dev wlan0 set power_save on | iwconfig wlan0 power on | Enabling power save. |

**Note:** Depending on your hardware and encryption type, some of these steps may not be necessary. Some cards are known to require interface activation and/or access point scanning before being associated to an access point and being given an IP address. Some experimentation may be required. For instance, WPA/WPA2 users may try to directly activate their wireless network from step [#Association](#Association).

#### Getting some useful information

**Tip:** See [official documentation](http://wireless.kernel.org/en/users/Documentation/iw) of the *iw* tool for more examples.

*   First you need to find the name of wireless interface. You can do it with following command:

 `$ iw dev` 
```
phy#0
	Interface **wlan0**
		ifindex 3
		wdev 0x1
		addr 12:34:56:78:9a:bc
		type managed
		channel 1 (2412 MHz), width: 40 MHz, center1: 2422 MHz

```

*   To check link status, use following command. Example output when not connected to an AP:

 `$ iw dev wlan0 link` 
```
Not connected.

```

When connected to an AP, you will see something like:

 `$ iw dev wlan0 link` 
```
Connected to 12:34:56:78:9a:bc (on wlan0)
	SSID: MyESSID
	freq: 2412
	RX: 33016518 bytes (152703 packets)
	TX: 2024638 bytes (11477 packets)
	signal: -53 dBm
	tx bitrate: 150.0 MBit/s MCS 7 40MHz short GI

	bss flags:	short-preamble short-slot-time
	dtim period:	1
	beacon int:	100

```

*   You can get statistic information, such as the amount of tx/rx bytes, signal strength etc., with following command:

 `$ iw dev wlan0 station dump` 
```
Station 12:34:56:78:9a:bc (on wlan0)
	inactive time:	1450 ms
	rx bytes:	24668671
	rx packets:	114373
	tx bytes:	1606991
	tx packets:	8557
	tx retries:	623
	tx failed:	1425
	signal:  	-52 dBm
	signal avg:	-53 dBm
	tx bitrate:	150.0 MBit/s MCS 7 40MHz short GI
	authorized:	yes
	authenticated:	yes
	preamble:	long
	WMM/WME:	yes
	MFP:		no
	TDLS peer:	no

```

#### Interface activation

**Tip:** Usually this step is not required.

Some cards require that the kernel interface be activated before you can use *iw* or *wireless_tools*:

```
# ip link set wlan0 up

```

**Note:** If you get errors like `RTNETLINK answers: Operation not possible due to RF-kill`, make sure that hardware switch is *on*. See [#Rfkill caveat](#Rfkill_caveat) for details.

To verify that the interface is up, inspect the output of the following command:

 `# ip link show wlan0` 
```
3: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state DOWN mode DORMANT group default qlen 1000
    link/ether 12:34:56:78:9a:bc brd ff:ff:ff:ff:ff:ff

```

The `UP` in `<BROADCAST,MULTICAST,UP,LOWER_UP>` is what indicates the interface is up, not the later `state DOWN`.

#### Access point discovery

See what access points are available:

```
# iw dev wlan0 scan | less

```

**Note:** If it displays `Interface does not support scanning`, then you probably forgot to install the firmware. In some cases this message is also displayed when not running *iw* as root.

**Tip:** Depending on your location, you might need to set the correct [regulatory domain](#Respecting_the_regulatory_domain) in order to see all available networks.

The important points to check:

*   **SSID:** the name of the network.
*   **Signal:** is reported in a wireless power ratio in dbm (e.g. from -100 to 0). The closer the negative value gets to zero, the better the signal. Observing the reported power on a good quality link and a bad one should give an idea about the individual range.
*   **Security:** it is not reported directly, check the line starting with `capability`. If there is `Privacy`, for example `capability: ESS Privacy ShortSlotTime (0x0411)`, then the network is protected somehow.
    *   If you see an `RSN` information block, then the network is protected by [Robust Security Network](https://en.wikipedia.org/wiki/IEEE_802.11i-2004 "wikipedia:IEEE 802.11i-2004") protocol, also known as WPA2.
    *   If you see an `WPA` information block, then the network is protected by [Wi-Fi Protected Access](https://en.wikipedia.org/wiki/Wi-Fi_Protected_Access "wikipedia:Wi-Fi Protected Access") protocol.
    *   In the `RSN` and `WPA` blocks you may find the following information:
        *   **Group cipher:** value in TKIP, CCMP, both, others.
        *   **Pairwise ciphers:** value in TKIP, CCMP, both, others. Not necessarily the same value than Group cipher.
        *   **Authentication suites:** value in PSK, 802.1x, others. For home router, you will usually find PSK (*i.e.* passphrase). In universities, you are more likely to find 802.1x suite which requires login and password. Then you will need to know which key management is in use (e.g. EAP), and what encapsulation it uses (e.g. PEAP). Find more details at [Wikipedia:Authentication protocol](https://en.wikipedia.org/wiki/Authentication_protocol "wikipedia:Authentication protocol") and the sub-articles.
    *   If you do not see neither `RSN` nor `WPA` blocks but there is `Privacy`, then WEP is used.

#### Operating mode

You might need to set the proper operating mode of the wireless card. More specifically, if you are going to connect an [ad-hoc network](/index.php/Ad-hoc_networking "Ad-hoc networking"), you need to set the operating mode to `ibss`:

```
# iw dev wlan0 set type ibss

```

**Note:** Changing the operating mode on some cards might require the wireless interface to be *down* (`ip link set wlan0 down`).

#### Association

Depending on the encryption, you need to associate your wireless device with the access point to use and pass the encryption key:

*   **No encryption** `# iw dev wlan0 connect "*your_essid*"` 
*   **WEP**
    *   using a hexadecimal or ASCII key (the format is distinguished automatically, because a WEP key has a fixed length): `# iw dev wlan0 connect "*your_essid*" key 0:*your_key*` 
    *   using a hexadecimal or ASCII key, specifying the third set up key as default (keys are counted from zero, four are possible): `# iw dev wlan0 connect "*your_essid*" key d:2:*your_key*` 
*   **WPA/WPA2** According to what you got from [#Access point discovery](#Access_point_discovery), issue this command: `# wpa_supplicant -D nl80211,wext -i wlan0 -c <(wpa_passphrase "*your_SSID*" "*your_key*")` 

If this does not work, you may need to adjust the options. If connected successfully, continue in a new terminal (or quit `wpa_supplicant` with `Ctrl+c` and add the `-B` switch to the above command to run it in the background). [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") contains more information on options and on how to create a permanent configuration file for the wireless access point.

Regardless of the method used, you can check if you have associated successfully:

```
# iw dev wlan0 link

```

#### Getting an IP address

**Note:** See [Network configuration#Configure the IP address](/index.php/Network_configuration#Configure_the_IP_address "Network configuration") for more examples. This part is identical.

Finally, provide an IP address to the network interface. Simple examples are:

```
# dhcpcd wlan0

```

for DHCP, or

```
# ip addr add 192.168.0.2/24 dev wlan0
# ip route add default via 192.168.0.1

```

for static IP addressing.

**Tip:** [dhcpcd](/index.php/Dhcpcd "Dhcpcd") provides a [hook](/index.php/Dhcpcd#10-wpa_supplicant "Dhcpcd"), which can be enabled to automatically launch [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") on wireless interfaces.

#### Example

Here is a complete example of setting up a wireless network with WPA supplicant and DHCP.

```
# ip link set dev wlp13s1 up
# wpa_supplicant -B -i wlp13s1 -c /etc/wpa_supplicant/wpa_supplicant.conf
# dhcpcd wlp13s1

```

And then to close the connection, you can simply disable the interface:

```
# ip link set dev wlp13s1 down

```

For a static IP, you would replace the dhcpcd command with

```
# ip addr add 192.168.0.10/24 broadcast 192.168.0.255 dev wlp13s1
# ip route add default via 192.168.0.1

```

And before disabling the interface you would first flush the IP address and gateway:

```
# ip addr flush dev wlp13s1
# ip route flush dev wlp13s1

```

### Automatic setup

There are many solutions to choose from, but remember that all of them are mutually exclusive; you should not run two daemons simultaneously. The following table compares the different connection managers, additional notes are in subsections below.

| Connection manager | Network
profiles
support | Roaming
(auto connect dropped
or changed location) | [PPP](https://en.wikipedia.org/wiki/Point-to-Point_Protocol "wikipedia:Point-to-Point Protocol") support
(e.g. 3G modem) | Official
GUI | Console tools |
| [Connman](/index.php/Connman "Connman") | Yes | Yes | Yes | No | `connmanctl` |
| [netctl](/index.php/Netctl "Netctl") | Yes | Yes | Yes | No | `netctl`,`wifi-menu` |
| [NetworkManager](/index.php/NetworkManager "NetworkManager") | Yes | Yes | Yes | Yes | `nmcli`,`nmtui` |
| [Wicd](/index.php/Wicd "Wicd") | Yes | Yes | No | Yes | `wicd-curses` |
| [Wifi Radar](/index.php/Wifi_Radar "Wifi Radar") | Yes |  ? |  ? | Yes | `wifi-radar` |

#### Connman

*ConnMan* is an alternative to *NetworkManager* and *Wicd*, designed to be light on resources making it ideal for netbooks, and other mobile devices. It is modular in design takes advandage of the dbus API and provides proper abstraction on top of *wpa_supplicant*.

See [Connman](/index.php/Connman "Connman").

#### netctl

*netctl* is a replacement for *netcfg* designed to work with *systemd*. It uses a profile based setup and is capable of detection and connection to a wide range of network types. This is no harder than using graphical tools.

See [netctl](/index.php/Netctl "Netctl").

#### Wicd

*Wicd* is a network manager that can handle both wireless and wired connections. It is written in Python and Gtk with fewer dependencies than *NetworkManager*.

See [Wicd](/index.php/Wicd "Wicd").

#### NetworkManager

*NetworkManager* is an advanced network management tool that is enabled by default in most popular GNU/Linux distributions. In addition to managing wired connections, *NetworkManager* provides worry-free wireless roaming with an easy-to-use GUI program for selecting your desired network.

See [NetworkManager](/index.php/NetworkManager "NetworkManager").

#### WiFi Radar

*WiFi Radar* is a Python/PyGTK2 utility for managing wireless (and **only** wireless) profiles. It enables you to scan for available networks and create profiles for your preferred networks.

See [Wifi Radar](/index.php/Wifi_Radar "Wifi Radar").

## Troubleshooting

This section contains general troubleshooting tips, not strictly related to problems with drivers or firmware. For such topics, see next section [#Troubleshooting drivers and firmware](#Troubleshooting_drivers_and_firmware).

### Temporary internet access

If you have problematic hardware and need internet access to, for example, download some software or get help in forums, you can make use of Android's built-in feature for internet sharing via USB cable. See [Android tethering#USB tethering](/index.php/Android_tethering#USB_tethering "Android tethering") for more information.

### Rfkill caveat

Many laptops have a hardware button (or switch) to turn off wireless card, however, the card can also be blocked by kernel. This can be handled by [rfkill](https://www.archlinux.org/packages/?name=rfkill). Use *rfkill* to show the current status:

 `# rfkill list` 
```
0: phy0: Wireless LAN
	Soft blocked: yes
	Hard blocked: yes

```

If the card is *hard-blocked*, use the hardware button (switch) to unblock it. If the card is not *hard-blocked* but *soft-blocked*, use the following command:

```
# rfkill unblock wifi

```

**Note:** It is possible that the card will go from *hard-blocked* and *soft-unblocked* state into *hard-unblocked* and *soft-blocked* state by pressing the hardware button (i.e. the *soft-blocked* bit is just switched no matter what). This can be adjusted by tuning some options of the `rfkill` [kernel module](/index.php/Kernel_module "Kernel module").

More info: [http://askubuntu.com/questions/62166/siocsifflags-operation-not-possible-due-to-rf-kill](http://askubuntu.com/questions/62166/siocsifflags-operation-not-possible-due-to-rf-kill)

### Respecting the regulatory domain

The [regulatory domain](https://en.wikipedia.org/wiki/IEEE_802.11#Regulatory_domains_and_legal_compliance "wikipedia:IEEE 802.11"), or "regdomain", is used to reconfigure wireless drivers to make sure that wireless hardware usage complies with local laws set by the FCC, ETSI and other organizations. Regdomains use [ISO 3166-1 alpha-2 country codes](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2 "wikipedia:ISO 3166-1 alpha-2"). For example, the regdomain of the United States would be "US", China would be "CN", etc.

Regdomains affect the availability of wireless channels. In the 2.4GHz band, the allowed channels are 1-11 for the US, 1-14 for Japan, and 1-13 for most of the rest of the world. In the 5GHz band, the rules for allowed channels are much more complex. In either case, consult [this list of WLAN channels](https://en.wikipedia.org/wiki/List_of_WLAN_channels "wikipedia:List of WLAN channels") for more detailed information.

Regdomains also affect the limit on the [effective isotropic radiated power (EIRP)](https://en.wikipedia.org/wiki/Equivalent_isotropically_radiated_power "wikipedia:Equivalent isotropically radiated power") from wireless devices. This is derived from transmit power/"tx power", and is measured in [dBm/mBm (1dBm=100mBm) or mW (log scale)](https://en.wikipedia.org/wiki/DBm "wikipedia:DBm"). In the 2.4GHz band, the maximum is 30dBm in the US and Canada, 20dBm in most of Europe, and 20dB-30dBm for the rest of the world. In the 5GHz band, maximums are usually lower. Consult the [wireless-regdb](http://git.kernel.org/cgit/linux/kernel/git/linville/wireless-regdb.git/tree/db.txt) for more detailed information (EIRP dBm values are in the second set of brackets for each line).

Misconfiguring the regdomain can be useful - for example, by allowing use of an unused channel when other channels are crowded, or by allowing an increase in tx power to widen transmitter range. However, **this is not recommended** as it could break local laws and cause interference with other radio devices.

To configure the regdomain, install [crda](https://www.archlinux.org/packages/?name=crda) and reboot (to reload the `cfg80211` module and all related drivers). Check the boot log to make sure that CRDA is being called by `cfg80211`:

```
$ dmesg | grep cfg80211

```

The current regdomain can be set to the United States with:

```
# iw reg set US

```

And queried with:

```
$ iw reg get

```

**Note:** Your device may be set to country "00", which is the "world regulatory domain" and contains generic settings. If this cannot be unset, CRDA may be misconfigured.

However, setting the regdomain may not alter your settings. Some devices have a regdomain set in firmware/EEPROM, which dictates the limits of the device, meaning that setting regdomain in software [can only increase restrictions](http://wiki.openwrt.org/doc/howto/wireless.utilities#iw), not decrease them. For example, a CN device could be set in software to the US regdomain, but because CN has an EIRP maximum of 20dBm, the device will not be able to transmit at the US maximum of 30dBm.

For example, to see if the regdomain is being set in firmware for an Atheros device:

```
$ dmesg | grep ath:

```

For other chipsets, it may help to search for "EEPROM", "regdomain", or simply the name of the device driver.

To see if your regdomain change has been successful, and to query the number of available channels and their allowed transmit power:

```
$ iw list | grep -A 15 Frequencies:

```

A more permanent configuration of the regdomain can be achieved through editing `/etc/conf.d/wireless-regdom` and uncommenting the appropriate domain. `wpa_supplicant` can also use a regdomain in the `country=` line of `/etc/wpa_supplicant.conf`.

It is also possible to configure the [cfg80211](http://wireless.kernel.org/en/developers/Documentation/cfg80211) kernel module to use a specific regdomain by adding, for example, `options cfg80211 ieee80211_regdom=EU` as [module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules"). However, this is part of the [old regulatory implementation](http://wireless.kernel.org/en/developers/Regulatory#The_ieee80211_regdom_module_parameter).

For further information, read the [wireless.kernel.org regulatory documentation](http://wireless.kernel.org/en/developers/Regulatory/).

### Observing Logs

A good first measure to troubleshoot is to analyze the system's logfiles first. In order not to manually parse through them all, it can help to open a second terminal/console window and watch the kernels messages with

```
$ dmesg -w

```

while performing the action, e.g. the wireless association attempt.

When using a tool for network management, the same can be done for systemd with

```
# journalctl -f 

```

Frequently a wireless error is accompanied by a deauthentication with a particular reason code, for example:

```
wlan0: deauthenticating from XX:XX:XX:XX:XX:XX by local choice (reason=3)

```

Looking up [the reason code](http://www.aboutcher.co.uk/2012/07/linux-wifi-deauthenticated-reason-codes/) might give a first hint. Maybe it also helps you to look at the control message [flowchart](https://wireless.wiki.kernel.org/en/developers/documentation/mac80211/auth-assoc-deauth), the journal messages will follow it.

The individual tools used in this article further provide options for more detailed debugging output, which can be used in a second step of the analysis, if required.

### Power saving

See [Power saving#Network interfaces](/index.php/Power_saving#Network_interfaces "Power saving").

### Failed to get IP address

*   If getting an IP address repeatedly fails using the default [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) client, try installing and using [dhclient](https://www.archlinux.org/packages/?name=dhclient) instead. Do not forget to select *dhclient* as the primary DHCP client in your [connection manager](#Automatic_setup)!

*   If you can get an IP address for a wired interface and not for a wireless interface, try disabling the wireless card's [power saving](#Power_saving) features (specify `off` instead of `on`).

*   If you get a timeout error due to a *waiting for carrier* problem, then you might have to set the channel mode to `auto` for the specific device:

```
# iwconfig wlan0 channel auto

```

Before changing the channel to auto, make sure your wireless interface is down. After it has successfully changed it, you can bring the interface up again and continue from there.

### Valid IP address but cannot resolve host

If you are on a public wireless network that may have a [captive portal](https://en.wikipedia.org/wiki/Captive_portal "wikipedia:Captive portal"), it may be necessary to remove any custom DNS servers from [resolv.conf](/index.php/Resolv.conf "Resolv.conf").

### Connection always times out

The driver may suffer from a lot of tx excessive retries and invalid misc errors for some unknown reason, resulting in a lot of packet loss and keep disconnecting, sometimes instantly. Following tips might be helpful.

#### Lowering the rate

Try setting lower rate, for example 5.5M:

```
# iwconfig wlan0 rate 5.5M auto

```

Fixed option should ensure that the driver does not change the rate on its own, thus making the connection a bit more stable:

```
# iwconfig wlan0 rate 5.5M fixed

```

#### Lowering the txpower

You can try lowering the transmit power as well. This may save power as well:

```
# iwconfig wlan0 txpower 5

```

Valid settings are from `0` to `20`, `auto` and `off`.

#### Setting rts and fragmentation thresholds

Default iwconfig options have rts and fragmentation thresholds off. These options are particularly useful when there are many adjacent APs or in a noisy environment.

The minimum value for fragmentation value is 256 and maximum is 2346\. In many windows drivers the maximum is the default value:

```
# iwconfig wlan0 frag 2346

```

For rts minimum is 0, maximum is 2347\. Once again windows drivers often use maximum as the default:

```
# iwconfig wlan0 rts 2347

```

### Random disconnections

#### Cause #1

If dmesg says `wlan0: deauthenticating from MAC by local choice (reason=3)` and you lose your Wi-Fi connection, it is likely that you have a bit too aggressive power-saving on your Wi-Fi card[[2]](http://us.generation-nt.com/answer/gentoo-user-wireless-deauthenticating-by-local-choice-help-204640041.html). Try disabling the wireless card's [power saving](#Power_saving) features (specify `off` instead of `on`).

If your card does not support enabling/disabling power save mode, check the BIOS for power management options. Disabling PCI-Express power management in the BIOS of a Lenovo W520 resolved this issue.

#### Cause #2

If you are experiencing frequent disconnections and dmesg shows messages such as

`ieee80211 phy0: wlan0: No probe response from AP xx:xx:xx:xx:xx:xx after 500ms, disconnecting`

try changing the channel bandwidth to `20MHz` through your router's settings page.

#### Cause #3

On some laptop models with hardware rfkill switches (e.g., Thinkpad X200 series), due to wear or bad design, the switch (or its connection to the mainboard) might become loose over time resulting in seemingly random hardblocks/disconnects when you accidentally touch the switch or move the laptop. There is no software solution to this, unless your switch is electrical and the BIOS offers the option to disable the switch. If your switch is mechanical (most are), there are lots of possible solutions, most of which aim to disable the switch: Soldering the contact point on the mainboard/wifi-card, glueing or blocking the switch, using a screw nut to tighten the switch or removing it altogether.

#### Cause #4

Another cause for frequent disconnects or a complete failure to connect may also be a sub-standard router, incomplete settings of the router, or interference by other wireless devices.

To troubleshoot, first best try to connect to the router with no authentication.

If that works, enable WPA/WPA2 again but choose fixed and/or limited router settings. For example:

*   If the router is considerably older than the wireless device you use for the client, test if it works with setting the router to one wireless mode
*   Disable mixed-mode authentication (e.g. only WPA2 with AES, or TKIP if the router is old)
*   Try a fixed/free channel rather than "auto" channel (maybe the router next door is old and interfering)
*   Disable `40Mhz` channel bandwidth (lower throughput but less likely collisions)
*   If the router has quality of service settings, check completeness of settings (e.g. Wi-Fi Multimedia (WMM) is part of optional QoS flow control. An erroneous router firmware may advertise its existence although the setting is not enabled)

## Troubleshooting drivers and firmware

This section covers methods and procedures for installing kernel modules and *firmware* for specific chipsets, that differ from generic method.

See [Kernel modules](/index.php/Kernel_modules "Kernel modules") for general informations on operations with modules.

### Ralink

#### rt2x00

Unified driver for Ralink chipsets (it replaces `rt2500`, `rt61`, `rt73`, etc). This driver has been in the Linux kernel since 2.6.24, you only need to load the right module for the chip: `rt2400pci`, `rt2500pci`, `rt2500usb`, `rt61pci` or `rt73usb` which will autoload the respective `rt2x00` modules too.

A list of devices supported by the modules is available at the project's [homepage](http://rt2x00.serialmonkey.com/wiki/index.php/Hardware).

	Additional notes

*   Since kernel 3.0, rt2x00 includes also these drivers: `rt2800pci`, `rt2800usb`.
*   Since kernel 3.0, the staging drivers `rt2860sta` and `rt2870sta` are replaced by the mainline drivers `rt2800pci` and `rt2800usb`.
*   Some devices have a wide range of options that can be configured with `iwpriv`. These are documented in the [source tarballs](http://web.ralinktech.com/ralink/Home/Support/Linux.html) available from Ralink.

#### rt3090

For devices which are using the rt3090 chipset it should be possible to use `rt2800pci` driver, however, is not working with this chipset very well (e.g. sometimes it is not possible to use higher rate than 2Mb/s).

The best way is to use the [rt3090-dkms](https://aur.archlinux.org/packages/rt3090-dkms/) driver. Make sure to [blacklist](/index.php/Kernel_modules#Blacklisting "Kernel modules") the `rt2800pci` module and setup the `rt3090sta` module to [load](/index.php/Kernel_modules#Loading "Kernel modules") at boot.

**Note:** This driver also works with rt3062 chipsets. Also the [rt3090](https://aur.archlinux.org/packages/rt3090/) package is not supported by the latest kernel and has been orphaned; [rt3090-dkms](https://aur.archlinux.org/packages/rt3090-dkms/) should be used instead.

#### rt3290

The rt3290 chipset is recognised by the kernel `rt2800pci` module. However, some users experience problems and reverting to a patched Ralink driver seems to be beneficial in these [cases](https://bbs.archlinux.org/viewtopic.php?id=161952).

#### rt3573

New chipset as of 2012\. It may require proprietary drivers from Ralink. Different manufacturers use it, see the [Belkin N750 DB wireless usb adapter](https://bbs.archlinux.org/viewtopic.php?pid=1164228#p1164228) forums thread.

#### rt5572

New chipset as of 2012 with support for 5 Ghz bands. It may require proprietary drivers from Ralink and some effort to compile them. At the time of writing a how-to on compilation is available for a DLINK DWA-160 rev. B2 [here](http://bernaerts.dyndns.org/linux/229-ubuntu-precise-dlink-dwa160-revb2).

### Realtek

#### rtl8192cu

The driver is now in the kernel, but many users have reported being unable to make a connection although scanning for networks does work.

[8192cu-dkms](https://aur.archlinux.org/packages/8192cu-dkms/) includes many patches, try this if it does not work fine with the driver in kernel.

#### rtl8192e

The driver is part of the current kernel package. The module initialization may fail at boot giving this error message:

```
rtl819xE:ERR in CPUcheck_firmware_ready()
rtl819xE:ERR in init_firmware() step 2
rtl819xE:ERR!!! _rtl8192_up(): initialization is failed!
r8169 0000:03:00.0: eth0: link down

```

A workaround is to simply unload the module:

```
# modprobe -r r8192e_pci

```

and reload the module (after a pause):

```
# modprobe r8192e_pci

```

#### rtl8188eu

Some dongles, like the TP-Link TL-WN725N v2 (not sure, but it seems that uses the rtl8179 chipset), use chipsets compatible with this driver. In Linux 3.12 the driver [has been moved](http://lwn.net/Articles/564798/) to kernel staging source tree. For older kernels use out-of-tree driver sources built with [dkms](/index.php/Dkms "Dkms") - install [8188eu-dkms](https://aur.archlinux.org/packages/8188eu-dkms/). At the times of 3.15 kernel rtl8188eu driver is buggy and has many stability issues.

#### rtl8723ae/rtl8723be

The new `rtl8723ae` module is included in the mainline Linux kernel since version 3.6, the `rtl8723be` module since 3.15.

Some users may encounter errors with powersave on this card. This is shown with occasional disconnects that are not recognized by high level network managers ([netctl](/index.php/Netctl "Netctl"), [NetworkManager](/index.php/NetworkManager "NetworkManager")). This error can be confirmed by running `dmesg -w` or `journalctl -f` and looking for output related to powersave and the `rtl8723ae`/`rtl8723be` module. If you are having this issue, use the `fwlps=0` kernel option, which should prevent the WiFi card from automatically sleeping and halting connection.

 `/etc/modprobe.d/rtl8723ae.conf`  `options rtl8723ae fwlps=0` 

or

 `/etc/modprobe.d/rtl8723be.conf`  `options rtl8723be fwlps=0` 

### Atheros

The [MadWifi team](http://madwifi-project.org/) currently maintains three different drivers for devices with Atheros chipset:

*   `madwifi` is an old, obsolete driver. Not present in Arch kernel since 2.6.39.1.
*   `ath5k` is newer driver, which replaces the `madwifi` driver. Currently a better choice for some chipsets, but not all chipsets are supported (see below)
*   `ath9k` is the newest of these three drivers, it is intended for newer Atheros chipsets. All of the chips with 802.11n capabilities are supported.

There are some other drivers for some Atheros devices. See [Linux Wireless documentation](http://wireless.kernel.org/en/users/Drivers/Atheros#PCI_.2F_PCI-E_.2F_AHB_Drivers) for details.

#### ath5k

External resources:

*   [http://wireless.kernel.org/en/users/Drivers/ath5k](http://wireless.kernel.org/en/users/Drivers/ath5k)
*   [http://wiki.debian.org/ath5k](http://wiki.debian.org/ath5k)

If you find web pages randomly loading very slow, or if the device is unable to lease an IP address, try to switch from hardware to software encryption by loading the `ath5k` module with `nohwcrypt=1` option. See [Kernel modules#Setting module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules") for details.

Some laptops may have problems with their wireless LED indicator flickering red and blue. To solve this problem, do:

```
# echo none > /sys/class/leds/ath5k-phy0::tx/trigger
# echo none > /sys/class/leds/ath5k-phy0::rx/trigger

```

For alternatives, see [this bug report](https://bugzilla.redhat.com/show_bug.cgi?id=618232).

#### ath9k

External resources:

*   [http://wireless.kernel.org/en/users/Drivers/ath9k](http://wireless.kernel.org/en/users/Drivers/ath9k)
*   [http://wiki.debian.org/ath9k](http://wiki.debian.org/ath9k)

As of Linux 3.15.1, some users have been experiencing a decrease in bandwidth. In some cases this can fixed by editing `/etc/modprobe.d/ath9k.conf` and adding the line:

```
options ath9k nohwcrypt=1

```

**Note:** Check with the command lsmod what module(-name) is in use and change it if named otherwise (e.g. ath9k_htc).

In the unlikely event that you have stability issues that trouble you, you could try using the [backports-patched](https://aur.archlinux.org/packages/backports-patched/) package. An [ath9k mailing list](https://lists.ath9k.org/mailman/listinfo/ath9k-devel) exists for support and development related discussions.

##### Power saving

Although [Linux Wireless](http://wireless.kernel.org/en/users/Documentation/dynamic-power-save) says that dynamic power saving is enabled for Atheros ath9k single-chips newer than AR9280, for some devices (e.g. AR9285) [powertop](https://www.archlinux.org/packages/?name=powertop) might still report that power saving is disabled. In this case enable it manually.

On some devices (e.g. AR9285), enabling the power saving might result in the following error:

 `# iw dev wlan0 set power_save on` 
```
command failed: Operation not supported (-95)

```

The solution is to set the `ps_enable=1` option for the `ath9k` module:

 `/etc/modprobe.d/ath9k.conf`  `options ath9k ps_enable=1` 

##### ASUS

With some ASUS laptops (tested with ASUS U32U series), it could help to add `options asus_nb_wmi wapf=1` to `/etc/modprobe.d/asus_nb_wmi.conf` to fix rfkill-related issues.

You can also try to blacklist the module asus_nb_wmi (tested with ASUSPRO P550C):

```
# echo "blacklist asus_nb_wmi" >> /etc/modprobe.d/blacklist.conf

```

### Intel

#### ipw2100 and ipw2200

These modules are fully supported in the kernel, but they require additional firmware. Depending on which of the chipsets you have, [install](/index.php/Install "Install") either [ipw2100-fw](https://www.archlinux.org/packages/?name=ipw2100-fw) or [ipw2200-fw](https://www.archlinux.org/packages/?name=ipw2200-fw). Then [reload](/index.php/Kernel_modules#Manual_module_handling "Kernel modules") the appropriate module.

**Tip:** You may use the following [module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules"):

*   use the `rtap_iface=1` option to enable the radiotap interface
*   use the `led=1` option to enable a front LED indicating when the wireless is connected or not

#### iwlegacy

[iwlegacy](http://wireless.kernel.org/en/users/Drivers/iwlegacy) is the wireless driver for Intel's 3945 and 4965 wireless chips. The firmware is included in the [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) package.

[udev](/index.php/Udev "Udev") should load the driver automatically, otherwise load `iwl3945` or `iwl4965` manually. See [Kernel modules#Loading](/index.php/Kernel_modules#Loading "Kernel modules") for details.

If you have problems connecting to networks in general or your link quality is very poor, try to disable 802.11n:

 `/etc/modprobe.d/iwl4965.conf`  `options iwl4965 11n_disable=1` 

#### iwlwifi

[iwlwifi](http://wireless.kernel.org/en/users/Drivers/iwlwifi) is the wireless driver for Intel's current wireless chips, such as 5100AGN, 5300AGN, and 5350AGN. See the [full list of supported devices](http://wireless.kernel.org/en/users/Drivers/iwlwifi#Supported_Devices). The firmware is included in the [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) package.

If you have problems connecting to networks in general or your link quality is very poor, try to disable 802.11n, and perhaps also enable software encryption:

 `/etc/modprobe.d/iwlwifi.conf` 
```
options iwlwifi 11n_disable=1
options iwlwifi swcrypto=1
```

If you have a problem with slow uplink speed in 802.11n mode, for example 20Mbps, try to enable antenna aggregation:

 `/etc/modprobe.d/iwlwifi.conf`  `options iwlwifi 11n_disable=8` 

Do not be confused with the option name, when the value is set to `8` it does not disable anything but re-enables transmission antenna aggregation.[[5]](http://forums.gentoo.org/viewtopic-t-996692.html?sid=81bdfa435c089360bdfd9368fe0339a9) [[6]](https://bugzilla.kernel.org/show_bug.cgi?id=81571)

In case this does not work for you, you may try disabling power saving for your wireless adapter. For a permanent solution, add a new udev rule:

 `/etc/udev/rules.d/80-iwlwifi.rules`  `ACTION=="add", SUBSYSTEM=="net", ATTR{address}=="*your_mac_address*", RUN+="/usr/bin/iw dev %k set power_save off"` 

[Some](http://ubuntuforums.org/showthread.php?t=2183486&p=12845473#post12845473) have never gotten this to work. [Others](http://ubuntuforums.org/showthread.php?t=2205733&p=12935783#post12935783) found salvation by disabling N in their router settings after trying everything. This is known to have be the only solution on more than one occasion. The second link there mentions a 5ghz option that might be worth exploring.

**Note:** The [linux-lts](https://www.archlinux.org/packages/?name=linux-lts)-3.14 kernel may take several minutes to load the firmware and make the wireless card ready for use. The issue is reported to be fixed in [linux](https://www.archlinux.org/packages/?name=linux)-3.17 kernel.[[7]](https://bbs.archlinux.org/viewtopic.php?id=190757)

#### Disabling LED blink

**Note:** This works with the `iwlegacy` and `iwlwifi` drivers.

The default settings on the module are to have the LED blink on activity. Some people find this extremely annoying. To have the LED on solid when Wi-Fi is active, you can use the [systemd-tmpfiles](/index.php/Systemd#Temporary_files "Systemd"):

 `/etc/tmpfiles.d/phy0-led.conf` 
```
w /sys/class/leds/phy0-led/trigger - - - - phy0radio

```

Run `systemd-tmpfiles --create phy0-led.conf` for the change to take effect, or reboot.

To see all the possible trigger values for this LED:

```
# cat /sys/class/leds/phy0-led/trigger

```

**Tip:** If you do not have `/sys/class/leds/phy0-led`, you may try to use the `led_mode="1"` [module option](/index.php/Kernel_modules#Setting_module_options "Kernel modules"). It should be valid for both `iwlwifi` and `iwlegacy` drivers.

### Broadcom

See [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless").

### Other drivers/devices

#### Tenda w322u

Treat this Tenda card as an `rt2870sta` device. See [#rt2x00](#rt2x00).

#### orinoco

This should be a part of the kernel package and be installed already.

Some Orinoco chipsets are Hermes II. You can use the `wlags49_h2_cs` driver instead of `orinoco_cs` and gain WPA support. To use the driver, [blacklist](/index.php/Kernel_modules#Blacklisting "Kernel modules") `orinoco_cs` first.

#### prism54

The driver `p54` is included in kernel, but you have to download the appropriate firmware for your card from [this site](http://linuxwireless.org/en/users/Drivers/p54#firmware) and install it into the `/usr/lib/firmware` directory.

**Note:** There is also older, deprecated driver `prism54`, which might conflict with the newer driver (`p54pci` or `p54usb`). Make sure to [blacklist](/index.php/Kernel_modules#Blacklisting "Kernel modules") `prism54`.

#### ACX100/111

**Warning:** The drivers for these devices [are broken](https://mailman.archlinux.org/pipermail/arch-dev-public/2011-June/020669.html) and do not work with newer kernel versions.

Packages: `tiacx` `tiacx-firmware` (deleted from official repositories and AUR)

See [official wiki](http://sourceforge.net/apps/mediawiki/acx100/index.php?title=Main_Page) for details.

#### zd1211rw

[`zd1211rw`](http://zd1211.wiki.sourceforge.net/) is a driver for the ZyDAS ZD1211 802.11b/g USB WLAN chipset, and it is included in recent versions of the Linux kernel. See [[8]](http://www.linuxwireless.org/en/users/Drivers/zd1211rw/devices) for a list of supported devices. You only need to [install](/index.php/Install "Install") the firmware for the device, provided by the [zd1211-firmware](https://www.archlinux.org/packages/?name=zd1211-firmware) package.

#### hostap_cs

[Host AP](http://hostap.epitest.fi/) is a Linux driver for wireless LAN cards based on Intersil's Prism2/2.5/3 chipset. The driver is included in Linux kernel.

**Note:** Make sure to [blacklist](/index.php/Kernel_modules#Blacklisting "Kernel modules") the `orinico_cs` driver, it may cause problems.

### ndiswrapper

Ndiswrapper is a wrapper script that allows you to use some Windows drivers in Linux. You will need the `.inf` and `.sys` files from your Windows driver.

**Warning:** Be sure to use drivers appropriate to your architecture (x86 vs. x86_64).

**Tip:** If you need to extract these files from an `*.exe` file, you can use [cabextract](https://www.archlinux.org/packages/?name=cabextract).

Follow these steps to configure ndiswrapper.

1\. Install [ndiswrapper-dkms](https://www.archlinux.org/packages/?name=ndiswrapper-dkms)

2\. Install the driver to `/etc/ndiswrapper/*`

```
# ndiswrapper -i filename.inf

```

3\. List all installed drivers for ndiswrapper

```
$ ndiswrapper -l

```

4\. Let ndiswrapper write its configuration in `/etc/modprobe.d/ndiswrapper.conf`:

```
# ndiswrapper -m
# depmod -a

```

Now the ndiswrapper install is almost finished; follow the instructions on [Kernel modules#Loading](/index.php/Kernel_modules#Loading "Kernel modules") to automatically load the module at boot.

The important part is making sure that ndiswrapper exists on this line, so just add it alongside the other modules. It would be best to test that ndiswrapper will load now, so:

```
# modprobe ndiswrapper
# iwconfig

```

and *wlan0* should now exist. If you have problems, some help is available at: [ndiswrapper howto](http://sourceforge.net/p/ndiswrapper/ndiswrapper/HowTos/) and [ndiswrapper FAQ](http://sourceforge.net/p/ndiswrapper/ndiswrapper/FAQ/).

### compat-drivers-patched

Patched compat wireless drivers correct the "fixed-channel -1" issue, whilst providing better injection. Install the [compat-drivers-patched](https://aur.archlinux.org/packages/compat-drivers-patched/) package.

[compat-drivers-patched](https://aur.archlinux.org/packages/compat-drivers-patched/) does not conflict with any other package and the modules built reside in `/usr/lib/modules/*your_kernel_version*/updates`.

These patched drivers come from the [Linux Wireless project](http://wireless.kernel.org/) and support many of the above mentioned chips such as:

```
ath5k ath9k_htc carl9170 b43 zd1211rw rt2x00 wl1251 wl12xx ath6kl brcm80211

```

Supported groups:

```
atheros ath iwlagn rtl818x rtlwifi wl12xx atlxx bt

```

It is also possible to build a specific module/driver or a group of drivers by editing the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"), particularly uncommenting the **line #46**. Here is an example of building the atheros group:

```
scripts/driver-select atheros

```

Please read the package's [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") for any other possible modifications prior to compilation and installation.

## See also

*   [The Linux Wireless project](http://wireless.kernel.org/)
*   [Aircrack-ng guide on installing drivers](http://aircrack-ng.org/doku.php?id=install_drivers)