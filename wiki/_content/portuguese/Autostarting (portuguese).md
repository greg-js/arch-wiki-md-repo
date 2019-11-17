Artigos relacionados

*   [Daemons](/index.php/Daemons_(Portugu%C3%AAs) "Daemons (Português)")

Este artigo vincula a vários métodos para iniciar scripts ou aplicativos automaticamente quando algum evento específico está ocorrendo.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Na inicialização / no desligamento](#Na_inicialização_/_no_desligamento)
*   [2 No login / logout de usuário](#No_login_/_logout_de_usuário)
*   [3 No conectar / desconectar de dispositivo](#No_conectar_/_desconectar_de_dispositivo)
*   [4 Em eventos de tempo](#Em_eventos_de_tempo)
*   [5 Em eventos de sistemas de arquivos](#Em_eventos_de_sistemas_de_arquivos)
*   [6 No login / logout de shell](#No_login_/_logout_de_shell)
*   [7 Na inicialização de Xorg](#Na_inicialização_de_Xorg)
*   [8 Na inicialização de ambiente de desktop](#Na_inicialização_de_ambiente_de_desktop)
*   [9 Na inicialização do gerenciador de janela](#Na_inicialização_do_gerenciador_de_janela)

## Na inicialização / no desligamento

Use serviços de [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)").

## No login / logout de usuário

Use serviços [systemd/User](/index.php/Systemd/User "Systemd/User").

## No conectar / desconectar de dispositivo

Use regras [udev](/index.php/Udev "Udev").

## Em eventos de tempo

Periodicamente, em determinados horários, datas ou intervalos:

*   [systemd/Timers](/index.php/Systemd_(Portugu%C3%AAs)/Timers_(Portugu%C3%AAs) "Systemd (Português)/Timers (Português)")
*   [Cron](/index.php/Cron "Cron")

Uma vez por data e tempo:

*   [systemd/Timers](/index.php/Systemd_(Portugu%C3%AAs)/Timers_(Portugu%C3%AAs) "Systemd (Português)/Timers (Português)")
*   [at](https://www.archlinux.org/packages/?name=at)

## Em eventos de sistemas de arquivos

Use um monitoramento de evento [inotify](https://en.wikipedia.org/wiki/inotify "wikipedia:inotify"):

*   [inotify-tools](https://www.archlinux.org/packages/?name=inotify-tools), veja [inotifywait(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/inotifywait.1)
*   [incron](/index.php/Incron_(Portugu%C3%AAs) "Incron (Português)")
*   [fswatch](https://aur.archlinux.org/packages/fswatch/)

## No login / logout de shell

Veja [Shell de linha de comando#Arquivos de configuração](/index.php/Shell_de_linha_de_comando#Arquivos_de_configuração "Shell de linha de comando").

## Na inicialização de Xorg

*   [xinitrc](/index.php/Xinitrc_(Portugu%C3%AAs) "Xinitrc (Português)") se você está iniciando o [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)") manualmente com [xinit](/index.php/Xinit_(Portugu%C3%AAs) "Xinit (Português)").
*   [xprofile](/index.php/Xprofile_(Portugu%C3%AAs) "Xprofile (Português)") se você está usando um [gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição").

## Na inicialização de ambiente de desktop

A maioria dos [ambientes de desktops](/index.php/Ambientes_de_desktop "Ambientes de desktop") implementam [XDG Autostart](/index.php/XDG_Autostart_(Portugu%C3%AAs) "XDG Autostart (Português)").

Se os ambientes de desktop têm um artigo, veja sua seção *Inicialização automática* ou, se somente em inglês, *Autostart*.

*   [GNOME#Inicialização automática](/index.php/GNOME_(Portugu%C3%AAs)#Inicialização_automática "GNOME (Português)")
*   [KDE#Inicialização automática](/index.php/KDE_(Portugu%C3%AAs)#Inicialização_automática "KDE (Português)")
*   [Xfce#Inicialização automática](/index.php/Xfce_(Portugu%C3%AAs)#Inicialização_automática "Xfce (Português)")
*   [LXDE#Autostart](/index.php/LXDE#Autostart "LXDE")
*   [LXQt#Autostart](/index.php/LXQt#Autostart "LXQt")

## Na inicialização do gerenciador de janela

Muitos [gerenciadores de janela](/index.php/Gerenciadores_de_janela "Gerenciadores de janela") implementam [XDG Autostart](/index.php/XDG_Autostart_(Portugu%C3%AAs) "XDG Autostart (Português)").

Se o [gerenciador de janela](/index.php/Gerenciador_de_janela "Gerenciador de janela") tem um artigo, veja sua seção *Inicialização automática* ou, se somente em inglês, *Autostart*.

*   [Fluxbox#Autostart](/index.php/Fluxbox#Autostart "Fluxbox")
*   [Openbox#Autostart](/index.php/Openbox#Autostart "Openbox")
*   [Awesome#Autostart](/index.php/Awesome#Autostart "Awesome")
*   [i3#Autostart](/index.php/I3#Autostart "I3")