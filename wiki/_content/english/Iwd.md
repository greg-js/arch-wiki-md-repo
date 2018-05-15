Related articles

*   [Network configuration](/index.php/Network_configuration "Network configuration")
*   [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")
*   [WPA2 Enterprise](/index.php/WPA2_Enterprise "WPA2 Enterprise")

[IWD](https://iwd.wiki.kernel.org/) (iNet wireless daemon) is a wireless daemon for Linux, written by Intel aiming to replace [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant").[[1]](https://www.youtube.com/watch?v=F2Q86cphKDo) IWD works standalone or in combination with [ConnMan](/index.php/ConnMan "ConnMan") or [NetworkManager](/index.php/NetworkManager "NetworkManager"). It comes with different enhancements like an own crypto-library, called ELL, which docks directly into the Linux Kernel cryptography. IWD follows a more simple, more secure and more modern approach.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 iwctl](#iwctl)
*   [3 WPA Enterprise](#WPA_Enterprise)
    *   [3.1 EAP-PWD](#EAP-PWD)
*   [4 Optional configuration](#Optional_configuration)
    *   [4.1 Disable auto-connect for a particular network](#Disable_auto-connect_for_a_particular_network)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [iwd](https://www.archlinux.org/packages/?name=iwd) package.

## Usage

The [iwd](https://www.archlinux.org/packages/?name=iwd) package provides the client program `iwctl`, the daemon `iwd` and the Wi-Fi monitoring tool `iwmon`.

Once the iwd daemon is running ([start/enable](/index.php/Start/enable "Start/enable") `iwd.service`) you can control it using the `iwctl` command.

### iwctl

Running `iwctl` gets you an interactive prompt. From now on commands that need to be run in the `iwctl` prompt will be prefixed by `[iwd]#`.

**Tip:** In the `iwctl` prompt you can auto-complete commands and device names by hitting `Tab`.

List available commands:

```
[iwd]# help

```

List all wifi devices:

```
[iwd]# device list

```

Scan for networks:

```
[iwd]# device *interface* scan

```

List networks:

```
[iwd]# device *interface* get-networks

```

Connect to a WPA2 protected network (will prompt you for the passphrase):

```
[iwd]# device *interface* connect *network_name*

```

**Note:** `iwd` automatically stores network passphrases (as encrypted `PreSharedKey`) in the `/var/lib/iwd` directory and uses them to auto-connect in the future.

Displaying details of a WiFi device (like MAC address, state and connected network):

```
[iwd]# device *interface* show

```

List known networks:

```
[iwd]# known-networks list

```

Forget a known network:

```
[iwd]# known-networks forget *network_name*

```

## WPA Enterprise

### EAP-PWD

For connecting to a EAP-PWD protected enterprice access point you need to create a file called: `*essid*.8021x` in the folder `/var/lib/iwd` with the following content:

 `/var/lib/iwd/*essid*.8021x` 
```
[Security]
EAP-Method=PWD
EAP-Identity=*your_enterprise_email*
EAP-PWD-Password=*your_password*

[Settings]
Autoconnect=True
```

If you do not want autoconnect to the AP you can set the option to False and connect manually to the access point via `iwctl`. The same applies to the password, if you do not want to store it plaintext leave the option out of the file and just connect to the enterprise AP.

## Optional configuration

File `/etc/iwd/main.conf` can be used for main configuration.

Directory `/var/lib/iwd` can be used for network (SSID) configuration.

### Disable auto-connect for a particular network

Create / edit file `/var/lib/iwd/*network*.*type*`, where *network* is network SSID and *type* is network type i.e. one of "open", "wep", "psk", "8021x". Add the following section to it:

 `/var/lib/iwd/spaceship.psk (for example)` 
```
[Settings]
Autoconnect=false
```

## See also

*   [Getting Started with iwd](https://iwd.wiki.kernel.org/gettingstarted)
*   [More examples for Enterprise WPA](https://git.kernel.org/pub/scm/network/wireless/iwd.git/tree/autotests)