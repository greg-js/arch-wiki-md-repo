**Status de tradução:** Esse artigo é uma tradução de [NetworkManager](/index.php/NetworkManager "NetworkManager"). Data da última tradução: 2019-11-11\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=NetworkManager&diff=0&oldid=588634) na versão em inglês.

Related articles

*   [Configuração de rede](/index.php/Configura%C3%A7%C3%A3o_de_rede "Configuração de rede")
*   [Configuração de rede sem fio](/index.php/Configura%C3%A7%C3%A3o_de_rede_sem_fio "Configuração de rede sem fio")

O [NetworkManager](https://wiki.gnome.org/Projects/NetworkManager/) é um programa que provê a detecção e configuração automática de redes para computadores. As funcionalidades do NetworkManager são úteis para redes sem fio e cabeadas. Nas redes sem fio, o NetworkManager terá preferência pelas redes que já conhece, e possui a habilidade para trocar para a rede mais confiável sempre que disponível. Aplicativos preparados para o NetworkManager podem trocar do modo online para o offline. O NetworkManager tem preferência pelas redes cabeadas em detrimento das redes sem fio, e possui suporte a certos tipos de VPN. Foi originalmente desenvolvido pela Red Hat e agora, é hospedado no projeto [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)").

**Atenção:** Por padrão, as senhas de Wi-Fi são armazenadas em texto simples, veja [#Senhas de Wi-Fi criptografadas](#Senhas_de_Wi-Fi_criptografadas).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
    *   [1.1 Suporte a banda larga móvel](#Suporte_a_banda_larga_móvel)
    *   [1.2 Suporte a PPPoE / DSL](#Suporte_a_PPPoE_/_DSL)
    *   [1.3 Suporte a VPN](#Suporte_a_VPN)
*   [2 Uso](#Uso)
    *   [2.1 Exemplos de nmcli](#Exemplos_de_nmcli)
    *   [2.2 Editar uma conexão](#Editar_uma_conexão)
*   [3 Front-ends](#Front-ends)
    *   [3.1 GNOME](#GNOME)
    *   [3.2 KDE Plasma](#KDE_Plasma)
    *   [3.3 nm-applet](#nm-applet)
        *   [3.3.1 Appindicator](#Appindicator)
    *   [3.4 networkmanager-dmenu](#networkmanager-dmenu)
*   [4 Configuração](#Configuração)
    *   [4.1 Habilitar NetworkManager](#Habilitar_NetworkManager)
    *   [4.2 Habilitar NetworkManager Wait Online](#Habilitar_NetworkManager_Wait_Online)
    *   [4.3 Configurar as permissões de PolicyKit](#Configurar_as_permissões_de_PolicyKit)
    *   [4.4 Configurações de proxy](#Configurações_de_proxy)
    *   [4.5 Verificando conectividade](#Verificando_conectividade)
    *   [4.6 Cliente DHCP](#Cliente_DHCP)
    *   [4.7 Gerenciamento de DNS](#Gerenciamento_de_DNS)
        *   [4.7.1 Cache de DNS e encaminhamento condicional](#Cache_de_DNS_e_encaminhamento_condicional)
            *   [4.7.1.1 dnsmasq](#dnsmasq)
                *   [4.7.1.1.1 Configuração personalizada do dnsmasq](#Configuração_personalizada_do_dnsmasq)
                *   [4.7.1.1.2 IPv6](#IPv6)
                *   [4.7.1.1.3 DNSSEC](#DNSSEC)
            *   [4.7.1.2 systemd-resolved](#systemd-resolved)
            *   [4.7.1.3 Resolvedor de DNS com um assinante do openresolv](#Resolvedor_de_DNS_com_um_assinante_do_openresolv)
        *   [4.7.2 Servidores DNS personalizados](#Servidores_DNS_personalizados)
            *   [4.7.2.1 Configurando servidores DNS globais personalizados](#Configurando_servidores_DNS_globais_personalizados)
            *   [4.7.2.2 Configurando servidores DNS personalizados em uma conexão](#Configurando_servidores_DNS_personalizados_em_uma_conexão)
                *   [4.7.2.2.1 Configurando servidores DNS personalizados em uma conexão (GUI)](#Configurando_servidores_DNS_personalizados_em_uma_conexão_(GUI))
                *   [4.7.2.2.2 Configurando servidores DNS personalizados em uma conexão (nmcli / arquivo de conexão)](#Configurando_servidores_DNS_personalizados_em_uma_conexão_(nmcli_/_arquivo_de_conexão))
        *   [4.7.3 /etc/resolv.conf](#/etc/resolv.conf)
            *   [4.7.3.1 /etc/resolv.conf não gerenciado](#/etc/resolv.conf_não_gerenciado)
            *   [4.7.3.2 Usar openresolv](#Usar_openresolv)
*   [5 Serviços de rede com o NetworkManager dispatcher](#Serviços_de_rede_com_o_NetworkManager_dispatcher)
    *   [5.1 Evitando o esgotamento de tempo limite do dispatcher](#Evitando_o_esgotamento_de_tempo_limite_do_dispatcher)
    *   [5.2 Exemplos de dispatcher](#Exemplos_de_dispatcher)
        *   [5.2.1 Montar pasta remota com sshfs](#Montar_pasta_remota_com_sshfs)
        *   [5.2.2 Montagem de compartilhamentos SMB](#Montagem_de_compartilhamentos_SMB)
        *   [5.2.3 Montagem de compartilhamentos NFS](#Montagem_de_compartilhamentos_NFS)
        *   [5.2.4 Usar dispatcher para ativar rede sem fio automaticamente dependendo de cabo LAN estar conectado](#Usar_dispatcher_para_ativar_rede_sem_fio_automaticamente_dependendo_de_cabo_LAN_estar_conectado)
        *   [5.2.5 Usar dispatcher para conectar a uma VPN após uma conexão de rede ser estabelecida](#Usar_dispatcher_para_conectar_a_uma_VPN_após_uma_conexão_de_rede_ser_estabelecida)
        *   [5.2.6 Usar dispatcher para desabilitar IPv6 em conexões de provedor de VPN](#Usar_dispatcher_para_desabilitar_IPv6_em_conexões_de_provedor_de_VPN)
        *   [5.2.7 OpenNTPD](#OpenNTPD)
*   [6 Testando](#Testando)
*   [7 Dicas e truques](#Dicas_e_truques)
    *   [7.1 Senhas de Wi-Fi criptografadas](#Senhas_de_Wi-Fi_criptografadas)
        *   [7.1.1 Usando GNOME Keyring](#Usando_GNOME_Keyring)
        *   [7.1.2 Usando KDE Wallet](#Usando_KDE_Wallet)
    *   [7.2 Compartilhando conexão internet pelo Wi-Fi](#Compartilhando_conexão_internet_pelo_Wi-Fi)
    *   [7.3 Compartilhando conexão internet por Ethernet](#Compartilhando_conexão_internet_por_Ethernet)
    *   [7.4 Verificando se a conectividade está ativa dentro de um script ou trabalho cron](#Verificando_se_a_conectividade_está_ativa_dentro_de_um_script_ou_trabalho_cron)
    *   [7.5 Conectar a uma rede com segredo na inicialização](#Conectar_a_uma_rede_com_segredo_na_inicialização)
    *   [7.6 Desbloquear automaticamente o chaveiro após o login](#Desbloquear_automaticamente_o_chaveiro_após_o_login)
        *   [7.6.1 GNOME](#GNOME_2)
        *   [7.6.2 Gerenciador de login SLiM](#Gerenciador_de_login_SLiM)
    *   [7.7 OpenConnect com senha no KWallet](#OpenConnect_com_senha_no_KWallet)
    *   [7.8 Ignorar dispositivos específicos](#Ignorar_dispositivos_específicos)
    *   [7.9 Configurando aleatorização de endereço MAC](#Configurando_aleatorização_de_endereço_MAC)
    *   [7.10 Habilitar extensões de privacidade IPv6](#Habilitar_extensões_de_privacidade_IPv6)
    *   [7.11 Trabalhando com conexões cabeadas](#Trabalhando_com_conexões_cabeadas)
    *   [7.12 Usando iwd como o backend de Wi-Fi](#Usando_iwd_como_o_backend_de_Wi-Fi)
*   [8 Solução de problemas](#Solução_de_problemas)
    *   [8.1 Nenhum prompt para senha de redes Wi-Fi seguras](#Nenhum_prompt_para_senha_de_redes_Wi-Fi_seguras)
    *   [8.2 Nenhum tráfego via túnel PPTP](#Nenhum_tráfego_via_túnel_PPTP)
    *   [8.3 Gerenciamento de rede desabilitado](#Gerenciamento_de_rede_desabilitado)
    *   [8.4 Problemas com cliente DHCP interno](#Problemas_com_cliente_DHCP_interno)
    *   [8.5 Problemas DHCP com dhclient](#Problemas_DHCP_com_dhclient)
    *   [8.6 Modem 3G não detectado](#Modem_3G_não_detectado)
    *   [8.7 Desligando WLAN em laptops](#Desligando_WLAN_em_laptops)
    *   [8.8 Reversão de configurações de endereço IP estático para DHCP](#Reversão_de_configurações_de_endereço_IP_estático_para_DHCP)
    *   [8.9 Não é possível editar conexões como usuário normal](#Não_é_possível_editar_conexões_como_usuário_normal)
    *   [8.10 Esquecer rede sem fio oculta](#Esquecer_rede_sem_fio_oculta)
    *   [8.11 VPN não funciona no GNOME](#VPN_não_funciona_no_GNOME)
    *   [8.12 Impossibilidade de se conectar a redes sem fio europeias visíveis](#Impossibilidade_de_se_conectar_a_redes_sem_fio_europeias_visíveis)
    *   [8.13 Conexão automática a VPN na inicialização não funciona](#Conexão_automática_a_VPN_na_inicialização_não_funciona)
    *   [8.14 Gargalo no systemd](#Gargalo_no_systemd)
    *   [8.15 Desconexões de rede regulares, latência, pacotes perdidos (WiFi)](#Desconexões_de_rede_regulares,_latência,_pacotes_perdidos_(WiFi))
    *   [8.16 Impossibilidade de ligar o Wi-Fi com laptop Lenovo (IdeaPad, Legion, etc.)](#Impossibilidade_de_ligar_o_Wi-Fi_com_laptop_Lenovo_(IdeaPad,_Legion,_etc.))
    *   [8.17 Desligar envido de hostname](#Desligar_envido_de_hostname)
    *   [8.18 nm-applet desaparece no i3wm](#nm-applet_desaparece_no_i3wm)
    *   [8.19 Ícones de bandeja do nm-applet exibidos incorretamente](#Ícones_de_bandeja_do_nm-applet_exibidos_incorretamente)
    *   [8.20 Unit dbus-org.freedesktop.resolve1.service não encontrado](#Unit_dbus-org.freedesktop.resolve1.service_não_encontrado)
*   [9 Veja também](#Veja_também)

## Instalação

O NetworkManager pode ser [instalado](/index.php/Instala "Instala") com o pacote [networkmanager](https://www.archlinux.org/packages/?name=networkmanager), que contém um daemon, uma interface de linha de comando (`nmcli`) e uma interface baseada em curses (`nmtui`). Após a instalação, você deve [habilitar o daemon](#Habilitar_NetworkManager).

Interfaces adicionais:

*   [nm-connection-editor](https://www.archlinux.org/packages/?name=nm-connection-editor) para uma interface gráfica de usuário,
*   [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) para um miniaplicativo de bandeja de sistema (`nm-applet`).

**Nota:** Você deve garantir que nenhum outro serviço que deseje configurar a rede esteja em execução; na verdade, vários serviços de rede entrarão em conflito. Você pode encontrar uma lista dos serviços em execução no momento com `systemctl --type=service` e, em seguida, [parar](/index.php/Parar "Parar"). Veja [#Configuração](#Configuração) para ativar o serviço NetworkManager.

### Suporte a banda larga móvel

[Instale](/index.php/Instale "Instale") os pacotes [modemmanager](https://www.archlinux.org/packages/?name=modemmanager), [mobile-broadband-provider-info](https://www.archlinux.org/packages/?name=mobile-broadband-provider-info) e [usb_modeswitch](https://www.archlinux.org/packages/?name=usb_modeswitch) para um suporte a conexão de banda larga móvel. Veja [USB 3G Modem#NetworkManager](/index.php/USB_3G_Modem#NetworkManager "USB 3G Modem") para detalhes.

### Suporte a PPPoE / DSL

[Instale](/index.php/Instale "Instale") o pacote [rp-pppoe](https://www.archlinux.org/packages/?name=rp-pppoe) para suporte a conexão PPPoE/DSL. Para realmente adicionar uma conexão PPPoE, use `nm-connection-editor` e adicione uma nova conexão DSL/PPPoE.

### Suporte a VPN

O NetworkManager desde a versão 1.16 tem suporte nativo ao [WireGuard](/index.php/WireGuard "WireGuard"), veja o [WireGuard na publicação de blog do NetworkManager](https://blogs.gnome.org/thaller/2019/03/15/wireguard-in-networkmanager/).

O suporte para outros tipos de VPN é baseado em um sistema de plug-in. Eles são fornecidos nos seguintes pacotes:

*   [networkmanager-openconnect](https://www.archlinux.org/packages/?name=networkmanager-openconnect) para [OpenConnect](/index.php/OpenConnect_(Portugu%C3%AAs) "OpenConnect (Português)")
*   [networkmanager-openvpn](/index.php/Networkmanager-openvpn "Networkmanager-openvpn") para [OpenVPN](/index.php/OpenVPN "OpenVPN")
*   [networkmanager-pptp](https://www.archlinux.org/packages/?name=networkmanager-pptp) para [PPTP Client](/index.php/PPTP_Client "PPTP Client")
*   [networkmanager-vpnc](https://www.archlinux.org/packages/?name=networkmanager-vpnc) para [Vpnc](/index.php/Vpnc "Vpnc")
*   [networkmanager-strongswan](https://www.archlinux.org/packages/?name=networkmanager-strongswan) para [strongSwan](/index.php/StrongSwan "StrongSwan")
*   [networkmanager-fortisslvpn-git](https://aur.archlinux.org/packages/networkmanager-fortisslvpn-git/)
*   [networkmanager-iodine-git](https://aur.archlinux.org/packages/networkmanager-iodine-git/)
*   [networkmanager-libreswan](https://aur.archlinux.org/packages/networkmanager-libreswan/)
*   [networkmanager-l2tp](https://aur.archlinux.org/packages/networkmanager-l2tp/)
*   [networkmanager-ssh-git](https://aur.archlinux.org/packages/networkmanager-ssh-git/)
*   [network-manager-sstp](https://www.archlinux.org/packages/?name=network-manager-sstp)

**Atenção:** Suporte a VPN é [instável](https://bugzilla.gnome.org/buglist.cgi?quicksearch=networkmanager%20vpn), verifique as opções de processos daemon definidos via a GUI corretamente e certifique-se em cada lançamento do pacote.[[1]](https://bugzilla.gnome.org/show_bug.cgi?id=755350)

**Nota:** Pra ter uma resolução de DNS totalmente funcional ao usar VPN, você deve configurar [encaminhamento condicional](#Cache_de_DNS_e_encaminhamento_condicional).

## Uso

NetworkManager vem com [nmcli(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nmcli.1) e [nmtui(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nmtui.1).

### Exemplos de nmcli

Lista redes wifi próximas:

```
$ nmcli device wifi list

```

Conecta a uma rede wifi:

```
$ nmcli device wifi connect *SSID* password *senha*

```

Conecta a uma rede oculta:

```
$ nmcli device wifi connect *SSID* password *senha* hidden yes

```

Conecta a um wifi na interface de rede `wlan1`:

```
$ nmcli device wifi connect *SSID* password *senha* ifname wlan1 *nome_perfil*

```

Desconecta uma interface:

```
$ nmcli device disconnect ifname eth0

```

Reconecta uma interface marcada como desconectada:

```
$ nmcli connection up uuid *UUID*

```

Obtém uma lista de UUIDs:

```
$ nmcli connection show

```

Vê uma lista de dispositivos de rede e seus estados:

```
$ nmcli device

```

Desliga o wifi:

```
$ nmcli radio wifi off

```

### Editar uma conexão

Para uma lista compreensiva de configurações, veja [nm-settings(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nm-settings.5).

Em primeiro lugar você precisa obter lista de conexões:

 `$ nmcli connection` 
```
NAME                UUID                                  TYPE      DEVICE
Conexão cabeada 2   e7054040-a421-3bef-965d-bb7d60b7cecf  ethernet  enp5s0
Conexão cabeada 1   997f2782-f0fc-301d-bfba-15421a2735d8  ethernet  enp0s25
MEU-WIFI-DE-CASA    92a0f7b3-2eba-49ab-a899-24d83978f308  wifi       --

```

Aqui você pode usar a primeira coluna como ID de conexão usada posteriormente. Neste exemplo, escolhemos `Conexão cabeada 2` como um ID de conexão.

Você pode ter três métodos para configurar uma conexão após `Conexão cabeada 2` ter sido criada:

	Editor interativo do nmcli

	`nmcli connection edit *Conexão cabeada 2*`.
O uso está bem documentado no editor.

	Interface de linha de comando do nmcli

	`nmcli connection modify *Conexão cabeada 2* *definição*.*propriedade* *valor*`. Veja [nmcli(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nmcli.1) para seu uso. Por exemplo, você pode alterar sua métrica de rota IPv4 para 200 usando o comando `nmcli connection modify 'Conexão cabeada 2' ipv4.route-metric 200`.

	Arquivo de conexão

	Em `/etc/NetworkManager/system-connections/`, modifique o arquivo `*Conexão cabeada 2*.nmconnection` correspondente.
Não se esqueça de recarregar o arquivo de configuração com `nmcli connection reload`

## Front-ends

Para configurar e ter acesso fácil ao NetworkManager, a maioria dos usuários desejará instalar um applet. Esse front-end da GUI geralmente reside na bandeja do sistema (ou na área de notificação) e permite a seleção de rede e a configuração do NetworkManager. Vários ambientes de área de trabalho possuem seu próprio applet. Caso contrário, você pode usar [#nm-applet](#nm-applet).

### GNOME

O [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)") tem uma ferramenta embutida, acessível a partir das configurações de Rede.

### KDE Plasma

[Instale](/index.php/Instale "Instale") o pacote [plasma-nm](https://www.archlinux.org/packages/?name=plasma-nm). Em seguida, adicione-o à barra de tarefas do KDE por meio do menu *Opções de painel > Adicionar widgets > Redes*.

### nm-applet

[network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) é um front-end em GTK 3 que funciona sob ambientes Xorg com uma bandeja de sistema.

Para armazenar conexões secretas, instale e configure [GNOME/Keyring](/index.php/GNOME/Keyring "GNOME/Keyring").

Esteja ciente de que depois de ativar a opção caixa de seleção `Disponibilizar para outros usuários` para uma conexão, o NetworkManager armazena a senha em texto simples, embora o respectivo arquivo seja acessível apenas para root (ou outros usuários via `nm-applet`). Veja [#Senhas de Wi-Fi criptografadas](#Senhas_de_Wi-Fi_criptografadas).

Para executar `nm-applet` sem uma bandeja do sistema, você pode usar [trayer](https://www.archlinux.org/packages/?name=trayer) ou [stalonetray](https://www.archlinux.org/packages/?name=stalonetray). Por exemplo, você pode adicionar um script como este em seu caminho:

 `nmgui` 
```
#!/bin/sh
nm-applet    2>&1 > /dev/null &
stalonetray  2>&1 > /dev/null
killall nm-applet

```

Quando você fecha a janela *stalonetray*, ela fecha `nm-applet` também, então nenhuma memória extra é usada quando você terminar as configurações de rede.

O applet pode mostrar notificações de eventos, como conexão ou desconexão de uma rede WiFi. Para que essas notificações sejam exibidas, verifique se você tem um servidor de notificação instalado - consulte [Notificações na área de trabalho](/index.php/Desktop_notifications "Desktop notifications"). Se você usar o applet sem um servidor de notificação, poderá ver algumas mensagens em stdout/stderr e o aplicativo poderá ser interrompido. Veja [[2]](https://bugzilla.gnome.org/show_bug.cgi?id=788313).

Para executar `nm-applet` com tais notificações desabilitadas, inicie o miniaplicativo com o seguinte comando:

```
$ nm-applet --no-agent

```

**Dica:** `nm-applet` pode ser iniciado automaticamente com um [arquivo desktop de inicialização automática](/index.php/XDG_Autostart_(Portugu%C3%AAs) "XDG Autostart (Português)"), para adicionar a opção --no-agent, modifique a linha Exec, p.ex., `Exec=nm-applet --no-agent` 

#### Appindicator

O suporte do Appindicator está disponível em *nm-applet*, entretanto, ele não é compilado no pacote oficial, veja [FS#51740](https://bugs.archlinux.org/task/51740). Para usar o nm-applet em um ambiente Appindicator, substitua [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) por [network-manager-applet-indicator](https://aur.archlinux.org/packages/network-manager-applet-indicator/) e, em seguida, inicie o applet com o seguinte comando:

```
$ nm-applet --indicator

```

### networkmanager-dmenu

Como alternativa, existe o [networkmanager-dmenu-git](https://aur.archlinux.org/packages/networkmanager-dmenu-git/), que é um pequeno script para gerenciar as conexões do NetworkManager com o [dmenu](/index.php/Dmenu "Dmenu") ou [rofi](/index.php/Rofi "Rofi") em vez do `nm-applet`. Ele fornece todos os recursos essenciais, como conexão com conexões Wi-Fi ou com fio existentes do NetworkManager, conexão a novas conexões Wi-Fi, solicitações de senha, se necessário, conexão VPN existente, habilitação/desabilitação de rede e inicialização da interface gráfica *nm-connection-editor*, conexão a redes Bluetooth.

## Configuração

O NetworkManager exigirá algumas etapas adicionais para poder funcionar corretamente. Certifique-se de ter configurado `/etc/hosts` como descrito na seção [Configuração de rede#Configurando um hostname](/index.php/Configura%C3%A7%C3%A3o_de_rede#Configurando_um_hostname "Configuração de rede").

### Habilitar NetworkManager

O NetworkManager é [controlado](/index.php/Systemd_(Portugu%C3%AAs)#Usando_units "Systemd (Português)") com a unit de [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") `NetworkManager.service`. Depois que o daemon do NetworkManager for iniciado, ele se conectará automaticamente a qualquer "conexão do sistema" disponível que já tenha sido configurada. Quaisquer "conexões de usuário" ou conexões não configuradas precisarão de *nmcli* ou de um applet para configurar e conectar.

O NetworkManager possui um arquivo de configuração global em `/etc/NetworkManager/NetworkManager.conf`. Os arquivos de configuração de adição podem ser colocados em `/etc/NetworkManager/conf.d/`. Geralmente, nenhuma configuração precisa ser feita para os padrões globais.

### Habilitar NetworkManager Wait Online

Se você tiver serviços que falham se eles forem iniciados antes que a rede esteja ativa, você pode usar o `NetworkManager-wait-online.service` além do `NetworkManager.service`. Isso, no entanto, raramente é necessário porque a maioria dos daemons em rede é inicializada corretamente, mesmo que a rede ainda não tenha sido configurada.

Em alguns casos, o serviço ainda falhará ao iniciar com sucesso na inicialização devido à configuração de tempo limite em `/usr/lib/systemd/system/NetworkManager-wait-online.service` ser muito curta. Altere o tempo limite padrão de 30 para um valor mais alto.

### Configurar as permissões de PolicyKit

Veja [General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") para como configurar uma sessão de trabalho.

Com uma sessão de trabalho, você tem várias opções para conceder os privilégios necessários ao NetworkManager:

*   *Opção 1.* Execute um agente de autenticação [Polkit](/index.php/Polkit "Polkit") ao efetuar login, como `/usr/lib/polkit-gnome/polkit-gnome-authentication-agent-1` (parte do [polkit-gnome](https://www.archlinux.org/packages/?name=polkit-gnome)). Você será solicitado a fornecer sua senha sempre que adicionar ou remover uma conexão de rede.
*   *Opção 2.* [Adicione](/index.php/Usu%C3%A1rios_e_grupos#Gerenciamento_de_grupo "Usuários e grupos") a si próprio ao grupo `wheel`. Você não precisará inserir sua senha, mas a sua conta de usuário também poderá receber outras permissões, como a capacidade de usar o [sudo](/index.php/Sudo "Sudo") sem digitar a senha do root.
*   *Opção 3.* [Adicione](/index.php/Usu%C3%A1rios_e_grupos#Gerenciamento_de_grupo "Usuários e grupos") a si próprio ao grupo `network` e crie o seguinte arquivo:

 `/etc/polkit-1/rules.d/50-org.freedesktop.NetworkManager.rules` 
```
polkit.addRule(function(action, subject) {
  if (action.id.indexOf("org.freedesktop.NetworkManager.") == 0 && subject.isInGroup("network")) {
    return polkit.Result.YES;
  }
});

```

	Todos os usuários do grupo `network` poderão adicionar e remover redes sem uma senha. Isso não funcionará em [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") se você não tiver uma sessão ativa com *systemd-logind*.

### Configurações de proxy

O NetworkManager não lida diretamente com configurações de proxy, mas se você estiver usando o [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)") ou [KDE](/index.php/KDE_(Portugu%C3%AAs) "KDE (Português)"), você pode usar o [proxydriver](http://marin.jb.free.fr/proxydriver/) que lida com configurações de proxy usando Informações do NetworkManager. O proxydriver é encontrado no pacote [proxydriver](https://aur.archlinux.org/packages/proxydriver/).

Para que o *proxydriver* possa alterar as configurações do proxy, você precisaria executar este comando, como parte do processo de inicialização do GNOME (veja [GNOME (Português)#Inicialização automática](/index.php/GNOME_(Portugu%C3%AAs)#Inicialização_automática "GNOME (Português)")):

```
xhost +si:localuser:*nome_de_usuário*

```

Veja também as [configurações de proxy](/index.php/Proxy_settings "Proxy settings").

### Verificando conectividade

NetworkManager pode tentar alcançar uma página na Internet ao conectar a uma rede. [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) está configurado por padrão em `/usr/lib/NetworkManager/conf.d/20-connectivity.conf` para verificar a conectividade com o archlinux.org. Para usar um servidor web diferente ou desabilitar a verificação de conectividade, crie `/etc/NetworkManager/conf.d/20-connectivity.conf`, veja [NetworkManager.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/NetworkManager.conf.5#CONNECTIVITY_SECTION).

Para aqueles por trás de um [captive portal](https://en.wikipedia.org/wiki/Captive_portal "wikipedia:Captive portal"), o gerenciador de área de trabalhado pode abrir automaticamente uma janela pedindo por credenciais.

### Cliente DHCP

Por padrão, o NetworkManager usará seu cliente DHCP interno, baseado em systemd-networkd. Um novo cliente DHCP baseado em [nettools n-dhcp4](https://github.com/nettools/n-dhcp4) está sendo trabalhado atualmente, ele acabará se tornando o cliente DHCP `interno` substituindo aquele baseado no systemd-networkd. [[3]](https://gitlab.freedesktop.org/NetworkManager/NetworkManager/merge_requests/302)

Para usar um cliente DHCP diferente, [instale](/index.php/Instale "Instale") uma das alternativas:

*   [dhclient](https://www.archlinux.org/packages/?name=dhclient) - Cliente DHCP da ISC.
*   [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) - [dhcpcd](/index.php/Dhcpcd "Dhcpcd").

**Nota:**

*   NetworkManager não oferece suporte ao uso de dhcpcd para IPv6\. Veja [issue #5 do NetworkManager](https://gitlab.freedesktop.org/NetworkManager/NetworkManager/issues/5). Se dhcpcd está definido como o cliente DHCP, o NetworkManager vai usar o cliente DHCP interno para DHCPv6.
*   Não habilite as units de systemd fornecidas com os pacotes [dhclient](https://www.archlinux.org/packages/?name=dhclient) e [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd). Elas vão conflitar com o NetworkManager, veja a nota em [#Instalação](#Instalação) para detalhes.

Para alterar o backend do cliente DHCP, defina a opção `main.dhcp=*nome_cliente_dhcp*` com um arquivo de configuração em `/etc/NetworkManager/conf.d/`. Por exemplo:

 `/etc/NetworkManager/conf.d/dhcp-client.conf` 
```
[main]
dhcp=dhclient
```

### Gerenciamento de DNS

O gerenciamento de DNS do NetworkManager é descrito na página wiki do projeto GNOME — [Projects/NetworkManager/DNS](https://wiki.gnome.org/Projects/NetworkManager/DNS).

#### Cache de DNS e encaminhamento condicional

O NetworkManager possui um plugin para habilitar o cache DNS e encaminhamento condicional ([anteriormente](https://gitlab.freedesktop.org/NetworkManager/NetworkManager/merge_requests/143) chamado "DNS dividido" na documentação do NetworkManager) usando [dnsmasq](/index.php/Dnsmasq_(Portugu%C3%AAs) "Dnsmasq (Português)") ou [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved"), ou Unbound via dnssec-trigger. As vantagens dessa configuração são que as pesquisas de DNS serão armazenadas em cache, encurtando os tempos de resolução e as pesquisas de DNS dos hosts de VPN serão roteadas para os servidores DNS da VPN relevantes. Isso é especialmente útil se você estiver conectado a mais de uma VPN.

##### dnsmasq

Certifique-se que [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) está instalado. Então, defina `main.dns=dnsmasq` com um arquivo de configuração em `/etc/NetworkManager/conf.d/`:

 `/etc/NetworkManager/conf.d/dns.conf` 
```
[main]
dns=dnsmasq
```

Agora, [reinicie](/index.php/Reinicie "Reinicie") `NetworkManager.service`. NetworkManager vai iniciar automaticamente o dnsmasq e adicionar `127.0.0.1` ao `/etc/resolv.conf`. Os servidores DNS originais podem ser localizados no `/run/NetworkManager/no-stub-resolv.conf`. Você pode verificar se dnsmasq está sendo usado fazendo a mesma procura DNS duas vezes com `drill example.com` e verificando o servidor e tempos de consulta.

**Nota:**

*   Você não precisa iniciar `dnsmasq.service` ou editar `/etc/dnsmasq.conf`. O NetworkManager iniciará o dnsmasq sem usar o serviço systemd e sem ler o(s) arquivo(s) de configuração padrão do dnsmasq.
*   A instância do dnsmasq iniciada pelo NetworkManager será vinculada a `127.0.0.1:53`, você pode executar qualquer software (incluindo `dnsmasq.service`) no mesmo endereço e porta.

###### Configuração personalizada do dnsmasq

Configurações personalizadas podem ser criadas para o *dnsmasq* criando arquivos de configuração em `/etc/NetworkManager/dnsmasq.d/`. Por exemplo, para alterar o tamanho do cache DNS (armazenado na RAM):

 `/etc/NetworkManager/dnsmasq.d/cache.conf`  `cache-size=1000` 
**Dica:** Verifique a sintaxe do arquivo de configuração com `dnsmasq --test --conf-file=/dev/null --conf-dir=/etc/NetworkManager/dnsmasq.d`.

Veja [dnsmasq(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dnsmasq.8) para todas as opções disponíveis.

###### IPv6

Habilitar o `dnsmasq` no NetworkManager pode interromper as pesquisas de DNS somente do IPv6 (ou seja, `drill -6 [hostname`}) que, de outra forma, funcionariam. Para resolver isso, a criação do arquivo a seguir configurará o *dnsmasq* para também ouvir o loopback do IPv6:

 `/etc/NetworkManager/dnsmasq.d/ipv6_listen.conf`  `listen-address=::1` 

Além disso, o `dnsmasq` também não prioriza o DNS IPv6 upstream. Infelizmente, o NetworkManager não faz isso ([Bug do Ubuntu](https://bugs.launchpad.net/ubuntu/+source/network-manager/+bug/936712)). Uma solução alternativa seria desabilitar o DNS IPv4 na configuração do NetworkManager, supondo que exista.

###### DNSSEC

A instância dnsmasq iniciada pelo NetworkManager por padrão não validará [DNSSEC](/index.php/DNSSEC_(Portugu%C3%AAs) "DNSSEC (Português)") desde que seja iniciada com a opção `--proxy-dnssec`. Ele irá confiar em qualquer informação DNSSEC obtida do servidor DNS upstream.

Para que o dnsmasq valide corretamente o DNSSEC, quebrando assim a resolução de DNS com servidores de nomes que não suportam ele, crie o seguinte arquivo de configuração:

 `/etc/NetworkManager/dnsmasq.d/dnssec.conf` 
```
conf-file=/usr/share/dnsmasq/trust-anchors.conf
dnssec
```

##### systemd-resolved

O NetworkManager pode usar o [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved") como um resolvedor e cache de DNS. Certifique-se de que *systemd-resolved* esteja configurado corretamente e que `systemd-resolved.service` esteja [iniciado](/index.php/Iniciado "Iniciado") antes de usá-lo.

systemd-resolved vai ser usado automaticamente se `/etc/resolv.conf` é um [link simbólico](/index.php/Systemd-resolved#DNS "Systemd-resolved") para `/run/systemd/resolve/stub-resolv.conf`, `/run/systemd/resolve/resolv.conf` ou `/usr/lib/systemd/resolv.conf`.

Você pode habilitá-lo explicitamente definindo `main.dns=systemd-resolved` com um arquivo de configuração em `/etc/NetworkManager/conf.d/`:

 `/etc/NetworkManager/conf.d/dns.conf` 
```
[main]
dns=systemd-resolved
```

##### Resolvedor de DNS com um assinante do openresolv

Se o [openresolv](/index.php/Openresolv_(Portugu%C3%AAs) "Openresolv (Português)") tem um assinante para seu [resolvedor de DNS](/index.php/Resolvedor_de_DNS "Resolvedor de DNS") local, configure o assinante e [configure o NetworkManager para usar o openresolv](#Usar_openresolv).

Porque o NetworkManager anuncia uma única "interface" para o *resolvconf*, não é possível implementar encaminhamento condicional para conexões do NetworkManager. Veja [issue 153 do NetworkManager](https://gitlab.freedesktop.org/NetworkManager/NetworkManager/issues/153).

Isso pode ser parcialmente mitigado se você definir `private="*"` no `/etc/resolvconf.conf`[[4]](https://roy.marples.name/projects/openresolv/config). Quaisquer consultas por domínios que não estejam na lista de domínios de pesquisa não serão encaminhados. Elas serão tratadas conforme a configuração do resolvedor local. Por exemplo, encaminhadas para outro servidor DNS ou resolvidas recursivamente a partir da raiz do DNS.

#### Servidores DNS personalizados

##### Configurando servidores DNS globais personalizados

Para definir servidores DNS para todas as conexões, especifique-as em [NetworkManager.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/NetworkManager.conf.5) usando a sintaxe `servers=*endereçoservidorip1*,*endereçoservidorip2*,*endereçoservidorip3*` em uma seção chamada `[global-dns-domain-*]`. Por exemplo:

 `/etc/NetworkManager/conf.d/dns-servers.conf` 
```
[global-dns-domain-*]
servers=::1,127.0.0.1
```

**Nota:**

*   Se você usa [plugin de dnsmasq ou systemd-resolved do NetworkManager](#Cache_de_DNS_e_encaminhamento_condicional) ou [assinantes de openresolv](#Resolvedor_de_DNS_com_um_assinante_do_openresolv), então não especifique endereços de loopback com a opção `servers=`, pois isso pode quebrar a resolução de DNS.
*   Os servidores especificados não são enviados para [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved"), os servidores DNS da conexão são usados.

##### Configurando servidores DNS personalizados em uma conexão

###### Configurando servidores DNS personalizados em uma conexão (GUI)

A configuração vai depender do tipo de front-end usado; o processo geralmente envolve clicar com botão direito no miniaplicativo, editar (ou criar) um perfil e, então, escolher o tipo de DHCP como *Automático (especifique endereços)*. OS endereços DNS precisarão ser inseridos e são geralmente dessa formato: `127.0.0.1, *Servidor-DNS-um*, ...`.

###### Configurando servidores DNS personalizados em uma conexão (nmcli / arquivo de conexão)

Para configurar servidores DNS por conexão, você pode usar o campo `dns` (e os `dns-search` e `dns-options` associados) nas [configurações da conexão](#Editar_uma_conexão).

Se `method` estiver definido para `auto` (quando você usa DHCP), você precisa definir `ignore-auto-dns` para `yes`.

#### /etc/resolv.conf

Por padrão, `/etc/resolv.conf` é gerenciado pelo *NetworkManager* a menos que ele seja um link simbólico.

Ele pode ser configurado para escrever por meio do [openresolv](#Usar_openresolv) ou para [não tocar](#/etc/resolv.conf_não_gerenciado).

O uso do openresolv permite que o NetworkManager coexista com outro software com suporte a *resolvconf* ou, por exemplo, para executar um cache DNS local e um resolvedor de DNS dividido para o qual o openresolv tem um [assinante](/index.php/Openresolv_(Portugu%C3%AAs)#Assinantes "Openresolv (Português)").

**Nota:** Encaminhamento condicional [ainda não possui suporte completo](https://gitlab.freedesktop.org/NetworkManager/NetworkManager/issues/153) ao usar NetworkManager com openresolv.

O *NetworkManager* também oferece hooks via os scripts dispatchers que podem ser usados para alterar o `/etc/resolv.conf` após as alterações de rede. Veja [#Serviços de rede com o NetworkManager dispatcher](#Serviços_de_rede_com_o_NetworkManager_dispatcher) e [NetworkManager(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/NetworkManager.8) para mais informações.

**Nota:**

*   Se o NetworkManager estiver configurado para usar [dnsmasq](#dnsmasq) ou [systemd-resolved](#systemd-resolved), os endereços loopback apropriados serão escritos em `/etc/resolv.conf`.
*   O arquivo `resolv.conf` que o NetworkManager escreve, ou que escreveria em `/etc/resolv.conf`, pode ser encontrado em `/run/NetworkManager/resolv.conf`.
*   Um arquivo `resolv.conf` com os servidores de nome obtidos e domínios de pesquisa podem ser encontrados em `/run/NetworkManager/no-stub-resolv.conf`.

##### /etc/resolv.conf não gerenciado

Para evitar que o NetworkManager toque no `/etc/resolv.conf`, defina `main.dns=none` com um arquivo de configuração em `/etc/NetworkManager/conf.d/`:

 `/etc/NetworkManager/conf.d/dns.conf` 
```
[main]
dns=none
```

**Dica:** Você também pode querer definir `main.systemd-resolved=false`, de forma que o NetworkManager não envie a configuração DNS para [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved").

**Nota:** Veja [#Cache de DNS e encaminhamento condicional](#Cache_de_DNS_e_encaminhamento_condicional), para configurar o NetworkManager usando outros backends de DNS, como [dnsmasq](/index.php/Dnsmasq_(Portugu%C3%AAs) "Dnsmasq (Português)") e [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved"), em vez de usar `main.dns=none`.

Após isso, o `/etc/resolv.conf` pode ser um link simbólico quebrado que você precisará remover. Então, basta criar um novo arquivo `/etc/resolv.conf`.

##### Usar openresolv

**Nota:** Não defina `rc-manager=resolvconf` quando [systemd-resolvconf](https://www.archlinux.org/packages/?name=systemd-resolvconf) estiver instalado. *systemd-resolved* fornece suporte limitado à interface do *resolvconf* e o NetworkManager possui suporte a se comunicar com systemd-resolved por meio de D-Bus sem usar *resolvconf*.

Para configurar o NetworkManager para usar [openresolv](/index.php/Openresolv_(Portugu%C3%AAs) "Openresolv (Português)"), defina `main.rc-manager=resolvconf` com um arquivo de configuração em `/etc/NetworkManager/conf.d/`:

 `/etc/NetworkManager/conf.d/rc-manager.conf` 
```
[main]
rc-manager=resolvconf
```

## Serviços de rede com o NetworkManager dispatcher

Existem alguns serviços de rede que você não desejará executar até que o NetworkManager exiba uma interface. O NetworkManager tem a capacidade de iniciar serviços quando você se conecta a uma rede e os interrompe quando você desconecta (por exemplo, ao usar [NFS](/index.php/NFS "NFS"), [SMB](/index.php/SMB "SMB") e [NTPd](/index.php/NTPd "NTPd")).

Para ativar o recurso, você precisa [habilitar](/index.php/Habilitar "Habilitar") e [iniciar](/index.php/Inicia "Inicia") o `NetworkManager-dispatcher.service`.

Quando o serviço estiver ativo, os scripts poderão ser adicionados ao diretório `/etc/NetworkManager/dispatcher.d`.

Os scripts devem pertencer ao **root**, caso contrário o distribuidor não os executará. Para maior segurança, defina o [proprietário](/index.php/Propriet%C3%A1rio "Proprietário") e grupo para root:

```
# chown root:root /etc/NetworkManager/dispatcher.d/*10-script.sh*

```

Certifique-se que o arquivo tem as permissões corretas:

```
# chmod 755 /etc/NetworkManager/dispatcher.d/*10-script.sh*

```

Os scripts serão executados em ordem alfabética no momento da conexão e em ordem alfabética inversa no momento da desconexão. Para garantir a ordem em que aparecem, é comum usar caracteres numéricos antes do nome do script (por exemplo, `10-portmap` ou `30-netfs` (o que garante que *portmapper* esteja ativo antes que as montagens do NFS sejam tentadas).

Scripts vão receber os seguintes argumentos:

*   **Nome da interface:** p. ex., `eth0`
*   **Status da interface:** *up* ou *down*
*   **Status da VPN:** *vpn-up* ou *vpn-down*

**Atenção:** Se você se conectar a redes estrangeiras ou públicas, esteja ciente de quais serviços você está iniciando e quais servidores você espera que estejam disponíveis para eles se conectarem. Você pode criar uma falha de segurança iniciando os serviços errados enquanto estiver conectado a uma rede pública.

### Evitando o esgotamento de tempo limite do dispatcher

Se o acima está funcionando, então esta seção não é relevante. No entanto, há um problema geral relacionado à execução de scripts do dispatcher que demoram mais para serem executados. Inicialmente, foi utilizado um tempo limite interno de apenas três segundos. Se o script chamado não foi concluído a tempo, ele foi morto. Mais tarde, o tempo limite foi estendido para cerca de 20 segundos (veja o [Rastreador de erros](https://bugzilla.redhat.com/show_bug.cgi?id=982734) para mais informações). Se o tempo limite ainda criar o problema, uma solução alternativa poderá ser modificar o arquivo de serviço do distribuidor `/usr/lib/systemd/system/NetworkManager-dispatcher.service` para permanecer ativo após a saída:

 `/etc/systemd/system/NetworkManager-dispatcher.service.d/remain_after_exit.conf` 
```
[Service]
RemainAfterExit=yes
```

Agora, inicie e habilite o serviço modificado `NetworkManager-dispatcher` service.

**Atenção:** Adicionar a linha `RemainAfterExit` a ele impedirá que o dispatcher feche. Infelizmente, o dispatcher **tem** para fechar antes que possa executar seus scripts novamente. Com ele, o dispatcher não irá expirar, mas também não será fechado, o que significa que os scripts só serão executados uma vez por inicialização. Portanto, não adicione a linha a menos que o tempo limite esteja causando um problema.

### Exemplos de dispatcher

#### Montar pasta remota com sshfs

Como o script é executado em um ambiente muito restritivo, você precisa exportar `SSH_AUTH_SOCK` para se conectar ao seu agente SSH. Existem diferentes maneiras de conseguir isso, veja [esta mensagem](https://bbs.archlinux.org/viewtopic.php?pid=1042030#p1042030) para obter mais informações. O exemplo abaixo funciona com [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring"), e irá pedir a senha se você ainda não estiver desbloqueado. Caso o NetworkManager conecte-se automaticamente no login, é provável que o *gnome-keyring* ainda não tenha iniciado e a exportação irá falhar (daí o sleep). O `UUID` para correspondência pode ser encontrado com o comando `nmcli connection status` ou `nmcli connection list`.

```
#!/bin/sh
USER='nome_de_usuário'
REMOTE='usuário@host:/caminho/remoto'
LOCAL='/caminho/local'

interface=$1 status=$2
if [ "$CONNECTION_UUID" = "*uuid*" ]; then
  case $status in
    up)
      SSH_AUTH_SOCK=$(find /tmp -maxdepth 1 -type s -user "$USER" -name 'ssh')
      export SSH_AUTH_SOCK
      su "$USER" -c "sshfs $REMOTE $LOCAL"
      ;;
    down)
      fusermount -u "$LOCAL"
      ;;
  esac
fi

```

#### Montagem de compartilhamentos SMB

Alguns compartilhamentos [SMB](/index.php/SMB "SMB") estão disponíveis apenas em determinadas redes ou locais (por exemplo, em casa). Você pode usar o distribuidor para montar apenas compartilhamentos SMB que estejam presentes em seu local atual.

O script a seguir verificará se nos conectamos a uma rede específica e montamos os compartilhamentos de acordo:

 `/etc/NetworkManager/dispatcher.d/30-mount-smb.sh` 
```
#!/bin/sh

# Localiza o UUID de conexão com "nmcli connection show" no terminal.
# Todos os tipos de conexão do NetworkManager têm suporte: sem fio, VPN, com fio...
if [ "$2" = "up" ]; then
  if [ "$CONNECTION_UUID" = "uuid" ]; then
    mount /seu/ponto/de/montagem &
    # adicione mais compartilhamentos conforme necessário
  fi
fi

```

O script a seguir desmontará todos os compartilhamentos SMB antes de um software ter iniciado a desconexão de uma rede específica:

 `/etc/NetworkManager/dispatcher.d/pre-down.d/30-umount-smb.sh` 
```
#!/bin/sh

if [ "$CONNECTION_UUID" = "uuid" ]; then
  umount -a -l -t cifs
fi

```

**Nota:** Certifique-se de que este script esteja localizado no subdiretório `pre-down.d`, conforme mostrado acima, caso contrário, ele desmontará todos os compartilhamentos em qualquer alteração de estado de conexão.

O script a seguir tentará desmontar todos os compartilhamentos SMB após uma desconexão inesperada de uma rede específica:

 `/etc/NetworkManager/dispatcher.d/40-umount-smb.sh` 
```
#!/bin/sh

if [ "$CONNECTION_UUID" = "uuid" ]; then
  if [ "$2" = "down" ]; then
    umount -a -l -t cifs
  fi
fi

```

**Nota:**

*   Desde o NetworkManager 0.9.8, os eventos *pre-down* e *down* não são executados no desligamento ou reinicialização, veja [este relatório de erro](https://bugzilla.gnome.org/show_bug.cgi?id=701242) para mais informações.
*   Os scripts de *umount* anteriores ainda são propensos a deixar os aplicativos que realmente acessam a montagem para "travar".

Uma alternativa é usar o script como visto em [NFS#Using a NetworkManager dispatcher](/index.php/NFS#Using_a_NetworkManager_dispatcher "NFS"):

 `/etc/NetworkManager/dispatcher.d/30-smb.sh` 
```
#!/bin/bash

# Descubra O UUID da conexão com "nmcli con show" no terminal.
# Todos os tipos de conexão do NetworkManager têm suporte: wireless, VPN, wired...
WANTED_CON_UUID="CHANGE-ME-NOW-9c7eff15-010a-4b1c-a786-9b4efa218ba9"

if [[ "$CONNECTION_UUID" == "$WANTED_CON_UUID" ]]; then

    # Parâmetro do script $1: Nome da conexão do NetworkManager, não usado
    # Parâmetro do script $2: eventos despachado

    case "$2" in
        "up")
            mount -a -t cifs
            ;;
        "pre-down");&
        "vpn-pre-down")
            umount -l -a -t cifs >/dev/null
            ;;
    esac
fi

```

**Nota:** Este script ignora as montagens com a opção `noauto`, remove esta opção de montagem ou usa `auto` para permitir que o despachante gerencie essas montagens.

Crie um link simbólico dentro de `/etc/NetworkManager/dispatcher.d/pre-down` para pegar os eventos `pre-down`:

```
# ln -s /etc/NetworkManager/dispatcher.d/30-smb.sh /etc/NetworkManager/dispatcher.d/pre-down.d/30-smb.sh

```

#### Montagem de compartilhamentos NFS

Veja [NFS#Using a NetworkManager dispatcher](/index.php/NFS#Using_a_NetworkManager_dispatcher "NFS").

#### Usar dispatcher para ativar rede sem fio automaticamente dependendo de cabo LAN estar conectado

A ideia é ligar o Wi-Fi apenas quando o cabo LAN estiver desconectado (por exemplo, ao desconectá-lo de um laptop) e para que o Wi-Fi seja desativado automaticamente, assim que o cabo LAN for conectado novamente.

Crie o seguinte script de dispatcher ([Fonte](https://superuser.com/questions/233448/disable-wlan-if-wired-cable-network-is-available)), substituindo `LAN_interface` pelo seu.

 `/etc/NetworkManager/dispatcher.d/wlan_auto_toggle.sh` 
```
#!/bin/sh

if [ "$1" = "LAN_interface" ]; then
    case "$2" in
        up)
            nmcli radio wifi off
            ;;
        down)
            nmcli radio wifi on
            ;;
    esac
fi

```

**Nota:** Você obter uma lista de interfaces usando [nmcli](#Exemplos_de_nmcli). As interfaces ethernet (LAN) iniciam com `en`, p.ex., `enp0s5`

#### Usar dispatcher para conectar a uma VPN após uma conexão de rede ser estabelecida

Neste exemplo, queremos nos conectar automaticamente a uma conexão VPN definida anteriormente após a conexão a uma rede Wi-Fi específica. A primeira coisa a fazer é criar o script de dispatcher que define o que fazer depois de estarmos conectados à rede.

**Nota:** Esse script vai precisar de [wireless_tools](https://www.archlinux.org/packages/?name=wireless_tools) para usar `iwgetid`.
 `/etc/NetworkManager/dispatcher.d/vpn-up` 
```
#!/bin/sh
VPN_NAME="nome da conexão VPN definido no NetworkManager"
ESSID="ESSID da rede Wi-Fi (não o nome da conexão)"

interface=$1 status=$2
case $status in
  up|vpn-down)
    if iwgetid | grep -qs ":\"$ESSID\""; then
      nmcli connection up id "$VPN_NAME"
    fi
    ;;
  down)
    if iwgetid | grep -qs ":\"$ESSID\""; then
      if nmcli connection show --active | grep "$VPN_NAME"; then
        nmcli connection down id "$VPN_NAME"
      fi
    fi
    ;;
esac

```

Se você quiser se conectar automaticamente à VPN para todas as redes Wi-Fi, use a seguinte definição do ESSID: `ESSID=$(iwgetid -r)`. Lembre-se de definir as permissões do script [de acordo com isso](#Serviços_de_rede_com_o_NetworkManager_dispatcher).

A tentativa de se conectar com o script acima ainda pode falhar com `NetworkManager-dispatcher.service` reclamando sobre "nenhum segredo de VPN válido", por causa de [como os segredos VPN são armazenados](https://developer.gnome.org/NetworkManager/0.9/secrets-flags.html). Felizmente, existem diferentes opções para fornecer ao script acima acesso à sua senha de VPN.

1: Um deles requer a edição do arquivo de configuração de conexão VPN para fazer com que o NetworkManager armazene os segredos por si só, em vez de dentro de um chaveiro [que será inacessível por root](https://bugzilla.redhat.com/show_bug.cgi?id=710552): abra `/etc/NetworkManager/system-connections/*nome de sua conexão VPN*` e altere as `password-flags` e `secret-flags` de `1` para `0`.

Se isso não funcionar sozinho, talvez seja necessário criar um `passwd-file` em um local seguro com as mesmas permissões e propriedade que o script do dispatcher, contendo o seguinte:

 `/caminho/para/arquivo-passwd` 
```
vpn.secrets.password:SUA_SENHA

```

O script deve ser alterado de acordo, para que obtenha a senha do arquivo:

 `/etc/NetworkManager/dispatcher.d/vpn-up` 
```
#!/bin/sh
VPN_NAME="nome de conexão VPN definida no NetworkManager"
ESSID="ESSID de rede Wi-Fi (nenhum nome de conexão)"

interface=$1 status=$2
case $status in
  up|vpn-down)
    if iwgetid | grep -qs ":\"$ESSID\""; then
      nmcli connection up id "$VPN_NAME" passwd-file /path/to/passwd-file
    fi
    ;;
  down)
    if iwgetid | grep -qs ":\"$ESSID\""; then
      if nmcli connection show --active | grep "$VPN_NAME"; then
        nmcli connection down id "$VPN_NAME"
      fi
    fi
    ;;
esac

```

2: Alternativamente, altere a `password-flags` e coloque a senha diretamente no arquivo de configuração adicionando a seção `vpn-secrets`:

```
 [vpn]
 ....
 password-flags=0

 [vpn-secrets]
 password=*senha_senha*

```

**Nota:** Agora pode ser necessário reabrir o editor de conexão do NetworkManager e salvar as senhas/segredos da VPN novamente.

#### Usar dispatcher para desabilitar IPv6 em conexões de provedor de VPN

Muitos [provedores de VPN comercial](/index.php/Category:VPN_providers "Category:VPN providers") possuem suporte apenas a IPv4\. Isso significa que todo o tráfego IPv6 ignora a VPN e acaba por se tornar virtualmente desnecessário. Para evitar isso, o dispatcher pode ser usado para desabilitar todo o tráfego IPv5 para o período em que a conexão VPN está ativa.

 `/etc/NetworkManager/dispatcher.d/10-vpn-ipv6` 
```
#!/bin/sh

case "$2" in
    vpn-up)
        echo 1 > /proc/sys/net/ipv6/conf/all/disable_ipv6
        ;;
    vpn-down)
        echo 0 > /proc/sys/net/ipv6/conf/all/disable_ipv6
        ;;
esac

```

#### OpenNTPD

Veja [OpenNTPD#Using NetworkManager dispatcher](/index.php/OpenNTPD#Using_NetworkManager_dispatcher "OpenNTPD").

## Testando

Os miniaplicativos do NetworkManager são projetados para serem carregados no início da sessão, portanto, nenhuma configuração adicional deve ser necessária para a maioria dos usuários. Se você já desativou suas configurações de rede anteriores e desconectou-se da sua rede, agora pode testar se o NetworkManager funcionará. O primeiro passo é [iniciar](/index.php/Inicia "Inicia") `NetworkManager.service`.

Alguns miniaplicativos fornecerão um arquivo `.desktop` para que o miniaplicativo NetworkManager possa ser carregado através do menu do aplicativo. Se isso não acontecer, você terá que descobrir o comando para usar ou efetuar logout e efetuar login novamente para iniciar o miniaplicativo. Depois que o applet é iniciado, ele provavelmente começará a pesquisar conexões de rede com a autoconfiguração com um servidor DHCP.

Para iniciar o miniaplicativo do GNOME nos gerenciadores de janela não compatíveis com xdg, como [awesome](/index.php/Awesome "Awesome"):

```
nm-applet --sm-disable &

```

Para endereços IP estáticos, você terá que configurar o NetworkManager para entendê-los. O processo geralmente envolve clicar com o botão direito do mouse no applet e selecionar algo como 'Editar conexões'.

## Dicas e truques

### Senhas de Wi-Fi criptografadas

Por padrão, o NetworkManager armazena senhas em texto não criptografado nos arquivos de conexão em `/etc/NetworkManager/system-connections/`. Para imprimir as senhas armazenadas, use o seguinte comando:

```
# grep -H '^psk=' /etc/NetworkManager/system-connections/*

```

As senhas são acessíveis ao usuário root no sistema de arquivos e aos usuários com acesso às configurações através da GUI (por exemplo, `nm-applet`).

É preferível salvar as senhas em formato criptografado em um chaveiro, em vez de texto não criptografado. A desvantagem de usar um chaveiro é que as conexões precisam ser configuradas para cada usuário.

#### Usando GNOME Keyring

O daemon do conjunto de chaves deve ser iniciado e o chaveiro precisa ser desbloqueado para que o seguinte funcione.

Além disso, o NetworkManager precisa ser configurado para não armazenar a senha para todos os usuários. Usando o GNOME `nm-applet`, execute `nm-connection-editor` em um terminal, selecione uma conexão de rede, clique em `Editar`, selecione `Segurança Wi-Fi` e clique no ícone à direita da senha e marque `Armazenar a senha somente para este usuário`.

#### Usando KDE Wallet

Usando o [plasma-nm](https://www.archlinux.org/packages/?name=plasma-nm) do KDE, clique no applet, clique no ícone `Configurações` na parte superior direita, clique em uma conexão de rede, na guia `Configurações gerais`, desmarque `Todos os usuários podem se conectar nesta rede`. Se a opção estiver marcada, as senhas ainda serão armazenadas em texto não criptografado, mesmo que um daemon de chaveiro esteja em execução.

Se a opção foi selecionada anteriormente e você desmarcá-la, você pode ter que usar a opção `reset` primeiro para fazer a senha desaparecer do arquivo. Como alternativa, exclua a conexão primeiro e configure-a novamente.

### Compartilhando conexão internet pelo Wi-Fi

Você pode compartilhar sua conexão com a Internet (por exemplo, 3G ou com fio) com apenas alguns cliques. Você precisará de uma placa Wi-Fi (placas baseadas em Atheros AR9xx ou pelo menos AR5xx são provavelmente a melhor escolha). Por favor, note que um [firewall](/index.php/Firewall "Firewall") pode interferir no compartilhamento de internet.

[Instale](/index.php/Instale "Instale") o pacote [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) para poder realmente compartilhar a conexão.

Crie a conexão compartilhada:

*   Clique no miniaplicativo e escolha *Criar nova rede sem fio*.
*   Siga o assistente (se estiver usando WEP, certifique-se de usar uma senha com 5 a 13 caracteres, pois tamanhos diferentes falharão).
    *   Escolha [Hotspot](https://fedoraproject.org/wiki/Features/RealHotspot "fedora:Features/RealHotspot") ou Ad-hoc como modo Wi-Fi.

A conexão será salva e permanecerá armazenada para a próxima vez que você precisar dela.

**Nota:** O Android não possui suporte a conexão a redes ad-hoc. Para compartilhar uma conexão com o Android, use o modo infraestrutura (por exemplo, defina o modo Wi-Fi como "Hotspot").

### Compartilhando conexão internet por Ethernet

Cenário: o seu dispositivo está conectado à Internet através de wi-fi e pretende compartilhar a conexão à Internet a outros dispositivos através da rede ethernet.

Requisitos:

*   [Instale](/index.php/Instale "Instale") o pacote [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) para ser capaz de compartilhar a conexão.
*   Seu dispositivo conectado à internet e outros dispositivos estarem conectados por um cabo ethernet adequado (isso geralmente significa um cabo *cross* ou um switch entre eles).
*   Compartilhamento de Internet não estar bloqueado por um [firewall](/index.php/Firewall "Firewall").

Etapas:

*   Executar `nm-connection-editor` do terminal.
*   Adicionar uma nova conexão ethernet.
*   Dê um nome sensato. Por exemplo, "Internet compartilhada"
*   Acesse "Configurações IPv4".
*   Para "Método:" selecione "Compartilhado com outros computadores".
*   Salve

Agora, você deve ter uma nova opção "Internet compartilhada" sob as conexões cabeadas no NetworkManager.

### Verificando se a conectividade está ativa dentro de um script ou trabalho cron

Alguns trabalhos de *cron* exigem conectividade para serem bem-sucedidos. Você pode evitar a execução desses trabalhos quando a rede estiver inoperante. Para isso, adicione um teste **if** para redes que consulte a *nm-tool* do NetworkManager e verifique o estado da rede. O teste mostrado aqui é bem-sucedido se qualquer interface estiver ativa e falhará se todos estiverem inativos. Isso é conveniente para laptops que podem ser conectados, podem estar sem fio ou podem estar fora da rede.

```
if [ $(nm-tool|grep State|cut -f2 -d' ') == "connected" ]; then
    #Qualquer coisa que você deseje fazer se a rede estiver online
else
    #Qualquer coisa que você deseje fazer se a rede estiver offline - note, isso e qualquer outra coisa acima é opcional
fi

```

Isso é útil para um script `cron.hourly` que executa o *fpupdate* para a atualização da assinatura do scanner de vírus F-Prot, como exemplo. Outra maneira que pode ser útil, com uma pequena modificação, é diferenciar entre redes usando várias partes da saída do *nm-tool*; por exemplo, como a rede sem fio ativa é denotada com um asterisco, você pode usar o nome da rede e, em seguida, o grep para um asterisco literal.

### Conectar a uma rede com segredo na inicialização

Por padrão, o NetworkManager não se conectará a redes que exigem um segredo automaticamente na inicialização. Isso ocorre porque ele bloqueia essas conexões para o usuário que faz isso por padrão, conectando-se somente depois de terem efetuado login. Para alterar isso, faça o seguinte:

1.  Clique com o botão direito do mouse no ícone do `nm-applet` em seu painel e selecione Editar conexões e abra a guia Sem fio
2.  Selecione a conexão com a qual você deseja trabalhar e clique no botão Editar
3.  Marque as caixas "Conectar automaticamente" e "Disponível para todos os usuários"

Encerre e inicie novamente a sessão para completar.

### Desbloquear automaticamente o chaveiro após o login

O NetworkManager requer acesso ao chaveiro de login para se conectar a redes que exigem um segredo. Na maioria das circunstâncias, esse chaveiro é desbloqueado automaticamente no login, mas se não for, e o NetworkManager não está se conectando no login, você pode tentar o seguinte.

#### GNOME

*   No `/etc/pam.d/gdm` (ou seu daemon correspondente no `/etc/pam.d`), adicione estas linhas no final dos blocos "auth" e "session" se eles ainda não existirem:

```
 auth            optional        pam_gnome_keyring.so
 session         optional        pam_gnome_keyring.so  auto_start

```

*   No `/etc/pam.d/passwd`, use essa linha para o bloco "password":

```
 password    optional    pam_gnome_keyring.so

```

	Na próxima vez que fizer login, você deverá ser perguntado se deseja que a senha seja desbloqueada automaticamente no login.

#### Gerenciador de login SLiM

Veja [SLiM#Gnome Keyring](/index.php/SLiM#Gnome_Keyring "SLiM").

### OpenConnect com senha no KWallet

Enquanto você pode digitar os dois valores no momento da conexão, o [plasma-nm](https://www.archlinux.org/packages/?name=plasma-nm) 0.9.3.2-1 e acima são capazes de obter o nome de usuário e a senha do OpenConnect diretamente do [KWallet](/index.php/KWallet "KWallet").

Abra o "Gerenciador de carteiras do KDE" e procure a sua conexão OpenConnect VPN em "Gerenciamento de rede | Mapas". Clique em "Mostrar valores" e insira suas credenciais na chave "VpnSecrets" neste formulário (substitua "nome_de_usuário" e "senha"):

```
form:main:username%SEP%*nome_de_usuário*%SEP%form:main:password%SEP%*senha*

```

Da próxima vez que você se conectar, o nome de usuário e a senha deverão aparecer na caixa de diálogo "Segredos de VPN".

### Ignorar dispositivos específicos

Às vezes, pode ser desejado que o NetworkManager ignore dispositivos específicos e não tente configurar endereços e rotas para eles. Você pode rapidamente e facilmente ignorar dispositivos por MAC ou por nome de interface usando o seguinte em `/etc/NetworkManager/conf.d/unmanaged.conf`:

```
[keyfile]
unmanaged-devices=mac:00:22:68:1c:59:b1;mac:00:1E:65:30:D1:C4;interface-name:eth0

```

Depois de colocar isso, [reinicie](/index.php/Reinicie "Reinicie") o `NetworkManager.service`, e você deve ser capaz de configurar interfaces sem o NetworkManager alterar o que você definiu.

### Configurando aleatorização de endereço MAC

**Nota:** Desabilitar a aleatorização de endereço MAC pode ser necessário para obter uma conexão de link (estável) [[5]](https://bbs.archlinux.org/viewtopic.php?id=220101) e/ou redes que restrinjam dispositivos com base em seu endereço MAC ou tenham uma rede de limite capacidade.

A aleatorização de MAC pode ser usada para aumentar a privacidade, não revelando seu endereço MAC real à rede.

O NetworkManager oferece suporte a dois tipos de aleatorização de endereços MAC: aleatorização durante a digitalização e para conexões de rede. Ambos os modos podem ser configurados modificando o `/etc/NetworkManager/NetworkManager.conf` ou criando um arquivo de configuração separado no `/etc/NetworkManager/conf.d/`, que é recomendado já que o primeiro arquivo de configuração acima pode ser substituído pelo NetworkManager.

A aleatorização durante a varredura de Wi-Fi é ativada por padrão, mas pode ser desativada adicionando as seguintes linhas ao `/etc/NetworkManager/NetworkManager.conf` ou a um arquivo de configuração dedicado em `/etc/NetworkManager/conf.d`:

 `/etc/NetworkManager/conf.d/wifi_rand_mac.conf` 
```
[device]
wifi.scan-rand-mac-address=no
```

A aleatorização de MAC para conexões de rede pode ser definida para modos diferentes para interfaces sem fio e Ethernet. Veja a [publicação de blog do GNOME](https://blogs.gnome.org/thaller/2016/08/26/mac-address-spoofing-in-networkmanager-1-4-0/) para mais detalhes sobre os diferentes modos.

Em termos de aleatorização de MAC, os modos mais importantes são `stable` e `random`. `stable` gera um endereço MAC aleatório quando você se conecta a uma nova rede e associa os dois permanentemente. Isso significa que você usará o mesmo endereço MAC sempre que se conectar a essa rede. Em contraste, `random` irá gerar um novo endereço MAC toda vez que você se conectar a uma rede, nova ou previamente conhecida. Você pode configurar a aleatorização do MAC adicionando a configuração desejada em `/etc/NetworkManager/conf.d`:

 `/etc/NetworkManager/conf.d/wifi_rand_mac.conf` 
```
[device-mac-randomization]
# "yes" já é o padrão para fazer varredura
wifi.scan-rand-mac-address=yes

[connection-mac-randomization]
# Aleatoriza o MAC para cada conexão ethernet
ethernet.cloned-mac-address=random
# Gera um MAC aleatório para cada WiFi e associa a dois permanentemente.
wifi.cloned-mac-address=stable
```

Veja a seguinte [publicação de blog do GNOME](https://blogs.gnome.org/thaller/2016/08/26/mac-address-spoofing-in-networkmanager-1-4-0/) para mais detalhes.

### Habilitar extensões de privacidade IPv6

Veja [IPv6 (Português)#NetworkManager](/index.php/IPv6_(Portugu%C3%AAs)#NetworkManager "IPv6 (Português)").

### Trabalhando com conexões cabeadas

Por padrão, o NetworkManager gera um perfil de conexão para cada conexão Ethernet com fio que encontrar. No momento em que gera a conexão, ele não sabe se haverá mais adaptadores Ethernet disponíveis. Por isso, ele chama a primeira conexão com fio "Conexão cabeada 1". Você pode evitar gerar essa conexão, configurando `no-auto-default` (consulte [NetworkManager.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/NetworkManager.conf.5)) ou simplesmente excluindo-a. Em seguida, o NetworkManager se lembrará de não gerar uma conexão para essa interface novamente.

Você também pode editar a conexão (e persistir no disco) ou excluí-la. O NetworkManager não irá gerar novamente uma nova conexão. Então, você pode mudar o nome para o que você quiser. Você pode usar algo como o *nm-connection-editor* para esta tarefa.

### Usando iwd como o backend de Wi-Fi

Instale [networkmanager-iwd](https://aur.archlinux.org/packages/networkmanager-iwd/) ou habilite o backend experimental [iwd](/index.php/Iwd "Iwd") criando o seguinte arquivo de configuração:

 `/etc/NetworkManager/conf.d/wifi_backend.conf` 
```
[device]
wifi.backend=iwd
```

## Solução de problemas

### Nenhum prompt para senha de redes Wi-Fi seguras

Ao tentar se conectar a uma rede Wi-Fi protegida, nenhum prompt de senha é exibido e nenhuma conexão é estabelecida. Isso acontece quando nenhum pacote de chaveiro é instalado. Uma solução fácil é instalar o [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring). Se você quiser que as senhas sejam armazenadas em formato criptografado, siga [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring") para configurar o *gnome-keyring-daemon*.

### Nenhum tráfego via túnel PPTP

Logins de conexão PPTP com êxito; você vê uma interface ppp0 com o endereço IP da VPN correto, mas não é possível efetuar o ping do endereço IP remoto. É devido à falta de suporte MPPE (Microsoft Point-to-Point Encryption) no arquivo Arch pppd. Recomenda-se primeiro tentar com o [ppp](https://www.archlinux.org/packages/?name=ppp) padrão do Arch, pois pode funcionar como pretendido.

Para resolver o problema, deve ser suficiente instalar o pacote [ppp-mppe](https://aur.archlinux.org/packages/ppp-mppe/).

Veja também [WPA2 Empresarial#MS-CHAPv2](/index.php/WPA2_Empresarial#MS-CHAPv2 "WPA2 Empresarial").

### Gerenciamento de rede desabilitado

Quando o NetworkManager for desligado, mas o arquivo pid (estado) não for removido, você verá uma mensagem `Network management disabled`. Se isso acontecer, remova o arquivo manualmente:

```
# rm /var/lib/NetworkManager/NetworkManager.state

```

### Problemas com cliente DHCP interno

Se você tiver problemas para obter um endereço IP usando o cliente DHCP interno, considere usar outro cliente DHCP, consulte [#Cliente DHCP](#Cliente_DHCP) para obter instruções. Essa solução alternativa pode resolver problemas em grandes redes sem fio, como o eduroam.

### Problemas DHCP com dhclient

Se você tiver problemas ao obter um endereço IP via DHCP, tente adicionar o seguinte ao seu `/etc/dhclient.conf`:

```
 interface "eth0" {
   send dhcp-client-identifier 01:*aa:bb:cc:dd:ee:ff*;
 }

```

sendo `*aa:bb:cc:dd:ee:ff*` o endereço MAC desta NIC. O endereço MAC pode ser localizado usando o comando `ip link show *interface*` com o pacote [iproute2](https://www.archlinux.org/packages/?name=iproute2).

### Modem 3G não detectado

Veja [USB 3G Modem#NetworkManager](/index.php/USB_3G_Modem#NetworkManager "USB 3G Modem").

### Desligando WLAN em laptops

Às vezes o NetworkManager não funciona quando você desabilita o seu adaptador Wi-Fi com um botão em seu laptop e tenta habilitá-lo novamente depois. Isso geralmente é um problema com *rfkill*. Para verificar se o driver notifica *rfkill* sobre o status do adaptador sem fio, use:

```
$ watch -n1 rfkill list all

```

Se um identificador permanecer bloqueado depois de ligar o adaptador, você pode tentar desbloqueá-lo manualmente (onde X é o número do identificador fornecido pela saída acima):

```
# rfkill event unblock X

```

### Reversão de configurações de endereço IP estático para DHCP

Devido a um erro não resolvido, ao alterar as conexões padrão para um endereço IP estático, o `nm-applet` pode não armazenar adequadamente a alteração de configuração e voltará ao DHCP automático.

Para contornar este problema você tem que editar a conexão padrão (por exemplo, "Auto eth0") em `nm-applet`, alterar o nome da conexão (por exemplo "meu eth0"), desmarque a caixa de seleção "Disponível para todos os usuários", altere suas configurações de endereço IP estático conforme desejado e clique em **Aplicar**. Isso salvará uma nova conexão com o nome fornecido.

Em seguida, você desejará fazer com que a conexão padrão não seja conectada automaticamente. Para fazer isso, execute `nm-connection-editor` (**não** como root). No editor de conexão, edite a conexão padrão (por exemplo, "Auto eth0") e desmarque "Conectar automaticamente". Clique em **Aplicar** e feche o editor de conexão.

### Não é possível editar conexões como usuário normal

Veja [#Configurar as permissões de PolicyKit](#Configurar_as_permissões_de_PolicyKit).

### Esquecer rede sem fio oculta

Como as redes ocultas não são exibidas na lista de seleção da tela de redes sem fio, elas não podem ser esquecidas (removidas) com a GUI. Você pode excluir um com o seguinte comando:

```
# rm /etc/NetworkManager/system-connections/*SSID*

```

Isso funciona para qualquer outra conexão.

### VPN não funciona no GNOME

Ao configurar conexões OpenConnect ou vpnc no NetworkManager enquanto estiver usando o GNOME, você algumas vezes nunca verá a caixa de diálogo aparecer e o seguinte erro aparecerá em `/var/log/errors.log`:

```
localhost NetworkManager[399]: <error> [1361719690.10506] [nm-vpn-connection.c:1405] get_secrets_cb(): Failed to request VPN secrets #3: (6) No agents were available for this request.

```

Isso é causado pelo fato do miniaplicativo de NM do GNOME esperar que os scripts de diálogo estejam em `/usr/lib/gnome-shell`, quando os pacotes do NetworkManager os colocam em `/usr/lib/networkmanager`. Como uma correção "temporária" (este bug já existe há algum tempo), faça os seguintes links simbólicos:

*   Para OpenConnect: `ln -s /usr/lib/networkmanager/nm-openconnect-auth-dialog /usr/lib/gnome-shell/`
*   Para VPNC (isto é, Cisco VPN): `ln -s /usr/lib/networkmanager/nm-vpnc-auth-dialog /usr/lib/gnome-shell/`

Isso pode precisar ser feito para qualquer outro plug-in de VPN do NM, mas esses são os dois mais comuns.

### Impossibilidade de se conectar a redes sem fio europeias visíveis

Os chips WLAN são fornecidos com um padrão [domínio regulatório](/index.php/Configura%C3%A7%C3%A3o_de_rede_sem_fio#Respeitar_o_domínio_regulatório "Configuração de rede sem fio"). Se o seu ponto de acesso não operar dentro dessas limitações, você não conseguirá se conectar à rede. Consertar isso é fácil:

1.  [Instale](/index.php/Instale "Instale") [crda](https://www.archlinux.org/packages/?name=crda)
2.  Descomente o código de país correto em `/etc/conf.d/wireless-regdom`
3.  Reinicie o sistema, pois a configuração está como somente leitura na inicialização

### Conexão automática a VPN na inicialização não funciona

O problema ocorre quando o sistema (ou seja, o NetworkManager em execução como usuário root) tenta estabelecer uma conexão VPN, mas a senha não está acessível porque está armazenada no GNOME Keyring de um usuário específico.

Uma solução é manter a senha em sua VPN em texto simples, conforme descrito na etapa (2.) de [#Usar dispatcher para conectar a uma VPN após uma conexão de rede ser estabelecida](#Usar_dispatcher_para_conectar_a_uma_VPN_após_uma_conexão_de_rede_ser_estabelecida).

Você não precisa mais usar o dispatcher descrito na etapa (1.) para se conectar automaticamente, se você usar a nova opção "autoconectar VPN" na interface gráfica do `nm-applet`.

### Gargalo no systemd

Com o tempo, os arquivos de log (`/var/log/journal`) podem se tornar muito grandes. Isso pode ter um grande impacto no desempenho da inicialização ao usar o NetworkManager, consulte: [Systemd (Português)#Tempo de inicialização aumentando com o tempo](/index.php/Systemd_(Portugu%C3%AAs)#Tempo_de_inicialização_aumentando_com_o_tempo "Systemd (Português)").

### Desconexões de rede regulares, latência, pacotes perdidos (WiFi)

O NetworkManager faz uma varredura a cada 2 minutos.

Alguns drivers de WiFi apresentam problemas ao procurar estações base enquanto conectados/associados. Os sintomas incluem desconexões/reconexões de VPN e perda de pacotes, páginas da Web que não podem ser carregadas e, em seguida, atualizadas corretamente.

A execução `journalctl -f` indicará que isso está ocorrendo, mensagens como as seguintes estarão contidas nos logs em intervalos regulares.

```
NetworkManager[410]: <info>  (wlp3s0): roamed from BSSID 00:14:48:11:20:CF (my-wifi-name) to (none) ((none))

```

Existe uma versão corrigida do NetworkManager que deve evitar esse tipo de verificação: [networkmanager-noscan](https://aur.archlinux.org/packages/networkmanager-noscan/).

Como alternativa, se o roaming não for importante, o comportamento de varredura periódica poderá ser desabilitado bloqueando o BSSID do ponto de acesso no perfil de conexão WiFi.

### Impossibilidade de ligar o Wi-Fi com laptop Lenovo (IdeaPad, Legion, etc.)

Há um problema com o módulo `ideapad_laptop` em alguns modelos da Lenovo, devido ao driver wi-fi relatar incorretamente um bloco virtual. A placa ainda pode ser manipulada com `netctl`, mas os gerenciadores como o NetworkManager quebram. Você pode verificar se este é o problema, verificando a saída de `rfkill list` depois de alternar sua chave de hardware e ver que o bloco de software persiste.

[Descarregar](/index.php/Kernel_module_(Portugu%C3%AAs)#Manuseio_de_módulos_de_kernel "Kernel module (Português)") o módulo `ideapad_laptop` deve corrigir isso. (**atenção**: isso também pode desabilitar o teclado e o touchpad do laptop!).

### Desligar envido de hostname

O NetworkManager, por padrão, envia o nome do host para o servidor DHCP. O envio de nome de host só pode ser desativado por conexão não globalmente ([Bug 768076 do GNOME](https://bugzilla.gnome.org/show_bug.cgi?id=768076)).

Para desabilitar o envio do seu nome de host para o servidor DHCP para uma conexão específica, adicione o seguinte ao seu arquivo de conexão de rede:

 `/etc/NetworkManager/system-connections/*seu_arquivo_de_conexão*` 
```
...
[ipv4]
dhcp-send-hostname=false
...
[ipv6]
dhcp-send-hostname=false
...
```

### nm-applet desaparece no i3wm

Se você usar o `xfce4-notifyd.service` para notificações, deverá [editar](/index.php/Editar "Editar") a unidade e adicionar o seguinte:

 `/etc/systemd/user/xfce4-notifyd.service.d/display_env.conf` 
```
[Service]
Environment="DISPLAY=:0.0"
```

Depois de recarregar os daemons, [reinicie](/index.php/Reinicie "Reinicie") o `xfce4-notifyd.service`. Saia do i3 e reinicie-o novamente, e o miniaplicativo deverá aparecer na área de notificação.

### Ícones de bandeja do nm-applet exibidos incorretamente

Atualmente, os ícones da área de notificação do nm-applet são desenhados uns em cima dos outros, ou seja, o ícone exibindo a força sem fio pode ser exibido na parte superior do ícone, indicando que não há conexão com fio. Isso aparentemente é um problema/bug do GTK3: [https://gitlab.gnome.org/GNOME/gtk/issues/1280](https://gitlab.gnome.org/GNOME/gtk/issues/1280) .

Uma versão corrigida do GTK3 existe no AUR, que aparentemente corrige o erro do ícone da área de notificação: [gtk3-mushrooms](https://aur.archlinux.org/packages/gtk3-mushrooms/) .

### Unit dbus-org.freedesktop.resolve1.service não encontrado

Se `systemd-resolved.service` não tiver sido iniciado, NetworkManager vai tentar iniciá-lo usando D-Bus e vai falhar:

```
dbus-daemon[991]: [system] Activating via systemd: service name='org.freedesktop.resolve1' unit='dbus-org.freedesktop.resolve1.service' requested by ':1.23' (uid=0 pid=1012 comm="/usr/bin/NetworkManager --no-daemon ")
dbus-daemon[991]: [system] Activation via systemd failed for unit 'dbus-org.freedesktop.resolve1.service': Unit dbus-org.freedesktop.resolve1.service not found.
dbus-daemon[991]: [system] Activating via systemd: service name='org.freedesktop.resolve1' unit='dbus-org.freedesktop.resolve1.service' requested by ':1.23' (uid=0 pid=1012 comm="/usr/bin/NetworkManager --no-daemon ")

```

Isso é porque o NetworkManager vai tentar enviar informações DNS para [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved") independentemente da configuração `main.dns=` no [NetworkManager.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/NetworkManager.conf.5).[[6]](https://gitlab.freedesktop.org/NetworkManager/NetworkManager/commit/d4eb4cb45f41b1751cacf71da558bf8f0988f383)

Isso pode ser desabilitado com um arquivo de configuração em `/etc/NetworkManager/conf.d/`:

 `/etc/NetworkManager/conf.d/no-systemd-resolved.conf` 
```
[main]
systemd-resolved=false
```

Veja [FS#62138](https://bugs.archlinux.org/task/62138).

## Veja também

*   [NetworkManager para Administradores Parte 1](https://blogs.gnome.org/dcbw/2015/02/16/networkmanager-for-administrators-part-1/)
*   [Wikipedia:pt:NetworkManager](https://en.wikipedia.org/wiki/pt:NetworkManager "wikipedia:pt:NetworkManager")