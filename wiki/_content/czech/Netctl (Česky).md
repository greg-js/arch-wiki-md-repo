Netctl je aplikací vyvíjenou v rámci Arch Linuxu, která má za cíl nahradit původní *netcfg*. Netctl představuje budoucnost (a současnot) ve správě síťového nastavení v Arch Linuxu .

## Contents

*   [1 Instalace](#Instalace)
*   [2 Required reading](#Required_reading)
*   [3 Konfigurace](#Konfigurace)
    *   [3.1 Automatic operation](#Automatic_operation)
        *   [3.1.1 Just one profile](#Just_one_profile)
        *   [3.1.2 Multiple profiles](#Multiple_profiles)
    *   [3.2 Migrating from netcfg](#Migrating_from_netcfg)
    *   [3.3 Passphrase obfuscation (256-bit PSK)](#Passphrase_obfuscation_.28256-bit_PSK.29)
*   [4 Support](#Support)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Replace 'netcfg current'](#Replace_.27netcfg_current.27)
    *   [5.2 Eduroam](#Eduroam)

## Instalace

Balíček [netctl](https://www.archlinux.org/packages/?name=netctl) je dostupný v oficiálních repozitářích. Installing netctl will replace [netcfg](https://aur.archlinux.org/packages/netcfg/).

Balíčky [netctl](https://www.archlinux.org/packages/?name=netctl) a [netcfg](https://aur.archlinux.org/packages/netcfg/) jsou konfliktní (pouze jeden z nich může být nainstalován). You will be potentially connectionless after installing **netctl** if your profiles are misconfigured.

## Required reading

Před samotnou instalací si prosím prostudujte následjící manuálové stránky:

*   [netctl](https://github.com/joukewitteveen/netctl/blob/master/docs/netctl.1.txt)
*   [netctl.profile](https://github.com/joukewitteveen/netctl/blob/master/docs/netctl.profile.5.txt)
*   [netctl.special](https://github.com/joukewitteveen/netctl/blob/master/docs/netctl.special.7.txt)

## Konfigurace

`netctl` may be used to introspect and control the state of the systemd services for the network profile manager. Example configuration files are provided for the user to assist them in configuring their network connection. These example profiles are located in `/etc/netctl/examples/`. The common configurations include:

*   ethernet-dhcp
*   ethernet-static
*   wireless-wpa
*   wireless-wpa-static

For wireless settings, use **wifi-menu -o** will generate the config file in /etc/netctl.

To use an example profile, simply copy one of them from `/etc/netctl/examples/` to `/etc/netctl/` and configure it to your needs:

```
# cp /etc/netctl/examples/wireless-wpa /etc/netctl/

```

Once you have created your profile, make an attempt to establish a connection using the newly created profile by running:

```
# netctl start *profile*

```

If issuing the above command results in a failure, then use `journalctl -xn` and `netctl status <profile>` in order to obtain a more in depth explanation of the failure. Make the needed corrections to the failed configuration and retest.

### Automatic operation

#### Just one profile

If you are using only one profile, once that profile is started successfully, it can be `enabled` using

```
# netctl enable *profile* 

```

This will create and enable a [systemd](/index.php/Systemd "Systemd") service that will start when the computer boots.

**Note:** The connection to a dhcp-server is only established if the interface is connected and up at boot time (or when the service starts). In order to have an automatic connection established on cable connect, proceed to [#Multiple Profiles](#Multiple_Profiles).

#### Multiple profiles

Whereas with `netcfg` there was `net-auto-wireless.service` and `net-auto-wired.service`, `netctl` uses `netctl-auto@*interface*.service` for wireless profiles, and `netctl-ifplugd@*interface*.service` for wired profiles. In order to make the `netctl-auto@*interface*.service` work for wireless interfaces, the package [wpa_actiond](https://www.archlinux.org/packages/?name=wpa_actiond) is required to be installed. In order to make the `netctl-ifplugd@*interface*.service` work for wired interfaces, the package [ifplugd](https://www.archlinux.org/packages/?name=ifplugd) is required to be installed. Configure `/etc/ifplugd/ifplugd.conf` accordingly. Automatic selection of a WPA-enabled profile by netctl-auto is not possible with option `Security=wpa-config`, please use `Security=wpa-configsection` instead.

To set preferred wired profile for auto-connecting specify `AutoWired=yes` in that profile. By default on failure [ifplugd](https://www.archlinux.org/packages/?name=ifplugd) will pass to other DHCP wired profiles, then to static ones. If you don't want it to do so, set `ForceConnect=yes`.

Once your profiles are set and verified to be working, simply enable these services with

```
# systemctl enable netctl-auto@*interface*.service 
# systemctl enable netctl-ifplugd@*interface*.service  

```

**Note:** If any of the profiles contain errors, such as an empty `Key=` variable, the unit will fail to load at boot.

If you have previously enabled a profile through `netctl`, run

```
# netctl disable *profile*

```

to prevent the profile from starting twice at boot, and possibly causing issues with wpa_supplicant.

**Note:**

*   If there is ever a need to alter a currently enabled profile, execute `netctl reenable <profile>` to apply the changes.
*   *interface* is hardware minus, e.g netctl-auto@wlan0.service or netctl-auto@wlo1.service

### Migrating from netcfg

**Warning:** `netctl` conflicts with `netcfg` so disable existing `netcfg@*profile*` service before installing `netctl`.

`netctl` uses `/etc/netctl` to store its profiles, *not* `/etc/network.d` (`netcfg`'s profile storage location).

In order to migrate from netcfg, at least the following is needed:

*   Move network profile files to the new directory.
*   Rename variables therein according to netctl.profile(5) (Most variable names have only UpperCamelCase i.e CONNECTION= becomes Connection=).
*   For static IP configuration make sure the Address= variables have a netmask after the IP (e.g. Address=('192.168.1.23**/24'** '192.168.1.87**/24'**) in the example profile).
*   If you setup a wireless profile according in the `wireless-wpa-configsection` example, note that this overrides `wpa_supplicant` options defined above the brackets. For a connection to a hidden wireless network, add `scan_ssid=1` to the options in the `wireless-wpa-configsection`; `Hidden=yes` does not work there.
*   Unquote interface variables and other variables that don't strictly need quoting (this is mainly a style thing).
*   Run `netctl enable *profile*` for every profile in the old NETWORKS array. 'last' doesn't work this way, see netctl.special(7).
*   Use `netctl list`/`netctl start *profile*` instead of **netcfg-menu**. **wifi-menu** remains available.
*   It may be a good idea to use `systemctl --type=service` to ensure that no other service is running that may want to configure the network. Multiple networking services will conflict.

### Passphrase obfuscation (256-bit PSK)

Users *not* wishing to have the passphrase to their wireless network stored in *plain text* have the option of storing the corresponding 256-bit pre-shared key (PSK) instead, which is calculated from the passphrase and the SSID using standard algorithms.

*   Method 1: Use `wifi-menu -o` to generate a config file in `/etc/netctl`
*   Method 2: Manual settings as follows. If the passphrase fails, try removing the \" in Key= (see note below)

For both methods it is suggested to `chmod 600 /etc/netctl/<config_file>` to prevent user access to the password.

Calculate your 256-bit PSK using [wpa_passphrase](/index.php/WPA_supplicant#Configuration_file "WPA supplicant"):

 `Usage: wpa_passphrase [ssid] [passphrase]`  `$ wpa_passphrase archlinux freenode` 

In a second terminal window, copy the example file `wireless-wpa` from `/etc/netctl/examples` to `/etc/netctl`:

```
# cp /etc/netctl/examples/wireless-wpa /etc/netctl/wireless-wpa

```

You will then need to edit `/etc/netctl/wireless-wpa` using your favorite text editor and add the *pre-shared key*, that was generated earlier using wpa_passphrase, to the `**Key**` variable of this profile.

Once completed your network profile `wireless-wpa` containing a 256-bit PSK should resemble:

 `/etc/netctl/wireless-wpa` 
```
Description='A simple WPA encrypted wireless connection using 256-bit PSK'
Interface=wlp2s2
Connection=wireless
Security=wpa
IP=dhcp
ESSID=archlinux
Key=\"64cf3ced850ecef39197bb7b7b301fc39437a6aa6c6a599d0534b16af578e04a
```

**Note:**

*   Make sure to use the **special non-quoted rules** for `Key=` that are explained at the end of [netctl.profile(5)](https://github.com/joukewitteveen/netctl/blob/master/docs/netctl.profile.5.txt).
*   The key that you put in the profile configuration is enough to connect to a WPA-PSK network, which means this procedure is only good to hide the human-readable passphrase but will not prevent anyone with read access to this file from connecting to the network. You should ask yourself if there is any use in this at all, since using the same passphrase for anything else is a very poor security measure.

## Support

Official announcement thread: [https://bbs.archlinux.org/viewtopic.php?id=157670](https://bbs.archlinux.org/viewtopic.php?id=157670)

## Tips and tricks

### Replace 'netcfg current'

As of April 2013 there is no netctl alternative to `netcfg current`. If you relied on it for something, like a status bar for a tiling window manager, you can now use:

```
# netctl list | awk '/*/ {print $2}'

```

or, when `netctl-auto` was used to connect:

```
# wpa_cli -i *interface* status | sed -n 's/^id_str=//p'

```

### Eduroam

To connect ta a wireless network at university it is very likely you need a profile looking like this (tested in Freiburg, Germany):

 `/etc/netctl/wlan0-eduroam` 
```
Description='Eduroam-profile for <user>'
Interface=wlan0
Connection=wireless
Security=wpa-configsection
IP=dhcp
WPAConfigSection=(
 'ssid="eduroam"'
 'proto=RSN'
 'key_mgmt=WPA-EAP'
 'pairwise=CCMP'
 'auth_alg=OPEN'
 'eap=PEAP'
 'identity="<user>"'
 'password="<password>"'
)

```