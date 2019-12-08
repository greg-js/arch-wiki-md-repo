Related articles

*   [Network configuration](/index.php/Network_configuration "Network configuration")
*   [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")
*   [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant")

[iwd](https://iwd.wiki.kernel.org/) (iNet wireless daemon) is a wireless daemon for Linux written by Intel. The core goal of the project is to optimize resource utilization by not depending on any external libraries and instead utilizing features provided by the Linux Kernel to the maximum extent possible. [[1]](https://www.youtube.com/watch?v=F2Q86cphKDo)

iwd can work in standalone mode or in combination with comprehensive network managers like [ConnMan](/index.php/ConnMan "ConnMan"), [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") and [NetworkManager](/index.php/NetworkManager#Using_iwd_as_the_Wi-Fi_backend "NetworkManager").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 iwctl](#iwctl)
        *   [2.1.1 Connect to a network](#Connect_to_a_network)
        *   [2.1.2 Disconnect from a network](#Disconnect_from_a_network)
        *   [2.1.3 Show device and connection information](#Show_device_and_connection_information)
        *   [2.1.4 Manage known networks](#Manage_known_networks)
*   [3 WPA Enterprise](#WPA_Enterprise)
    *   [3.1 EAP-PWD](#EAP-PWD)
    *   [3.2 EAP-PEAP](#EAP-PEAP)
    *   [3.3 TTLS-PAP](#TTLS-PAP)
    *   [3.4 TLS Based EAP Methods on older kernels](#TLS_Based_EAP_Methods_on_older_kernels)
    *   [3.5 Other cases](#Other_cases)
*   [4 Optional configuration](#Optional_configuration)
    *   [4.1 Disable auto-connect for a particular network](#Disable_auto-connect_for_a_particular_network)
    *   [4.2 Disable periodic scan for available networks](#Disable_periodic_scan_for_available_networks)
    *   [4.3 Enable built-in network configuration](#Enable_built-in_network_configuration)
        *   [4.3.1 Setting static IP address in network configuration](#Setting_static_IP_address_in_network_configuration)
        *   [4.3.2 Select DNS manager](#Select_DNS_manager)
    *   [4.4 Deny console (local) user from modifying the settings](#Deny_console_(local)_user_from_modifying_the_settings)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Connect issues after reboot](#Connect_issues_after_reboot)
    *   [5.2 Systemd unit fails on startup due to device not being available](#Systemd_unit_fails_on_startup_due_to_device_not_being_available)
    *   [5.3 Wireless device is not renamed by udev](#Wireless_device_is_not_renamed_by_udev)
    *   [5.4 WPA Enterprise connection with NetworkManager](#WPA_Enterprise_connection_with_NetworkManager)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [iwd](https://www.archlinux.org/packages/?name=iwd) package.

## Usage

The [iwd](https://www.archlinux.org/packages/?name=iwd) package provides the client program `iwctl`, the daemon `iwd` and the Wi-Fi monitoring tool `iwmon`.

[Start/enable](/index.php/Start/enable "Start/enable") `iwd.service` so it can be controlled using the `iwctl` command.

### iwctl

To get an interactive prompt do:

```
$ iwctl

```

The interactive prompt is then displayed with a prefix of `[iwd]#`.

**Tip:**

*   In the `iwctl` prompt you can auto-complete commands and device names by hitting `Tab`.
*   You can use all commands as command line arguments without entering an interactive prompt. For example: `iwctl device wlp3s0 show`.

To list all available commands:

```
[iwd]# help

```

#### Connect to a network

First, if you do not know your wireless device name, list all wifi devices:

```
[iwd]# device list

```

Then, to scan for networks:

```
[iwd]# station *device* scan

```

You can then list all available networks:

```
[iwd]# station *device* get-networks

```

Finally, to connect to a network:

```
[iwd]# station *device* connect *SSID*

```

If a passphrase is required, you will be prompted to enter it.

**Note:**

*   `iwd` automatically stores network passphrases in the `/var/lib/iwd` directory and uses them to auto-connect in the future. See [#Optional configuration](#Optional_configuration).
*   To connect to a network with spaces in the SSID, the network name should be double quoted when connecting.
*   iwd only supports PSK pass-phrases from 8 to 63 ASCII-encoded characters. The following error message will be given if the requirements are not met: "PMK generation failed. Ensure Crypto Engine is properly configured"

#### Disconnect from a network

To disconnect from a network:

```
[iwd]# station *device* disconnect

```

#### Show device and connection information

To display the details of a WiFi device, like MAC address:

```
[iwd]# device *device* show

```

To display the connection state, including the connected network of a WiFi device:

```
[iwd]# station *device* show

```

#### Manage known networks

To list networks you have connected to previously:

```
[iwd]# known-networks list

```

To forget a known network:

```
[iwd]# known-networks *SSID* forget

```

## WPA Enterprise

### EAP-PWD

For connecting to a EAP-PWD protected enterprice access point you need to create a file called: `*essid*.8021x` in the folder `/var/lib/iwd` with the following content:

 `/var/lib/iwd/*essid*.8021x` 
```
[Security]
EAP-Method=PWD
EAP-Identity=*your_enterprise_email*
EAP-Password=*your_password*

[Settings]
AutoConnect=True
```

If you do not want autoconnect to the AP you can set the option to False and connect manually to the access point via `iwctl`. The same applies to the password, if you do not want to store it plaintext leave the option out of the file and just connect to the enterprise AP.

### EAP-PEAP

Like EAP-PWD, you also need to create a `*essid*.8021x` in the folder. Before you proceed to write the configuration file, this is also a good time to find out which CA certificate your organization uses. This is an example configuration file that uses MSCHAPv2 password authentication:

 `/var/lib/iwd/*essid*.8021x` 
```
[Security]
EAP-Method=PEAP
EAP-Identity=anonymous@realm.edu
EAP-PEAP-CACert=/path/to/root.crt
EAP-PEAP-ServerDomainMask=radius.realm.edu
EAP-PEAP-Phase2-Method=MSCHAPV2
EAP-PEAP-Phase2-Identity=johndoe@realm.edu
EAP-PEAP-Phase2-Password=hunter2

[Settings]
AutoConnect=true
```

**Tip:** If you are planning on using *eduroam* and you are affiliated with a US-based institution, your CA is likely `Addtrust External CA Root`, as your institution probably issues certificates through Internet2's InCommon. However, you should always refer to your organization's help desk if in doubt.

### TTLS-PAP

Like EAP-PWD, you also need to create a `*essid*.8021x` in the folder. Before you proceed to write the configuration file, this is also a good time to find out which CA certificate your organization uses. This is an example configuration file that uses PAP password authentication:

 `/var/lib/iwd/*essid*.8021x` 
```
[Security]
EAP-Method=TTLS
EAP-Identity=anonymous@uni-test.de
EAP-TTLS-CACert=cert.pem
EAP-TTLS-ServerDomainMask=*.uni-test.de
EAP-TTLS-Phase2-Method=Tunneled-PAP
EAP-TTLS-Phase2-Identity=user
EAP-TTLS-Phase2-Password=password

[Settings]
AutoConnect=true
```

### TLS Based EAP Methods on older kernels

Linux kernels older than v4.20 (e.g. [linux-lts](https://www.archlinux.org/packages/?name=linux-lts)) have to be patched to connect to EAP-TLS, EAP-TTLS, and EAP-PEAP. Edit the PKGBUILD for the kernel and add the following sources

 `PKGBUILD` 
```
"iwd1.patch::[https://git.kernel.org/pub/scm/linux/kernel/git/dhowells/linux-fs.git/patch/?id=ab2a33c1c0b1b0a45c16746dd0101057c6d432ed](https://git.kernel.org/pub/scm/linux/kernel/git/dhowells/linux-fs.git/patch/?id=ab2a33c1c0b1b0a45c16746dd0101057c6d432ed)"
"iwd2.patch::[https://git.kernel.org/pub/scm/linux/kernel/git/dhowells/linux-fs.git/patch/?id=3a478ace6154e33009f9b01acbd4eaf7615fef0e](https://git.kernel.org/pub/scm/linux/kernel/git/dhowells/linux-fs.git/patch/?id=3a478ace6154e33009f9b01acbd4eaf7615fef0e)"
"iwd3.patch::[https://git.kernel.org/pub/scm/linux/kernel/git/dhowells/linux-fs.git/patch/?id=5faadff684460b7f4064f9f28db8915a56601147](https://git.kernel.org/pub/scm/linux/kernel/git/dhowells/linux-fs.git/patch/?id=5faadff684460b7f4064f9f28db8915a56601147)"
"iwd4.patch::[https://git.kernel.org/pub/scm/linux/kernel/git/dhowells/linux-fs.git/patch/?id=3c7f3a6c70b47858a065b7a86313f390b083ee40](https://git.kernel.org/pub/scm/linux/kernel/git/dhowells/linux-fs.git/patch/?id=3c7f3a6c70b47858a065b7a86313f390b083ee40)" 
"iwd5.patch::[https://git.kernel.org/pub/scm/linux/kernel/git/dhowells/linux-fs.git/patch/?id=5362bbfdf2a8a5810d4237e4dbbf5da043e47fb6](https://git.kernel.org/pub/scm/linux/kernel/git/dhowells/linux-fs.git/patch/?id=5362bbfdf2a8a5810d4237e4dbbf5da043e47fb6)"
"iwd6.patch::[https://git.kernel.org/pub/scm/linux/kernel/git/dhowells/linux-fs.git/patch/?id=5c93ce3acc010425eab01dc8e0ffb5529f3f85c1](https://git.kernel.org/pub/scm/linux/kernel/git/dhowells/linux-fs.git/patch/?id=5c93ce3acc010425eab01dc8e0ffb5529f3f85c1)"
"iwd7.patch::[https://git.kernel.org/pub/scm/linux/kernel/git/dhowells/linux-fs.git/patch/?id=ca4d545b92cf52ffe777cc7cfbaf64100dfa6e9c](https://git.kernel.org/pub/scm/linux/kernel/git/dhowells/linux-fs.git/patch/?id=ca4d545b92cf52ffe777cc7cfbaf64100dfa6e9c)"
"iwd8.patch::[https://git.kernel.org/pub/scm/linux/kernel/git/dhowells/linux-fs.git/patch/?id=f2ac228eaba9fe3f4fcf80b121eb92707afdd4de](https://git.kernel.org/pub/scm/linux/kernel/git/dhowells/linux-fs.git/patch/?id=f2ac228eaba9fe3f4fcf80b121eb92707afdd4de)"
```

And add the following line to the end of the kernel config:

 `config`  `CONFIG_PKCS8_PRIVATE_KEY_PARSER=y` 

Then update the checksums of the PKGBUILD with `updpkgsums` (from [pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib)):

```
$ updpkgsums

```

and build the package.

### Other cases

More example tests can be [found in the test cases](https://git.kernel.org/pub/scm/network/wireless/iwd.git/tree/autotests) of the upstream repository.

## Optional configuration

File `/etc/iwd/main.conf` can be used for main configuration. See [iwd.config(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/iwd.config.5).

By default, `iwd` stores the network configuration in `/var/lib/iwd` directory. The configuration file is named as `*network*.*type*` where *network* is network SSID and *type* is network type i.e. one of "open", "wep", "psk", "8021x". The file is used to store the encrypted `PreSharedKey` and optionally the cleartext `Passphrase` and can be created by the user without invoking `iwctl`. The file can also be used for other configuration pertaining to that network SSID. For more settings, see [iwd.network(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/iwd.network.5).

A minimal example file to connect to a WPA2/PSK secured network with SSID "spaceship" and passphrase "test1234":

 `/var/lib/iwd/spaceship.psk` 
```
[Security]
PreSharedKey=aafb192ce2da24d8c7805c956136f45dd612103f086034c402ed266355297295
```

The PreSharedKey can be calculated from the SSID and the WiFi passphrase using *wpa_passphrase* (from [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant)) or [wpa-psk](https://aur.archlinux.org/packages/wpa-psk/):

 `$ wpa_passphrase "spaceship" "test1234"` 
```
network={
        ssid="spaceship"
        #psk="test1234"
        psk=aafb192ce2da24d8c7805c956136f45dd612103f086034c402ed266355297295
}
```

**Note:** The SSID of the network is used as a filename only when it contains only alphanumeric characters or one of `- _`. If it contains any other characters, the name will instead be an `=`-character followed by the hex-encoded version of the SSID.

### Disable auto-connect for a particular network

Create / edit file `/var/lib/iwd/*network*.*type*`. Add the following section to it:

 `/var/lib/iwd/spaceship.psk (for example)` 
```
[Settings]
AutoConnect=false

```

### Disable periodic scan for available networks

By default when `iwd` is in disconnected state, it periodically scans for available networks. To disable periodic scan (so as to always scan manually), create / edit file `/etc/iwd/main.conf` and add the following section to it:

 `/etc/iwd/main.conf` 
```
[Scan]
DisablePeriodicScan=true
```

### Enable built-in network configuration

Since version 0.19, iwd can assign IP address(es) and set up routes using a built-in DHCP client or with static configuration.

To activate iwd's network configuration feature, create/edit `/etc/iwd/main.conf` and add the following section to it:

 `/etc/iwd/main.conf` 
```
[General]
EnableNetworkConfiguration=true
```

There is also ability to set route metric with `route_priority_offset`:

 `/etc/iwd/main.conf` 
```
[General]
route_priority_offset=300
```

#### Setting static IP address in network configuration

Add the following section to `/var/lib/iwd/*network*.*type*` file. For example:

 `/var/lib/iwd/spaceship.psk` 
```
[IPv4]
ip=192.168.1.10
netmask=255.255.255.0
gateway=192.168.1.1
broadcast=192.168.1.255
dns=192.168.1.1
```

#### Select DNS manager

At the moment, iwd supports two DNS managers—[systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved") and [resolvconf](/index.php/Resolvconf "Resolvconf").

Add the following section to `/etc/iwd/main.conf` for `systemd-resolved`:

 `/etc/iwd/main.conf` 
```
[Network]
NameResolvingService=systemd
```

For `resolvconf`:

 `/etc/iwd/main.conf` 
```
[Network]
NameResolvingService=resolvconf
```

### Deny console (local) user from modifying the settings

By default `iwd` D-Bus interface allows *any* console user to connect to `iwd` daemon and modify the settings, even if that user is not a *root* user.

If you do not want to allow console user to modify the settings but allow reading the status information, then create a D-Bus configuration file as follows.

 `/etc/dbus-1/system.d/iwd-strict.conf` 
```
<!-- prevent local users from changing iwd settings, but allow
     reading status information. overrides some part of
     /usr/share/dbus-1/system.d/iwd-dbus.conf. -->

<!-- This configuration file specifies the required security policies
     for iNet Wireless Daemon to work. -->

<!DOCTYPE busconfig PUBLIC "-//freedesktop//DTD D-BUS Bus Configuration 1.0//EN"
 "http://www.freedesktop.org/standards/dbus/1.0/busconfig.dtd">
<busconfig>

  <policy at_console="true">
    <deny send_destination="net.connman.iwd"/>
    <allow send_destination="net.connman.iwd" send_interface="org.freedesktop.DBus.Properties" send_member="GetAll" />
    <allow send_destination="net.connman.iwd" send_interface="org.freedesktop.DBus.Properties" send_member="Get" />
    <allow send_destination="net.connman.iwd" send_interface="org.freedesktop.DBus.ObjectManager" send_member="GetManagedObjects" />
    <allow send_destination="net.connman.iwd" send_interface="net.connman.iwd.Device" send_member="RegisterSignalLevelAgent" />
    <allow send_destination="net.connman.iwd" send_interface="net.connman.iwd.Device" send_member="UnregisterSignalLevelAgent" />
  </policy>

</busconfig>

```

**Tip:** Remove *<allow>* lines above to deny reading the status information as well.

## Troubleshooting

### Connect issues after reboot

A low entropy pool can cause connection problems in particular noticeable after reboot. See [Random number generation](/index.php/Random_number_generation "Random number generation") for suggestions to increase the entropy pool.

### Systemd unit fails on startup due to device not being available

Some users have reported that the provided systemd unit does not wait for the wireless device to become available [[2]](https://bbs.archlinux.org/viewtopic.php?id=241803). Unfortunately, if iwd is started before udev renaming is done, the network device will be blocked and renaming will fail. Thus, the unit fails on startup [[3]](https://iwd.wiki.kernel.org/interface_lifecycle#udev_interface_renaming). The issue can be fixed by forcing iwd to legacy mode and thus, not renaming newly detected devices, by adding an option to `/etc/iwd/main.conf` as follows:

 `/etc/iwd/main.conf` 
```
[General]
use_default_interface=true
```

Optionally, bind iwd to a specific wireless device by creating a systemd unit with the following content. As of *0.21*, it has been observed that this will not prevent iwd from renaming the wireless device later, thus the use of iwd's legacy mode is mandatory:

 `/etc/systemd/system/iwd@.service` 
```
[Unit]
Description=Wireless service on %I
BindsTo=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device

[Service]
Type=dbus
BusName=net.connman.iwd
ExecStart=/usr/lib/iwd/iwd --interface %i
LimitNPROC=1
Restart=on-failure
```

Then, disable `iwd.service` and enable `iwd@*device*.service` unit for the specific wireless *device*.

Alternatively, set a proper dependency for iwd to run after systemd/udevd by creating a [drop-in file](/index.php/Drop-in_file "Drop-in file") as follows: [[4]](https://lists.01.org/pipermail/iwd/2019-March/005837.html)

 `/etc/systemd/system/iwd.service.d/override.conf` 
```
[Unit]
After=systemd-udevd.service
```

If systemd-networkd is used, since both systemd-udevd/networkd play relatively well together, and both are involved, it is reasonable to start iwd after both of them:

 `/etc/systemd/system/iwd.service.d/override.conf` 
```
[Unit]
After=systemd-udevd.service systemd-networkd.service
```

See [FS#61367](https://bugs.archlinux.org/task/61367).

### Wireless device is not renamed by udev

Upgrade to [iwd](https://www.archlinux.org/packages/?name=iwd) 1.0 introduces the systemd network link configuration file:

 `/usr/lib/systemd/network/80-iwd.link` 
```
[Match]
Type=wlan

[Link]
NamePolicy=keep kernel
```

This prevents udev from renaming the interface to `wlp#s#`. As a result the wireless link name `wlan#` is kept after boot.

If this results to issues disabling this file helps:

```
# ln -s /dev/null /etc/systemd/network/80-iwd.link

```

### WPA Enterprise connection with NetworkManager

If you try to connect to an WPA Enterprise network like 'eduroam' with NetworkManager with the iwd backend then you will get the following error from NetworkManager:

```
 Connection 'eduroam' is not avialable on device wlan0 because profile is not compatible with device (802.1x connections must have IWD provisioning files)

```

This is because NetworkManager can not configure a WPA Enterprise network. Therefore you have to configure it using an iwd config file `/var/lib/iwd/*essid*.8021x` like described in [#WPA_Enterprise](#WPA_Enterprise).

## See also

*   [Getting Started with iwd](https://iwd.wiki.kernel.org/gettingstarted)
*   [Network Configuration Settings](https://iwd.wiki.kernel.org/networkconfigurationsettings)
*   [More Examples for WPA Enterprise](https://git.kernel.org/pub/scm/network/wireless/iwd.git/tree/autotests)