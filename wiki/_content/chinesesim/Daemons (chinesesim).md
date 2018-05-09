**翻译状态：** 本文是英文页面 [Daemon](/index.php/Daemon "Daemon") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-05-09，点击[这里](https://wiki.archlinux.org/index.php?title=Daemon&diff=0&oldid=519085)可以查看翻译后英文页面的改动。

**守护进程**（daemon），指后台运行的、等待特定事件发生并提供服务的程序。典型的例子如网页服务器，等待网页传输请求并提供传输服务；又如ssh服务器，等待用户登入操作。许多守护进程提供**不可见的服务**，比如记录日志（syslog，metalog）、校准时间（ntpd）。详情见手册: [daemon(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/daemon.7)

尽管实际意义有所不同，守护进程也可以叫做**系统服务**。实际上，后者似乎是个更好理解的名称。

在 Arch Linux 中, 守护进程是通过[systemd](/index.php/Systemd "Systemd")进行管理的。[systemctl](/index.php/Systemd#Basic_systemctl_usage "Systemd")命令是用户界面。 systemctl 读取*<service>*.service 文件中包含的进程启动方式等相关信息。 Service 文件保存在 `/{etc,usr/lib,run}/systemd/system` 中. [systemd#Using units](/index.php/Systemd#Using_units "Systemd") 提供了使用 systemctl 管理守护进程的更多信息。

## 守护进程列表

守护进程列表，任何软件包都可能提供守护进程，所以此列表不可能涵盖所有守护进程。请按照字母顺序添加缺失的守护进程。启动进程的方式请阅读[Daemons List (简体中文)](/index.php/Daemons_List_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Daemons List (简体中文)").

| initscripts | systemd | 描述 |
| [acpid](/index.php/Acpid "Acpid") | acpid.service | 传递 ACPI 事件. |
| [alsa](/index.php/Advanced_Linux_Sound_Architecture "Advanced Linux Sound Architecture") | alsa-store.service

alsa-restore.service

 | 高级Linux声音架构,为声卡提供设备驱动. |
| atd | atd.service | 为之后执行而运行任务队列. |
| [avahi-daemon](/index.php/Avahi "Avahi") | avahi-daemon.service | 让程序自动发现本地网络服务. |
| [chrony](/index.php/Chrony "Chrony") | chrony.service | 为不经常在线系统设计的 NTP 客户端/服务器架构。 |
| [clamav](/index.php/ClamAV "ClamAV") | clamd.service

freshclamd.service

 | 杀毒程序 |
| [avahi-dnsconfd](/index.php/Avahi "Avahi") | avahi-dnsconfd.service |
| [bitlbee](/index.php/Bitlbee "Bitlbee") | bitlbee.service | BitlBee IRC/IM 网关. |
| [cpupower](/index.php/CPU_frequency_scaling "CPU frequency scaling") | cpupower.service | 内核 cpufreq 子系统的用户空间工具 |
| craftbukkit | 未实现 | CraftBukkit Minecraft 服务 |
| [crond](/index.php/Cron "Cron") | cronie.service | 预定日程和时间触发事件的守护进程。 [cronie](https://www.archlinux.org/packages/?name=cronie) 和 [dcron](https://aur.archlinux.org/packages/dcron/) 都会使用 *crond* 这个名字。 |
| [cupsd](/index.php/CUPS "CUPS") | org.cups.cupsd.service | 通用UNIX打印系统守护进程. |
| [dovecot](/index.php/Dovecot "Dovecot") | dovecot.service | IMAP 和 POP3 服务器. |
| [dropboxd](/index.php/Dropbox "Dropbox") | 未实现 | 带版本控制的跨平台文件同步. |
| [dbus](/index.php/D-Bus "D-Bus") | dbus.service | 用于软件通信的消息总线系统。 |
| [dcron](/index.php/Cron "Cron") | dcron.service | 定时执行任务的守护进程，两个软件包 [cronie](https://www.archlinux.org/packages/?name=cronie) 和 [dcron](https://aur.archlinux.org/packages/dcron/) 都提供了 *crond*。[cronie](https://www.archlinux.org/packages/?name=cronie)是Arch的默认 cron 程序。 |
| sockd | sockd.service | 电路级 SOCKS 客户端/服务器。 |
| [deluged](/index.php/Deluge "Deluge") | deluged.service | 跨平台的全功能 BitTorrent 客户端。 |
| [deluge-web](/index.php/Deluge "Deluge") | deluge-web.service | 跨平台的全功能 BitTorrent 客户端网页界面。 |
| [fam](/index.php/FAM "FAM") | 已过时 | 文件变更监视器.(已过时) |
| fancontrol | fancontrol.service | 风扇控制进程，lm_sensors的一部分 |
| [fbsplash](/index.php/Fbsplash "Fbsplash") | 未实现 | 图形化启动屏幕 |
| [fluidsynth](/index.php/FluidSynth "FluidSynth") | fluidsynth.service | Software synthesizer |
| ftpd | 未实现 | Inetutils ftp daemon |
| [gdm](/index.php/GDM "GDM") | gdm.service | Gnome 显示管理器 (登陆屏幕) |
| [gensplash](/index.php/Fbsplash "Fbsplash") | 未实现 | (参见 fbsplash) |
| [git-daemon](/index.php/Git "Git") | git-daemon.socket |
| [gpm](/index.php/Console_mouse_support "Console mouse support") | gpm.service | 控制台鼠标支持 |
| [hal](/index.php/HAL "HAL") | 以过时 | 硬件守护进程.(已过时) |
| hddtemp | hddtemp.service | 硬盘温度监控进程 |
| healthd | healthd.service | 在硬件健康有问题时给出警报，lm_sensors 的一部分. |
| iptables | iptables.service | 装入防火墙规则 |
| ip6tables | ip6tables.service | 装入 IPv6 防火墙规则 |
| [httpd](/index.php/LAMP "LAMP") | httpd.service | Apache HTTP 服务 (Web Server) |
| [hwclock](/index.php/Hwclock "Hwclock") | 并非真的守护进程，在关机时根据漂移调整时间。和 ntpd 互斥，它们都会调整硬件时间，所以只能开一个。 |
| irqbalance | irqbalance.service | Irqbalance 是一个 Linux 工具任务，用来保证硬件中断的有效处理。 |
| [kdm](/index.php/KDE "KDE") | kdm.service | KDE 显示管理器(图形登陆) |
| krb5-kadmind | krb5-kadmind.service | Kerberos 5 管理服务 |
| krb5-kdc | krb5-kdc.service | Kerberos 5 KDC |
| krb5-kpropd | krb5-kpropd.service | Kerberos 5 propagation server |
| [laptop-mode](/index.php/Laptop_Mode_Tools "Laptop Mode Tools") | laptop-mode.service | Laptop 节能工具 |
| [lighttpd](/index.php/Lighttpd "Lighttpd") | lighttpd.service | Lighttpd HTTP 服务(Web Server). |
| [lxdm](/index.php/LXDE "LXDE") | lxdm.service | LXDE 显示管理器 |
| mdadm | mdadm.service | MD Administration (Linux Software RAID). |
| [miniDLNA](/index.php/MiniDLNA "MiniDLNA") | minidlna.service | 简单的 DLNA/UPnP 媒体服务及 |
| [mpd](/index.php/MPD "MPD") | mpd.service | MPD (Music Player Daemon) 音乐播放器守护进程. |
| [mysqld](/index.php/MySQL "MySQL") | mysqld.service | MySQL 数据库服务。 |
| [mythbackend](/index.php/MythTV "MythTV") | mythbackend.service | 家庭影院程序 MythTV 的后端. |
| [named](/index.php/BIND "BIND") | named.service | BIND DNS 服务器. |
| netfs | 未使用，自动处理，见 remote-fs.target | 挂载网络文件系统。 |
| [net-auto-wired](/index.php/Netcfg "Netcfg") | net-auto-wired.service | Netcfg 提供的替代 `network` 的服务- 连接到有线网络 |
| [net-auto-wireless](/index.php/Netcfg "Netcfg") | net-auto-wireless.service | Netcfg 提供的替代 `network` 的服务 - 连接到无线网络 |
| [net-profiles](/index.php/Netcfg "Netcfg") | netcfg.service

netcfg@<profile-name>.service

 | Netcfg 提供的替代 `network` 的服务 - 连接到 profile |
| [network](/index.php/Configuring_Network "Configuring Network") | dhcpcd@<interface>.service | 启用网络连接 |
| [networkmanager](/index.php/NetworkManager "NetworkManager") | NetworkManager.service | 替代 network，同时提供自动网络连接配置和探测。 |
| [nginx](/index.php/Nginx "Nginx") | nginx.service | Nginx HTTP 服务器和 IMAP/POP3 代理服务器 (Web Server) |
| nscd | nscd.service | 名称服务缓存进程 |
| [ntpd](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon") | ntpd.service | 网络时间协议守护进程 (客户端和服务器). |
| [Ntop](/index.php/Ntop "Ntop") | ntop.service | Ntop 是基于 libcap 的网络流量监控程序. |
| [openntpd](/index.php/OpenNTP "OpenNTP") | openntpd.service | 网络时间协议守护进程的一个替代 (客户端和服务器). |
| osspd | osspd.service | OSS 用户空间桥接. |
| [openvpn](/index.php/OpenVPN "OpenVPN") | openvpn@<profile-name>.service | 对应 /etc/openvpn/<profile-name>.conf 配置文件 |
| [pdnsd](/index.php/Pdnsd "Pdnsd") | pdnsd.service | 支持永久缓存的 DNS 代理服务器。 |
| [php-fpm](/index.php/Nginx#1st_Method_.22New.22_.28as_of_PHP_5.3.3.29 "Nginx") | php-fpm.service | PHP FastCGI 处理进程 |
| [oss](/index.php/OSS "OSS") | oss.service | Open Sound System. |
| [postgresql](/index.php/PostgreSQL "PostgreSQL") | postgresql.service | PostgreSQL 数据库服务 |
| [postfix](/index.php/Postfix "Postfix") | postfix.service |
| [powernowd](/index.php/Powernowd "Powernowd") | 根据系统负载调整 CPU 频率. 参见 [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") |
| [pptpd](/index.php/PPTP_server "PPTP server") | pptpd.service | 使用点对点隧道协议的 VPN。 |
| [prosody](/index.php/Prosody "Prosody") | prosody.service | XMPP 服务器. |
| [Pppd](/index.php/Pppd "Pppd") | ppp@provider.service | 负责拨号网络的点对点协议交互 |
| [preload](/index.php/Preload "Preload") | preload.service | 预读二进制程序和共享库，加速程序启动. |
| [psd](/index.php/Psd "Psd") | psd.service | 在 tmpfs 中管理浏览器的配置，定期回写到硬盘。 |
| pure-ftpd | FTP 服务器. |
| rfkill | rfkill.service | 开启/关闭无线设备。 |
| [rsyncd](/index.php/Rsync "Rsync") | rsyncd.service | Rsync 守护进程. |
| [rsyslogd](/index.php/Rsyslog "Rsyslog") | rsyslog.service | 最新版本的系统日志记录守护进程 |
| [samba](/index.php/Samba "Samba") | smb.service
nmb.service
winbind.service | 与 Microsoft Windows 客户端进行文件共享 |
| [saned](/index.php/USB_Scanner_Support "USB Scanner Support") | saned@.service | 在网络上共享扫描仪 |
| sensord | sensord.service | 传感器信息日志进程，lm_sensors 的一部分 |
| [sensors](/index.php/Lm_sensors "Lm sensors") | lm_sensors.service | 硬件监视器(温度、风扇等等) |
| [slim](/index.php/SLiM "SLiM") | slim.service | 简单登陆管理器 |
| [smartd](/index.php/SMART "SMART") | smartd.service | 硬盘监控 S.M.A.R.T(Self-Monitoring, Analysis, and Reporting Technology) |
| [smbnetfs](/index.php/Samba#smbnetfs "Samba") | smbnetfs.service | 自动挂载 Samba/Microsoft 网络共享。 |
| snmpd | 实现 SNMP 的一个程序集 |
| soundmodem | 多平台声卡 Radio Modem |
| [spamd](/index.php/SOHO_Postfix "SOHO Postfix") | spamassassin.service | 垃圾邮件过滤服务 |
| [sshd](/index.php/Secure_Shell "Secure Shell") | sshd.service

sshd@.service sshdgenkeys.service

 | OpenSSH (secure shell) 守护进程 |
| stbd | 过时 | 以前 gnome-system-tools 需要此进程，gnome-tools 2.28 之后就不需要了 |
| [stunnel](/index.php?title=Stunnel&action=edit&redlink=1 "Stunnel (page does not exist)") | stunnel.service | 将任意 TCP 连接用 SSL 加密. |
| svnserve | svnserve.service | Subversion 服务 |
| syslogd | 过时 | 这是基本的，但比较老旧的系统日志记录守护进程. |
| [syslog-ng](/index.php/Syslog-ng "Syslog-ng") | syslog-ng.service | 新一代系统日志记录守护进程. |
| [tor](/index.php/Tor "Tor") | tor.service | 匿名通信 Onion 路由。 |
| [transmissiond](/index.php/Transmission "Transmission") | transmission.service | Bit Torrent 守护进程. |
| [ufw](/index.php/Ufw "Ufw") | ufw.service | 简单的防火墙FireWall. |
| [vboxdrv](/index.php/VirtualBox "VirtualBox") | vboxservice.service | VirtualBox 需要的服务进程 |
| [timidity++](/index.php/Timidity "Timidity") | 软件 MIDI 合成器 |
| [vsftpd](/index.php/Very_Secure_FTP_Daemon "Very Secure FTP Daemon") | vsftpd.service

vsftpd@.service vsftpd-ssl.service

 | 文件传输专用协议服务器（ftp）守护进程. |
| [wicd](/index.php/Wicd "Wicd") | wicd.service | Wicd是一个既能管理有线网络又能管理无线网络的网络接入管理器，是 NetworkManager 的一个功能相似的替代,有cli,gtk+多管理方式. |
| [x11vnc](/index.php/X11vnc "X11vnc") | VNC 远程桌面服务 |

## 参见

*   [Systemd](/index.php/Systemd "Systemd")