Um [daemon](https://en.wikipedia.org/wiki/Daemon_(computing) é um programa que roda em "background" como um processo(sem terminal ou interface), que comumente espera por eventos para oferecer serviços. Um bom exemplo é um servidor web que espera por requisições para entregar uma página, ou um servidor ssh que espera por alguma tentativa de login. Apesar destes serem exemplos de aplicações bastante conhecidas e difundidas, há daemons cujo trabalho não é visível. Daemons que as tarefas são enviar logs para arquivos(ex: `syslog`, `metalog`) ou manter o horário do sistema sincronizado como o [ntpd](/index.php/Ntpd "Ntpd"). Para maiores informações veja `man 7 daemon`.

No Arch Linux, daemons são gerenciados pelo [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)"). O [systemctl](/index.php/Systemd_(Portugu%C3%AAs)#Uso_b.C3.A1sico_systemctl "Systemd (Português)") é o comando usado como interface para gerenciá-los. Ele lê arquivos na estrutura `*nome_do_serviço*.service` que contém informação sobre como e quando iniciar o daemon a eles associados. Os arquivos de serviço são armazenados em `/{etc,usr/lib,run}/systemd/system`. Veja [usando units](/index.php/Systemd_(Portugu%C3%AAs)#Usando_units "Systemd (Português)") para maiores detalhes.

## Lista de daemons

Aqui há uma lista dos daemons. Note que qualquer pacote pode fornecer um daemon, portanto, esta lista nunca será completa. Sinta-se livre para adicionar daemons nesta lista em ordem alfabética. Você pode ter pacotes que incluem daemons oriundos do [AUR](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)"). Estes arquivos possivelmente estão localizados em `/usr/lib/systemd/system/`.

A coluna do *Pacote* contem um link para a Wiki relacionada daquele daemon(ou para o pacote onde ele está). A coluna *initscripts* denota o nome legado *rc.d* e a coluna *systemd* contem o nome do arquivo de serviço no [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)"). Note que alguns serviços podem ser específicos do systemd ou dos initscripts, e uma das colunas poderá estar vazia. Na coluna *Descrição* haverá uma pequena descrição preferivelmente do daemon e não de seu pacote correspondente.

| Pacote | initscripts | systemd | Descrição |
| [acpid](/index.php/Acpid "Acpid") | acpid | acpid.service | Um daemon para gerenciamento de eventos de energia através de ACPI com suporte ao netlink. |
| [alsa](/index.php/Advanced_Linux_Sound_Architecture_(Portugu%C3%AAs) "Advanced Linux Sound Architecture (Português)") | alsa | *sempre ligados* – alsa-store.service, alsa-restore.service | Salva o estado de uma placa de som(ex: volume) durante o desligamento, e restaura na inicialização. |
| [at](https://www.archlinux.org/packages/?name=at) | atd | atd.service | Agenda tarefas para posterior execução. |
| [Autofs](/index.php/Autofs "Autofs") | autofs | autofs.service | Montagem automática de mídias removíveis quando inseridas ou compartilhamentos de rede quando acessados. |
| [Avahi](/index.php/Avahi "Avahi") | avahi-daemon | avahi-daemon.service | Permite que programas encontrem automaticamente serviços na rede. |
| avahi-dnsconfd | avahi-dnsconfd.service | Framework multicast/unicast DNS-SD. |
| [Audit framework](/index.php/Audit_framework "Audit framework") | auditd | auditd.service | Framework de auditoria do Linux. |
| [Bitlbee](/index.php/Bitlbee "Bitlbee") | bitlbee | bitlbee.service | Faz a ponte de mensageiros instantâneos diversos (XMPP, MSN, Yahoo!, AIM, ICQ, Twitter) para o IRC. |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | bluetooth | bluetooth.service | Protocolo, framework, pilha e subsistema Bluetooth. |
| [Chrony](/index.php/Chrony "Chrony") | chrony | chrony.service | Cliente e servidor NTP leve. |
| [CDemu](/index.php/CDemu "CDemu") | cdemud | cdemu-daemon.service | Emulador de CD/DVD-ROM. |
| [ClamAV](/index.php/ClamAV "ClamAV") | clamav | clamd.service
freshclamd.service | Anti-virus para Unix. |
| [Connman](/index.php/Connman "Connman") | connmand | connman.service | Gerenciador de redes sem fio. |
| [Cpupower](/index.php/Cpupower "Cpupower") | cpupower | cpupower.service | Configura governador de [frequência de cpu](/index.php/Cpufreq "Cpufreq") e outros parâmetros de inicialização. |
 craftbukkit | craftbukkit.service | Servidor de Minecraft CraftBukkit . |
| [Cron](/index.php/Cron "Cron") | crond | cronie.service (se usando [cronie](https://www.archlinux.org/packages/?name=cronie)) ou dcron.service (se usando [dcron](https://aur.archlinux.org/packages/dcron/)) | Daemon para agendamento de eventos baseados em horário. O nome *crond* é utilizado por pelo menos dois pacotes, [cronie](https://www.archlinux.org/packages/?name=cronie) e [dcron](https://aur.archlinux.org/packages/dcron/). |
| [CUPS](/index.php/CUPS "CUPS") | cupsd | org.cups.cupsd.service | Daemon do serviço de impressão CUPS. |
| [D-Bus](/index.php/D-Bus "D-Bus") | dbus | *sempre ligado* – dbus.service | Systema de barramento de mensagens Freedesktop.org. |
| [dante](https://www.archlinux.org/packages/?name=dante) | sockd | sockd.service | Servidor/cliente SOCKS a nível de circuito. |
| [Deluge](/index.php/Deluge "Deluge") | deluged | deluged.service | Cliente de BitTorrent cross-platform e com diversas funcionalidades. |
| deluge-web | deluge-web.service | Cliente de BitTorrent cross-platform e com diversas funcionalidades. Daemon de interface web. |
| [Dhcpcd](/index.php/Dhcpcd "Dhcpcd") | dhcpcd | dhcpcd@.service | Daemon DHCP . |
| [Dovecot](/index.php/Dovecot "Dovecot") | dovecot | dovecot.service | Servidor IMAP e POP3. |
| [Dropbox](/index.php/Dropbox "Dropbox") | dropboxd | dropbox@.service | Sistema de sincronização de arquivos e controle de versão. |
| [fail2ban](/index.php/Fail2ban "Fail2ban") | fail2ban | fail2ban.service | Fail2ban verifica arquivos de log e bane endereços ip que demonstram atividade maliciosa. |
| [Fan speed control](/index.php/Fan_speed_control "Fan speed control") | fancontrol | fancontrol.service | Daemon de controle de ventoinhas(parte do lm_sensors) |
| [Fbsplash](/index.php/Fbsplash "Fbsplash") | fbsplash | *não implementado* | Ferramenta para configuração de boot gráfico. |
| [FluidSynth](/index.php/FluidSynth "FluidSynth") | fluidsynth | fluidsynth.service | Sintetizador via software. |
| [inetutils](https://www.archlinux.org/packages/?name=inetutils) | ftpd | ftpd.service | Daemon ftp do inetutils. |
| [GDM](/index.php/GDM "GDM") | gdm | gdm.service | GNOME Display Manager. |
| [Git](/index.php/Git "Git") | git-daemon | git-daemon.socket | Daemon Git. |
| [gpm](/index.php/Console_mouse_support "Console mouse support") | gpm | gpm.service | Habilita o mouse na console. |
| [hddtemp](/index.php/Hddtemp "Hddtemp") | hddtemp | hddtemp.service | Monitor de temperatura de HDs. |
 healthd | healthd.service | Um daemon para alertar eventos de saúde de hardware (parte do [lm_sensors](/index.php/Lm_sensors "Lm sensors")). |
| [apache](/index.php/Apache "Apache") | httpd | httpd.service | Apache HTTP Server (Web Server). |
 i8kmon | i8kmon.service | Monitore a temperatura de CPU e ventoinhas em laptops da Dell série Inspiron. |
 ifplugd | ifplugd@.service | Inicia/para a rede baseado em eventos de plugar o cabo. |
| [iptables](/index.php/Iptables "Iptables") | iptables | iptables.service | Carrega regras de firewall para IPv4. |
| ip6tables | ip6tables.service | Carrega regras de firewall para IPv6. |
| [IPFS](/index.php/IPFS "IPFS") | ipfs daemon |  ? | Nó de protocolo p2p hypermidia. |
 irqbalance | irqbalance.service | Utilitário que faz o balanceamento de interrupções de hardware tornando-as o mais performático possível. |
| [KDE](/index.php/KDE "KDE") | kdm | kdm.service | KDE Display Manager. |
| [krb5](https://www.archlinux.org/packages/?name=krb5) | krb5-kadmind | krb5-kadmind.service | Servidor de administração Kerberos 5. |
| krb5-kdc | krb5-kdc.service | KDC Kerberos 5. |
| krb5-kpropd | krb5-kpropd.service | Servidor de propagação Kerberos 5. |
| [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools") | laptop-mode | laptop-mode.service | Ferramentas de economia de energia para laptops. |
| [lighttpd](/index.php/Lighttpd "Lighttpd") | lighttpd | lighttpd.service | Lighttpd HTTP Server (Web Server). |
| [libvirt](/index.php/Libvirt "Libvirt") | libvirt | libvirtd.service | API de virtualização e daemon para gerenciamento de máquinas virtuais. |
| [lxdm](/index.php/LXDE "LXDE") | lxdm | lxdm.service | LXDE Display Manager. |
 mdadm | mdadm.service | Administração do MD(tecnologia de raid via software para Linux). |
| [miniDLNA](/index.php/MiniDLNA "MiniDLNA") | minidlna | minidlna.service | Servidor DLNA/UPnP simples. |
  ? | ModemManager.service | Torna internet móvel(3G) disponível para o [NetworkManager](/index.php/NetworkManager_(Portugu%C3%AAs) "NetworkManager (Português)"). |
| [mpd](/index.php/Mpd "Mpd") | mpd | mpd.service | Daemon de tocador de músicas |
| [MySQL](/index.php/MySQL "MySQL") | mysqld | mysqld.service | Servidor de banco de dados MySQL. |
| [MythTV](/index.php/MythTV "MythTV") | mythbackend | mythbackend.service | Backend para o gravador de vídeo e home theater MythTV. |
| [BIND](/index.php/BIND "BIND") | named | named.service | Servidor DNS "de facto" Berkeley Internet Name Daemon (BIND) |