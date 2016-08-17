[Wicd](https://launchpad.net/wicd) is a network connection manager that can manage wireless and wired interfaces, similar and an alternative to [NetworkManager](/index.php/NetworkManager "NetworkManager"). Wicd is written in [Python](/index.php/Python "Python") and [GTK+](/index.php/GTK%2B "GTK+"). Alternatively, a version of Wicd for [KDE](/index.php/KDE "KDE"), written in [Qt](/index.php/Qt "Qt"), is available from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). Wicd can also run from the terminal in a curses interface, requiring no X server session or task panel (see [#Running Wicd in Text Mode](#Running_Wicd_in_Text_Mode)).

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Base package](#Base_package)
    *   [1.2 GTK+ client](#GTK.2B_client)
    *   [1.3 KDE client](#KDE_client)
    *   [1.4 Notifications](#Notifications)
    *   [1.5 Alternative](#Alternative)
*   [2 Getting started](#Getting_started)
    *   [2.1 Initial setup](#Initial_setup)
    *   [2.2 Running Wicd in Desktop Environment](#Running_Wicd_in_Desktop_Environment)
    *   [2.3 Running Wicd in Text Mode](#Running_Wicd_in_Text_Mode)
    *   [2.4 Switching WPA supplicant driver](#Switching_WPA_supplicant_driver)
    *   [2.5 Autostart](#Autostart)
    *   [2.6 Scripts](#Scripts)
        *   [2.6.1 Stop ARP spoofing attacks](#Stop_ARP_spoofing_attacks)
        *   [2.6.2 Change MAC using macchanger](#Change_MAC_using_macchanger)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Autoconnect on resume from hibernation/suspension](#Autoconnect_on_resume_from_hibernation.2Fsuspension)
    *   [3.2 Importing pynotify failed, notifications disabled](#Importing_pynotify_failed.2C_notifications_disabled)
    *   [3.3 D-Bus connection error message](#D-Bus_connection_error_message)
    *   [3.4 Problems after package update](#Problems_after_package_update)
    *   [3.5 Note about graphical sudo programs](#Note_about_graphical_sudo_programs)
    *   [3.6 Eduroam](#Eduroam)
    *   [3.7 Two instances of wicd-client (and possibly two icons in tray)](#Two_instances_of_wicd-client_.28and_possibly_two_icons_in_tray.29)
    *   [3.8 Bad password using PEAP with TKIP/MS-CHAPv2](#Bad_password_using_PEAP_with_TKIP.2FMS-CHAPv2)
    *   [3.9 Wicd skips obtaining IP address on wlp](#Wicd_skips_obtaining_IP_address_on_wlp)
    *   [3.10 dhcpcd not running](#dhcpcd_not_running)
*   [4 See also](#See_also)

## Installation

### Base package

[Install](/index.php/Install "Install") [wicd](https://www.archlinux.org/packages/?name=wicd), available in the [official repositories](/index.php/Official_repositories "Official repositories"). It includes everything needed to run the wicd daemon and the `wicd-cli` and `wicd-curses` interfaces.

### GTK+ client

For a GTK+ front-end, install [wicd-gtk](https://www.archlinux.org/packages/?name=wicd-gtk), available in the official repositories. It includes everything needed to run the GTK interface of wicd and the autostart file for the client to appear in the system tray.

### KDE client

For a KDE front-end, install [wicd-kde](https://aur.archlinux.org/packages/wicd-kde/), available in the [AUR](/index.php/AUR "AUR").

### Notifications

To enable visual notifications about network status, you need to install the packages [notification-daemon](https://www.archlinux.org/packages/?name=notification-daemon) and [python2-notify](https://www.archlinux.org/packages/?name=python2-notify).

If you are not using [GNOME](/index.php/GNOME "GNOME"), you may want to install [xfce4-notifyd](https://www.archlinux.org/packages/?name=xfce4-notifyd) instead of the notification-daemon, because it pulls a lot of unnecessary GNOME packages.

### Alternative

The [wicd-bzr](https://aur.archlinux.org/packages/wicd-bzr/) buildscript is available in the [AUR](/index.php/AUR "AUR"), which should build the latest development branch. If you need an alternative version or you just want to roll your own package, you can easily build it using [ABS](/index.php/ABS "ABS").

## Getting started

### Initial setup

Wicd provides a daemon that must be started.

**Warning:** Running multiple network managers *will* cause problems, so it is important to *disable all other network management daemons*.

First, stop all previously running network daemons (like netctl, netcfg, dhcpcd, NetworkManager).

Disable any existing network management services, including `netctl`, `netcfg`, `dhcpcd`, and `networkmanager`. Refer to [Systemd#Using units](/index.php/Systemd#Using_units "Systemd").

**Note:** You might need to stop and disable the **network** daemon instead of **netctl**, which is a current replacement for **network** service. If unsure, try disabling both.

Start the **wicd** [systemd](/index.php/Systemd "Systemd") [daemon](/index.php/Daemon "Daemon") and enable it at system start up.

Add your account to **users** group:

```
# gpasswd -a USERNAME users

```

**Note:** The Unix group that D-Bus allows to access *wicd* is subject to change, and it may be different than *users*. Check which policy group is specified in `/etc/dbus-1/system.d/wicd.conf`, and add your user to that group.

If you added your user to a new group, log out and then log in.

### Running Wicd in Desktop Environment

If you have installed the [wicd-gtk](https://www.archlinux.org/packages/?name=wicd-gtk) and entered the desktop environment. Open a virtual terminal to run one of the following commands.

*   To start Wicd as system service, [start](/index.php/Start "Start") the `wicd.service` systemd unit.

*   To load Wicd, run:

```
$ wicd-client

```

*   To force it to start minimized in the notification area, run:

```
$ wicd-client --tray

```

*   If your desktop environment does not have a notification area, or if you don't want wicd to show tray icon, run:

```
$ wicd-client -n

```

### Running Wicd in Text Mode

If you did not install [wicd-gtk](https://www.archlinux.org/packages/?name=wicd-gtk) then use wicd-cli or wicd-curses:

```
$ wicd-curses

```

**Note:** Wicd does not prompt you for a passkey. To use encrypted connections (WPA/WEP), expand the network you want to connect to, click **Advanced** and enter the needed info.

**Note:** *wicd-curses* is less stable than *wicd-gtk*, and is known to crash regularly. If a crash occurs when attempting to configure a wireless network, try [wicd-patched](https://aur.archlinux.org/packages/wicd-patched/)

### Switching WPA supplicant driver

*Wicd* still suggests to "almost always" use Wext as WPA supplicant driver and defaults to it. This is [outdated behavior](http://linuxwireless.org/en/developers/Documentation/Wireless-Extensions/index.html#Do_we_still_use_WE_.3F). One should use nl80211 instead, except with old drivers that do not support it. The relevant option is located in *Preferences > Advanced Settings*.

### Autostart

The [wicd-gtk](https://www.archlinux.org/packages/?name=wicd-gtk) package puts a file in `/etc/xdg/autostart/wicd-tray.desktop`, which will autostart `wicd-client` upon login to your DE/WM. If so, [enable](/index.php/Enable "Enable") the `wicd` systemd unit.

If `/etc/xdg/autostart/wicd-tray.desktop` does not exist, you can add **wicd-client** to your DE/WM startup to have the application start when you log in.

**Note:** If **wicd-client** is added to DE/WM startup when `/etc/xdg/autostart/wicd-tray.desktop` exists, you will have an issue of two `wicd-client` instances running.

### Scripts

Wicd has the ability to run scripts during all stages of the connection process (post/pre connect/disconnect). Simply place a script inside the relevant stage folder within `/etc/wicd/scripts/` and make it executable.

The scripts are able to receive three parameters, these being:

```
$1 - the connection type (wireless/wired).
$2 - the ESSID (network name).
$3 - the BSSID (gateway MAC).

```

#### Stop ARP spoofing attacks

The script below can be used to set a static ARP, to stop ARP spoofing attacks. Simply change the values within the case statement to match those of the networks you want to set static ARP entries for. Launch it as root:

```
#!/bin/bash
#Set the parameters passed to this script to meaningful variable names.
connection_type="$1"
essid="$2"
bssid="$3"

if [ "${connection_type}" == "wireless" ]; then

        #Change below to match your networks.
        case "$essid" in
        YOUR-NETWORK-NAME-ESSID)
                arp -s 192.168.0.1 00:11:22:33:44:55
         ;;
         Netgear01923)
                arp -s 192.168.0.1 10:11:20:33:40:50
         ;;
         ANOTHER-ESSID)
                arp -s 192.168.0.1 11:33:55:77:99:00
         ;;
         *)
                echo "Static ARP not set. No network defined."
         ;;
       esac
fi

```

#### Change MAC using macchanger

See [MAC address spoofing#systemd + macchanger + dhcpcd (no NetworkManager)](/index.php/MAC_address_spoofing#systemd_.2B_macchanger_.2B_dhcpcd_.28no_NetworkManager.29 "MAC address spoofing").

The script below can be used to change the MAC address of your network interfaces.

To change the MAC whenever you connect to a network, place this script under `/etc/wicd/scripts/preconnect/`.

Take a look at `macchanger --help` to adjust the macchanger command to your liking.

```
#!/usr/bin/env bash

connection_type="$1"

if [[ "${connection_type}" == "wireless" ]]; then
        ip link set wlp2s0 down
        macchanger -A wlp2s0
        ip link set wlp2s0 up
elif [[ "${connection_type}" == "wired" ]]; then
        ip link set enp1s0 down
        macchanger -A enp1s0
        ip link set enp1s0 up
fi

```

## Troubleshooting

See [Network configuration#Troubleshooting](/index.php/Network_configuration#Troubleshooting "Network configuration") for troubleshooting wired connections and [Wireless network configuration#Troubleshooting](/index.php/Wireless_network_configuration#Troubleshooting "Wireless network configuration") for troubleshooting wireless connections. This section covers only problems specific to *wicd*.

### Autoconnect on resume from hibernation/suspension

If for some reasons autoconnect on resume from hibernation or suspension does not work automatically, you can manually restart Wicd by enabling the following service file for your user.

 `/etc/systemd/system/wicd-resume@.service` 
```
[Unit]
Description=Restart Wicd autoconnect service on resume
After=suspend.target

[Service]
Type=oneshot
User=%i
RemainAfterExit=no
ExecStart=/usr/share/wicd/daemon/autoconnect.py

[Install]
WantedBy=suspend.target

```

### Importing pynotify failed, notifications disabled

In case the [python2-notify](https://www.archlinux.org/packages/?name=python2-notify) package did not get installed automatically. You can [install](/index.php/Install "Install") it from [official repositories](/index.php/Official_repositories "Official repositories").

### D-Bus connection error message

If wicd suddenly stopped working and it complains about D-Bus, it is quite likely that you just need to remove wicd fully, including and all its configuration files, and re-install it from scratch by first removing [wicd](https://www.archlinux.org/packages/?name=wicd). Then remove its configuration files:

```
# rm -rf /etc/wicd /var/log/wicd /etc/dbus-1/system.d/wicd*

```

Then reinstall the package. Check this link for more details: [https://bbs.archlinux.org/viewtopic.php?pid=577141#p577141](https://bbs.archlinux.org/viewtopic.php?pid=577141#p577141)

Wicd-client also throws a D-Bus connection error message ("Could not connect to wicd's D-Bus interface.") when wicd is not running due to a problem with a config file. It seems that sometimes an empty account gets added to `/etc/wicd/wired-settings.conf` in which case you simply have to remove the

```
[] 

```

and restart wicd.

If the above does not work, you could try [https://bbs.archlinux.org/viewtopic.php?pid=1268721](https://bbs.archlinux.org/viewtopic.php?pid=1268721)

### Problems after package update

Sometimes the wicd client fails to load after a package update due to D-Bus errors.

A solution is to remove the config files in the `/etc/wicd/` directory.

```
# systemctl stop wicd
# rm /etc/wicd/*.conf
# systemctl start wicd

```

### Note about graphical sudo programs

If you are receiving an error about wicd failing to find a graphical sudo program, install one of [gksu](https://www.archlinux.org/packages/?name=gksu), [ktsuss](https://aur.archlinux.org/packages/ktsuss/), or [kdebase-runtime](https://www.archlinux.org/packages/?name=kdebase-runtime), then use the relative command:

```
$ ktsuss wicd-client -n

```

```
$ gksudo wicd-client -n

```

```
$ kdesu wicd-client -n

```

### Eduroam

See [WPA2 Enterprise#Wicd](/index.php/WPA2_Enterprise#Wicd "WPA2 Enterprise").

### Two instances of wicd-client (and possibly two icons in tray)

See the note in [#Running Wicd](#Running_Wicd) about the autostart file in `/etc/xdg/autostart` and the forum post and bug report provided in [#External Links](#External_Links). Essentially, if `/etc/xdg/autostart/wicd-tray.desktop` exists, remove it. You only need the `wicd` service enabled in systemd.

### Bad password using PEAP with TKIP/MS-CHAPv2

The connection template PEAP with TKIP/MS-CHAPv2 requires the user to enter the path to a CA certificate besides entering username and password. However this can cause troubles resulting in an error message of a bad password [[1]](https://bbs.archlinux.org/viewtopic.php?pid=990385). A possible solution is the usage of PEAP with GTC instead of TKIP/MS-CHAPv2 which does not require one to enter the path of the CA cert.

### Wicd skips obtaining IP address on wlp

This can be caused by dhcpcd running alongside wicd as systemd service. A solution would be to stop/disable **dhcpcd**.

### dhcpcd not running

Normally it should not be required, nor recommended to run the dhcpcd service next to wicd. However, if you encounter the error message that dhcpcd is not running, then you can try [starting](/index.php/Start "Start") the `dhcpcd` systemd unit and see if you encounter any incompatibilities when using both services at the same time.

Alternatively, as a workaround you might consider switching to [dhclient](https://www.archlinux.org/packages/?name=dhclient) in the Wicd settings.

**Note:** If you get *send_packet: Network is unreachable* errors, then try increasing the timeout in /usr/share/dhclient/dhclient.conf.

## See also

*   [Forum post](https://bbs.archlinux.org/viewtopic.php?id=114803) about two instances of wicd-client and `/etc/xdg/autostart`
*   [Bug report mentioning /etc/xdg/autostart and wicd-client behavior](https://bugs.archlinux.org/task/22423)