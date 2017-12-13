Artigos relacionados

*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Display manager (Português)](/index.php/Display_manager_(Portugu%C3%AAs) "Display manager (Português)")
*   [Window manager](/index.php/Window_manager "Window manager")
*   [GTK+](/index.php/GTK%2B "GTK+")
*   [GDM (Português)](/index.php/GDM_(Portugu%C3%AAs) "GDM (Português)")
*   [GNOME/Tips and tricks](/index.php/GNOME/Tips_and_tricks "GNOME/Tips and tricks")
*   [GNOME/Troubleshooting](/index.php/GNOME/Troubleshooting "GNOME/Troubleshooting")
*   [GNOME/Files](/index.php/GNOME/Files "GNOME/Files")
*   [GNOME/Gedit](/index.php/GNOME/Gedit "GNOME/Gedit")
*   [GNOME/Web](/index.php/GNOME/Web "GNOME/Web")
*   [GNOME/Evolution](/index.php/GNOME/Evolution "GNOME/Evolution")
*   [GNOME/Flashback](/index.php/GNOME/Flashback "GNOME/Flashback")
*   [GNOME/Keyring](/index.php/GNOME/Keyring "GNOME/Keyring")
*   [GNOME/Document viewer](/index.php/GNOME/Document_viewer "GNOME/Document viewer")
*   [Cinnamon](/index.php/Cinnamon "Cinnamon")
*   [MATE](/index.php/MATE "MATE")
*   [Official repositories (Português)#gnome-unstable](/index.php/Official_repositories_(Portugu%C3%AAs)#gnome-unstable "Official repositories (Português)")

[GNOME](https://www.gnome.org/) (pronunciado *gah-nohm* ou *nohm*) é um [ambiente de desktop](/index.php/Desktop_environment "Desktop environment"), ou *desktop environment*, que visa ser simples e fácil de usar. Ele é projetado por [O Projeto GNOME](https://en.wikipedia.org/wiki/The_GNOME_Project "wikipedia:The GNOME Project") e é composto interiramente de software livre e código aberto. O GNOME é uma parte do [Projeto GNU](https://en.wikipedia.org/wiki/pt:Projeto_GNU "wikipedia:pt:Projeto GNU"). O *display* padrão é o [Wayland](/index.php/Wayland "Wayland") em vez do [Xorg](/index.php/Xorg "Xorg").

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
    *   [1.1 Pacotes adicionais](#Pacotes_adicionais)
*   [2 Sessões do GNOME](#Sess.C3.B5es_do_GNOME)
*   [3 Iniciando o GNOME](#Iniciando_o_GNOME)
    *   [3.1 Graficamente](#Graficamente)
    *   [3.2 Manualmente](#Manualmente)
        *   [3.2.1 Sessões Xorg](#Sess.C3.B5es_Xorg)
        *   [3.2.2 Sessões Wayland](#Sess.C3.B5es_Wayland)
    *   [3.3 Aplicativos do GNOME no Wayland](#Aplicativos_do_GNOME_no_Wayland)
*   [4 Navegação](#Navega.C3.A7.C3.A3o)
    *   [4.1 Nomes legados](#Nomes_legados)
*   [5 Configuração](#Configura.C3.A7.C3.A3o)
    *   [5.1 Configurações do sistema](#Configura.C3.A7.C3.B5es_do_sistema)
        *   [5.1.1 Cor](#Cor)
        *   [5.1.2 Data & hora](#Data_.26_hora)
        *   [5.1.3 Aplicativos padrões](#Aplicativos_padr.C3.B5es)
        *   [5.1.4 Mouse e touchpad](#Mouse_e_touchpad)
        *   [5.1.5 Rede](#Rede)
        *   [5.1.6 Contas on-line](#Contas_on-line)
        *   [5.1.7 Pesquisa](#Pesquisa)
    *   [5.2 Configurações avançadas](#Configura.C3.A7.C3.B5es_avan.C3.A7adas)
        *   [5.2.1 Aparência](#Apar.C3.AAncia)
            *   [5.2.1.1 Temas GTK+ e temas de ícone](#Temas_GTK.2B_e_temas_de_.C3.ADcone)
                *   [5.2.1.1.1 Tema global escuro](#Tema_global_escuro)
            *   [5.2.1.2 Temas de gerenciador de janelas](#Temas_de_gerenciador_de_janelas)
                *   [5.2.1.2.1 Altura da barra de título](#Altura_da_barra_de_t.C3.ADtulo)
                *   [5.2.1.2.2 Ordem de botão de barra de título](#Ordem_de_bot.C3.A3o_de_barra_de_t.C3.ADtulo)
                *   [5.2.1.2.3 Ocultar barra de título quando maximizado](#Ocultar_barra_de_t.C3.ADtulo_quando_maximizado)
            *   [5.2.1.3 Temas do GNOME Shell](#Temas_do_GNOME_Shell)
            *   [5.2.1.4 Ícones no menu](#.C3.8Dcones_no_menu)
        *   [5.2.2 Área de trabalho](#.C3.81rea_de_trabalho)
            *   [5.2.2.1 Ícones na área de trabalho](#.C3.8Dcones_na_.C3.A1rea_de_trabalho)
            *   [5.2.2.2 Tela de bloqueio e plano de fundo](#Tela_de_bloqueio_e_plano_de_fundo)
        *   [5.2.3 Extensões](#Extens.C3.B5es)
        *   [5.2.4 Métodos de entrada](#M.C3.A9todos_de_entrada)
        *   [5.2.5 Fontes](#Fontes)
        *   [5.2.6 Inicialização de aplicativos](#Inicializa.C3.A7.C3.A3o_de_aplicativos)
        *   [5.2.7 Energia](#Energia)
            *   [5.2.7.1 Configurar o comportamento do fechamento da tela de notebook](#Configurar_o_comportamento_do_fechamento_da_tela_de_notebook)
            *   [5.2.7.2 Alterar ação de nível crítico da bateria](#Alterar_a.C3.A7.C3.A3o_de_n.C3.ADvel_cr.C3.ADtico_da_bateria)
        *   [5.2.8 Ordenar aplicativos em pastas de aplicativo (app)](#Ordenar_aplicativos_em_pastas_de_aplicativo_.28app.29)
*   [6 Veja também](#Veja_tamb.C3.A9m)

## Instalação

Dois grupos estão disponíveis:

*   [gnome](https://www.archlinux.org/groups/x86_64/gnome/) contém o ambiente base do GNOME e um subconjunto de [aplicativos](https://wiki.gnome.org/Apps) bem integrados;
*   [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/) contém mais aplicativos do GNOME, incluindo um gerenciador de pacote, gerenciador de disco, [editor de texto](/index.php/Gedit "Gedit") e um conjunto de jogos. Note que esse grupo compila no grupo [gnome](https://www.archlinux.org/groups/x86_64/gnome/).

O ambiente base consiste no [GNOME Shell](https://en.wikipedia.org/wiki/GNOME_Shell "wikipedia:GNOME Shell"), um plug-in para o gerenciador de janelas [Mutter](https://en.wikipedia.org/wiki/Mutter_(software) "wikipedia:Mutter (software)"). Ele pode ser instalado separadamente com [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell).

**Nota:** *mutter* age como um gerenciador de composição para o ambiente, empregando aceleração gráfica de hardware para fornecer efeitos mirando reduzir desordem da tela. O gerenciador de sessão do GNOME detecta automaticamente se seu driver de vídeo é capaz de executar o GNOME Shell e se não, retrocede para renderização de software usando *llvmpipe*.

### Pacotes adicionais

Esses pacotes não estão nos grupos mencionados acima:

*   **[Boxes](https://en.wikipedia.org/wiki/GNOME_Boxes "wikipedia:GNOME Boxes")** — Uma interface de usuário simples para acessar máquinas virtuais [libvirt](/index.php/Libvirt "Libvirt").

	[https://wiki.gnome.org/Apps/Boxes](https://wiki.gnome.org/Apps/Boxes) || [gnome-boxes](https://www.archlinux.org/packages/?name=gnome-boxes)

*   **Games** — Inicializador simples de jogos para o GNOME.

	[https://wiki.gnome.org/Apps/Games](https://wiki.gnome.org/Apps/Games) || [gnome-games](https://www.archlinux.org/packages/?name=gnome-games)

*   **Definições iniciais do GNOME** — Uma forma simples, fácil e segura de preparar um novo sistema.

	[https://github.com/GNOME/gnome-initial-setup](https://github.com/GNOME/gnome-initial-setup) || [gnome-initial-setup](https://www.archlinux.org/packages/?name=gnome-initial-setup)

*   **GNOME MultiWriter** — Escreve um arquivo ISO para múltiplos dispositivos USB de uma só vez.

	[https://wiki.gnome.org/Apps/MultiWriter](https://wiki.gnome.org/Apps/MultiWriter) || [gnome-multi-writer](https://www.archlinux.org/packages/?name=gnome-multi-writer)

*   **GNOME PackageKit** — Coleção de ferramentas gráficas para o PackageKit ser usado no ambiente GNOME.

	[https://github.com/GNOME/gnome-packagekit](https://github.com/GNOME/gnome-packagekit) || [gnome-packagekit](https://www.archlinux.org/packages/?name=gnome-packagekit)

*   **[Nemiver](https://en.wikipedia.org/wiki/Nemiver "wikipedia:Nemiver")** — Um depurador de C/C++.

	[https://wiki.gnome.org/Apps/Nemiver](https://wiki.gnome.org/Apps/Nemiver) || [nemiver](https://www.archlinux.org/packages/?name=nemiver)

*   **Recipes** — Aplicativo de gerenciamento de receitas para GNOME.

	[https://wiki.gnome.org/Apps/Recipes](https://wiki.gnome.org/Apps/Recipes) || [gnome-recipes](https://www.archlinux.org/packages/?name=gnome-recipes)

*   **Simple Scan** — Utilitário simples para digitalização.

	[https://launchpad.net/simple-scan](https://launchpad.net/simple-scan) || [simple-scan](https://www.archlinux.org/packages/?name=simple-scan)

*   **[Software](https://en.wikipedia.org/wiki/GNOME_Software "wikipedia:GNOME Software")** — Permite que você instale e atualize aplicativos e extensões de sistema.

	[https://wiki.gnome.org/Apps/Software/](https://wiki.gnome.org/Apps/Software/) || [gnome-software](https://www.archlinux.org/packages/?name=gnome-software)

## Sessões do GNOME

GNOME possui três sessões disponíveis, todos usando o GNOME Shell.

*   **GNOME** é o padrão que usa Wayland. Aplicativos X tradicionais são executados pelo Xwayland.
*   **GNOME Clássico** é uma disposição do ambiente tradicional com uma interface similar à do GNOME 2, usando extensões e parâmetros pré-ativados. [[1]](http://worldofgnome.org/welcome-to-gnome-3-8-flintstones-mode/) Portanto, é mais um GNOME Shell personalizado do que um modo realmente distinto.
*   **GNOME sobre Xorg** executa o GNOME Shell usando o Xorg.

## Iniciando o GNOME

O GNOME pode ser iniciado tanto graficamente, usando um [gerenciador de exibição](/index.php/Display_manager "Display manager"), ou manualmente pelo console.

**Nota:** Suporte para bloqueio de tela no GNOME é fornecido pelo GDM. Se o GNOME não for iniciado usando o GDM, você terá que usar outro bloqueador de tela para fornecer esta funcionalidade - veja [List of applications/Security#Screen lockers](/index.php/List_of_applications/Security#Screen_lockers "List of applications/Security").

### Graficamente

Selecione a sessão: *GNOME*, *GNOME Clássico* ou *GNOME sobre Xorg* a partir do menu de sessões do gerenciador de exibição.

### Manualmente

#### Sessões Xorg

*   Para a sessão do GNOME sobre Xorg, adicione ao arquivo `~/.xinitrc`: `exec gnome-session`.
*   Para a sessão do GNOME Clássico, adicione ao arquivo `~/.xinitrc`:
    ```
    export XDG_CURRENT_DESKTOP=GNOME-Classic:GNOME
    export GNOME_SHELL_SESSION_MODE=classic
    exec gnome-session --session=gnome-classic
    ```

Após editar o arquivo `~/.xinitrc`, GNOME pode ser iniciado com o comando `startx` (veja [xinitrc](/index.php/Xinitrc "Xinitrc") para detalhes adicionais, tal como preservar a sessão de logind). Após configurar o arquivo `~/.xinitrc`, também é possível ser arranjado para [Iniciar o X na autenticação](/index.php/Start_X_at_login "Start X at login").

#### Sessões Wayland

**Nota:**

*   Um servidor X — fornecido pelo pacote [xorg-server-xwayland](https://www.archlinux.org/packages/?name=xorg-server-xwayland) — ainda é necessário para executar aplicativos que ainda não foram portados para o [Wayland](/index.php/Wayland "Wayland").
*   Wayland com o driver proprietário da [NVIDIA](/index.php/NVIDIA "NVIDIA") atualmente sofre de um desempenho muito ruim: [FS#53284](https://bugs.archlinux.org/task/53284).

Iniciar manualmente uma sessão Wayland é possível com `XDG_SESSION_TYPE=wayland dbus-run-session gnome-session`.

Para iniciar ao autenticar no tty1, adicione o seguinte ao seu `.bash_profile`:

```
if [[ -z $DISPLAY ]] && [[ $(tty) = /dev/tty1 ]] && [[ -z $XDG_SESSION_TYPE ]]; then
  XDG_SESSION_TYPE=wayland exec dbus-run-session gnome-session
fi

```

### Aplicativos do GNOME no Wayland

Quando a sessão *GNOME* é usada, aplicativos do GNOME serão executados usando o Wayland. Veja o status atual do Wayland para aplicativos do GNOMEem [Aplicativos do GNOME sob Wayland](https://wiki.gnome.org/Initiatives/Wayland/Applications/). Para casos de depuração, o [manual do GTK+](https://developer.gnome.org/gtk3/stable/gtk-running.html) lista opções e variáveis de ambiente.

## Navegação

Para aprender como usar o GNOME Shell efetivamente, leia a [folha de dicas do GNOME Shell](https://wiki.gnome.org/Projects/GnomeShell/CheatSheet); ela realça os recursos e atalhos de teclado do GNOME Shell. Recursos incluem realce de tarefa, uso de teclado, controle de janela, o painel, modo de visão geral e mais. Alguns dos atalhos são:

*   `Super` + `m`: mostra a área de notificação
*   `Super` + `a`: mostra o menu de aplicativos
*   `Alt-` + `Tab`: alterna entre aplicativos ativos
*   `Alt-` + ``` (a tecla logo acima de `Tab` nos teclados americanos): alterna entre janelas do aplicativo em primeiro plano
*   `Alt` + `F2`, e depois insira `r` ou `restart`: reinicia o shell no caso de problemas no shell gráfico (apenas no modo X/legado, não no modo Wayland).

### Nomes legados

**Nota:** Alguns programas do GNOME sofreram alteração de nomes, casos em que o nome do aplicativo na documentação e diálogos de "sobre" foram alterados, mas o nome do executável não foi. Alguns poucos aplicativos estão listados na tabela abaixo.

**Dica:** Pesquisar pelo nome legado de um aplicativo na barra de pesquisa do Shell retornará com sucesso o aplicativo em questão. Por exemplo, pesquisar por *nautilus* vai retornar *Arquivos*.

| Atual | Legado |
| [Arquivos](/index.php/Files "Files") | Nautilus |
| [Web](/index.php/GNOME/Web "GNOME/Web") | Epiphany |
| Vídeos | Totem |
| Menu principal | Alacarte |
| Visualizador de documentos | Evince |
| Analisador de uso de disco | Baobab |
| Visualizador de imagens | EoG (Eye of GNOME) |
| [Chaves e senhas](/index.php/GNOME/Keyring "GNOME/Keyring") | Seahorse |

## Configuração

O painel Configurações do sistema do GNOME (*gnome-control-center*) e os aplicativos do GNOME usam o sistema de configuração [dconf](https://en.wikipedia.org/wiki/Dconf "wikipedia:Dconf") para armazenar suas configurações.

Você pode acessar diretamente o banco de dados dconf usando as ferramentas de linha de comando `gsettings` ou `dconf`. Isso também permite que você alterar as configurações não expostas pelas interfaces de usuário.

Até o GNOME 3.24, as configurações eram aplicadas por um daemon de configurações do GNOME, os quais poderiam estar fora de uma sessão do GNOME usando:

```
$ nohup /usr/lib/gnome-settings-daemon/gnome-settings-daemon > /dev/null &

```

GNOME 3.24, porém, substituiu o daemon de configurações do GNOME com diversos outros plug-ins `/usr/lib/gnome-settings-daemon/gsd-*` separados. Esses plug-ins são agora controlados via arquivos desktop sob `/etc/xdg/autostart` (org.gnome.SettingsDaemon.*.desktop). Para executar esses plug-ins fora de uma sessão do GNOME, você agora precisará copiar/editar as [entradas desktop](/index.php/Desktop_entries "Desktop entries") apropriadas para `~/.config/autostart`.

A configuração geralmente é realizada para cada usuário, essa seção não cobre o como criar modelos de configuração para múltiplos usuários.

### Configurações do sistema

#### Cor

O daemon `colord` lê o EDID da tela e extrai o perfil de cor apropriado. A maioria dos perfis de cor são precisos e nenhuma configuração é necessária; porém, para aqueles que não forem precisos, ou para telas antigas, perfis de cores podem ser colocadas em `~/.local/share/icc/` e direcionado para ele.

#### Data & hora

Se o sistema possuir o [daemon de Network Time Protocol](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon") configurado, ele será usado pelo GNOME também. A sincronização pode ser definida para controle manual pelo menu, se necessário.

Para mostrar a data na barra superior, execute:

```
$ gsettings set org.gnome.desktop.interface clock-show-date true

```

Adicionalmente, para mostrar números da semana no calendário aberto na barra superior, execute:

```
$ gsettings set org.gnome.desktop.calendar show-weekdate true

```

#### Aplicativos padrões

Ao instalar o GNOME pela primeira vez, você pode descobrir que os aplicativos errados estão lidando com certos protocolos. Por exemplo, *totem* abre vídeos em vez de o previamente usado [VLC](/index.php/VLC "VLC"). Algumas das associações podem ser definidas pelas configurações do sistema via: *Sistema* > *Detalhes* > *Aplicativos padrões*.

Para outros protocolos e métodos, veja [Default applications](/index.php/Default_applications "Default applications") para configuração.

#### Mouse e touchpad

Para ajudar a reduzir interferência do touchpad, você pode preferir implementar as configurações abaixo via *gnome-control-center*:

*   Desabilitar touchpad enquanto digita
*   Desabilitar rolagem
*   Desabilitar toque para clicar

Dependendo de seu dispositivo, outras configurações podem estar disponíveis, mas não expostas via GUI padrão. Por exemplo, um `click-method` diferente de touchpad

 `$ gsettings range org.gnome.desktop.peripherals.touchpad click-method` 
```

enum
'default'
'none'
'areas'
'fingers'
```

a ser definido manualmente:

```
$ gsettings set org.gnome.desktop.peripherals.touchpad click-method 'fingers'

```

Ou via *gnome-tweak-tool*.

**Nota:** O driver [synaptics](/index.php/Synaptics "Synaptics") não possui suporte no GNOME. Em vez disso, você deve usar [libinput](/index.php/Libinput "Libinput"). Veja [esse relatório de erro](https://bugzilla.gnome.org/show_bug.cgi?id=764257#c12).

#### Rede

[NetworkManager](/index.php/NetworkManager_(Portugu%C3%AAs) "NetworkManager (Português)") é a ferramenta nativa do projeto GNOME para controlar as configurações de rede pelo Shell. [Instale](/index.php/Instale "Instale") o pacote [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) e [habilite](/index.php/Habilite "Habilite") a unit do systemd `NetworkManager.service`.

Enquanto qualquer outro [gerenciador de rede](/index.php/Network_manager "Network manager") pode ser usado, NetworkManager fornece a integração completa via configurações de rede shell e um miniaplicativo indicador de status [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) (não exigido para o GNOME).

#### Contas on-line

Backends para o aplicativo de mensagem do GNOME [empathy](https://www.archlinux.org/packages/?name=empathy), assim como a seção de Contas On-line do GNOME do painel de Configurações de sistema, são fornecidos em um grupo separado: [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/). Veja [Impossibilidade de adicionar contas no Empathy e Contas on-line GNOME](/index.php/GNOME/Troubleshooting#Unable_to_add_accounts_in_Empathy_and_GNOME_Online_Accounts "GNOME/Troubleshooting"). Algumas contas on-line, tal como [ownCloud](/index.php/OwnCloud "OwnCloud"), exige que [gvfs-goa](https://www.archlinux.org/packages/?name=gvfs-goa) esteja instalado par funcionalidade completa nos aplicativos do GNOME tal como [GNOME Arquivos](/index.php/GNOME_Files "GNOME Files") e GNOME Documentos [[2]](https://wiki.gnome.org/ThreePointSeven/Features/Owncloud).

#### Pesquisa

O shell do GNOME possui uma pesquisa que possa ser rapidamente acessada pressionando a tecla `Super` e comece a digitar. O pacote [tracker](https://www.archlinux.org/packages/?name=tracker) é instalado por padrão como parte do grupo [gnome](https://www.archlinux.org/groups/x86_64/gnome/) e fornece um aplicativo de indexação e banco de dados de metadados. Ele pode ser configurado com o item de menu *Pesquisa e indexação*; monitore o status com *tracker-control*. É iniciado automaticamente pelo *gnome-session* quando o usuário inicia a sessão. Indexação pode ser iniciada manualmente com `tracker-control -s`. As configurações de pesquisa também podem ser configuradas no painel *Configurações de sistema*.

O bando de dados do Tracker pode ser consultado usando o comando *tracker-sparql*. Veja sua página de manual com [tracker-sparql(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/tracker-sparql.1) para mais informações.

### Configurações avançadas

Como anotado acima, muitas opções de configuração tal como alterar o tema do [GTK+](/index.php/GTK%2B "GTK+") ou o tema do [gerenciador de janelas](/index.php/Window_manager "Window manager"), não são expostas no painel de Configurações do sistema (*gnome-control-center*). Aqueles usuários que desejem alterar essas configurações pode desejar usar a Ferramenta de Ajustes do GNOME ([gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool)), uma ferramenta gráfica conveniente que expõe muitas das configurações.

Configurações do GNOME (que são armazenadas no banco de dados DConf) também podem ser alteradas usando o [*dconf-editor*](https://developer.gnome.org/dconf/unstable/dconf-editor.html) (uma ferramenta gráfica de configuração de DConf) ou a ferramenta de linha de comando [*gsettings*](https://developer.gnome.org/gio/stable/GSettings.html). A Ferramenta de Ajustes do GNOME não faz nada no plano de fundo do GUI; note que você não encontrará nela todas as configurações descritas nas seções a seguir.

#### Aparência

##### Temas GTK+ e temas de ícone

Para instalar um novo tema ou conjunto de ícone, adicione `~/.local/share/themes` ou `~/.local/share/icons` relevantes, respectivamente (adicione a `/usr/share/` em vez de `~/.local/share/` para temas estarem disponíveis para todo sistema). Eles e outras configurações de GUI também pode ser definida em `~/.config/gtk-3.0/settings.ini`:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-theme-name = Adwaita
# próxima opção é aplicável apenas se o tema selecionado oferecer suporte
gtk-application-prefer-dark-theme = true
# define o nome e dimensão da fonte
gtk-font-name = Sans 10

```

Localizações adicionais de tema:

*   [DeviantArt](http://www.deviantart.com/browse/all/customization/skins/linuxutil/desktopenv/gnome/gtk3/).
*   [gnome-look.org](http://gnome-look.org/index.php?xcontentmode=167).
*   [Temas do GTK+ 3 no AUR](https://aur.archlinux.org/packages.php?O=0&K=gtk3&do_Search=Go).
*   [Temas de cursor no AUR](https://aur.archlinux.org/packages.php?O=0&K=xcursor&do_Search=Go&PP=50&SB=v&SO=d).
*   [Temas de ícones no AUR](https://aur.archlinux.org/packages.php?O=0&K=icon-theme&do_Search=Go&PP=50&SB=v&SO=d).

Uma vez instalados, eles podem ser selecionados usando a Ferramenta de Ajustes do GNOME ou GSettings - veja abaixo por comandos do GSettings:

Para o tema do GTK+:

```
$ gsettings set org.gnome.desktop.interface gtk-theme *nome-do-tema*

```

Para o tema de ícones:

```
$ gsettings set org.gnome.desktop.interface icon-theme *nome-do-tema*

```

###### Tema global escuro

GNOME vai usar o tema leve do Adwaita por padrão, porém uma variante escura deste tema (chamada de *Tema global escuro*) também existe e pode ser selecionada usando a Ferramenta de Ajustes ou editando o arquivo de configurações do GTK+ 3 - veja [GTK+#Dark theme variant](/index.php/GTK%2B#Dark_theme_variant "GTK+"). Alguns aplicativos, tal como o Visualizador de imagens (*eog*), usam o tema escuro por padrão. Deve-se observar que o tema global escuro só funciona com aplicativos GTK+ 3; alguns aplicativos GTK+ 3 só podem ter suporte parcial para o tema global escuro. Suporte no Qt e no GTK+ 2 ao tema global escuro podem ser adicionados no futuro.

##### Temas de gerenciador de janelas

O tema do gerenciador de janelas segue o tema do GTK+. O uso de `org.gnome.desktop.wm.preferences theme` está obsoleto e é ignorado.

###### Altura da barra de título

**Nota:** Aplicar essa configuração reduz a barra de título do terminal do GNOME e do Chromium, mas não parece ter efeito sobre o tamanho da barra de título do Nautilus.
 `~/.config/gtk-3.0/gtk.css` 
```
headerbar.default-decoration {
 padding-top: 0px;
 padding-bottom: 0px;
 min-height: 0px;
 font-size: 0.6em;
}

headerbar.default-decoration button.titlebutton {
 padding: 0px;
 min-height: 0px;
}

```

Veja [[3]](https://ask.fedoraproject.org/en/question/10035/shrink-title-bar/?answer=86149#post-id-86149) para mais informações.

###### Ordem de botão de barra de título

Para definir a ordem para o gerenciador de janelas do GNOME (Mutter, Metacity):

```
$ gsettings set org.gnome.desktop.wm.preferences button-layout ':minimize,maximize,close'

```

**Dica:** O caractere de dois pontos indica em qual lado da barra de título os botões de janela aparecerão.

###### Ocultar barra de título quando maximizado

*   [Instale](/index.php/Instale "Instale") [gnome-shell-extension-pixel-saver-git](https://aur.archlinux.org/packages/gnome-shell-extension-pixel-saver-git/) ou [gnome-shell-extension-pixel-saver](https://aur.archlinux.org/packages/gnome-shell-extension-pixel-saver/). Janelas maximizadas mesclam a barra de título com a barra de atividade, salvando pixels preciosos.

*   [Instale](/index.php/Instale "Instale") [mutter-hide-legacy-decorations](https://aur.archlinux.org/packages/mutter-hide-legacy-decorations/). Isso altera a configuração padrão no gerenciador de janelas, assim como oculta automaticamente a barra de título em aplicativos legados (sem barra de título) quando eles são maximizados ou colados lado a lado na lateral.

*   [Instale](/index.php/Instale "Instale") [maximus](https://aur.archlinux.org/packages/maximus/). Para começar o aplicativo, execute *maximus* de um terminal. Ao executar, o daemon vai maximizar janelas automaticamente. Isso vai retirar decoração de janelas maximizadas e vai redecorá-las quando elas tiverem seu tamanho anterior restaurado. Se você não deseja que todas as janelas iniciem maximizadas, execute `maximus -m`. Note que isso só vai funcionar com janelas decoradas pelo gerenciador de janelas; aplicativos que usam decoração no lado do cliente, tal como o [GNOME Arquivos](/index.php/GNOME_Files "GNOME Files"), não terão decoração retirada ao maximizar.

##### Temas do GNOME Shell

O tema do GNOME Shell em si é configurável. Para usar um tema de Shell, primeiro assegure-se de que você tenha o pacote [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) instalado. Então, habilite a extensão *User Themes*, pela Ferramenta de Ajustes do GNOME ou pela página web [GNOME Shell Extensions](https://extensions.gnome.org). Temas de shell podem então ser carregadas e selecionadas usando a Ferramenta de Ajustes do GNOME.

Há vários temas de GNOME Shell disponíveis [no AUR](https://aur.archlinux.org/packages.php?O=0&K=gnome-shell-theme&do_Search=Go&PP=50&SB=v&SO=d).

Temas de shell também pode ser baixados do [gnome-look.org](http://gnome-look.org/index.php?xcontentmode=191).

##### Ícones no menu

O esquema padrão do GNOME não exibe qualquer ícone nos menus. Para exibir ícones nos menus, execute o seguinte comando.

```
$ gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/ButtonImages': <1>, 'Gtk/MenuImages': <1>}"

```

#### Área de trabalho

Várias configurações de área de trabalho podem ser aplicadas.

##### Ícones na área de trabalho

Veja [GNOME/Files#Desktop Icons](/index.php/GNOME/Files#Desktop_Icons "GNOME/Files").

##### Tela de bloqueio e plano de fundo

Ao definir o plano de fundo da área de trabalho ou da tela de bloqueio, é importante notar que a aba Imagens são exibirá imagens localizadas na pasta `/home/*nome-de-usuário*/Imagens`. Se você deseja usar uma imagem não localizada nesta pasta, use os comandos indicados abaixo.

Para o plano de fundo da área de trabalho:

```
$ gsettings set org.gnome.desktop.background picture-uri 'file:///caminho/para/minha/imagem.jpg'

```

Para o plano de fundo da tela de bloqueio:

```
$ gsettings set org.gnome.desktop.screensaver picture-uri 'file:///caminho/para/minha/imagem.jpg'

```

#### Extensões

**Nota:** O plugin de navegador do GNOME Shell que permite que usuários instalem extensões do [extensions.gnome.org](https://extensions.gnome.org) funciona sem mais configurações para navegadores como o [GNOME/Web](/index.php/GNOME/Web "GNOME/Web"). Para os navegadores [Firefox](/index.php/Firefox "Firefox"), Google Chrome/Chromium, Opera e Vivaldi, é necessário instralar [chrome-gnome-shell-git](https://aur.archlinux.org/packages/chrome-gnome-shell-git/) e a extensão de navegador apropriada.

GNOME Shell pode ser personalizado com extensões por usuário ou para todo o sistema.

O catálogo de extensões está disponível em [extensions.gnome.org](https://extensions.gnome.org). Por um usuário, elas podem ser instaladas e ativadas no navegador definindo o botão no canto superior direito da tela para **ON** e clicando em **Install** no diálogo resultante (se a extensão em questão não estiver instalada). Após a instalação, é mostrar na aba [extensions.gnome.org/local/](https://extensions.gnome.org/local/), qual tem que ser visitado, assim como verificar por atualizações disponíveis. Extensões instaladas também podem ser habilitadas ou desabilitadas usando [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool).

Mais informações sobre extensões do GNOME shell estão disponíveis na [página de manual do GNOME Shell Extensions](https://extensions.gnome.org/about/).

[Instalar](/index.php/Instalar "Instalar") extensões por um pacote torna-os disponível para todos os usuários do sistema e automatiza o processo de atualização.

O pacote [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) fornece um conjunto de extensões mantidas como parte do projeto GNOME (muitas das extensões incluídas são usadas pela sessão do GNOME Clássico).

Usuários que desejem uma barra de tarefas, mas não desejam usar a sessão do GNOME Clássico, podem querer habilitar a extensão *Window list* (fornecida pelo pacote [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions)).

A listagem de extensões atualmente habilitadas podem ser obtida com:

```
$ gsettings get org.gnome.shell enabled-extensions

```

#### Métodos de entrada

O GNOME possui suporte integrado para métodos de entrada por meio do [IBus](/index.php/IBus "IBus"), só sendo necessário instalar [ibus](https://www.archlinux.org/packages/?name=ibus) e o motor do método de entrada (ex.: [ibus-libpinyin](https://www.archlinux.org/packages/?name=ibus-libpinyin) para Intelligent Pinyin); após a instalação, o motor de método de entrada podem ser adicionados como disposição de teclado nas configurações de "Idioma & região" do GNOME.

#### Fontes

**Dica:** Se você definiu o *Fator de escala* para um valor acima de 1.00, o menu de Acessibilidade será habilitado automaticamente.

Fontes podem ser definidas para *Títulos de janelas*, *Interface* (aplicativos), *Documentos* e *Monoespaçada*. Veja a aba Fontes na Ferramenta de Ajustes para opções relevantes.

Para *hinting*, RGBA provavelmente é melhor por atender a maioria dos tipos de monitores. Se as fontes aparecerem bloqueadas demais, reduza *hinting* para *Slight* ou *None*.

#### Inicialização de aplicativos

Para iniciar certos aplicativos no início da sessão, copie o arquivo `.desktop` relevante do `/usr/share/applications/` para `~/.config/autostart/`.

A Ferramenta de Ajustes, [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool), permite gerenciar entradas de de "autostart".

**Dica:** Se o botão de sinal de mais na seção de inicialização da Ferramenta de Ajustes não estiver responsivo, tente iniciá-la a partir do terminal usando o seguinte comando: `gnome-tweak-tool`. Veja o seguinte [tópico de fórum](https://bbs.archlinux.org/viewtopic.php?pid=1413631#p1413631).

**Nota:** O diálogo obsoleto *gnome-session-properties* pode ser adicionado [instalando](/index.php/Instala "Instala") o pacote [gnome-session-properties](https://aur.archlinux.org/packages/gnome-session-properties/).

#### Energia

Quando você está usando um notebook, você pode querer alterar as seguintes configurações:

```
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-timeout *3600*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-type *hibernate*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-battery-timeout *1800*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-battery-type *hibernate*
$ gsettings set org.gnome.settings-daemon.plugins.power power-button-action *suspend*
$ gsettings set org.gnome.desktop.lockdown disable-lock-screen *true*

```

Para manter o monitor ativo quando a tampa está fechada:

```
$ gsettings set org.gnome.settings-daemon.plugins.xrandr default-monitors-setup do-nothing

```

GNOME 3.24 tornou obsoletas as seguintes configurações:

```
org.gnome.settings-daemon.plugins.power button-hibernate
org.gnome.settings-daemon.plugins.power button-power
org.gnome.settings-daemon.plugins.power button-sleep
org.gnome.settings-daemon.plugins.power button-suspend
org.gnome.settings-daemon.plugins.power critical-battery-action

```

##### Configurar o comportamento do fechamento da tela de notebook

A Ferramenta de Ajustes do GNOME pode opcionalmente *inibir* a configuração do *systemd* para o evento de ACPI de fechar a tampa.[[4]](http://ftp.gnome.org/pub/GNOME/sources/gnome-tweak-tool/3.17/gnome-tweak-tool-3.17.1.news) Para *inibir* a configuração, inicie a ferramenta de ajustes e, sob a aba energia, marque a opção *Suspender quando a tampa do notebook é fechada*. Isso significa que o ssitema fará nada ao fechar a tampa do notebook em vez de suspender - o comportamento padrão. Marcando essa configuração, cria `~/.config/autostart/ignore-lid-switch-tweak.desktop` que vai iniciar automaticamente o inibor da Ferramenta de Ajustes.

Se você não deseja suspender ou fazer nada ao fechar a tampa do notebook, você precisará se certificar de que a configuração acima **não** esteja marcada e, então, configure *systemd* com `HandleLidSwitch=*preferred_behaviour*` como descrito em [Power management#ACPI events](/index.php/Power_management#ACPI_events "Power management").

##### Alterar ação de nível crítico da bateria

O painel de configurações não fornece uma opção para alterar a ação de nível crítico de bateria. Essas configurações foram removidas também do dconf. Eles agora são gerenciados pelo upower. Edite as configurações do upower em `/etc/UPower/UPower.conf`. Encontre essas configurações e ajuste a suas necessidades.

 `/etc/UPower/UPower.conf` 
```
PercentageLow=10
PercentageCritical=3
PercentageAction=2
CriticalPowerAction=HybridSleep
```

#### Ordenar aplicativos em pastas de aplicativo (app)

**Dica:** O script [gnome-catgen](https://github.com/prurigro/gnome-catgen) ([gnome-catgen-git](https://aur.archlinux.org/packages/gnome-catgen-git/)) permite que você gerencie as pastas por meio da criação de arquivos nos `~/.local/share/applications-categories` nomeados após cada categoria e contendo uma lista de arquivos desktop pertencendo aos aplicativos que você gostaria de ter dentro. Opcionalmente, você pode fazê-lo passar por cada aplicativo sem uma pasta e inserir a categoria desejada até pressionar Ctrl+C ou acabarem os aplicativos.

No **dconf-editor**, navegue para `org.gnome.desktop.app-folders` e defina o valor de `folder-children` para um vetor de nomes de pastas separados por vírgula:

```
['Utilities', 'Sundry']

```

Adicione aplicativos usando `gsettings`:

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ apps "['alacarte.desktop', 'dconf-editor.desktop']"

```

Isso adiciona os aplicativos `alacarte.desktop` e `dconf-editor.desktop` à pasta Sundry. Isso também vai criar a pasta `org.gnome.desktop.app-folders.folders.Sundry`.

Para nomear a pasta (se ela não tiver um nome que aparece no topo dos aplicativos):

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ name "Sundry"

```

Aplicativos também podem ser ordenados por sua categoria (especificado em seus arquivos *.desktop*):

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ categories "['Office']"

```

Se certos aplicativos correspondendo a uma categoria não forem desejados em certa pasta, exclusões podem ser definidas:

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ excluded-apps "['libreoffice-draw.desktop']"

```

Para mais informações, veja o [esquema app-folders](https://git.gnome.org/browse/gsettings-desktop-schemas/tree/schemas/org.gnome.desktop.app-folders.gschema.xml.in).

## Veja também

*   [O site oficial do GNOME](https://www.gnome.org/)
*   [Extensões para o GNOME Shell](https://extensions.gnome.org/)
*   [Folha de dicas do GNOME Shell](https://wiki.gnome.org/Projects/GnomeShell/CheatSheet), comandos, atalhos de teclados e outras dicas para o uso do GNOME Shell.
*   Temas, ícones e planos de fundo:
    *   [Personalize GNOME](https://wiki.gnome.org/Personalization)
    *   [GNOME Look](https://www.gnome-look.org/)
*   Programas GTK+/GNOME:
    *   [Índice dos aplicativos do GNOME](https://wiki.gnome.org/Apps)
*   [Customizing the GNOME Shell](http://blog.fpmurphy.com/2011/03/customizing-the-gnome-3-shell.html)
*   Código-fonte/Espelhos do GNOME:
    *   [Repositório Git do GNOME](https://git.gnome.org/browse/)
    *   [Espelho do GNOME no Github](https://github.com/GNOME)