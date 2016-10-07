O [NetworkManager](http://www.gnome.org/projects/NetworkManager/) é um programa que provê a detecção e configuração automática de redes para computadores. As funcionalidades do NetworkManager são úteis para redes sem fio e cabeadas. Nas redes sem fio, o NetworkManager terá preferência pelas redes que já conhece, e possui a habilidade para trocar para a rede mais confiável sempre que disponível. Aplicações preparadas para o NetworkManager podem trocar do modo online para o offline. O NetworkManager tem preferência pelas redes cabeadas em detrimento das wireless, e possui suporte a certos tipos de VPN. Foi originalmente desenvolvido pela Red Hat e agora, é hospedado no projeto [GNOME](/index.php/GNOME "GNOME").

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
    *   [1.1 Suporte a VPN](#Suporte_a_VPN)
    *   [1.2 PPPoE / DSL](#PPPoE_.2F_DSL)
*   [2 Front-ends](#Front-ends)
    *   [2.1 GNOME](#GNOME)
    *   [2.2 KDE Plasma](#KDE_Plasma)
    *   [2.3 XFCE](#XFCE)
    *   [2.4 Openbox](#Openbox)
    *   [2.5 Outros desktops ou gerenciadores de janelas](#Outros_desktops_ou_gerenciadores_de_janelas)
    *   [2.6 Linha de comando](#Linha_de_comando)
        *   [2.6.1 nmcli](#nmcli)
        *   [2.6.2 nmtui](#nmtui)
        *   [2.6.3 nmcli-dmenu](#nmcli-dmenu)
*   [3 Veja também](#Veja_tamb.C3.A9m)

## Instalação

Basta instalar o pacote [networkmanager](https://www.archlinux.org/packages/?name=networkmanager). Este pacote não inclui o software de bandeja(tray) *nm-applet*, que é parte integrante do pacote [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet). Possui funcionalidades básicas de DHCP. Para que todas as funcionalidades estejam acessíveis, incluindo as que envolvem IPv6, instale o pacote [dhclient](https://www.archlinux.org/packages/?name=dhclient).

**Note:** Garanta que nenhum outro serviço de configuração de rede esteja rodando; de fato, caso hajam vários eles irão conflitar. Você pode encontrar a lista dos serviços com `systemctl --type=service` e então poderá pará-los através do [stop](/index.php/Systemd_(Portugu%C3%AAs)#Usando_units "Systemd (Português)").

### Suporte a VPN

O suporte a VPN é dado através de um sistema de plug-in. Instale o pacote do sistema de VPN que lhe for conveniente da seguinte lista:

*   [networkmanager-openconnect](https://www.archlinux.org/packages/?name=networkmanager-openconnect)
*   [networkmanager-openvpn](https://www.archlinux.org/packages/?name=networkmanager-openvpn)
*   [networkmanager-pptp](https://www.archlinux.org/packages/?name=networkmanager-pptp)
*   [networkmanager-vpnc](https://www.archlinux.org/packages/?name=networkmanager-vpnc)
*   [networkmanager-l2tp](https://aur.archlinux.org/packages/networkmanager-l2tp/)

**Warning:** Suporte a VPN é [instável](https://bugzilla.gnome.org/buglist.cgi?quicksearch=networkmanager%20vpn), verifique se os parâmetros dos serviços foram corretamente aplicados de acordo com o que foi configurado na interface gráfica a cada atualização de pacotes.[[1]](https://bugzilla.gnome.org/show_bug.cgi?id=755350) [[2]](https://bugzilla.gnome.org/show_bug.cgi?id=758772) [FS#47535](https://bugs.archlinux.org/task/47535)

### PPPoE / DSL

Instale o pacote [rp-pppoe](https://www.archlinux.org/packages/?name=rp-pppoe) para suporte a conexões PPPoE / DSL.

## Front-ends

Para facilidade de configuração de novas redes, provavelmente usuários irão utilizar algum applet. Interfaces gráficas deste tipo geralmente ficam na área de notificação(tray) permitindo a seleção de redes e configuração do NetworkManager. Diversos tipos de applets existem para cada conjunto de interfaces gráficas.

### GNOME

O [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) do [GNOME](/index.php/GNOME "GNOME") funciona em todos os ambientes.

Para armazenar credenciais de conexões (Wireless/DSL) instale e configure o [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring").

Esteja ciente que marcar a opção de conexão `Tornar disponível para todos`, fará com que o NetworkManager armazene as senhas arquivo texto, e tal arquivo só será acessível pelo usuário root ou outros usando o via `nm-applet`.

### KDE Plasma

Instale o applet [plasma-nm](https://www.archlinux.org/packages/?name=plasma-nm).

### XFCE

Apesar do [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) funcionar no [Xfce](/index.php/Xfce "Xfce"), para que as notificações sejam exibidas corretamente(inclusive as de erro), o `nm-applet` precisa de alguma implementação das especificações de notificação do Freedesktop (veja [Projeto Galapago](http://www.galago-project.org/specs/notification/0.9/index.html)). Para habilitar tais notificações, instale o pacote [xfce4-notifyd](https://www.archlinux.org/packages/?name=xfce4-notifyd).

Sem este daemon de notificação, o `nm-applet` irá imprimir mensagens como as abaixo no stdout/stderr:

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

`nm-applet` funcionará normalmente, mas sem as devidas notificações.

Caso o `nm-applet` não exiba a tela de captura de senhas para a rede wifi, desconectando imediatamente após uma tentativa de conexão, você pode precisar do pacote [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring).

Caso o applet não apareça, instale o pacote [xfce4-indicator-plugin](https://aur.archlinux.org/packages/xfce4-indicator-plugin/). [[3]](http://askubuntu.com/questions/449658/networkmanager-tray-nm-applet-is-gone-after-upgrade-to-14-04-trusty)

### Openbox

Para funcionar corretamente no [Openbox](/index.php/Openbox "Openbox"), o applet do GNOME requer o pacote [xfce4-notifyd](https://www.archlinux.org/packages/?name=xfce4-notifyd) para gerenciar as notificações pelos mesmos motivos do XFCE, e o pacote [gnome-icon-theme](https://www.archlinux.org/packages/?name=gnome-icon-theme) para que o applet seja exibido corretamente na área de notificação.

Se você deseja armazenar credenciais de autenticação, poderá ter que configurar o [gnome-keyring](/index.php/Gnome-keyring "Gnome-keyring").

O `nm-applet` instala o arquivo de autostart `/etc/xdg/autostart/nm-applet.desktop`. Caso você tenha problemas(`nm-applet` iniciando duplicado ou não iniciando), veja [Openbox#autostart](/index.php/Openbox#autostart "Openbox") ou [[4]](https://bbs.archlinux.org/viewtopic.php?pid=993738) para obter a solução.

### Outros desktops ou gerenciadores de janelas

Nos cenários restantes, é recomendado a utilização do applet GNOME. Certifique-se de que o pacote [gnome-icon-theme](https://www.archlinux.org/packages/?name=gnome-icon-theme) está instalado, e para armazenar credenciais o [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring") configurado.

Para rodar o `nm-applet` sem uma área de notificação, você pode usar o [trayer](https://www.archlinux.org/packages/?name=trayer) ou [stalonetray](https://www.archlinux.org/packages/?name=stalonetray). Exemplo de script para ser adicionado ao seu path:

 `nmgui` 
```
#!/bin/sh
nm-applet    2>&1 > /dev/null &
stalonetray  2>&1 > /dev/null
killall nm-applet

```

Ao fechar o *stalonetray*, também fechará o `nm-applet` economizando recursos logo após você terminar a configuração de rede.

### Linha de comando

Os seguintes aplicativos são úteis para o gerenciamento de redes sem um servidor X.

#### nmcli

Um frontend de linha de comando, incluído no pacote [networkmanager](https://www.archlinux.org/packages/?name=networkmanager).

Para maiores detalhes veja [nmcli(1)](https://www.mankier.com/1/nmcli). Exemplos:

*   Para conectar a uma rede sem fio: `nmcli dev wifi connect <name> password <password>` 
*   Para conectar a uma rede sem fio através da interface `wlan1`: `nmcli dev wifi connect <name> password <password> iface wlan1 [profile name]` 
*   Para desconectar uma interface: `nmcli dev disconnect iface eth0` 
*   Para reconectar uma interface marcada como desconectada: `nmcli con up uuid <uuid>` 
*   Para gerar uma lista dos UUIDs: `nmcli con show` 
*   Para gerar uma lista das conexões e seus estados: `nmcli dev` 
*   Para desabilitar a rede sem fio: `nmcli r wifi off` 

#### nmtui

A interface em curses *nmtui* é parte integrante do pacote [networkmanager](https://www.archlinux.org/packages/?name=networkmanager).

Para maiores detalhes veja [nmtui(1)](https://www.mankier.com/1/nmtui).

#### nmcli-dmenu

Outra alternativa existente é o pacote [networkmanager-dmenu-git](https://aur.archlinux.org/packages/networkmanager-dmenu-git/) que é um pequeno script para gerenciar conexões do NetworkManager através do *dmenu* ao invés do `nm-applet`. Provê todas as funcionalidades essenciais já existentes no NetworkManager como conectar a redes cabeadas ou sem fio, criar novas conexões wifi, capturar senhas quando necessário, iniciar conexões de VPN já existentes, habilitar/desabilitar a rede e executar o utilitário gráfico *nm-connection-editor*.

## Veja também

*   [NetworkManager para Administradores Parte 1](http://blogs.gnome.org/dcbw/2015/02/16/networkmanager-for-administrators-part-1/)