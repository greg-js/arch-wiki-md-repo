Related articles

*   [Network configuration](/index.php/Network_configuration "Network configuration")
*   [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")
*   [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant")

[iwd](https://iwd.wiki.kernel.org/) (iNet wireless daemon) is a wireless daemon for Linux written by Intel that aims to replace [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant"). The core goal of the project is to optimize resource utilization by not depending on any external libraries and instead utilizing features provided by the Linux Kernel to the maximum extent possible. [[1]](https://www.youtube.com/watch?v=F2Q86cphKDo)

iwd can work in standalone mode or in combination with comprehensive network managers like [ConnMan](/index.php/ConnMan "ConnMan"), [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") and [NetworkManager](/index.php/NetworkManager#Using_iwd_as_the_Wi-Fi_backend "NetworkManager").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 iwctl](#iwctl)
        *   [2.1.1 Connect to a network](#Connect_to_a_network)
        *   [2.1.2 Disconnect from a network](#Disconnect_from_a_network)
        *   [2.1.3 Show device information](#Show_device_information)
        *   [2.1.4 Manage known networks](#Manage_known_networks)
*   [3 WPA Enterprise](#WPA_Enterprise)
    *   [3.1 EAP-PWD](#EAP-PWD)
    *   [3.2 TLS Based EAP Methods](#TLS_Based_EAP_Methods)
*   [4 Optional configuration](#Optional_configuration)
    *   [4.1 Disable auto-connect for a particular network](#Disable_auto-connect_for_a_particular_network)
    *   [4.2 Disable periodic scan for available networks](#Disable_periodic_scan_for_available_networks)
    *   [4.3 Deny console (local) user from modifying the settings](#Deny_console_(local)_user_from_modifying_the_settings)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Connect issues after reboot](#Connect_issues_after_reboot)
    *   [5.2 Systemd unit fails on startup due to device not being available](#Systemd_unit_fails_on_startup_due_to_device_not_being_available)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [iwd](https://www.archlinux.org/packages/?name=iwd) package.

## Usage

The [iwd](https://www.archlinux.org/packages/?name=iwd) package provides the client program `iwctl`, the daemon `iwd` and the Wi-Fi monitoring tool `iwmon`.

[Start/enable](/index.php/Start/enable "Start/enable") `iwd.service` so it can be controlled using the `iwctl` command.

### iwctl

To get an interactive prompt do:

```
# iwctl

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

#### Show device information

To display the details of a WiFi device, like MAC address, state and connected network:

```
[iwd]# device *device* show

```

#### Manage known networks

To list networks you have connected to previously:

```
[iwd]# known-networks list

```

To forget a known network:

```
[iwd]# known-networks forget *SSID*

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

### TLS Based EAP Methods

Until Linux kernel v4.20, to connect to EAP-TLS, EAP-TTLS, and EAP-PEAP, the kernel has to be patched. Edit the PKGBUILD for the kernel and add the following sources

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

Example configuration files for these network types can be found in subdirectories here [https://git.kernel.org/pub/scm/network/wireless/iwd.git/tree/autotests](https://git.kernel.org/pub/scm/network/wireless/iwd.git/tree/autotests)

## Optional configuration

File `/etc/iwd/main.conf` can be used for main configuration.

By default, `iwd` stores the network configuration in `/var/lib/iwd` directory. The configuration file is named as `*network*.*type*` where *network* is network SSID and *type* is network type i.e. one of "open", "wep", "psk", "8021x". The file is used to store the encrypted `PreSharedKey` and optionally the cleartext `Passphrase` and can be created by the user without invoking `iwctl`. The file can also be used for other configuration pertaining to that network SSID.

A minimal example file to connect to a WPA2/PSK secured network with SSID "spaceship" and passphrase "test1234":

 `/var/lib/iwd/spaceship.psk` 
```
[Security]
PreSharedKey=aafb192ce2da24d8c7805c956136f45dd612103f086034c402ed266355297295
```

The PreSharedKey can be calculated with wpa_passphrase from the SSID and the WIFI passphrase:

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
Autoconnect=false

```

### Disable periodic scan for available networks

By default when `iwd` is in disconnected state, it periodically scans for available networks. To disable periodic scan (so as to always scan manually), create / edit file `/etc/iwd/main.conf` and add the following section to it:

 `/etc/iwd/main.conf` 
```
[Scan]
disable_periodic_scan=true
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

Some users have reported that the provided systemd unit does not wait for the wireless device to become available. [[2]](https://bbs.archlinux.org/viewtopic.php?id=241803) Thus, the unit fails on startup. To fix this, one can create a systemd unit with the following content:

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

Then one can enable the `iwd@*device*.service` unit for the specific wireless *device*.

See [FS#61367](https://bugs.archlinux.org/task/61367).

## See also

*   [Getting Started with iwd](https://iwd.wiki.kernel.org/gettingstarted)
*   [More examples for Enterprise WPA](https://git.kernel.org/pub/scm/network/wireless/iwd.git/tree/autotests)