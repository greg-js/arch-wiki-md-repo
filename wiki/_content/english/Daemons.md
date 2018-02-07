A [daemon](https://en.wikipedia.org/wiki/Daemon_(computing) is a program that runs as a "background" process (without a terminal or user interface), commonly waiting for events to occur and offering services. A good example is a web server that waits for a request to deliver a page, or a ssh server waiting for someone trying to log in. While these are full featured applications, there are daemons whose work is not that visible. Daemons are for tasks like writing messages into a log file (e.g. `syslog`, `metalog`) or keeping your system time accurate (e.g. [ntpd](/index.php/Ntpd "Ntpd")). For more information see [daemon(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/daemon.7).

In Arch Linux, daemons are managed by [systemd](/index.php/Systemd "Systemd"). The [systemctl](/index.php/Systemd#Basic_systemctl_usage "Systemd") command is the user interface used to manage them. It reads `*name*.service` files that contain information about how and when to start the associated daemon. Service files are stored in `/{etc,usr/lib,run}/systemd/system`. See [systemd#Using units](/index.php/Systemd#Using_units "Systemd") for details.

## List of daemons

Here is a list of daemons. Note that any package can provide a daemon, so this list will never be complete. Please feel free to add any missing daemons here, in alphabetical order. You may have packages that include other daemons from the [AUR](/index.php/AUR "AUR"). These files will likely be located in `/usr/lib/systemd/system/`.

The *Package* column contains a link to ArchWiki page for each daemon (or link to the package if no such page exists). The *initscripts* column contains the name of the legacy *rc.d* script and the *systemd* column contains the name of the [systemd](/index.php/Systemd "Systemd") service file. Note that there may be daemons specific to either initscripts or systemd, with the respective column empty. The *Description* column provides short description, preferably of *the daemon* (not of the package).

| Package | initscripts | systemd | Description |
| [acpid](/index.php/Acpid "Acpid") | acpid | acpid.service | A daemon for delivering ACPI power management events with netlink support. |
| [alsa](/index.php/Alsa "Alsa") | alsa | *always on* – alsa-store.service, alsa-restore.service | Saves the state of a sound card (e.g. volume) on shutdown and restores it on startup. |
| [at](https://www.archlinux.org/packages/?name=at) | atd | atd.service | Runs jobs queued for later execution. |
| [Autofs](/index.php/Autofs "Autofs") | autofs | autofs.service | Automounting of removable media or network shares when they are inserted or accessed. |
| [Avahi](/index.php/Avahi "Avahi") | avahi-daemon | avahi-daemon.service | Allows programs to automatically find local network services. |
| avahi-dnsconfd | avahi-dnsconfd.service | Multicast/unicast DNS-SD framework. |
| [Audit framework](/index.php/Audit_framework "Audit framework") | auditd | auditd.service | Linux audit framework |
| [Bitlbee](/index.php/Bitlbee "Bitlbee") | bitlbee | bitlbee.service | Brings instant messaging (XMPP, Yahoo!, ICQ, Twitter) to IRC. |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | bluetooth | bluetooth.service | Bluetooth protocol stack, framework, subsystem. |
| [Chrony](/index.php/Chrony "Chrony") | chrony | chrony.service | Lightweight NTP client and server. |
| [CDemu](/index.php/CDemu "CDemu") | cdemud | cdemu-daemon.service | CD/DVD-ROM device emulator. |
| [ClamAV](/index.php/ClamAV "ClamAV") | clamav | clamd.service
freshclamd.service | Anti-virus toolkit for Unix. |
| [ConnMan](/index.php/ConnMan "ConnMan") | connmand | connman.service | Wireless LAN network manager. |
| [Cpupower](/index.php/Cpupower "Cpupower") | cpupower | cpupower.service | Sets [cpufreq](/index.php/Cpufreq "Cpufreq") governor and other parameters on startup. |
 craftbukkit | craftbukkit.service | CraftBukkit Minecraft server. |
| [Cron](/index.php/Cron "Cron") | crond | cronie.service (if using [cronie](https://www.archlinux.org/packages/?name=cronie)) or dcron.service (if using [dcron](https://aur.archlinux.org/packages/dcron/)) | Daemon to schedule and time events. The daemon name *crond* is used by at least two packages, [cronie](https://www.archlinux.org/packages/?name=cronie) and [dcron](https://aur.archlinux.org/packages/dcron/). |
| [CUPS](/index.php/CUPS "CUPS") | cupsd | org.cups.cupsd.service | The CUPS Printing System daemon. |
| [D-Bus](/index.php/D-Bus "D-Bus") | dbus | *always on* – dbus.service | Freedesktop.org message bus system. |
| [dante](https://www.archlinux.org/packages/?name=dante) | sockd | sockd.service | A circuit-level SOCKS client/server. |
| [Deluge](/index.php/Deluge "Deluge") | deluged | deluged.service | Cross-platform and full-featured BitTorrent client - main daemon. |
| deluge-web | deluge-web.service | Cross-platform and full-featured BitTorrent client - web interface daemon. |
| [Dhcpcd](/index.php/Dhcpcd "Dhcpcd") | dhcpcd | dhcpcd@.service | DHCP daemon. |
| [Dovecot](/index.php/Dovecot "Dovecot") | dovecot | dovecot.service | IMAP and POP3 server. |
| [Dropbox](/index.php/Dropbox "Dropbox") | dropboxd | dropbox@.service | Cross-platform file synchronisation with version control. |
| [fail2ban](/index.php/Fail2ban "Fail2ban") | fail2ban | fail2ban.service | Fail2ban scans log files and bans IP addresses that show malicious activity. |
| [Fan speed control](/index.php/Fan_speed_control "Fan speed control") | fancontrol | fancontrol.service | Fan control daemon (part of lm_sensors) |
| [Fbsplash](/index.php/Fbsplash "Fbsplash") | fbsplash | *not yet implemented* | Graphical boot splash screen for the user. |
| [FluidSynth](/index.php/FluidSynth "FluidSynth") | fluidsynth | fluidsynth.service | Software synthesizer. |
| [inetutils](https://www.archlinux.org/packages/?name=inetutils) | ftpd | ftpd.service | inetutils FTP daemon. |
| [GDM](/index.php/GDM "GDM") | gdm | gdm.service | GNOME Display Manager. |
| [Git](/index.php/Git "Git") | git-daemon | git-daemon.socket | Git daemon. |
| [gpm](/index.php/Console_mouse_support "Console mouse support") | gpm | gpm.service | Console mouse support. |
| [hddtemp](/index.php/Hddtemp "Hddtemp") | hddtemp | hddtemp.service | Hard drive temperature monitor daemon. |
 healthd | healthd.service | A daemon which can be used to alert you in the event of a hardware health monitoring alarm (part of [lm_sensors](/index.php/Lm_sensors "Lm sensors")). |
| [apache](/index.php/Apache "Apache") | httpd | httpd.service | Apache HTTP Server (Web Server). |
 i8kmon | i8kmon.service | Monitor the CPU temperature and fan status on Dell Inspiron laptops. |
 ifplugd | ifplugd@.service | Start/stop network on network cable plugged in/out. |
| [iptables](/index.php/Iptables "Iptables") | iptables | iptables.service | Load firewall rules for IPv4. |
| ip6tables | ip6tables.service | Load firewall rules for IPv6. |
| [IPFS](/index.php/IPFS "IPFS") | ipfs daemon |  ? | A peer-to-peer hypermedia protocol node |
 irqbalance | irqbalance.service | Irqbalance is the Linux utility tasked with making sure that interrupts from your hardware devices are handled in as efficient a manner as possible. |
| [KDE](/index.php/KDE "KDE") | kdm | kdm.service | KDE Display Manager. |
| [krb5](https://www.archlinux.org/packages/?name=krb5) | krb5-kadmind | krb5-kadmind.service | Kerberos 5 administration server. |
| krb5-kdc | krb5-kdc.service | Kerberos 5 KDC. |
| krb5-kpropd | krb5-kpropd.service | Kerberos 5 propagation server. |
| [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools") | laptop-mode | laptop-mode.service | Laptop power saving tools. |
| [lighttpd](/index.php/Lighttpd "Lighttpd") | lighttpd | lighttpd.service | Lighttpd HTTP Server (Web Server). |
| [libvirt](/index.php/Libvirt "Libvirt") | libvirt | libvirtd.service | libvirt is a virtualization API and a daemon for managing virtual machines (VMs). |
| [lxdm](/index.php/LXDE "LXDE") | lxdm | lxdm.service | LXDE Display Manager. |
| [mandb](https://www.archlinux.org/packages/?name=mandb) |  ? | man-db.timer

man-db.service

 | Daily man-db cache update. |
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
| [glibc](https://www.archlinux.org/packages/?name=glibc) | nscd | nscd.service | Name service caching daemon. |
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
| [PPTP server](/index.php/PPTP_server "PPTP server") | pptpd | pptpd.service | A Virtual Private Network (VPN) server using the Point-to-Point Tunneling Protocol (PPTP). |
| [pppd](/index.php/Pppd "Pppd") | pppd | ppp@.service | A daemon which implements the Point-to-Point Protocol for dial-up networking. |
| [preload](/index.php/Preload "Preload") | preload | preload.service | Makes applications run faster by prefetching binaries and shared objects. |
| [Prosody](/index.php/Prosody "Prosody") | prosody | prosody.service | XMPP server. |
| [Profile-sync-daemon](/index.php/Profile-sync-daemon "Profile-sync-daemon") | psd | psd.service | Manages your browser's profile in tmpfs and periodically syncs it back to your physical disk. |
 pure-ftpd | pure-ftpd.servicecups.service | A fast, production quality, standards-compliant FTP server. |
| [Rsync](/index.php/Rsync "Rsync") | rsyncd | rsyncd.service | rsync daemon. |
| [Rsyslog](/index.php/Rsyslog "Rsyslog") | rsyslogd | rsyslog.service | Alternative system logger. |
| [Redis](/index.php/Redis "Redis") | redis-server | redis.service | Key-value store |
| [samba](/index.php/Samba "Samba") | samba | smbd.service
nmbd.service
winbindd.service | File and print services for Microsoft Windows clients. |
| [LVM](/index.php/LVM "LVM") |  ? | blk-availability.service
lvm2-lvmetad.service
lvm2-monitor.service
lvm2-pvscan.service | LVM is a logical volume manager for the Linux kernel; it manages disk drives and similar mass-storage devices. |
| [SANE](/index.php/SANE "SANE") | saned | saned@.service | SANE network daemon. |
 saslauthd | saslauthd.service | SASL authentication daemon. |
| [lm_sensors](/index.php/Lm_sensors "Lm sensors") | sensord | sensord.service | Sensor information logging daemon. |
| sensors | lm_sensors.service | Initialize hardware monitoring sensors (load necessary kernel modules). |
| [shadow](https://www.archlinux.org/packages/?name=shadow) |  ? | shadow.timer

shadow.service

 | Daily verification of password and group files. |
| [SLiM](/index.php/SLiM "SLiM") | slim | slim.service | Simple Login Manager. |
| [SMART](/index.php/SMART "SMART") | smartd | smartd.service | Self-Monitoring, Analysis, and Reporting Technology (S.M.A.R.T.) Hard Disk Monitoring. |
| [smbnetfs](/index.php/Samba#smbnetfs "Samba") | smbnetfs | smbnetfs.service | Automatically mount Samba/Microsoft network shares. |
| [snmpd](/index.php/Snmpd "Snmpd") | snmpd | snmpd.service | A suite of applications used to implement SNMP |
 soundmodem | soundmodem.service | Multiplatform Soundcard Packet Radio Modem |
| [spamassassin](https://www.archlinux.org/packages/?name=spamassassin) | spamd | spamassassin.service | e-mail spam filtering service. |
| [openssh](/index.php/Openssh "Openssh") | sshd | sshd.service | OpenSSH (secure shell) daemon. |
 stunnel | stunnel.service | Allows encrypting arbitrary TCP connections inside SSL. |
 svnserve | svnserve.service | Subversion server. |
| [syslog-ng](/index.php/Syslog-ng "Syslog-ng") | syslog-ng | syslog-ng.service | System logger next generation. |
| [Timidity](/index.php/Timidity "Timidity") | timidity++ | timidity.service | Software synthesizer for MIDI. |
| [Tinc](/index.php/Tinc "Tinc") |  ? | tincd@.service | One for each configuration directory like /etc/tinc/*<vpnname>*/ |
| [Tor](/index.php/Tor "Tor") | tor | tor.service | Onion routing for anonymous communication. |
| [Transmission](/index.php/Transmission "Transmission") | transmissiond | transmission.service | BitTorrent Daemon. |
| [Ufw](/index.php/Ufw "Ufw") | ufw | ufw.service | Uncomplicated FireWall. |
| [Urxvtd](/index.php/Urxvt "Urxvt") |  ? | urxvtd.service | urxvt daemon. |
| [VirtualBox](/index.php/VirtualBox "VirtualBox") | vboxservice | vboxservice.service | VirtualBox Guest Service. |
| [vnStat](/index.php/VnStat "VnStat") | vnstat | vnstat.service | Lightweight network traffic monitor. |
| [Very Secure FTP Daemon](/index.php/Very_Secure_FTP_Daemon "Very Secure FTP Daemon") | vsftpd | vsftpd.service (permanent)

vsftpd.socket (on-demand)

vsftpd-ssl.service (permanent)

vsftpd-ssl.socket (on-demand)

 | FTP server. |
| [wicd](/index.php/Wicd "Wicd") | wicd | wicd.service | A lightweight alternative to NetworkManager. |
| [x11vnc](/index.php/X11vnc "X11vnc") | x11vnc | x11vnc.service | VNC remote desktop daemon. |
| [XDM](/index.php/XDM "XDM") | xdm | xdm.service | X display manager. |
| [xdm-archlinux](/index.php/XDM "XDM") | xdm-archlinux | xdm-archlinux.service | X display manager with Arch Linux theme. |