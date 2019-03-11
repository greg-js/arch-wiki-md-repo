**Estado de la traducción**
Este artículo es una traducción de [Daemons](/index.php/Daemons "Daemons"), revisada por última vez el **2019-01-12**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Daemons&diff=0&oldid=561789) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Un [demonio](https://en.wikipedia.org/wiki/es:Demonio_(inform%C3%A1tica) es un programa que se ejecuta como un proceso en segundo plano (o de fondo, sin una terminal o interfaz de usuario), comúnmente esperando que ocurran eventos y ofreciendo servicios. Un buen ejemplo es un servidor web que espera una solicitud para entregar una página, o un servidor ssh esperando a que alguien intente iniciar sesión. Si bien estas son aplicaciones completas, hay demonios cuyo trabajo no es tan visible. Los demonios son para tareas como escribir mensajes en un archivo de registro (por ejemplo, `syslog`, `metalog`) o para mantener la precisión del reloj de su sistema (por ejemplo, [ntpd](/index.php/Network_Time_Protocol_daemon_(Espa%C3%B1ol) "Network Time Protocol daemon (Español)")). Para obtener más información, véase [daemon(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/daemon.7).

En Arch Linux, los demonios son administrados por [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"). El comando [systemctl](/index.php/Systemctl "Systemctl") es la interfaz de usuario utilizada para administrarlos. Lee los archivos `*nombre*.Service` que contienen información sobre como y cuándo iniciar el demonio asociado. Los archivos de servicio se almacenan en `/{etc,usr/lib,run}/systemd/system`. Véase [Utilizar las unidades](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") para más detalles.

## Listado de demonios

He aquí un listado de <a class="mw-selflink selflink">demonios</a>. Tenga en cuenta que cualquier paquete puede proporcionar un demonio, por lo que esta lista no debe considerarse exhaustiva. Por favor, siéntase libre de añadir cualquier demonio que falte aquí, en orden alfabético. Se pueden tener paquetes que incluyan otros demonios desde [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"). Estos archivos es probable que se encuentren en `/usr/lib/systemd/system/`.

La columna *Paquete* contiene un enlace a la página de ArchWiki relativa a cada demonio (o enlaza al paquete, si tal página no existe). La columna *initscripts* contiene el nombre del script de initscripts y la columna *systemd* contiene el nombre del archivo de servicio de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"). Tenga en cuenta que puede haber demonios específicos tanto para initscripts como para systemd, con la correspondiente columna vacía. La columna *Descripción* proporciona una descripción corta, preferiblemente del **demonio** (antes que del paquete).

| Paquete | initscripts | systemd | Descripción |
| [acpid](/index.php/Acpid_(Espa%C3%B1ol) "Acpid (Español)") | acpid | acpid.service | Un demonio transmisor de los eventos de la gestión de energía por ACPI con soporte para netlink. |
| [alsa](/index.php/Advanced_Linux_Sound_Architecture_(Espa%C3%B1ol) "Advanced Linux Sound Architecture (Español)") | alsa | *siempre activo* – alsa-store.service, alsa-restore.service | Guarda el estado de una tarjeta de sonido (por ejemplo, el volumen) al cierre y lo restaura en el arranque. |
| [at](https://www.archlinux.org/packages/?name=at) | atd | atd.service | Guarda trabajos en cola para su posterior ejecución. |
| [Autofs](/index.php/Autofs "Autofs") | autofs | autofs.service | Monta automáticamente medios extraibles o recursos compartidos de red cuando se insertan o se accede a ellos. |
| [Avahi](/index.php/Avahi "Avahi") | avahi-daemon | avahi-daemon.service | Permite a los programas encontrar automáticamente servicios de redes locales. |
| avahi-dnsconfd | avahi-dnsconfd.service | Marco multidifusión/unidifusión DNS-SD. |
| [Audit framework](/index.php/Audit_framework "Audit framework") | auditd | auditd.service | Marco de auditoría de Linux |
| [Bitlbee](/index.php/Bitlbee "Bitlbee") | bitlbee | bitlbee.service | Aporta mensajería instantánea (XMPP, MSN, Yahoo!, AIM, ICQ, Twitter) para IRC. |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | bluetooth | bluetooth.service | Protocolo de Bluetooth, marco y subsistema. |
| [Chrony](/index.php/Chrony "Chrony") | chrony | chrony.service | Ligero cliente y servidor NTP. |
| [CDemu](/index.php/CDemu "CDemu") | cdemud | cdemu-daemon.service | Emulador de dispositivo CD/DVD-ROM. |
| [ClamAV](/index.php/ClamAV "ClamAV") | clamav | clamd.service
freshclamd.service | Conjunto de herramientas de antivirus para Unix. |
| [ConnMan](/index.php/ConnMan "ConnMan") | connmand | connman.service | Administrador de conexiones de red cableadas e inalámbricas. |
| [Cpupower](/index.php/Cpupower "Cpupower") | cpupower | cpupower.service | Ajusta el gobernador de [cpufreq](/index.php/CPU_frequency_scaling "CPU frequency scaling") y otros parámetros en el arranque. |
 craftbukkit | *aún no implementado* | Servidor CraftBukkit Minecraft. |
| [Cron](/index.php/Cron "Cron") | crond | cronie.service (si se usa [cronie](https://www.archlinux.org/packages/?name=cronie)) o dcron.service (si se una [dcron](https://aur.archlinux.org/packages/dcron/)) | Demonio para programar y temporizar eventos. El nombre del demonio *crond* es usado, al menos, por dos paquetes: [cronie](https://www.archlinux.org/packages/?name=cronie) y [dcron](https://aur.archlinux.org/packages/dcron/). |
| [CUPS](/index.php/CUPS "CUPS") | cupsd | org.cups.cupsd.service | Demonio del sistema de impresión CUPS. |
| [D-Bus](/index.php/D-Bus "D-Bus") | dbus | *siempre que esté on* – dbus.service | Sistema bus de mensajes de Freedesktop.org. |
| [dante](https://www.archlinux.org/packages/?name=dante) | sockd | sockd.service | Un cliente/servidor de SOCKS. |
| [Deluge](/index.php/Deluge "Deluge") | deluged | deluged.service | Multiplataforma y cliente BitTorrent completo - demonio principal. |
| deluge-web | deluge-web.service | Multiplataforma y cliente BitTorrent completo - demonio para la interfaz web. |
| [Dhcpcd](/index.php/Dhcpcd_(Espa%C3%B1ol) "Dhcpcd (Español)") | dhcpcd | dhcpcd@.service | Demonio de DHCP. |
| [Dovecot](/index.php/Dovecot "Dovecot") | dovecot | dovecot.service | Servidor IMAP y POP3. |
| [Dropbox](/index.php/Dropbox "Dropbox") | dropboxd | dropbox@.service | Archivo multiplataforma de sincronización con control de versión. |
| [fail2ban](/index.php/Fail2ban "Fail2ban") | fail2ban | fail2ban.service | Escanedados fail2ban de archivos de registros y baneados de IP que muestran los elementos maliciosos. |
| [Fan speed control](/index.php/Fan_speed_control "Fan speed control") | fancontrol | fancontrol.service | Demonio de control del ventilador (parte de lm_sensors) |
| [Fbsplash](/index.php/Fbsplash "Fbsplash") | fbsplash | *aún no implementado* | Pantalla de arranque gráfica para el usuario. |
| [FluidSynth](/index.php/FluidSynth "FluidSynth") | fluidsynth | fluidsynth.service | Sintetizador de software. |
| [inetutils](https://www.archlinux.org/packages/?name=inetutils) | ftpd | ftpd.service | Demonio de ftp Inetutils. |
| [GDM](/index.php/GDM "GDM") | gdm | gdm.service | Administrador de pantalla de Gnome. |
| [Git](/index.php/Git "Git") | git-daemon | git-daemon.socket | Demonio de GIT. |
| [gpm](/index.php/Console_mouse_support "Console mouse support") | gpm | gpm.service | Soporte para el ratón de consola. |
| [hddtemp](/index.php/Hddtemp "Hddtemp") | hddtemp | hddtemp.service | Demonio para monitorizar la temperatura del disco duro. |
 healthd | healthd.service | Un demonio que se puede utilizar para que le avise cuando detecte el mal estado de un hardware (parte de lm_sensors). |
| [apache](/index.php/Apache "Apache") | httpd | httpd.service | Servidor HTTP Apache (Servidor Web). |
 i8kmon | i8kmon.service | Monitorización de la temperatura de la cpu y del estado del ventilador en un portatil Dell Inspiron. |
 ifplugd | ifplugd@.service | Inicio/parada de la conexión de red cuando el cable de red esté conectado o no. |
| [iptables](/index.php/Iptables "Iptables") | iptables | iptables.service | Carga las reglas del cortafuegos para ipv4. |
| ip6tables | ip6tables.service | Carga las reglas del cortafuegos para ipv6. |
| [IPFS](/index.php/IPFS "IPFS") | demonio ipfs | ? | Un nodo de protocolo hipermedia punto-a-punto |
 irqbalance | irqbalance.service | Irqbalance es la utilidad Linux encargada de asegurarse de que las interrupciones de los dispositivos de hardware se manejan de una manera lo más eficiente posible. |
| [KDE](/index.php/KDE "KDE") | kdm | kdm.service | Administrador de pantalla KDE. |
| [krb5](https://www.archlinux.org/packages/?name=krb5) | krb5-kadmind | krb5-kadmind.service | Servidor para la administración de Kerberos 5. |
| krb5-kdc | krb5-kdc.service | Kerberos 5 KDC. |
| krb5-kpropd | krb5-kpropd.service | Servidor de programación de Kerberos 5. |
| [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools") | laptop-mode | laptop-mode.service | Herramientas para la gestión de energía del portatil. |
| [lighttpd](/index.php/Lighttpd "Lighttpd") | lighttpd | lighttpd.service | Server HTTP Lighttpd (Servidor Web). |
| [libvirt](/index.php/Libvirt "Libvirt") | libvirt | libvirtd.service | libvirt es una API de virtualización y un demonio para la gestión de máquinas virtuales (VMs). |
| [lxdm](/index.php/LXDE "LXDE") | lxdm | lxdm.service | Administrador de pantallas LXDE. |
| [man-db](https://www.archlinux.org/packages/?name=man-db) | ? | man-db.timer

man-db.service

 | Actualización diaria del caché man-db. |
 mdadm | mdadm.service | Administración MD (Linux Software RAID). |
| [miniDLNA](/index.php/MiniDLNA "MiniDLNA") | minidlna | minidlna.service | Sencillo servidor multimedia DLNA/UPnP. |
 ? | ModemManager.service | Gestión de banda ancha por módem (3G) disponible para [NetworkManager](/index.php/NetworkManager "NetworkManager"). |
| [mpd](/index.php/Music_Player_Daemon "Music Player Daemon") | mpd | mpd.service | Demonio de Music Player. |
| [MariaDB](/index.php/MariaDB "MariaDB") | mysqld | mysqld.service | Servidor de base de datos MySQL. |
| [MythTV](/index.php/MythTV "MythTV") | mythbackend | mythbackend.service | Backend para el software de vídeo digital MythTV. |
| [BIND](/index.php/BIND "BIND") | named | named.service | Berkeley Internet Name Daemon (BIND), servidor DNS. |
| [netctl](/index.php/Netctl "Netctl") | netctl@.service | Activa manualmente el perfil específico. |
 netctl-ifplugd@.service | Inicio/parada automática de perfiles de netctl de red cableada dependiendo de si el cable de red están enchufado o no. |
 netctl-auto@.service | Inicio/parada automática de perfiles inalámbricos de netctl dependiendo de si el punto de acceso está o no dentro del rango. |
 network | dhcpcd@.service | Abre las conexiones de red (Ethernet dinámica). |
| [NetworkManager](/index.php/NetworkManager "NetworkManager") | networkmanager | NetworkManager.service
NetworkManager-wait-online.service | Demonio de NetworkManager, proporciona la detección y configuración automática de conexiones de red. |
| [Nginx](/index.php/Nginx "Nginx") | nginx | nginx.service | Nginx HTTP Server and IMAP/Servidor proxy POP3 (Servidor Web ). |
| [glibc](https://www.archlinux.org/packages/?name=glibc) | nscd | nscd.service | Demonio para la memoria caché del servicio de nombres. |
| [ntpd](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon") | ntpd | ntpd.service | Demonio de Network Time Protocol (cliente y servidor). |
| [Ntop](/index.php/Ntop "Ntop") | ntop | ntop.service | Ntop es una sonda de tráfico de red basada en libcap. |
| [OpenNTPD](/index.php/OpenNTPD "OpenNTPD") | openntpd | openntpd.service | Demonio alternativo a Network Time Protocol (cliente y servidor). |
 osspd | osspd.service | OSS Userspace Bridge. |
| [OpenVPN](/index.php/OpenVPN "OpenVPN") | openvpn | openvpn@.service | Uno para cada archivo de configuración vpn guardado como /etc/openvpn/<nombre-del-perfil>.conf |
| [OSS](/index.php/OSS "OSS") | oss | oss.service | Open Sound System. Alternativa a ALSA. |
| [Pdnsd](/index.php/Pdnsd "Pdnsd") | pdnsd | pdnsd.service | Servidor proxy DNS con memoria caché permanente. |
| [php-fpm](https://www.archlinux.org/packages/?name=php-fpm) | php-fpm | php-fpm.service | Administrador de procesos FastCGI para PHP. |
| [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") | postgresql | postgresql.service | Servidor de base de datos PostgreSQL. |
| [Postfix](/index.php/Postfix_(Espa%C3%B1ol) "Postfix (Español)") | postfix | postfix.service |
| [Postgrey](/index.php/Postgrey_(Espa%C3%B1ol) "Postgrey (Español)") | postgrey | postgrey.service | Servicio de lista gris, utilizado con Postfix |
| [PPTP server](/index.php/PPTP_server "PPTP server") | pptpd | pptpd.service | Una red privada virtual (VPN) que usa el protocolo de túnel punto a punto (PPTP). |
| [pppd](/index.php/Pppd "Pppd") | pppd | ppp@.service | Un demonio que implementa el protocolo punto-a-punto al acceso telefónico a redes. |
| [preload](/index.php/Preload "Preload") | preload | preload.service | Demonio que hace que las aplicaciones se ejecuten más rápido por la obtención previa de los archivos binarios y objetos compartidos. |
| [Prosody](/index.php/Prosody "Prosody") | prosody | prosody.service | Servidor XMPP. |
| [Profile-sync-daemon](/index.php/Profile-sync-daemon "Profile-sync-daemon") | psd | psd.service | Gestiona el perfil del navegador en tmpfs y lo sincroniza periódicamente de nuevo con el disco físico. |
 pure-ftpd | pure-ftpd.service | Servidor FTP ajustado a los estándares, rápido y de calidad. |
| [Rsync](/index.php/Rsync "Rsync") | rsyncd | rsyncd.service | Demonio de Rsync. |
| [Rsyslog](/index.php/Rsyslog "Rsyslog") | rsyslogd | rsyslog.service | Registro alternativo del sistema. |
| [Redis](/index.php/Redis "Redis") | redis-server | redis.service | Almacén clave-valor |
| [samba](/index.php/Samba "Samba") | samba | smbd.service
nmbd.service
winbindd.service | Servicios de archivos e impresión para los clientes de Microsoft Windows. |
| [LVM](/index.php/LVM "LVM") | ? | blk-availability.service
lvm2-lvmetad.service
lvm2-monitor.service
lvm2-pvscan.service | LVM es un administrador de volumen lógico para el kernel de Linux; administra unidades de disco y dispositivos similares de almacenamiento masivo. |
| [SANE](/index.php/SANE "SANE") | saned | saned@.service | Demonio de red de SANE. |
 saslauthd | saslauthd.service | Demonio de autenticación SASL. |
| [lm_sensors](/index.php/Lm_sensors "Lm sensors") | sensord | sensord.service | Demonio para el registro de la información de los sensores. |
| sensors | lm_sensors.service | Inicialización de los sensores que monitorizan el hardware (cargados necesariamente por lo módulos del kernel). |
| [shadow](https://www.archlinux.org/packages/?name=shadow) | ? | shadow.timer

shadow.service

 | Comprobación diaria de los archivos de contraseña y grupo. |
| [SLiM](/index.php/SLiM "SLiM") | slim | slim.service | Administrador sencillo de inicio de sesión. |
| [SMART](/index.php/SMART "SMART") | smartd | smartd.service | Autoanálisis, análisis e información técnica (S.M.A.R.T) tras monitorizar el disco duro. |
| [smbnetfs](/index.php/Samba#smbnetfs "Samba") | smbnetfs | smbnetfs.service | Montaje automático de recursos compartidos Samba/Microsoft. |
| [snmpd](/index.php/Snmpd "Snmpd") | snmpd | snmpd.service | Una suite de aplicaciones que se utilizan para implementar SNMP |
 soundmodem | *not yet implemented* | Tarjeta de sonido multiplataforma Packet Radio Modem |
| [spamassassin](https://www.archlinux.org/packages/?name=spamassassin) | spamd | spamassassin.service | Servicio para filtrar el spam de los email. |
| [OpenSSH](/index.php/OpenSSH_(Espa%C3%B1ol) "OpenSSH (Español)") | sshd | sshd.service | Demonio de OpenSSH (shell segura). |
 stunnel | stunnel.service | Permite encriptar arbitrariamente conexión TCP con SSL. |
 svnserve | svnserve.service | Servidor de Subversion. |
| [syslog-ng](/index.php/Syslog-ng "Syslog-ng") | syslog-ng | syslog-ng.service | Nueva generación del registro del sistema. |
| [Timidity](/index.php/Timidity "Timidity") | timidity++ | timidity.service | Sintetizador de software para MIDI. |
| [Tinc](/index.php/Tinc "Tinc") | ? | tincd@.service | Uno para cada directorio de configuración como /etc/tinc/*<nombrevpn>*/ |
| [Tor](/index.php/Tor "Tor") | tor | tor.service | Enrutamiento para comunicaciones anónimas. |
| [Transmission](/index.php/Transmission "Transmission") | transmissiond | transmission.service | Demonio de Bit Torrent. |
| [Ufw](/index.php/Ufw "Ufw") | ufw | ufw.service | Uncomplicated FireWall. |
| [Urxvtd](/index.php/Urxvt "Urxvt") | ? | urxvtd.service | Demonio urxvt. |
| [VirtualBox](/index.php/VirtualBox "VirtualBox") | vboxservice | vboxservice.service | Servicio VirtualBox Guest. |
| [vnStat](/index.php/VnStat "VnStat") | vnstat | vnstat.service | Monitor de tráfico de red ligero. |
| [Very Secure FTP Daemon](/index.php/Very_Secure_FTP_Daemon "Very Secure FTP Daemon") | vsftpd | vsftpd.service (permanente)

vsftpd.socket (bajo demanda)

vsftpd-ssl.service (permanente)

vsftpd-ssl.socket (bajo demanda)

 | FTP server. |
| [wicd](/index.php/Wicd "Wicd") | wicd | wicd.service | Un administrador de conexiones de red ligero y alternativo a NetworkManager. |
| [x11vnc](/index.php/X11vnc "X11vnc") | x11vnc | x11vnc.service | Demonio de escritorio remoto de VNC. |
| [XDM](/index.php/XDM "XDM") | xdm | xdm.service | Administrador de pantalla X. |
| [xdm-archlinux](/index.php/XDM "XDM") | xdm-archlinux | xdm-archlinux.service | Administrador de pantalla X con el tema de Arch Linux. |