[NetworkManager](http://projects.gnome.org/NetworkManager/) - это программа, облегчающая определение и конфигурацию средств для автоматического подключения к сети. Функционал NetworkManager полезен как для беспроводных, так и проводных сетей. Для подключения к беспроводным сетям, NetworkManager отдаёт предпочтение ранее известным сетям и обеспечивает переключение на наиболее стабильную сеть, но при их наличии, отдаёт предпочтение проводным сетям. Также поддерживаются подключения с использованием модема, и некоторые типы VPN. NetworkManager был разработан Red Hat, и в настоящее время содержится проектом [GNOME](/index.php/GNOME "GNOME").

**Важно:** По умолчанию все пароли хранятся в чистом виде. См. [шифрование паролей к wifi](#.D0.A8.D0.B8.D1.84.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B0.D1.80.D0.BE.D0.BB.D0.B5.D0.B9_.D0.BA_wifi).

## Contents

*   [1 Базовая установка](#.D0.91.D0.B0.D0.B7.D0.BE.D0.B2.D0.B0.D1.8F_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Поддержка VPN](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0_VPN)
*   [2 Графические интерфейсы](#.D0.93.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.D1.8B)
    *   [2.1 GNOME](#GNOME)
    *   [2.2 KDE](#KDE)
    *   [2.3 Xfce](#Xfce)
    *   [2.4 Openbox](#Openbox)
    *   [2.5 Other desktops and window managers](#Other_desktops_and_window_managers)
    *   [2.6 Управление через командную строку](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D0.BD.D1.83.D1.8E_.D1.81.D1.82.D1.80.D0.BE.D0.BA.D1.83)
        *   [2.6.1 nmcli examples](#nmcli_examples)
        *   [2.6.2 nmcli-dmenu](#nmcli-dmenu)
*   [3 Configuration](#Configuration)
    *   [3.1 Автозапуск NetworkManager](#.D0.90.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_NetworkManager)
    *   [3.2 Enable NetworkManager Wait Online](#Enable_NetworkManager_Wait_Online)
    *   [3.3 Настройка разрешений PolicyKit](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.80.D0.B0.D0.B7.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B9_PolicyKit)
    *   [3.4 Network services with NetworkManager dispatcher](#Network_services_with_NetworkManager_dispatcher)
        *   [3.4.1 Avoiding the three seconds timeout](#Avoiding_the_three_seconds_timeout)
        *   [3.4.2 Start OpenNTPD](#Start_OpenNTPD)
        *   [3.4.3 Mount remote folder with sshfs](#Mount_remote_folder_with_sshfs)
        *   [3.4.4 Use dispatcher to connect to a VPN after a network-connection is established](#Use_dispatcher_to_connect_to_a_VPN_after_a_network-connection_is_established)
    *   [3.5 Proxy settings](#Proxy_settings)
    *   [3.6 Disable NetworkManager](#Disable_NetworkManager)
*   [4 Testing](#Testing)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 No prompt for password of secured wifi networks](#No_prompt_for_password_of_secured_wifi_networks)
    *   [5.2 No traffic via PPTP tunnel](#No_traffic_via_PPTP_tunnel)
    *   [5.3 Network management disabled](#Network_management_disabled)
    *   [5.4 Customizing resolv.conf](#Customizing_resolv.conf)
    *   [5.5 DHCP problems with dhclient](#DHCP_problems_with_dhclient)
    *   [5.6 Hostname problems](#Hostname_problems)
        *   [5.6.1 Option 2: Configure dhclient to push the hostname to the DHCP server](#Option_2:_Configure_dhclient_to_push_the_hostname_to_the_DHCP_server)
        *   [5.6.2 Option 3: Configure NetworkManager to use dhcpcd](#Option_3:_Configure_NetworkManager_to_use_dhcpcd)
    *   [5.7 Missing default route](#Missing_default_route)
    *   [5.8 3G modem not detected](#3G_modem_not_detected)
    *   [5.9 Switching off WLAN on laptops](#Switching_off_WLAN_on_laptops)
    *   [5.10 Static IP settings revert to DHCP](#Static_IP_settings_revert_to_DHCP)
    *   [5.11 Cannot edit connections as normal user](#Cannot_edit_connections_as_normal_user)
    *   [5.12 Forget hidden wireless network](#Forget_hidden_wireless_network)
    *   [5.13 VPN not working in Gnome](#VPN_not_working_in_Gnome)
    *   [5.14 Unable to connect to visible european wireless networks](#Unable_to_connect_to_visible_european_wireless_networks)
    *   [5.15 Automatically connect to VPN not working on boot](#Automatically_connect_to_VPN_not_working_on_boot)
    *   [5.16 NetworkManager dispatcher does not run using systemd](#NetworkManager_dispatcher_does_not_run_using_systemd)
*   [6 Tips and tricks](#Tips_and_tricks)
    *   [6.1 Шифрование паролей к wifi](#.D0.A8.D0.B8.D1.84.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B0.D1.80.D0.BE.D0.BB.D0.B5.D0.B9_.D0.BA_wifi)
    *   [6.2 Sharing internet connection over Wi-Fi](#Sharing_internet_connection_over_Wi-Fi)
        *   [6.2.1 Ad-hoc](#Ad-hoc)
        *   [6.2.2 Real AP](#Real_AP)
    *   [6.3 Checking if networking is up inside a cron job or script](#Checking_if_networking_is_up_inside_a_cron_job_or_script)
    *   [6.4 Automatically unlock keyring after login](#Automatically_unlock_keyring_after_login)
        *   [6.4.1 GNOME](#GNOME_2)
        *   [6.4.2 KDE](#KDE_2)
        *   [6.4.3 SLiM login manager](#SLiM_login_manager)
    *   [6.5 KDE and OpenConnect VPN with password authentication](#KDE_and_OpenConnect_VPN_with_password_authentication)
    *   [6.6 Ignore specific devices](#Ignore_specific_devices)
    *   [6.7 Connect faster](#Connect_faster)
        *   [6.7.1 Disabling IPv6](#Disabling_IPv6)
        *   [6.7.2 Use OpenDNS servers](#Use_OpenDNS_servers)
    *   [6.8 Enable DNS Caching](#Enable_DNS_Caching)

## Базовая установка

NetworkManager устанавливается пакетом [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)")

**Примечание:** Убедитесь что не запущены никакие другие сервисы, претендующие на настройку сети, т.к. это вызовет их конфликт. Вы можете отобразить список запущенных сервисов командой `systemctl --type=service`, и затем [остановить](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)") нужные.

### Поддержка VPN

Поддержка VPN программой NetworkManager осуществляется системой плагинов. Для получения поддержки VPN, установите один из следующих пакетов из [официальных репозиторий](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"):

*   [networkmanager-openconnect](https://www.archlinux.org/packages/?name=networkmanager-openconnect)
*   [networkmanager-openvpn](https://www.archlinux.org/packages/?name=networkmanager-openvpn)
*   [networkmanager-pptp](https://www.archlinux.org/packages/?name=networkmanager-pptp)
*   [networkmanager-vpnc](https://www.archlinux.org/packages/?name=networkmanager-vpnc)

## Графические интерфейсы

Большинство пользователей используют апплеты для удобного доступа к функционалу NetworkManager. Как правило, апплеты располагаются в системном трее и позволяют переключение сетей и конфигурацию NetworkManager. Несколько различных апплетов существует для различных сред рабочего стола.

### GNOME

Для GNOME используется [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) - лёгкий универсальный апплет.

Для сохранения логинов/паролей к беспроводным сетям и применения глобальных настроек (доступных всем пользователям) необходимо установить [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring").

### KDE

The Plasma-nm front-end is a Plasma widget available in the official repositories as package [kdeplasma-applets-plasma-nm](https://www.archlinux.org/packages/?name=kdeplasma-applets-plasma-nm). The older KNetworkManager front-end Plasma widget is also available as package [kdeplasma-applets-networkmanagement](https://aur.archlinux.org/packages/kdeplasma-applets-networkmanagement/) from the aur.

If you have both the Plasma widget and `nm-applet` installed and do not want to start `nm-applet` when using KDE, add the following line to `/etc/xdg/autostart/nm-applet.desktop`:

```
NotShowIn=KDE

```

See [Userbase page](http://userbase.kde.org/NetworkManagement) for more info.

### Xfce

[network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) will work fine in Xfce, but in order to see notifications, *including error messages*, `nm-applet` needs an implementation of the Freedesktop desktop notifications specification (see the [Galapago Project](http://www.galago-project.org/specs/notification/0.9/index.html)) to display them. To enable notifications install [xfce4-notifyd](https://www.archlinux.org/packages/?name=xfce4-notifyd), a package that provides an implementation for the specification.

Without such a notification daemon, `nm-applet` outputs the following errors to stdout/stderr:

```
(nm-applet:24209): libnotify-WARNING **: Failed to connect to proxy
** (nm-applet:24209): WARNING **: get_all_cb: couldn't retrieve
system settings properties: (25) Launch helper exited with unknown
return code 1.
** (nm-applet:24209): WARNING **: fetch_connections_done: error
fetching connections: (25) Launch helper exited with unknown return
code 1.
** (nm-applet:24209): WARNING **: Failed to register as an agent:
(25) Launch helper exited with unknown return code 1

```

`nm-applet` will still work fine, though, but without notifications.

If nm-applet is not prompting for a password when connecting to new wifi networks, and is just disconnecting immediately, you probably need to install [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring).

### Openbox

Для правильной работы в среде Openbox, помимо апплета требуется демон нотификаций [xfce4-notifyd](https://www.archlinux.org/packages/?name=xfce4-notifyd).

Для сохранения логинов/паролей к беспроводным сетям и применения глобальных настроек (доступных всем пользователям) необходимо установить [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring").

`nm-applet` installs the autostart file at `/etc/xdg/autostart/nm-applet.desktop`. If you have issues with it (e.g. `nm-applet` is started twice or is not started at all), see [Openbox#autostart](/index.php/Openbox#autostart "Openbox") or [[1]](https://bbs.archlinux.org/viewtopic.php?pid=993738) for solution.

### Other desktops and window managers

In all other scenarios it is recommended to use the GNOME applet. You will also need to be sure that the [gnome-icon-theme](https://www.archlinux.org/packages/?name=gnome-icon-theme) package is installed to be able to display the applet.

To store connection secrets install and configure [gnome-keyring](/index.php/Gnome-keyring "Gnome-keyring").

In order to run `nm-applet` without a systray, you can use [trayer](https://www.archlinux.org/packages/?name=trayer) or [stalonetray](https://www.archlinux.org/packages/?name=stalonetray). For example, you can add a script like this one in your path:

 `nmgui` 
```
#!/bin/sh
nm-applet    > /dev/null 2>/dev/null &
stalonetray  > /dev/null 2>/dev/null
killall nm-applet

```

When you close the stalonetray window, it closes `nm-applet` too, so no extra memory is used once you are done with network settings.

### Управление через командную строку

Для управления через командную строку [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) начиная с версии 0.8.1 содержит пакет [nmcli](http://manpages.ubuntu.com/manpages/maverick/man1/nmcli.1.html).

#### nmcli examples

Для подключения к беспроводной сети:

```
nmcli dev wifi connect <name> password <password>

```

Для подключения к беспроводной сети через интерфейс wlan1 :

```
nmcli dev wifi connect <name> password <password> iface wlan1 [profile name]

```

Для отключения интерфейса:

```
nmcli dev disconnect iface eth0

```

To reconnect an interface marked as disconnected

```
nmcli con up uuid <uuid>

```

To get a list of UUIDs

```
nmcli con list

```

To see a list of network devices and their state

```
nmcli dev

```

#### nmcli-dmenu

Alternatively there is [nmcli-dmenu](https://github.com/firecat53/nmcli-dmenu) which is a small script to manage NetworkManager connections with dmenu instead of nm-applet. It provides all essential features such as connect to existing NetworkManager wifi or wired connections, connect to new wifi connections, requests passphrase if required, connect to _existing_ VPN connections, enable/disable networking, launch nm-connection-editor GUI.

## Configuration

NetworkManager will require some additional steps to be able run properly. Make sure you have configured `/etc/hosts` as described [Network configuration (Русский)#Установка имени узла](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B8.D0.BC.D0.B5.D0.BD.D0.B8_.D1.83.D0.B7.D0.BB.D0.B0 "Network configuration (Русский)").

### Автозапуск NetworkManager

NetworkManager запускается ([Использование юнитов](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)")) с помощью `NetworkManager.service`. После запуска демона NetworkManager, он автоматически подключатется к любой доступной сети, которые уже были настроены. Для любых "пользовательских соединений" или не настроенных соединений нужен *nmcli* или апплет для настройки и подключения.

**Note:** NetworkManager возможно будет печатать бессмысленные предупреждения ([FS#34971](https://bugs.archlinux.org/task/34971)) в ваш системный лог, когда [NetworkManager-dispatcher.service](/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher "NetworkManager") и [ModemManager.service](https://www.archlinux.org/packages/?name=modemmanager) не запущены. Чтобы сохранить журнал в чистоте и убрать эти сообщения, запустите оба сервиса, даже если они не требуются вашей среде.

### Enable NetworkManager Wait Online

If you have services which fail if they are started before the network is up, you have to use `NetworkManager-wait-online.service` in addition to `NetworkManager.service`. This is however hardly ever necessary since most network daemons start up fine, even if the network has not been configured yet.

In some cases the service will still fail to start sucessfully on boot due to the timeout setting in `/usr/lib/systemd/system/NetworkManager-wait-online.service` being too short. Change the default timeout from 30 to a higher value.

### Настройка разрешений PolicyKit

Смотрите [General troubleshooting (Русский)#Разрешения сессии](/index.php/General_troubleshooting_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A0.D0.B0.D0.B7.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D1.8F_.D1.81.D0.B5.D1.81.D1.81.D0.B8.D0.B8 "General troubleshooting (Русский)") для создания рабочей сессии.

With a working session, you have several options for granting the necessary privileges to NetworkManager:

*Option 1.* Run a [PolicyKit](/index.php/PolicyKit "PolicyKit") authentication agent when you log in, such as `/usr/lib/polkit-gnome/polkit-gnome-authentication-agent-1` (part of [polkit-gnome](https://www.archlinux.org/packages/?name=polkit-gnome)). You will be prompted for your password whenever you add or remove a network connection.

*Option 2.* Add yourself to the `wheel` group. You will not have to enter your password, but your user account may be granted other permissions as well, such as the ability to use [sudo (Русский)](/index.php/Sudo_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Sudo (Русский)") without entering the root password.

*Option 3.* Add yourself to the `network` group and create the following file:

 `/etc/polkit-1/rules.d/50-org.freedesktop.NetworkManager.rules` 
```
polkit.addRule(function(action, subject) {
  if (action.id.indexOf("org.freedesktop.NetworkManager.") == 0 && subject.isInGroup("network")) {
    return polkit.Result.YES;
  }
});

```

All users in the `network` group will be able to add and remove networks without a password. This will not work under systemd if you do not have an active session with [systemd-logind](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)").

### Network services with NetworkManager dispatcher

There are quite a few network services that you will not want running until NetworkManager brings up an interface. Good examples are [NTPd](/index.php/NTPd "NTPd") and network filesystem mounts of various types (e.g. **netfs**). NetworkManager has the ability to start these services when you connect to a network and stop them when you disconnect. To activate the feature you need to [start](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)") the `NetworkManager-dispatcher.service`.

Once the feature is active, scripts can be added to the `/etc/NetworkManager/dispatcher.d` directory. These scripts will need to have executable, user permissions. For security, it is good practice to make them owned by **root:root** and writable only by the owner.

The scripts will be run in alphabetical order at connection time, and in reverse alphabetical order at disconnect time. They receive two arguments: the name of the interface (e.g. *eth0*) and the status (*up* or *down* for interfaces and *vpn-up* or *vpn-down* for vpn connections). To ensure what order they come up in, it is common to use numerical characters prior to the name of the script (e.g. `10_portmap` or `30_netfs` (which ensures that the portmapper is up before NFS mounts are attempted).

**Warning:**

*   For security reason. You should disable write access for group and other. For example use 755 mask. In other case it can refuse to execute script, with error message "nm-dispatcher.action: Script could not be executed: writable by group or other, or set-UID." in `/var/log/messages.log`.
*   If you connect to foreign or public networks, be aware of what services you are starting and what servers you expect to be available for them to connect to. You could make a security hole by starting the wrong services while connected to a public network.

#### Avoiding the three seconds timeout

If the above is working, then this section is not relevant. However, there is a general problem related to running dispatcher scripts which take longer than 3 seconds to be executed. NetworkManager uses an internal timeout of 3 seconds (see the [Bugtracker](https://bugzilla.redhat.com/show_bug.cgi?id=982734) for more information) and automatically kills scripts that take longer than 3 seconds to finish. In this case, the dispatcher service file, located in `/usr/lib/systemd/system/NetworkManager-dispatcher.service`, has to be modified to remain active after exit. Create the service file `/etc/systemd/system/NetworkManager-dispatcher.service` with the following content:

```
.include /usr/lib/systemd/system/NetworkManager-dispatcher.service
[Service]
RemainAfterExit=yes

```

Now enable the modified `NetworkManager-dispatcher` script.

#### Start OpenNTPD

Install the [networkmanager-dispatcher-openntpd](https://www.archlinux.org/packages/?name=networkmanager-dispatcher-openntpd) package.

#### Mount remote folder with sshfs

As the script is run in a very restrictive environment, you have to export `SSH_AUTH_SOCK` in order to connect to your SSH agent. There are different ways to accomplish this, see [this link](https://bbs.archlinux.org/viewtopic.php?pid=1042030#p1042030) for more information. The example below works with [gnome-keyring](/index.php/Gnome-keyring "Gnome-keyring"), and will ask you for the password if not unlocked already. In case NetworkManager connects automatically on login, it is likely gnome-keyring has not yet started and the export will fail (hence the sleep). The `UUID` to match can be found with the command `nmcli con status` or `nmcli con list`.

```
#!/bin/sh
USER='username'
REMOTE='user@host:/remote/path'
LOCAL='/local/path'

interface=$1 status=$2
if [ "$CONNECTION_UUID" = "*uuid*" ]; then
  case $status in
    up)
      export SSH_AUTH_SOCK=$(find /tmp -maxdepth 1 -type s -user "$USER" -name 'ssh')
      su "$USER" -c "sshfs $REMOTE $LOCAL"
      ;;
    down)
      fusermount -u "$LOCAL"
      ;;
  esac
fi

```

#### Use dispatcher to connect to a VPN after a network-connection is established

In this example we want to connect automatically to a previously defined VPN connection after connecting to a specific Wi-Fi network. First thing to do is to create the dispatcher script that defines what to do after we are connected to the network.

	1\. Create the dispatcher script:

 `/etc/NetworkManager/dispatcher.d/vpn-up` 
```
#!/bin/sh
VPN_NAME="name of VPN connection defined in NetworkManager"
ESSID="wifi network ESSID (not connection name)"

interface=$1 status=$2
case $status in
  up|vpn-down)
    if iwgetid | grep -qs ":\"$ESSID\""; then
      nmcli con up id "$VPN_NAME"
    fi
    ;;
  down)
    if iwgetid | grep -qs ":\"$ESSID\""; then
      if nmcli con status id "$VPN_NAME" | grep -qs activated; then
        nmcli con down id "$VPN_NAME"
      fi
    fi
    ;;
esac

```

Remember to make it executable with `chmod +x` and to make the VPN connection available to all users.

Trying to connect using this setup will fail and NetworkManager will complain about 'no valid VPN secrets', because of [the way VPN secrets are stored](http://projects.gnome.org/NetworkManager/developers/migrating-to-09/secrets-flags.html) which brings us to step 2:

	2\. Edit your VPN connection configuration file to make NetworkManager store the secrets by itself rather than inside a keyring [that will be inaccessible for root](https://bugzilla.redhat.com/show_bug.cgi?id=710552): open up `/etc/NetworkManager/system-connections/*name of your VPN connection*` and change the `password-flags` and `secret-flags` from `1` to `0`.

Alternatively put the password directly in the configuration file adding the section `vpn-secrets`:

```
 [vpn]
 ....
 password-flags=0

 [vpn-secrets]
 password=your_password

```

**Note:** It may now be necessary to re-open the NetworkManager connection editor and re-enter the VPN passwords/secrets.

### Proxy settings

NetworkManager does not directly handle proxy settings, but if you are using GNOME, you could use [proxydriver](http://marin.jb.free.fr/proxydriver/) wich handles proxy settings using NetworkManager's informations. You can find the package for [proxydriver](https://aur.archlinux.org/packages/proxydriver/) in the [AUR](/index.php/AUR "AUR").

In order for proxydriver to be able to change the proxy settings, you would need to execute this command, as part of the GNOME startup process (System -> Preferences -> Startup Applications):

```
xhost +si:localuser:your_username

```

See: [Proxy settings](/index.php/Proxy_settings "Proxy settings")

### Disable NetworkManager

It might not be obvious, but the service automatically starts through dbus, to completely disable it you can mask the service with systemctl :

```
systemctl mask NetworkManager
systemctl mask NetworkManager-dispatcher

```

## Testing

NetworkManager applets are designed to load upon login so no further configuration should be necessary for most users. If you have already disabled your previous network settings and disconnected from your network, you can now test if NetworkManager will work. The first step is to [start](/index.php/Daemon "Daemon") the *networkmanager* daemon.

Some applets will provide you with a `.desktop` file so that the NetworkManager applet can be loaded through the application menu. If it does not, you are going to either have to discover the command to use or logout and login again to start the applet. Once the applet is started, it will likely begin polling network connections with for auto-configuration with a DHCP server.

To start the GNOME applet in non-xdg-compliant window managers like [Awesome](/index.php/Awesome "Awesome"):

```
nm-applet --sm-disable &

```

For static IPs you will have to configure NetworkManager to understand them. The process usually involves right-clicking the applet and selecting something like 'Edit Connections'.

## Troubleshooting

Some fixes to common problems.

### No prompt for password of secured wifi networks

When trying to connect to a secured wifi network, no prompt for a password is shown and no connection is established. This happens when no keyring package is installed. An easy solution is to install[gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring). If you want the passwords to be stored in encrypted form, follow [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring") to set up the gnome-keyring-daemon.

### No traffic via PPTP tunnel

PPTP connection logins successfully, you see ppp0 interface with correct VPN IP, but you cannot even ping remote IP. It is due to lack of MPPE (Microsoft Point-to-Point Encryption) support in stock Arch pppd. It is recommended to first try with the stock Arch [ppp](https://www.archlinux.org/packages/?name=ppp) as it may work as intended.

To solve the problem it should be sufficient to install [ppp-mppe](https://aur.archlinux.org/packages/ppp-mppe/).

WPA2-Enterprise wireless networks demanding MSCHAPv2 type-2 authentication with PEAP sometimes require ppp-mppe rather than the stock ppp package. [netctl](/index.php/Netctl_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Netctl (Русский)") seems to work out of the box without ppp-mppe, however. In either case, usage of MSCHAPv2 is discouraged as it is highly vulnerable, although using another method is usually not an option. See this [blog post](https://www.cloudcracker.com/blog/2012/07/29/cracking-ms-chap-v2/).

### Network management disabled

Sometimes when NetworkManager shuts down but the pid (state) file does not get removed and you will get a 'Network management disabled' message. If this happens, you'll have to remove it manually:

```
# rm /var/lib/NetworkManager/NetworkManager.state

```

If this happens upon reboot, you can add an action to your `/etc/rc.local` to have it removed upon bootup:

```
nmpid=/var/lib/NetworkManager/NetworkManager.state
[ -f $nmpid ] && rm $nmpid
```

### Customizing resolv.conf

See the main page: [resolv.conf](/index.php/Resolv.conf "Resolv.conf"). Also make sure that NetworkManager uses [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) and not [dhclient](https://www.archlinux.org/packages/?name=dhclient). If you want to use [dhclient](https://www.archlinux.org/packages/?name=dhclient), you may try the [networkmanager-dispatch-resolv](https://aur.archlinux.org/packages/networkmanager-dispatch-resolv/) package.

### DHCP problems with dhclient

If you have problems with getting an IP via DHCP, try to add the following to your `/etc/dhclient.conf`:

```
 interface "eth0" {
   send dhcp-client-identifier 01:aa:bb:cc:dd:ee:ff;
 }

```

Where `aa:bb:cc:dd:ee:ff` is the MAC address of this NIC. The MAC address can be found using the `ip link show eth0` command from the [iproute2](https://www.archlinux.org/packages/?name=iproute2) package.

### Hostname problems

It depends on the NetworkManager plugins used, whether the hostname is forwarded to a router on connect. The generic "keyfile" plugin does not forward the hostname in default configuration. To make it forward the hostname, add the following to

 `/etc/NetworkManager/NetworkManager.conf` 
```
[keyfile]
hostname=*your_hostname*
```

The options under `[keyfile]` will be applied to network connections in the default `/etc/NetworkManager/system-connections` path.

Another option is to configure the DHCP client, which NetworkManager starts automatically, to forward it. NetworkManager utilizes [dhclient](https://www.archlinux.org/packages/?name=dhclient) in default and falls back to [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd), if the former is not installed. To make *dhclient* forward the hostname requires to set a non-default option, *dhcpcd* forwards the hostname by default.

First, check which DHCP client is used (*dhclient* in this example):

 `# journalctl -b | egrep "dhclient|dhcpcd"` 
```
...
Nov 17 21:03:20 zenbook dhclient[2949]: Nov 17 21:03:20 zenbook dhclient[2949]: Bound to *:546
Nov 17 21:03:20 zenbook dhclient[2949]: Listening on Socket/wlan0
Nov 17 21:03:20 zenbook dhclient[2949]: Sending on   Socket/wlan0
Nov 17 21:03:20 zenbook dhclient[2949]: XMT: Info-Request on wlan0, interval 1020ms.
Nov 17 21:03:20 zenbook dhclient[2949]: RCV: Reply message on wlan0 from fe80::126f:3fff:fe0c:2dc.

```

#### Option 2: Configure dhclient to push the hostname to the DHCP server

Copy the example configuration file:

```
# cp /usr/share/dhclient/dhclient.conf.example /etc/dhclient.conf

```

Take a look at the file - there will only really be one line we want to keep and dhclient will use it's defaults (as it has been using if you didn't have this file) for the other options. This is the important line:

 `/etc/dhclient.conf`  `send host-name = pick-first-value(gethostname(), "ISC-dhclient");` 

Force an IP address renewal by your favorite means, and you should now see your hostname on your DHCP server.

#### Option 3: Configure NetworkManager to use dhcpcd

[Install](/index.php/Pacman "Pacman") [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) and tell NetworkManager about it:

 `/etc/NetworkManager/NetworkManager.conf`  `dhcp=dhcpcd` 

Then [restart](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)") `NetworkManager.service`.

### Missing default route

On at least one KDE4 system, no default route was created when establishing wireless connections with NetworkManager. Changing the route settings of the wireless connection to remove the default selection "Use only for resources on this connection" solved the issue.

### 3G modem not detected

See [USB 3G Modem#Network Manager](/index.php/USB_3G_Modem#Network_Manager "USB 3G Modem").

### Switching off WLAN on laptops

Sometimes NetworkManager will not work when you disable your Wi-Fi adapter with a switch on your laptop and try to enable it again afterwards. This is often a problem with `rfkill`. Install [rfkill](https://www.archlinux.org/packages/?name=rfkill) from the [official repositories](/index.php/Official_repositories "Official repositories") and use

```
$ watch -n1 rfkill list all

```

to check if the driver notifies `rfkill` about the wireless adapter's status. If one identifier stays blocked after you switch on the adapter you could try to manually unblock it with (where X is the number of the identifier provided by the above output):

```
# rfkill event unblock X

```

### Static IP settings revert to DHCP

Due to an unresolved bug, when changing default connections to static IP, `nm-applet` may not properly store the configuration change, and will revert to automatic DHCP.

To work around this issue you have to edit the default connection (e.g. "Auto eth0") in `nm-applet`, change the connection name (e.g. "my eth0"), uncheck the "Available to all users" checkbox, change your static IP settings as desired, and click **Apply**. This will save a new connection with the given name.

Next, you will want to make the default connection not connect automatically. To do so, run `nm-connection-editor` (*not* as root). In the connection editor, edit the default connection (eg "Auto eth0") and uncheck "Connect automatically". Click **Apply** and close the connection editor.

### Cannot edit connections as normal user

See [#Set_up_PolicyKit_permissions](#Set_up_PolicyKit_permissions).

### Forget hidden wireless network

Since hidden network are not displayed in the selection list of the Wireless view, they cannot be forgotten (removed) with the GUI. You can delete one with the following command:

```
# rm /etc/NetworkManager/system-connections/[SSID]

```

This works for any other connection.

### VPN not working in Gnome

When setting up openconnect or vpnc connections in NetworkManager while using Gnome, you'll sometimes never see the dialog box pop up and the following error appears in /var/log/errors.log:

```
localhost NetworkManager[399]: <error> [1361719690.10506] [nm-vpn-connection.c:1405] get_secrets_cb(): Failed to request VPN secrets #3: (6) No agents were available for this request.

```

This is caused by the Gnome NM Applet expecting dialog scripts to be at /usr/lib/gnome-shell, when NetworkManager's packages put them in /usr/lib/networkmanager. As a "temporary" fix (this bug has been around for a while now), make the following symlink(s):

```
# For OpenConnect
ln -s /usr/lib/networkmanager/nm-openconnect-auth-dialog /usr/lib/gnome-shell/ 

```

```
# For VPNC (i.e. Cisco VPN)
ln -s /usr/lib/networkmanager/nm-vpnc-auth-dialog /usr/lib/gnome-shell/

```

This may need to be done for any other NM VPN plugins as well, but these are the two most common.

### Unable to connect to visible european wireless networks

Wlan chips are shipped with a default regulatory domain. If your AccessPoint doesn't operate within these limitations, you will not be able to connect to the network. Fixing this is easy:

*   Install [crda](https://www.archlinux.org/packages/?name=crda) with pacman, see [Wireless network configuration#Regulatory_domain](/index.php/Wireless_network_configuration#Regulatory_domain "Wireless network configuration")
*   Uncomment the correct Country Code in '/etc/conf.d/wireless-regdom'
*   reboot the system, because the setting is only read on boot.

### Automatically connect to VPN not working on boot

The problem seems to be with the keyring as mentioned in the dispatcher section. You don't need to use the dispatcher to auto-connect. The solution is to keep the password to your VPN in plaintext.

Edit `/etc/NetworkManager/system-connections/VPN_NAME`:

```
 [vpn]
 ....
 password-flags=0

 [vpn-secrets]
 password=your_password

```

### NetworkManager dispatcher does not run using systemd

Check your log with the command `journalctl -b -u NetworkManager`, search for the following line:

```
 <warn> Dispatcher failed: (32) Unit dbus-org.freedesktop.nm-dispatcher.service failed to load: No such file or directory.

```

if this line present, enable the dbus unit by running:

```
 systemctl enable NetworkManager-dispatcher.service

```

## Tips and tricks

### Шифрование паролей к wifi

By default NetworkManager stores passwords in clear text in the connection files at `/etc/NetworkManager/system-connections/`. To print the stored passwords, use the following command:

```
# grep -H '^psk=' /etc/NetworkManager/system-connections/*

```

It is preferable to save the passwords in encrypted form instead of clear text. This can be achieved by storing passwords in a keyring which NetworkManager then queries for the passwords. A suggested keyring daemon is [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring"). The keyring daemon has to be started and the keyring needs to be unlocked for the following to work.

Furthermore NetworkManager needs to be configured like so: Right-click the nm-applet, go to `Edit connections`, select a network connection, click `edit`, select the `General` tab and untick `All users may connect to this network`. If the option is ticked, the passwords will still be stored in clear text, even if a keyring daemon is running.

### Sharing internet connection over Wi-Fi

You can share your internet connection (e.g.: 3G or wired) with a few clicks using nm. You will need a supported Wi-Fi card (Cards based on Atheros AR9xx or at least AR5xx are probably best choice)

#### Ad-hoc

*   [Install](/index.php/Pacman "Pacman") the [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) package to be able to actually share the connection.
*   Custom dnsmasq.conf may interfere with nm (not sure about this, but i think so).
*   Click on nm-applet -> Create new wireless network.
*   Follow wizard (if using WEP be sure to use 5 or 13 character long password, different lengths will fail).
*   Settings will remain stored for the next time you need it.

#### Real AP

Support of infrastructure mode (which is needed by Android phones as they intentionally do not support ad-hoc) is supported by NetworkManager as of late 2012.

See: [http://fedoraproject.org/wiki/Features/RealHotspot](http://fedoraproject.org/wiki/Features/RealHotspot)

### Checking if networking is up inside a cron job or script

Some cron jobs require networking to be up to succeed. You may wish to avoid running these jobs when the network is down. To accomplish this, add an **if** test for networking that queries NetworkManager's `nm-tool` and checks the state of networking. The test shown here succeeds if any interface is up, and fails if they are all down. This is convenient for laptops that might be hardwired, might be on wireless, or might be off the network.

```
if [ $(nm-tool|grep State|cut -f2 -d' ') == "connected" ]; then
    #Whatever you want to do if the network is online
else
    #Whatever you want to do if the network is offline - note, this and the else above are optional
fi

```

This useful for a `cron.hourly` script that runs `fpupdate` for the F-Prot virus scanner signature update, as an example. Another way it might be useful, with a little modification, is to differentiate between networks using various parts of the output from `nm-tool`; for example, since the active wireless network is denoted with an asterisk, you could grep for the network name and then grep for a literal asterisk.

### Automatically unlock keyring after login

#### GNOME

1.  Right click on the `nm-applet` icon in your panel and select Edit Connections and open the Wireless tab
2.  Select the connection you want to work with and click the Edit button
3.  Check the boxes “Connect Automatically” and “Available to all users”

Log out and log back in to complete.

**Note:** The following method is dated and known not to work on at least one machine!

*   In `/etc/pam.d/gdm` (or your corresponding daemon in `/etc/pam.d`), add these lines at the end of the "auth" and "session" blocks if they do not exist already:

```
 auth            optional        pam_gnome_keyring.so
 session         optional        pam_gnome_keyring.so  auto_start

```

*   In `/etc/pam.d/passwd`, use this line for the 'password' block:

```
 password    optional    pam_gnome_keyring.so

```

	Next time you log in, you should be asked if you want the password to be unlocked automatically on login.

#### KDE

**Примечание:** See [http://live.gnome.org/GnomeKeyring/Pam](http://live.gnome.org/GnomeKeyring/Pam) for reference, and if you are using [KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)") with [KDM](/index.php/KDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDM (Русский)"), you can use [pam-keyring-tool](https://aur.archlinux.org/packages/pam-keyring-tool/)

Put a script like the following in `~/.kde4/Autostart`:

```
 #!/bin/sh
 echo ПАРОЛЬ | /usr/bin/pam-keyring-tool --unlock --keyring=default -s

```

Similar should work with [openbox](/index.php/Openbox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Openbox (Русский)"), [LXDE](/index.php/LXDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LXDE (Русский)"), etc.

#### SLiM login manager

See [SLiM#SLiM and Gnome Keyring](/index.php/SLiM#SLiM_and_Gnome_Keyring "SLiM").

### KDE and OpenConnect VPN with password authentication

[kdeplasma-applets-plasma-nm](https://www.archlinux.org/packages/?name=kdeplasma-applets-plasma-nm) does not support to configure username and password for OpenConnect VPN connections in its GUI. You have to type both values everytime you connect. [kdeplasma-applets-plasma-nm](https://www.archlinux.org/packages/?name=kdeplasma-applets-plasma-nm) 0.9.3.2-1 and above is however capable of retrieving OpenConnect username and password directly from KWallet.

Open "KDE Wallet Manager" and look up your OpenConnect VPN connection under "Network Management|Maps". Click "Show values" and enter your credentials in key "VpnSecrets" in this form (replace THE_USERNAME and THE_PASSWORD with your actual values):

```
form:main:username%SEP%THE_USERNAME%SEP%form:main:password%SEP%THE_PASSWORD

```

Next time you connect, username and password should appear in the "VPN secrets" dialog box.

### Ignore specific devices

Sometimes it may be desired that NetworkManager ignores specific devices and does not try to configure addresses and routes for them.You can quickly and easily ignore devices by MAC by using the following in `/etc/NetworkManager/NetworkManager.conf` :

```
[keyfile]
unmanaged-devices=mac:00:22:68:1c:59:b1;mac:00:1E:65:30:D1:C4

```

After you have put this in, [restart](/index.php/Daemon "Daemon") NetworkManager, and you should be able to configure interfaces without NetworkManager altering what you have set.

### Connect faster

#### Disabling IPv6

Slow connection or reconnection to the network may be due to superfluous IPv6 queries in NetworkManager. If there is no IPv6 support on the local network, connecting to a network may take longer than normal while NetworkManager tries to establish an IPv6 connection that eventually times out. The solution is to disable IPv6 within NetworkManager which will make network connection faster. This has to be done once for every network you connect to.

*   Right-click on the network status icon.
*   Click on "Edit Connections".
*   Go to the "Wired" or "Wireless" tab, as appropriate.
*   Select the name of the network.
*   Click on "Edit".
*   Go to the "IPv6 Settings" tab.
*   In the "Method" dropdown, choose "Ignore/Disabled".
*   Click on "Save".

#### Use OpenDNS servers

Create `/etc/resolv.conf.opendns` with the [alternative DNS server addresses](/index.php/Resolv.conf#Alternative_DNS_servers "Resolv.conf").

And have the dispatcher replace the discovered DHCP servers with the OpenDNS ones:

 `/etc/NetworkManager/dispatcher.d/dns-servers-opendns` 
```
#!/bin/bash
# Use OpenDNS servers over DHCP discovered servers

cp -f /etc/resolv.conf.opendns /etc/resolv.conf
```

Make the script executable:

```
# chmod +x /etc/NetworkManager/dispatcher.d/dns-servers-opendns

```

### Enable DNS Caching

DNS requests can be sped up by caching previous requests locally for subsequent lookup. NetworkManager has a plugin to enable DNS caching using dnsmasq, but it is not enabled in the default configuration. It is, however, easy to enable using the following instructions.

Start by [installing](/index.php/Pacman "Pacman") [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq). Then, edit `/etc/NetworkManager/NetworkManager.conf` and add the following line under the `[main]` section:

```
dns=dnsmasq

```

Now restart NetworkManager or reboot. NetworkManager will automatically start dnsmasq and add 127.0.0.1 to `/etc/resolv.conf`. The actual DNS servers can be found in `/var/run/NetworkManager/dnsmasq.conf`. You can verify dnsmasq is being used by doing the same DNS lookup twice with dig and verifying the server and query times.