Related articles

*   [Network configuration](/index.php/Network_configuration "Network configuration")
*   [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")
*   [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant")

[IWD](https://iwd.wiki.kernel.org/) (iNet wireless daemon) is a wireless daemon for Linux written by Intel that aims to replace [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant"). The core goal of the project is to optimize resource utilization by not depending on any external libraries and instead utilizing features provided by the Linux Kernel to the maximum extent possible. [[1]](https://www.youtube.com/watch?v=F2Q86cphKDo)

IWD can work in standalone mode or in combination with comprehensive network managers like [ConnMan](/index.php/ConnMan "ConnMan"), [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") and [NetworkManager](/index.php/NetworkManager "NetworkManager").

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 iwctl](#iwctl)
*   [3 WPA Enterprise](#WPA_Enterprise)
    *   [3.1 EAP-PWD](#EAP-PWD)
    *   [3.2 TLS Based EAP Methods](#TLS_Based_EAP_Methods)
*   [4 Optional configuration](#Optional_configuration)
    *   [4.1 Disable auto-connect for a particular network](#Disable_auto-connect_for_a_particular_network)
    *   [4.2 Deny console (local) user from modifying the settings](#Deny_console_.28local.29_user_from_modifying_the_settings)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [iwd](https://www.archlinux.org/packages/?name=iwd) package.

## Usage

The [iwd](https://www.archlinux.org/packages/?name=iwd) package provides the client program `iwctl`, the daemon `iwd` and the Wi-Fi monitoring tool `iwmon`.

Once the iwd daemon is running, [start/enable](/index.php/Start/enable "Start/enable") `iwd.service` so it can be controlled using the `iwctl` command.

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
[iwd]# station *interface* scan

```

List networks:

```
[iwd]# station *interface* get-networks

```

Connect to a WPA2 protected network (will prompt you for the passphrase):

```
[iwd]# station *interface* connect *network_name*

```

To disconnect from a network:

```
[iwd]# station *interface* disconnect

```

**Note:**

*   `iwd` automatically stores network passphrases (as encrypted `PreSharedKey`) in the `/var/lib/iwd` directory and uses them to auto-connect in the future.
*   To connect to a network with spaces in the SSID, the network name should be double quoted when connecting.
*   IWD only supports PSK pass-phrases from 8 to 63 ASCII-encoded characters. The following error message will be given if the requirements are not met: "PMK generation failed. Ensure Crypto Engine is properly configured"

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

**Tip:** You can use all commands from the interactive session as command line arguments. For example: `iwctl device wlp3s0 show`.

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

As of now, to connect to EAP-TLS, EAP-TTLS, and EAP-PEAP, the kernel has to be patched. Edit the PKGBUILD for the kernel and add the following sources

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

Then update the checksums of the PKGBUILD:

```
$ updpkgsums

```

and build the package.

Example configuration files for these network types can be found in subdirectories here [https://git.kernel.org/pub/scm/network/wireless/iwd.git/tree/autotests](https://git.kernel.org/pub/scm/network/wireless/iwd.git/tree/autotests)

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

## See also

*   [Getting Started with iwd](https://iwd.wiki.kernel.org/gettingstarted)
*   [More examples for Enterprise WPA](https://git.kernel.org/pub/scm/network/wireless/iwd.git/tree/autotests)