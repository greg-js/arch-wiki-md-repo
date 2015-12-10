# Daemons

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

A [daemon](https://en.wikipedia.org/wiki/Daemon_(computing) "wikipedia:Daemon (computing)") is a program that runs as a "background" process (without a terminal or user interface), commonly waiting for events to occur and offering services. A good example is a web server that waits for a request to deliver a page, or a ssh server waiting for someone trying to log in. While these are full featured applications, there are daemons whose work is not that visible. Daemons are for tasks like writing messages into a log file (e.g. `syslog`, `metalog`) or keeping your system time accurate (e.g. [ntpd](/index.php/Ntpd "Ntpd")). For more information see `man 7 daemon`.

In Arch Linux, daemons are managed by [systemd](/index.php/Systemd "Systemd"). The [systemctl](/index.php/Systemd#Basic_systemctl_usage "Systemd") command is the user interface used to manage them. It reads `_name_.service` files that contain information about how and when to start the associated daemon. Service files are stored in `/{etc,usr/lib,run}/systemd/system`. See [systemd#Using units](/index.php/Systemd#Using_units "Systemd") for details.

## List of daemons

Here is a list of daemons. Note that any package can provide a daemon, so this list will never be complete. Please feel free to add any missing daemons here, in alphabetical order. You may have packages that include other daemons from the [AUR](/index.php/AUR "AUR"). These files will likely be located in `/usr/lib/systemd/system/`.

The _Package_ column contains a link to ArchWiki page for each daemon (or link to the package if no such page exists). The _initscripts_ column contains the name of the legacy _rc.d_ script and the _systemd_ column contains the name of the [systemd](/index.php/Systemd "Systemd") service file. Note that there may be daemons specific to either initscripts or systemd, with the respective column empty. The _Description_ column provides short description, preferably of _the daemon_ (not of the package).

<table class="wikitable sortable">

<tbody>

<tr>

<th>Package</th>

<th>initscripts</th>

<th>systemd</th>

<th>Description</th>

</tr>

<tr>

<td>[acpid](/index.php/Acpid "Acpid")</td>

<td>acpid</td>

<td>acpid.service</td>

<td>A daemon for delivering ACPI power management events with netlink support.</td>

</tr>

<tr>

<td>[alsa](/index.php/Alsa "Alsa")</td>

<td>alsa</td>

<td>_always on_ – alsa-store.service, alsa-restore.service</td>

<td>Saves the state of a sound card (e.g. volume) on shutdown and restores it on startup.</td>

</tr>

<tr>

<td>[at](https://www.archlinux.org/packages/?name=at)</td>

<td>atd</td>

<td>atd.service</td>

<td>Runs jobs queued for later execution.</td>

</tr>

<tr>

<td>[Autofs](/index.php/Autofs "Autofs")</td>

<td>autofs</td>

<td>autofs.service</td>

<td>Automounting of removable media or network shares when they are inserted or accessed.</td>

</tr>

<tr>

<td rowspan="2">[Avahi](/index.php/Avahi "Avahi")</td>

<td>avahi-daemon</td>

<td>avahi-daemon.service</td>

<td>Allows programs to automatically find local network services.</td>

</tr>

<tr>

<td>avahi-dnsconfd</td>

<td>avahi-dnsconfd.service</td>

<td>Multicast/unicast DNS-SD framework.</td>

</tr>

<tr>

<td>[Bitlbee](/index.php/Bitlbee "Bitlbee")</td>

<td>bitlbee</td>

<td>bitlbee.service</td>

<td>Brings instant messaging (XMPP, MSN, Yahoo!, AIM, ICQ, Twitter) to IRC.</td>

</tr>

<tr>

<td>[Bluetooth](/index.php/Bluetooth "Bluetooth")</td>

<td>bluetooth</td>

<td>bluetooth.service</td>

<td>Bluetooth protocol stack, framework, subsystem.</td>

</tr>

<tr>

<td>[Chrony](/index.php/Chrony "Chrony")</td>

<td>chrony</td>

<td>chrony.service</td>

<td>Lightweight NTP client and server.</td>

</tr>

<tr>

<td>[CDemu](/index.php/CDemu "CDemu")</td>

<td>cdemud</td>

<td>cdemu-daemon.service</td>

<td>CD/DVD-ROM device emulator.</td>

</tr>

<tr>

<td>[ClamAV](/index.php/ClamAV "ClamAV")</td>

<td>clamav</td>

<td>clamd.service  
freshclamd.service</td>

<td>Anti-virus toolkit for Unix.</td>

</tr>

<tr>

<td>[Connman](/index.php/Connman "Connman")</td>

<td>connmand</td>

<td>connman.service</td>

<td>Wireless LAN network manager.</td>

</tr>

<tr>

<td>[Cpupower](/index.php/Cpupower "Cpupower")</td>

<td>cpupower</td>

<td>cpupower.service</td>

<td>Sets [cpufreq](/index.php/Cpufreq "Cpufreq") governor and other parameters on startup.</td>

</tr>

<tr>

<td>craftbukkit</td>

<td>_not yet implemented_</td>

<td>CraftBukkit Minecraft server.</td>

</tr>

<tr>

<td>[Cron](/index.php/Cron "Cron")</td>

<td>crond</td>

<td>cronie.service (if using [cronie](https://www.archlinux.org/packages/?name=cronie)) or dcron.service (if using [dcron](https://aur.archlinux.org/packages/dcron/)<sup><small>AUR</small></sup>)</td>

<td>Daemon to schedule and time events. The daemon name _crond_ is used by at least two packages, [cronie](https://www.archlinux.org/packages/?name=cronie) and [dcron](https://aur.archlinux.org/packages/dcron/)<sup><small>AUR</small></sup>.</td>

</tr>

<tr>

<td>[CUPS](/index.php/CUPS "CUPS")</td>

<td>cupsd</td>

<td>org.cups.cupsd.service</td>

<td>The CUPS Printing System daemon.</td>

</tr>

<tr>

<td>[D-Bus](/index.php/D-Bus "D-Bus")</td>

<td>dbus</td>

<td>_always on_ – dbus.service</td>

<td>Freedesktop.org message bus system.</td>

</tr>

<tr>

<td>[dante](https://www.archlinux.org/packages/?name=dante)</td>

<td>sockd</td>

<td>sockd.service</td>

<td>A circuit-level SOCKS client/server.</td>

</tr>

<tr>

<td rowspan="2">[Deluge](/index.php/Deluge "Deluge")</td>

<td>deluged</td>

<td>deluged.service</td>

<td>Cross-platform and full-featured BitTorrent client - main daemon.</td>

</tr>

<tr>

<td>deluge-web</td>

<td>deluge-web.service</td>

<td>Cross-platform and full-featured BitTorrent client - web interface daemon.</td>

</tr>

<tr>

<td>[Dhcpcd](/index.php/Dhcpcd "Dhcpcd")</td>

<td>dhcpcd</td>

<td>dhcpcd@.service</td>

<td>DHCP daemon.</td>

</tr>

<tr>

<td>[Dovecot](/index.php/Dovecot "Dovecot")</td>

<td>dovecot</td>

<td>dovecot.service</td>

<td>IMAP and POP3 server.</td>

</tr>

<tr>

<td>[Dropbox](/index.php/Dropbox "Dropbox")</td>

<td>dropboxd</td>

<td>dropbox@.service</td>

<td>Cross-platform file synchronisation with version control.</td>

</tr>

<tr>

<td>[fail2ban](/index.php/Fail2ban "Fail2ban")</td>

<td>fail2ban</td>

<td>fail2ban.service</td>

<td>Fail2ban scans log files and bans IP addresses that show malicious activity.</td>

</tr>

<tr>

<td>[Fan speed control](/index.php/Fan_speed_control "Fan speed control")</td>

<td>fancontrol</td>

<td>fancontrol.service</td>

<td>Fan control daemon (part of lm_sensors)</td>

</tr>

<tr>

<td>[Fbsplash](/index.php/Fbsplash "Fbsplash")</td>

<td>fbsplash</td>

<td>_not yet implemented_</td>

<td>Graphical boot splash screen for the user.</td>

</tr>

<tr>

<td>[FluidSynth](/index.php/FluidSynth "FluidSynth")</td>

<td>fluidsynth</td>

<td>fluidsynth.service</td>

<td>Software synthesizer.</td>

</tr>

<tr>

<td>ftpd</td>

<td>ftpd.service</td>

<td>inetutils FTP daemon.</td>

</tr>

<tr>

<td>[GDM](/index.php/GDM "GDM")</td>

<td>gdm</td>

<td>gdm.service</td>

<td>GNOME Display Manager.</td>

</tr>

<tr>

<td>[Git](/index.php/Git "Git")</td>

<td>git-daemon</td>

<td>git-daemon.socket</td>

<td>Git daemon.</td>

</tr>

<tr>

<td>[gpm](/index.php/Console_mouse_support "Console mouse support")</td>

<td>gpm</td>

<td>gpm.service</td>

<td>Console mouse support.</td>

</tr>

<tr>

<td>[hddtemp](/index.php/Hddtemp "Hddtemp")</td>

<td>hddtemp</td>

<td>hddtemp.service</td>

<td>Hard drive temperature monitor daemon.</td>

</tr>

<tr>

<td>healthd</td>

<td>healthd.service</td>

<td>A daemon which can be used to alert you in the event of a hardware health monitoring alarm (part of [lm_sensors](/index.php/Lm_sensors "Lm sensors")).</td>

</tr>

<tr>

<td>[apache](/index.php/Apache "Apache")</td>

<td>httpd</td>

<td>httpd.service</td>

<td>Apache HTTP Server (Web Server).</td>

</tr>

<tr>

<td>i8kmon</td>

<td>i8kmon.service</td>

<td>Monitor the CPU temperature and fan status on Dell Inspiron laptops.</td>

</tr>

<tr>

<td>ifplugd</td>

<td>ifplugd@.service</td>

<td>Start/stop network on network cable plugged in/out.</td>

</tr>

<tr>

<td rowspan="2">[iptables](/index.php/Iptables "Iptables")</td>

<td>iptables</td>

<td>iptables.service</td>

<td>Load firewall rules for IPv4.</td>

</tr>

<tr>

<td>ip6tables</td>

<td>ip6tables.service</td>

<td>Load firewall rules for IPv6.</td>

</tr>

<tr>

<td>irqbalance</td>

<td>irqbalance.service</td>

<td>Irqbalance is the Linux utility tasked with making sure that interrupts from your hardware devices are handled in as efficient a manner as possible.</td>

</tr>

<tr>

<td>[KDE](/index.php/KDE "KDE")</td>

<td>kdm</td>

<td>kdm.service</td>

<td>KDE Display Manager.</td>

</tr>

<tr>

<td rowspan="3">[krb5](https://www.archlinux.org/packages/?name=krb5)</td>

<td>krb5-kadmind</td>

<td>krb5-kadmind.service</td>

<td>Kerberos 5 administration server.</td>

</tr>

<tr>

<td>krb5-kdc</td>

<td>krb5-kdc.service</td>

<td>Kerberos 5 KDC.</td>

</tr>

<tr>

<td>krb5-kpropd</td>

<td>krb5-kpropd.service</td>

<td>Kerberos 5 propagation server.</td>

</tr>

<tr>

<td>[Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools")</td>

<td>laptop-mode</td>

<td>laptop-mode.service</td>

<td>Laptop power saving tools.</td>

</tr>

<tr>

<td>[lighttpd](/index.php/Lighttpd "Lighttpd")</td>

<td>lighttpd</td>

<td>lighttpd.service</td>

<td>Lighttpd HTTP Server (Web Server).</td>

</tr>

<tr>

<td>[libvirt](/index.php/Libvirt "Libvirt")</td>

<td>libvirt</td>

<td>libvirtd.service</td>

<td>libvirt is a virtualization API and a daemon for managing virtual machines (VMs).</td>

</tr>

<tr>

<td>[lxdm](/index.php/LXDE "LXDE")</td>

<td>lxdm</td>

<td>lxdm.service</td>

<td>LXDE Display Manager.</td>

</tr>

<tr>

<td>mdadm</td>

<td>mdadm.service</td>

<td>MD Administration (Linux software RAID).</td>

</tr>

<tr>

<td>[miniDLNA](/index.php/MiniDLNA "MiniDLNA")</td>

<td>minidlna</td>

<td>minidlna.service</td>

<td>simple DLNA/UPnP media server.</td>

</tr>

<tr>

<td> ?</td>

<td>ModemManager.service</td>

<td>Makes mobile broadband (3G) modem available to [NetworkManager](/index.php/NetworkManager "NetworkManager").</td>

</tr>

<tr>

<td>[mpd](/index.php/Mpd "Mpd")</td>

<td>mpd</td>

<td>mpd.service</td>

<td>Music Player Daemon.</td>

</tr>

<tr>

<td>[MySQL](/index.php/MySQL "MySQL")</td>

<td>mysqld</td>

<td>mysqld.service</td>

<td>MySQL database server.</td>

</tr>

<tr>

<td>[MythTV](/index.php/MythTV "MythTV")</td>

<td>mythbackend</td>

<td>mythbackend.service</td>

<td>Back-end for the MythTV digital video recording/home theater software.</td>

</tr>

<tr>

<td>[BIND](/index.php/BIND "BIND")</td>

<td>named</td>

<td>named.service</td>

<td>The Berkeley Internet Name Daemon (BIND) DNS server.</td>

</tr>

<tr>

<td rowspan="3">[netctl](/index.php/Netctl "Netctl")</td>

<td>netctl@.service</td>

<td>Manually activate specific profile.</td>

</tr>

<tr>

<td>netctl-ifplugd@.service</td>

<td>Automatically start/stop netctl profiles depending on whether the cable is plugged in or not.</td>

</tr>

<tr>

<td>netctl-auto@.service</td>

<td>Automatically start/stop netctl wireless profiles depending on which access points are in range.</td>

</tr>

<tr>

<td>network</td>

<td>dhcpcd@.service</td>

<td>Brings up the network connections (dynamic Ethernet).</td>

</tr>

<tr>

<td>[NetworkManager](/index.php/NetworkManager "NetworkManager")</td>

<td>networkmanager</td>

<td>NetworkManager.service  
NetworkManager-wait-online.service</td>

<td>NetworkManager daemon, provides configuration and detection for automatic network connections.</td>

</tr>

<tr>

<td>[Nginx](/index.php/Nginx "Nginx")</td>

<td>nginx</td>

<td>nginx.service</td>

<td>Nginx HTTP Server and IMAP/POP3 proxy server (Web Server).</td>

</tr>

<tr>

<td>nscd</td>

<td>nscd.service</td>

<td>Name service caching daemon.</td>

</tr>

<tr>

<td>[ntpd](/index.php/Ntpd "Ntpd")</td>

<td>ntpd</td>

<td>ntpd.service</td>

<td>Network Time Protocol daemon (client and server).</td>

</tr>

<tr>

<td>[Ntop](/index.php/Ntop "Ntop")</td>

<td>ntop</td>

<td>ntop.service</td>

<td>Ntop is a network traffic probe based on libcap.</td>

</tr>

<tr>

<td>[OpenNTPD](/index.php/OpenNTPD "OpenNTPD")</td>

<td>openntpd</td>

<td>openntpd.service</td>

<td>Alternative Network Time Protocol daemon (client and server).</td>

</tr>

<tr>

<td>osspd</td>

<td>osspd.service</td>

<td>OSS Userspace Bridge.</td>

</tr>

<tr>

<td>[OpenVPN](/index.php/OpenVPN "OpenVPN")</td>

<td>openvpn</td>

<td>openvpn@.service</td>

<td>One for each VPN configuration file saved like `/etc/openvpn/_<profile-name>_.conf`</td>

</tr>

<tr>

<td>[OSS](/index.php/OSS "OSS")</td>

<td>oss</td>

<td>oss.service</td>

<td>Open Sound System. Alternative to [ALSA](/index.php/ALSA "ALSA").</td>

</tr>

<tr>

<td>[Pdnsd](/index.php/Pdnsd "Pdnsd")</td>

<td>pdnsd</td>

<td>pdnsd.service</td>

<td>Proxy DNS server with permanent caching.</td>

</tr>

<tr>

<td>[php-fpm](https://www.archlinux.org/packages/?name=php-fpm)</td>

<td>php-fpm</td>

<td>php-fpm.service</td>

<td>FastCGI Process Manager for PHP.</td>

</tr>

<tr>

<td>[PostgreSQL](/index.php/PostgreSQL "PostgreSQL")</td>

<td>postgresql</td>

<td>postgresql.service</td>

<td>PostgreSQL database server.</td>

</tr>

<tr>

<td>[Postfix](/index.php/Postfix "Postfix")</td>

<td>postfix</td>

<td>postfix.service</td>

<td>Mail server, which is an alternative to using [sendmail](/index.php/Sendmail "Sendmail").</td>

</tr>

<tr>

<td>[Postgrey](/index.php/Postgrey "Postgrey")</td>

<td>postgrey</td>

<td>postgrey.service</td>

<td>Greylisting service, used with Postfix</td>

</tr>

<tr>

<td>[powernowd](/index.php/Powernowd "Powernowd")</td>

<td>powernowd</td>

<td>_not yet implemented_</td>

<td>To adjust speed of CPU depending on system load.</td>

</tr>

<tr>

<td>[PPTP server](/index.php/PPTP_server "PPTP server")</td>

<td>pptpd</td>

<td>pptpd.service</td>

<td>A Virtual Private Network (VPN) server using the Point-to-Point Tunneling Protocol (PPTP).</td>

</tr>

<tr>

<td>[pppd](/index.php/Pppd "Pppd")</td>

<td>pppd</td>

<td>ppp@.service</td>

<td>A daemon which implements the Point-to-Point Protocol for dial-up networking.</td>

</tr>

<tr>

<td>[preload](/index.php/Preload "Preload")</td>

<td>preload</td>

<td>preload.service</td>

<td>Makes applications run faster by prefetching binaries and shared objects.</td>

</tr>

<tr>

<td>[Prosody](/index.php/Prosody "Prosody")</td>

<td>prosody</td>

<td>prosody.service</td>

<td>XMPP server.</td>

</tr>

<tr>

<td>[Profile-sync-daemon](/index.php/Profile-sync-daemon "Profile-sync-daemon")</td>

<td>psd</td>

<td>psd.service</td>

<td>Manages your browser's profile in tmpfs and periodically syncs it back to your physical disk.</td>

</tr>

<tr>

<td>pure-ftpd</td>

<td>pure-ftpd.servicecups.service</td>

<td>A fast, production quality, standards-compliant FTP server.</td>

</tr>

<tr>

<td>[rfkill](https://www.archlinux.org/packages/?name=rfkill)</td>

<td>rfkill</td>

<td>rfkill-block@.service  
rfkill-unblock@.service</td>

<td>(Un)blocks radio devices.</td>

</tr>

<tr>

<td>[Rsync](/index.php/Rsync "Rsync")</td>

<td>rsyncd</td>

<td>rsyncd.service</td>

<td>rsync daemon.</td>

</tr>

<tr>

<td>[Rsyslog](/index.php/Rsyslog "Rsyslog")</td>

<td>rsyslogd</td>

<td>rsyslog.service</td>

<td>Alternative system logger.</td>

</tr>

<tr>

<td>[samba](/index.php/Samba "Samba")</td>

<td>samba</td>

<td>smbd.service  
nmbd.service  
winbindd.service</td>

<td>File and print services for Microsoft Windows clients.</td>

</tr>

<tr>

<td>[SANE](/index.php/SANE "SANE")</td>

<td>saned</td>

<td>saned@.service</td>

<td>SANE network daemon.</td>

</tr>

<tr>

<td>saslauthd</td>

<td>saslauthd.service</td>

<td>SASL authentication daemon.</td>

</tr>

<tr>

<td rowspan="2">[lm_sensors](/index.php/Lm_sensors "Lm sensors")</td>

<td>sensord</td>

<td>sensord.service</td>

<td>Sensor information logging daemon.</td>

</tr>

<tr>

<td>sensors</td>

<td>lm_sensors.service</td>

<td>Initialize hardware monitoring sensors (load necessary kernel modules).</td>

</tr>

<tr>

<td>[SLiM](/index.php/SLiM "SLiM")</td>

<td>slim</td>

<td>slim.service</td>

<td>Simple Login Manager.</td>

</tr>

<tr>

<td>[SMART](/index.php/SMART "SMART")</td>

<td>smartd</td>

<td>smartd.service</td>

<td>Self-Monitoring, Analysis, and Reporting Technology (S.M.A.R.T.) Hard Disk Monitoring.</td>

</tr>

<tr>

<td>[smbnetfs](/index.php/Samba#smbnetfs "Samba")</td>

<td>smbnetfs</td>

<td>smbnetfs.service</td>

<td>Automatically mount Samba/Microsoft network shares.</td>

</tr>

<tr>

<td>[snmpd](/index.php/Snmpd "Snmpd")</td>

<td>snmpd</td>

<td>snmpd.service</td>

<td>A suite of applications used to implement SNMP</td>

</tr>

<tr>

<td>soundmodem</td>

<td>_not yet implemented_</td>

<td>Multiplatform Soundcard Packet Radio Modem</td>

</tr>

<tr>

<td>[spamassassin](https://www.archlinux.org/packages/?name=spamassassin)</td>

<td>spamd</td>

<td>spamassassin.service</td>

<td>e-mail spam filtering service.</td>

</tr>

<tr>

<td>[openssh](/index.php/Openssh "Openssh")</td>

<td>sshd</td>

<td>sshd.service</td>

<td>OpenSSH (secure shell) daemon.</td>

</tr>

<tr>

<td>stunnel</td>

<td>stunnel.service</td>

<td>Allows encrypting arbitrary TCP connections inside SSL.</td>

</tr>

<tr>

<td>svnserve</td>

<td>svnserve.service</td>

<td>Subversion server.</td>

</tr>

<tr>

<td>[syslog-ng](/index.php/Syslog-ng "Syslog-ng")</td>

<td>syslog-ng</td>

<td>syslog-ng.service</td>

<td>System logger next generation.</td>

</tr>

<tr>

<td>[Timidity](/index.php/Timidity "Timidity")</td>

<td>timidity++</td>

<td>timidity.service</td>

<td>Software synthesizer for MIDI.</td>

</tr>

<tr>

<td>[Tinc](/index.php/Tinc "Tinc")</td>

<td> ?</td>

<td>tincd@.service</td>

<td>One for each configuration directory like /etc/tinc/_<vpnname>_/</td>

</tr>

<tr>

<td>[Tor](/index.php/Tor "Tor")</td>

<td>tor</td>

<td>tor.service</td>

<td>Onion routing for anonymous communication.</td>

</tr>

<tr>

<td>[Transmission](/index.php/Transmission "Transmission")</td>

<td>transmissiond</td>

<td>transmission.service</td>

<td>BitTorrent Daemon.</td>

</tr>

<tr>

<td>[Ufw](/index.php/Ufw "Ufw")</td>

<td>ufw</td>

<td>ufw.service</td>

<td>Uncomplicated FireWall.</td>

</tr>

<tr>

<td>[Urxvtd](/index.php/Urxvt "Urxvt")</td>

<td> ?</td>

<td>urxvtd.service</td>

<td>urxvt daemon.</td>

</tr>

<tr>

<td>[VirtualBox](/index.php/VirtualBox "VirtualBox")</td>

<td>vboxservice</td>

<td>vboxservice.service</td>

<td>VirtualBox Guest Service.</td>

</tr>

<tr>

<td>[vnStat](/index.php/VnStat "VnStat")</td>

<td>vnstat</td>

<td>vnstat.service</td>

<td>Lightweight network traffic monitor.</td>

</tr>

<tr>

<td>[Very Secure FTP Daemon](/index.php/Very_Secure_FTP_Daemon "Very Secure FTP Daemon")</td>

<td>vsftpd</td>

<td>vsftpd.service (permanent)

vsftpd.socket (on-demand)

vsftpd-ssl.service (permanent)

vsftpd-ssl.socket (on-demand)

</td>

<td>FTP server.</td>

</tr>

<tr>

<td>[wicd](/index.php/Wicd "Wicd")</td>

<td>wicd</td>

<td>wicd.service</td>

<td>A lightweight alternative to NetworkManager.</td>

</tr>

<tr>

<td>[x11vnc](/index.php/X11vnc "X11vnc")</td>

<td>x11vnc</td>

<td>x11vnc.service</td>

<td>VNC remote desktop daemon.</td>

</tr>

<tr>

<td>[XDM](/index.php/XDM "XDM")</td>

<td>xdm</td>

<td>xdm.service</td>

<td>X display manager.</td>

</tr>

<tr>

<td>[xdm-archlinux](/index.php/XDM "XDM")</td>

<td>xdm-archlinux</td>

<td>xdm-archlinux.service</td>

<td>X display manager with Arch Linux theme.</td>

</tr>

</tbody>

</table>

Retrieved from "[https://wiki.archlinux.org/index.php?title=Daemons&oldid=400578](https://wiki.archlinux.org/index.php?title=Daemons&oldid=400578)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Boot process](/index.php/Category:Boot_process "Category:Boot process")
*   [Daemons and system services](/index.php/Category:Daemons_and_system_services "Category:Daemons and system services")