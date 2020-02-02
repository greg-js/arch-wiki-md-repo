[Демон](https://en.wikipedia.org/wiki/ru:%D0%94%D0%B5%D0%BC%D0%BE%D0%BD_(%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B0) - это программа, которая запускается в фоновом режиме, ожидая событий и предлагая какие-то службы для их выполнения. Хорошим примером демона может служить веб-сервер, ожидающий запроса на доставку страницы, или сервер [SSH](/index.php/Secure_Shell_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Secure Shell (Русский)"), ожидающий чьего-нибудь логина. Существуют приложения, действия которых видны, а работа демонов не видна. К ним относятся, например, демон, записывающий системные сообщения в журналы (*syslog*, *metalog*), или демон, держащий время системы точным ([Ntpd](/index.php/Network_Time_Protocol_daemon_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Network Time Protocol daemon (Русский)")), когда ваши вычислительные ресурсы не используются. Для получения дополнительной информации смотрите страницу справочного руководства [daemon(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/daemon.7).

В Arch Linux демонами управляет [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"). Команда [systemctl](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Основы_использования_systemctl "Systemd (Русский)") используется для управления ими в пользовательском интерфейсе. *systemd* читает файлы *.service*, которые содержат информацию о том, как и когда запустить связанный демон. Файлы служб хранятся в каталогах `/{etc,usr/lib,run}/systemd/system`. Для получения дополнительной информации смотрите раздел [systemd (Русский)#Использование юнитов](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Использование_юнитов "Systemd (Русский)").

## Список демонов

Вот список демонов. Обратите внимание, что любой пакет может обеспечить демоном, так что этот список никогда не будет полным. Пожалуйста, не стесняйтесь добавлять недостающие демоны здесь, в алфавитном порядке. Вы можете иметь пакеты, которые включают другие демоны от [AUR](/index.php/AUR "AUR"). Эти файлы, скорее, будут расположены в `/usr/lib/systemd/system/`.

Столбец *Пакет* содержит ссылку на ArchWiki страницу для каждого демона (или ссылку на пакет, если такой страницы не существует). Столбец *initscripts* содержит имя унаследованное скриптом *rc.d* и столбец *systemd* содержит имя файла службы [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"). Обратите внимание, что могут быть демоны, специфичные для либо initscript'ов или Systemd, с соответствующей пустой колонкой. Столбец *Описание* представляет краткое описание, предпочтительно *демона* (не пакета).

| Пакет | initscripts | systemd | Описание |
| [acpid](/index.php/Acpid "Acpid") | acpid | acpid.service | Демон для доставки события управления питанием ACPI с поддержкой NETLink. |
| [alsa](/index.php/Alsa "Alsa") | alsa | *always on* – alsa-store.service, alsa-restore.service | Сохраняет состояние звуковой карты (например, уровень звука) и восстанавливает его при запуске. |
| [at](https://www.archlinux.org/packages/?name=at) | atd | atd.service | Runs jobs queued for later execution. |
| [Autofs](/index.php/Autofs "Autofs") | autofs | autofs.service | Автоматическое монтирование съемных носителей и сетевых шар (shares), когда они вставлены или доступны. |
| [Avahi](/index.php/Avahi "Avahi") | avahi-daemon | avahi-daemon.service | Позволяет программам автоматически находить локальные сетевые службы. |
| avahi-dnsconfd | avahi-dnsconfd.service | Multicast/unicast DNS-SD framework. |
| [Bitlbee](/index.php/Bitlbee "Bitlbee") | bitlbee | bitlbee.service | Выводит мгновенные сообщения (XMPP, MSN, Yahoo!, AIM, ICQ, Twitter) в IRC. |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | bluetooth | bluetooth.service | Bluetooth protocol stack, framework, subsystem. |
| [Chrony](/index.php/Chrony "Chrony") | chrony | chrony.service | Легкий клиент NTP и сервер. |
| [CDemu](/index.php/CDemu "CDemu") | cdemud | cdemu-daemon.service | Эмулятор устройств CD/DVD-ROM. |
| [ClamAV](/index.php/ClamAV "ClamAV") | clamav | clamd.service
freshclamd.service | Антивирус для Unix. |
| [ConnMan](/index.php/ConnMan "ConnMan") | connmand | connman.service | Менеджер беспроводного доступа в сеть интернет |
| [Cpupower](/index.php/Cpupower "Cpupower") | cpupower | cpupower.service | Sets [cpufreq](/index.php/Cpufreq "Cpufreq") governor and other parameters on startup. |
 craftbukkit | *not yet implemented* | Сервер CraftBukkit Minecraft. |
| [Cron](/index.php/Cron "Cron") | crond | cronie.service (if using [cronie](https://www.archlinux.org/packages/?name=cronie)) or dcron.service (if using [dcron](https://aur.archlinux.org/packages/dcron/)) | Daemon to schedule and time events. The daemon name *crond* is used by at least two packages, [cronie](https://www.archlinux.org/packages/?name=cronie) and [dcron](https://aur.archlinux.org/packages/dcron/). |
| [CUPS](/index.php/CUPS "CUPS") | cupsd | org.cups.cupsd.service | Демон системы печати CUPS. |
| [D-Bus](/index.php/D-Bus "D-Bus") | dbus | *always on* – dbus.service | Система шины сообщений Freedesktop.org. |
| [dante](https://www.archlinux.org/packages/?name=dante) | sockd | sockd.service | A circuit-level SOCKS client/server. |
| [Deluge](/index.php/Deluge "Deluge") | deluged | deluged.service | Главный демон кросс-платформенного и полнофункциональноко клиента BitTorrent. |
| deluge-web | deluge-web.service | Демон веб-интерфейса кросс-платформенного и полнофункциональноко клиента BitTorrent. |
| [Dhcpcd](/index.php/Dhcpcd "Dhcpcd") | dhcpcd | dhcpcd@.service | Демон DHCP. |
| [Dovecot](/index.php/Dovecot "Dovecot") | dovecot | dovecot.service | IMAP и POP3 сервер. |
| [Dropbox](/index.php/Dropbox "Dropbox") | dropboxd | dropbox@.service | Cross-platform file synchronisation with version control. |
| [fail2ban](/index.php/Fail2ban "Fail2ban") | fail2ban | fail2ban.service | Fail2ban scans log files and bans IP addresses that show malicious activity. |
| [Fan speed control](/index.php/Fan_speed_control "Fan speed control") | fancontrol | fancontrol.service | Демон контроля вентилятора (часть lm_sensors) |
| [FluidSynth](/index.php/FluidSynth "FluidSynth") | fluidsynth | fluidsynth.service | Software synthesizer. |
 ftpd | ftpd.service | inetutils FTP daemon. |
| [GDM](/index.php/GDM "GDM") | gdm | gdm.service | Экранный менеджер GNOME. |
| [Git](/index.php/Git "Git") | git-daemon | git-daemon.socket | Git daemon. |
| [gpm](/index.php/Console_mouse_support "Console mouse support") | gpm | gpm.service | Console mouse support. |
| [hddtemp](/index.php/Hddtemp "Hddtemp") | hddtemp | hddtemp.service | Hard drive temperature monitor daemon. |
 healthd | healthd.service | A daemon which can be used to alert you in the event of a hardware health monitoring alarm (part of [lm_sensors](/index.php/Lm_sensors "Lm sensors")). |
| [apache](/index.php/Apache "Apache") | httpd | httpd.service | Apache HTTP Server (Web Server). |
 i8kmon | i8kmon.service | Monitor the CPU temperature and fan status on Dell Inspiron laptops. |
 ifplugd | ifplugd@.service | Start/stop network on network cable plugged in/out. |
| [iptables](/index.php/Iptables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Iptables (Русский)") | iptables | iptables.service | Load firewall rules for IPv4. |
| ip6tables | ip6tables.service | Load firewall rules for IPv6. |
 irqbalance | irqbalance.service | Irqbalance is the Linux utility tasked with making sure that interrupts from your hardware devices are handled in as efficient a manner as possible. |
| [KDE](/index.php/KDE "KDE") | kdm | kdm.service | KDE Display Manager. |
| [krb5](https://www.archlinux.org/packages/?name=krb5) | krb5-kadmind | krb5-kadmind.service | Kerberos 5 administration server. |
| krb5-kdc | krb5-kdc.service | Kerberos 5 KDC. |
| krb5-kpropd | krb5-kpropd.service | Kerberos 5 propagation server. |
| [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools") | laptop-mode | laptop-mode.service | Laptop power saving tools. |
| [lighttpd](/index.php/Lighttpd "Lighttpd") | lighttpd | lighttpd.service | Lighttpd HTTP Server (Web Server). |
| [libvirt](/index.php/Libvirt "Libvirt") | libvirt | libvirtd.service | libvirt is a virtualization API and a daemon for managing virtual machines (VMs). |
| [lxdm](/index.php/LXDE "LXDE") | lxdm | lxdm.service | LXDE Display Manager. |
 mdadm | mdadm.service | MD Administration (Linux software RAID). |
| [miniDLNA](/index.php/MiniDLNA "MiniDLNA") | minidlna | minidlna.service | simple DLNA/UPnP media server. |
 ? | ModemManager.service | Makes mobile broadband (3G) modem available to [NetworkManager](/index.php/NetworkManager "NetworkManager"). |
| [mpd](/index.php/Mpd "Mpd") | mpd | mpd.service | Music Player Daemon. |
| [MySQL](/index.php/MySQL "MySQL") | mysqld | mysqld.service | MySQL database server. |
| [MythTV](/index.php/MythTV "MythTV") | mythbackend | mythbackend.service | Back-end for the MythTV digital video recording/home theater software. |
| [BIND](/index.php/BIND "BIND") | named | named.service | The Berkeley Internet Name Daemon (BIND) DNS server. |
| [netctl](/index.php/Netctl "Netctl") | netctl@.service | Manually activate specific profile. |
 netctl-ifplugd@.service | Automatically start/stop netctl profiles depending on whether the cable is plugged in or not. |
 netctl-auto@.service | Automatically start/stop netctl wireless profiles depending on which access points are in range. |
 network | dhcpcd@.service | Brings up the network connections (dynamic Ethernet). |
| [NetworkManager](/index.php/NetworkManager "NetworkManager") | networkmanager | NetworkManager.service
NetworkManager-wait-online.service | NetworkManager daemon, provides configuration and detection for automatic network connections. |
| [Nginx](/index.php/Nginx "Nginx") | nginx | nginx.service | Nginx HTTP Server and IMAP/POP3 proxy server (Web Server). |
 nscd | nscd.service | Name service caching daemon. |
| [ntpd](/index.php/Ntpd "Ntpd") | ntpd | ntpd.service | Network Time Protocol daemon (client and server). |
| [Ntop](/index.php/Ntop "Ntop") | ntop | ntop.service | Ntop is a network traffic probe based on libcap. |
| [OpenNTPD](/index.php/OpenNTPD "OpenNTPD") | openntpd | openntpd.service | Alternative Network Time Protocol daemon (client and server). |
 osspd | osspd.service | OSS Userspace Bridge. |
| [OpenVPN](/index.php/OpenVPN "OpenVPN") | openvpn | openvpn@.service | One for each VPN configuration file saved like `/etc/openvpn/*<profile-name>*.conf` |
| [OSS](/index.php/OSS "OSS") | oss | oss.service | Open Sound System. Alternative to [ALSA](/index.php/ALSA "ALSA"). |
| [Pdnsd](/index.php/Pdnsd "Pdnsd") | pdnsd | pdnsd.service | Proxy DNS server with permanent caching. |
| [php-fpm](https://www.archlinux.org/packages/?name=php-fpm) | php-fpm | php-fpm.service | FastCGI Process Manager for PHP. |
| [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") | postgresql | postgresql.service | PostgreSQL database server. |
| [Postfix](/index.php/Postfix "Postfix") | postfix | postfix.service | Mail server, which is an alternative to using [sendmail](/index.php/Sendmail "Sendmail"). |
| [Postgrey](/index.php/Postgrey "Postgrey") | postgrey | postgrey.service | Greylisting service, used with Postfix |
| [powernowd](/index.php/Powernowd "Powernowd") | powernowd | *not yet implemented* | To adjust speed of CPU depending on system load. |
| [PPTP server](/index.php/PPTP_server "PPTP server") | pptpd | pptpd.service | A Virtual Private Network (VPN) server using the Point-to-Point Tunneling Protocol (PPTP). |
| [pppd](/index.php/Pppd "Pppd") | pppd | ppp@.service | A daemon which implements the Point-to-Point Protocol for dial-up networking. |
| [preload](/index.php/Preload "Preload") | preload | preload.service | Makes applications run faster by prefetching binaries and shared objects. |
| [Prosody](/index.php/Prosody "Prosody") | prosody | prosody.service | XMPP server. |
| [Profile-sync-daemon](/index.php/Profile-sync-daemon "Profile-sync-daemon") | psd | psd.service | Управляет профилем браузера в TMPFS и периодически синхронизируется обратно с вашем физическим диском |
 pure-ftpd | pure-ftpd.servicecups.service | A fast, production quality, standards-compliant FTP server. |
| rfkill | rfkill | rfkill-block@.service
rfkill-unblock@.service | (Un)blocks radio devices. |
| [Rsync](/index.php/Rsync "Rsync") | rsyncd | rsyncd.service | Демон rsync. |
| [Rsyslog](/index.php/Rsyslog "Rsyslog") | rsyslogd | rsyslog.service | Alternative system logger. |
| [samba](/index.php/Samba "Samba") | samba | smbd.service
nmbd.service
winbindd.service | Служба Файлов и принтеров для клиентов Microsoft Windows. |
| [SANE](/index.php/SANE "SANE") | saned | saned@.service | Сетевой демон SANE. |
 saslauthd | saslauthd.service | SASL authentication daemon. |
| [lm_sensors](/index.php/Lm_sensors "Lm sensors") | sensord | sensord.service | Sensor information logging daemon. |
| sensors | lm_sensors.service | Initialize hardware monitoring sensors (load necessary kernel modules). |
| [SLiM](/index.php/SLiM "SLiM") | slim | slim.service | Simple Login Manager. |
| [SMART](/index.php/SMART "SMART") | smartd | smartd.service | Self-Monitoring, Analysis, and Reporting Technology (S.M.A.R.T.) Hard Disk Monitoring. |
| [smbnetfs](/index.php/Samba#smbnetfs "Samba") | smbnetfs | smbnetfs.service | Automatically mount Samba/Microsoft network shares. |
| [snmpd](/index.php/Snmpd "Snmpd") | snmpd | snmpd.service | A suite of applications used to implement SNMP |
 soundmodem | *not yet implemented* | Multiplatform Soundcard Packet Radio Modem |
| [spamassassin](https://www.archlinux.org/packages/?name=spamassassin) | spamd | spamassassin.service | e-mail spam filtering service. |
| [OpenSSH](/index.php/OpenSSH_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "OpenSSH (Русский)") | sshd | sshd.service | Демон OpenSSH (secure shell). |
 stunnel | stunnel.service | Allows encrypting arbitrary TCP connections inside SSL. |
 svnserve | svnserve.service | Subversion server. |
| [syslog-ng](/index.php/Syslog-ng "Syslog-ng") | syslog-ng | syslog-ng.service | System logger next generation. |
| [Timidity](/index.php/Timidity "Timidity") | timidity++ | timidity.service | Software synthesizer for MIDI. |
| [Tinc](/index.php/Tinc "Tinc") | ? | tincd@.service | One for each configuration directory like /etc/tinc/*<vpnname>*/ |
| [Tor](/index.php/Tor_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Tor (Русский)") | tor | tor.service | Onion routing for anonymous communication. |
| [Transmission](/index.php/Transmission "Transmission") | transmissiond | transmission.service | Демон BitTorrent. |
| [Ufw](/index.php/Ufw "Ufw") | ufw | ufw.service | Uncomplicated FireWall. |
| [Urxvtd](/index.php/Rxvt-unicode_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Rxvt-unicode (Русский)") | ? | urxvtd.service | Демон urxvt. |
| [VirtualBox](/index.php/VirtualBox "VirtualBox") | vboxservice | vboxservice.service | VirtualBox Guest Service. |
| [vnStat](/index.php/VnStat "VnStat") | vnstat | vnstat.service | Lightweight network traffic monitor. |
| [Very Secure FTP Daemon](/index.php/Very_Secure_FTP_Daemon "Very Secure FTP Daemon") | vsftpd | vsftpd.service (permanent)

vsftpd.socket (on-demand)

vsftpd-ssl.service (permanent)

vsftpd-ssl.socket (on-demand)

 | FTP server. |
| [wicd](/index.php/Wicd "Wicd") | wicd | wicd.service | A lightweight alternative to NetworkManager. |
| [x11vnc](/index.php/X11vnc "X11vnc") | x11vnc | x11vnc.service | VNC remote desktop daemon. |
| [XDM](/index.php/XDM "XDM") | xdm | xdm.service | Экранный менеджер X. |
| [xdm-archlinux](/index.php/XDM "XDM") | xdm-archlinux | xdm-archlinux.service | Экранный менеджер X с темой Arch Linux. |