**Status de tradução:** Esse artigo é uma tradução de [GNOME](/index.php/GNOME "GNOME"). Data da última tradução: 2019-10-21\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=GNOME&diff=0&oldid=586572) na versão em inglês.

Artigos relacionados

*   [GTK](/index.php/GTK_(Portugu%C3%AAs) "GTK (Português)")
*   [GDM](/index.php/GDM_(Portugu%C3%AAs) "GDM (Português)")
*   [GNOME/Tips and tricks](/index.php/GNOME/Tips_and_tricks "GNOME/Tips and tricks")
*   [GNOME/Troubleshooting](/index.php/GNOME/Troubleshooting "GNOME/Troubleshooting")
*   [GNOME/Files](/index.php/GNOME/Files "GNOME/Files")
*   [GNOME/Gedit](/index.php/GNOME/Gedit "GNOME/Gedit")
*   [GNOME/Web](/index.php/GNOME/Web "GNOME/Web")
*   [GNOME/Evolution](/index.php/GNOME/Evolution "GNOME/Evolution")
*   [GNOME/Flashback](/index.php/GNOME/Flashback "GNOME/Flashback")
*   [GNOME/Keyring](/index.php/GNOME/Keyring "GNOME/Keyring")
*   [GNOME/Document viewer](/index.php/GNOME/Document_viewer "GNOME/Document viewer")
*   [GNOME/Software](/index.php/GNOME/Software "GNOME/Software")
*   [Repositórios oficiais#gnome-unstable](/index.php/Reposit%C3%B3rios_oficiais#gnome-unstable "Repositórios oficiais")

[GNOME](https://en.wikipedia.org/wiki/pt:GNOME "wikipedia:pt:GNOME") (/(ɡ)noʊm/) é um [ambiente de desktop](/index.php/Ambiente_de_desktop "Ambiente de desktop"), ou *desktop environment*, que visa ser simples e fácil de usar. Ele é projetado por [O Projeto GNOME](https://en.wikipedia.org/wiki/The_GNOME_Project "wikipedia:The GNOME Project") e é composto interiramente de software livre e código aberto. O GNOME é uma parte do [Projeto GNU](/index.php/Projeto_GNU "Projeto GNU"). O *display* padrão é o [Wayland](/index.php/Wayland "Wayland") em vez do [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Sessões do GNOME](#Sessões_do_GNOME)
*   [3 Iniciando](#Iniciando)
    *   [3.1 Graficamente](#Graficamente)
    *   [3.2 Manualmente](#Manualmente)
        *   [3.2.1 Sessões Xorg](#Sessões_Xorg)
        *   [3.2.2 Sessões Wayland](#Sessões_Wayland)
    *   [3.3 Aplicativos do GNOME no Wayland](#Aplicativos_do_GNOME_no_Wayland)
*   [4 Navegação](#Navegação)
*   [5 Nomes legados](#Nomes_legados)
*   [6 Configuração](#Configuração)
    *   [6.1 Configurações do sistema](#Configurações_do_sistema)
        *   [6.1.1 Cor](#Cor)
        *   [6.1.2 Luz noturna](#Luz_noturna)
        *   [6.1.3 Data & hora](#Data_&_hora)
        *   [6.1.4 Aplicativos padrões](#Aplicativos_padrões)
        *   [6.1.5 Mouse e touchpad](#Mouse_e_touchpad)
        *   [6.1.6 Rede](#Rede)
        *   [6.1.7 Contas on-line](#Contas_on-line)
        *   [6.1.8 Pesquisa](#Pesquisa)
    *   [6.2 Configurações avançadas](#Configurações_avançadas)
        *   [6.2.1 Aparência](#Aparência)
            *   [6.2.1.1 Temas](#Temas)
            *   [6.2.1.2 Altura da barra de título](#Altura_da_barra_de_título)
            *   [6.2.1.3 Ordem de botão de barra de título](#Ordem_de_botão_de_barra_de_título)
            *   [6.2.1.4 Ocultar barra de título quando maximizado](#Ocultar_barra_de_título_quando_maximizado)
            *   [6.2.1.5 Temas do GNOME Shell](#Temas_do_GNOME_Shell)
            *   [6.2.1.6 Ícones no menu](#Ícones_no_menu)
        *   [6.2.2 Pastas de grade de aplicativos](#Pastas_de_grade_de_aplicativos)
        *   [6.2.3 Inicialização automática](#Inicialização_automática)
        *   [6.2.4 Área de trabalho](#Área_de_trabalho)
            *   [6.2.4.1 Ícones na área de trabalho](#Ícones_na_área_de_trabalho)
            *   [6.2.4.2 Tela de bloqueio e plano de fundo](#Tela_de_bloqueio_e_plano_de_fundo)
            *   [6.2.4.3 Desabilitar o canto superior esquerdo ativo](#Desabilitar_o_canto_superior_esquerdo_ativo)
        *   [6.2.5 Extensões](#Extensões)
        *   [6.2.6 Fontes](#Fontes)
        *   [6.2.7 Métodos de entrada](#Métodos_de_entrada)
        *   [6.2.8 Energia](#Energia)
            *   [6.2.8.1 Não suspender quando a tampa do notebook é fechada](#Não_suspender_quando_a_tampa_do_notebook_é_fechada)
            *   [6.2.8.2 Alterar ação de nível crítico da bateria](#Alterar_ação_de_nível_crítico_da_bateria)
    *   [6.3 Usar um gerenciador de janela diferente](#Usar_um_gerenciador_de_janela_diferente)
*   [7 Veja também](#Veja_também)

## Instalação

Dois grupos estão disponíveis:

*   [gnome](https://www.archlinux.org/groups/x86_64/gnome/) contém o ambiente base do GNOME e um subconjunto de [aplicativos](https://wiki.gnome.org/Apps) bem integrados;
*   [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/) contém mais aplicativos do GNOME, incluindo um gerenciador de pacote, gerenciador de disco, [editor de texto](/index.php/Gedit "Gedit") e um conjunto de jogos. Note que esse grupo compila no grupo [gnome](https://www.archlinux.org/groups/x86_64/gnome/).

O ambiente base consiste no [GNOME Shell](https://en.wikipedia.org/wiki/GNOME_Shell "wikipedia:GNOME Shell"), um plug-in para o gerenciador de janelas [Mutter](https://en.wikipedia.org/wiki/Mutter_(software) "wikipedia:Mutter (software)"). Ele pode ser instalado separadamente com [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell).

**Nota:** *mutter* age como um gerenciador de composição para o ambiente, empregando aceleração gráfica de hardware para fornecer efeitos mirando reduzir desordem da tela. O gerenciador de sessão do GNOME detecta automaticamente se seu driver de vídeo é capaz de executar o GNOME Shell e se não, retrocede para renderização de software usando *llvmpipe*.

## Sessões do GNOME

GNOME possui três sessões disponíveis, todos usando o GNOME Shell.

*   **GNOME** é o padrão que usa Wayland. Aplicativos X tradicionais são executados pelo Xwayland.
*   **GNOME Clássico** é uma disposição do ambiente tradicional com uma interface similar à do GNOME 2, usando extensões e parâmetros pré-ativados. [[1]](http://worldofgnome.org/welcome-to-gnome-3-8-flintstones-mode/) Portanto, é mais um GNOME Shell personalizado do que um modo realmente distinto.
*   **GNOME sobre Xorg** executa o GNOME Shell usando o Xorg.

## Iniciando

O GNOME pode ser iniciado tanto graficamente, com um [gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição"), ou manualmente pelo console (podem faltar alguns recursos).

**Nota:** Suporte para bloqueio de tela no GNOME (e muito mais) é fornecido pelo GDM. Se o GNOME não for iniciado com o GDM, outro bloqueador de tela pode ser usado para fornecer esta funcionalidade. Veja [List of applications/Security#Screen lockers](/index.php/List_of_applications/Security#Screen_lockers "List of applications/Security").

### Graficamente

Selecione a sessão: *GNOME*, *GNOME Clássico* ou *GNOME sobre Xorg* a partir do menu de sessões do gerenciador de exibição.

### Manualmente

#### Sessões Xorg

*   Para a sessão do GNOME sobre Xorg, adicione ao arquivo `~/.xinitrc` (veja [aqui](https://gitlab.gnome.org/GNOME/gtk/issues/1390#note_344758) para detalhes):
    ```
    export XDG_SESSION_TYPE=x11
    export GDK_BACKEND=x11
    exec gnome-session
    ```

*   Para a sessão do GNOME Clássico, adicione ao arquivo `~/.xinitrc`:
    ```
    export XDG_CURRENT_DESKTOP=GNOME-Classic:GNOME
    export GNOME_SHELL_SESSION_MODE=classic
    exec gnome-session --session=gnome-classic
    ```

Após editar o arquivo `~/.xinitrc`, GNOME pode ser iniciado com o comando `startx` (veja [xinitrc](/index.php/Xinitrc_(Portugu%C3%AAs) "Xinitrc (Português)") para detalhes adicionais, tal como preservar a sessão de logind). Após configurar o arquivo `~/.xinitrc`, também é possível ser arranjado para [Iniciar X no login](/index.php/Iniciar_X_no_login "Iniciar X no login"),por exemplo no tty2 adicionando ao `.bash_profile`:

```
if [[ -z $DISPLAY && $(tty) == /dev/tty2; ]]; then
  GDK_BACKEND=x11 exec startx
fi

```

#### Sessões Wayland

**Nota:**

*   Um servidor X — fornecido pelo pacote [xorg-server-xwayland](https://www.archlinux.org/packages/?name=xorg-server-xwayland) — ainda é necessário para executar aplicativos que ainda não foram portados para o [Wayland](/index.php/Wayland "Wayland"). Aplicativos usando certas bibliotecas gráficas, tal como Qt, podem ser forçadas a usar o Wayland definindo variáveis de ambiente. Veja [Wayland#GUI libraries](/index.php/Wayland#GUI_libraries "Wayland") para mais informações.
*   Quando estiver usando o driver proprietário da [NVIDIA](/index.php/NVIDIA "NVIDIA"), aplicativos não nativos de Wayland vão sofrer de um desempenho muito ruim por causa de XWayland sem aceleração de hardware. [Espera-se](https://blogs.gnome.org/uraeus/2019/09/23/fedora-workstation-31-whats-new/) resolver isso em outuno de 2020, mas ainda não há um cronograma comprometido pela [NVIDIA](/index.php/NVIDIA "NVIDIA").

Iniciar manualmente uma sessão Wayland é possível com `XDG_SESSION_TYPE=wayland dbus-run-session gnome-session`.

Para iniciar ao autenticar no tty1, adicione o seguinte ao seu `.bash_profile`:

```
if [[ -z $DISPLAY && $(tty) == /dev/tty1 && $XDG_SESSION_TYPE == tty ]]; then
   XDG_SESSION_TYPE=wayland exec dbus-run-session gnome-session
fi

```

### Aplicativos do GNOME no Wayland

Quando a sessão *GNOME* é usada, aplicativos do GNOME serão executados usando o Wayland. Para casos de depuração, o [manual do GTK](https://developer.gnome.org/gtk3/stable/gtk-running.html) lista opções e variáveis de ambiente.

## Navegação

Para aprender como usar o GNOME Shell efetivamente, leia a [folha de dicas do GNOME Shell](https://wiki.gnome.org/Projects/GnomeShell/CheatSheet); ela realça os recursos e atalhos de teclado do GNOME Shell. Recursos incluem realce de tarefa, uso de teclado, controle de janela, o painel, modo de visão geral e mais. Alguns dos atalhos são:

*   `Super` + `m`: mostra a área de notificação
*   `Super` + `a`: mostra o menu de aplicativos
*   `Alt` + `Tab`: alterna entre aplicativos ativos
*   `Alt` + ``` (a tecla logo acima de `Tab` nos teclados americanos): alterna entre janelas do aplicativo em primeiro plano
*   `Alt` + `F2`, e depois insira `r` ou `restart`: reinicia o shell no caso de problemas no shell gráfico (apenas no modo X/legado, não no modo Wayland).

**Dica:** Para fazer o `Alt+Tab` alternar aplicativos apenas no espaço de trabalho atual, você pode definir `current-workspace-only` para `true`:
```
$ gsettings set org.gnome.shell.app-switcher current-workspace-only true

```

## Nomes legados

**Nota:** Alguns programas do GNOME sofreram alteração de nomes, casos em que o nome do aplicativo na documentação e diálogos de "sobre" foram alterados, mas o nome do executável não foi. Alguns poucos aplicativos estão listados na tabela abaixo.

**Dica:** Pesquisar pelo nome legado de um aplicativo na barra de pesquisa do Shell retornará com sucesso o aplicativo em questão. Por exemplo, pesquisar por *nautilus* vai retornar *Arquivos*.

| Atual | Legado |
| [Arquivos](/index.php/GNOME/Files "GNOME/Files") | Nautilus |
| [Web](/index.php/GNOME/Web "GNOME/Web") | Epiphany |
| Vídeos | Totem |
| Menu principal | Alacarte |
| [Visualizador de documentos](/index.php/GNOME/Document_viewer "GNOME/Document viewer") | Evince |
| Analisador de uso de disco | Baobab |
| Visualizador de imagens | EoG (Eye of GNOME) |
| [Chaves e senhas](/index.php/GNOME/Keyring "GNOME/Keyring") | Seahorse |
| Editor de Tradução do GNOME | Gtranslator |

## Configuração

O painel Configurações do sistema do GNOME (*gnome-control-center*) e os aplicativos do GNOME usam o sistema de configuração [dconf](https://en.wikipedia.org/wiki/Dconf "wikipedia:Dconf") para armazenar suas configurações.

Você pode acessar diretamente o banco de dados dconf usando as ferramentas de linha de comando `gsettings` ou `dconf`. Isso também permite que você alterar as configurações não expostas pelas interfaces de usuário.

Até o GNOME 3.24, as configurações eram aplicadas por um daemon de configurações do GNOME (localizado em `/usr/lib/gnome-settings-daemon/gnome-settings-daemon`), o qual poderia ser executado fora de uma sessão do GNOME.

GNOME 3.24, porém, substituiu o daemon de configurações do GNOME com diversos outros plug-ins `/usr/lib/gnome-settings-daemon/gsd-*` separados, os quais posteriormente foram movidos para `/usr/lib/gsd-*`. Esses plug-ins são agora controlados via arquivos desktop sob `/etc/xdg/autostart` (org.gnome.SettingsDaemon.*.desktop). Para executar esses plug-ins fora de uma sessão do GNOME, você agora precisará copiar/editar as [entradas desktop](/index.php/Desktop_entries "Desktop entries") apropriadas para `~/.config/autostart`.

A configuração geralmente é realizada para cada usuário, essa seção não cobre o como criar modelos de configuração para múltiplos usuários.

### Configurações do sistema

#### Cor

O daemon `colord` lê o EDID da tela e extrai o perfil de cor apropriado. A maioria dos perfis de cor são precisos e nenhuma configuração é necessária; porém, para aqueles que não forem precisos, ou para telas antigas, perfis de cores podem ser colocadas em `~/.local/share/icc/` e direcionado para ele.

#### Luz noturna

O GNOME vem com um filtro de luz azul integrado similar ao [Redshift](/index.php/Redshift "Redshift"). Você pode ativar e personalizar a hora em que deseja ativar o modo Luz norturna no menu de configurações de exibição. Além disso, você pode ajustar a temperatura de kelvin com a seguinte configuração [dconf](https://www.archlinux.org/packages/?name=dconf), sendo 5000 um valor de exemplo:

```
$ gsettings set org.gnome.settings-daemon.plugins.color night-light-temperature 5000

```

**Dica:** Para alterar a temperatura do dia em uma sessão Wayland, instale [essa extensão](https://extensions.gnome.org/extension/1276/night-light-slider/).

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

Ao instalar o GNOME pela primeira vez, você pode descobrir que os aplicativos errados estão lidando com certos protocolos. Por exemplo, *totem* abre vídeos em vez de o previamente usado [VLC](/index.php/VLC "VLC"). Algumas das associações podem ser definidas pelas configurações do sistema via: *Detalhes* > *Aplicativos padrões*.

Para outros protocolos e métodos, veja [Default applications](/index.php/Default_applications "Default applications") para configuração.

#### Mouse e touchpad

A maioria das configurações de touchpad podem ser definidos nas configurações do sistema por: *Dipositivos* > *Mouse & touchpad*.

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

Ou via [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks).

**Nota:** O driver [synaptics](/index.php/Synaptics "Synaptics") não possui suporte no GNOME. Em vez disso, você deve usar [libinput](/index.php/Libinput "Libinput"). Veja [esse relatório de erro](https://bugzilla.gnome.org/show_bug.cgi?id=764257#c12).

#### Rede

[NetworkManager](/index.php/NetworkManager_(Portugu%C3%AAs) "NetworkManager (Português)") é a ferramenta nativa do projeto GNOME para controlar as configurações de rede pelo Shell. [Instale](/index.php/Instale "Instale") o pacote [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) e [habilite](/index.php/Habilite "Habilite") a unit do systemd `NetworkManager.service`.

Enquanto qualquer outro [gerenciador de rede](/index.php/Gerenciador_de_rede "Gerenciador de rede") pode ser usado, NetworkManager fornece a integração completa via configurações de rede shell e um miniaplicativo indicador de status [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) (não exigido para o GNOME).

**Nota:** Redes sem fio ocultas configuradas com o *nmtui* do [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) não conectam automaticamente. Você precisa criar um novo perfil usando o centro de controle do GNOME para restaurar as capacidades de autoconexão para aquela rede.

#### Contas on-line

Backends para o aplicativo de mensagem do GNOME [empathy](https://www.archlinux.org/packages/?name=empathy), assim como a seção de Contas On-line do GNOME do painel de Configurações de sistema, são fornecidos em um grupo separado: [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/). Veja [Impossibilidade de adicionar contas no Empathy e Contas on-line GNOME](/index.php/GNOME/Troubleshooting#Unable_to_add_accounts_in_Empathy_and_GNOME_Online_Accounts "GNOME/Troubleshooting"). Algumas contas on-line, tal como [ownCloud](/index.php/OwnCloud "OwnCloud"), exige que [gvfs-goa](https://www.archlinux.org/packages/?name=gvfs-goa) esteja instalado par funcionalidade completa nos aplicativos do GNOME tal como [GNOME Arquivos](/index.php/GNOME_Files "GNOME Files") e GNOME Documentos [[2]](https://wiki.gnome.org/ThreePointSeven/Features/Owncloud).

#### Pesquisa

O shell do GNOME possui uma pesquisa que possa ser rapidamente acessada pressionando a tecla `Super` e comece a digitar. O pacote [tracker](https://www.archlinux.org/packages/?name=tracker) é instalado por padrão como parte do grupo [gnome](https://www.archlinux.org/groups/x86_64/gnome/) e fornece um aplicativo de indexação e banco de dados de metadados. Ele pode ser configurado com o item de menu *Pesquisa e indexação*; monitore o status com *tracker-control*. É iniciado automaticamente pelo *gnome-session* quando o usuário inicia a sessão. Indexação pode ser iniciada manualmente com `tracker-control -s`. As configurações de pesquisa também podem ser configuradas no painel *Configurações de sistema*.

O bando de dados do Tracker pode ser consultado usando o comando *tracker-sparql*. Veja sua página de manual com [tracker-sparql(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tracker-sparql.1) para mais informações.

### Configurações avançadas

Como anotado acima, muitas opções de configuração tal como alterar o tema do [GTK](/index.php/GTK_(Portugu%C3%AAs) "GTK (Português)") ou o tema do [gerenciador de janela](/index.php/Gerenciador_de_janela "Gerenciador de janela"), não são expostas no painel de Configurações do sistema (*gnome-control-center*). Aqueles usuários que desejem alterar essas configurações pode desejar usar o Ajustes do GNOME ([gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks)), uma ferramenta gráfica conveniente que expõe muitas das configurações.

Configurações do GNOME (que são armazenadas no banco de dados DConf) também podem ser alteradas usando o [*dconf-editor*](https://developer.gnome.org/dconf/unstable/dconf-editor.html) (uma ferramenta gráfica de configuração de DConf) ou a ferramenta de linha de comando [*gsettings*](https://developer.gnome.org/gio/stable/GSettings.html). O Ajustes do GNOME não faz nada no plano de fundo do GUI; note que você não encontrará nela todas as configurações descritas nas seções a seguir.

#### Aparência

##### Temas

O GNOME usa Adwaita por padrão. Para aplicar Adwaita dark apenas para aplicativos GTK 2, use o link simbólico a seguir:

```
$ ln -s /usr/share/themes/Adwaita-dark ~/.themes/Adwaita

```

Para selecionar novos temas (mova-os para o diretório apropriado e) use o Ajustes do GNOME ou os comandos de GSettings abaixo:

Para o tema do GTK:

```
$ gsettings set org.gnome.desktop.interface gtk-theme *nome-do-tema*

```

Para o tema de ícones:

```
$ gsettings set org.gnome.desktop.interface icon-theme *nome-do-tema*

```

**Nota:** O gerenciador de janela segue o tema do GTK. Usar `org.gnome.desktop.wm.preferences theme` está obsoleto e é ignorado.

Veja [GTK (Português)#Temas](/index.php/GTK_(Portugu%C3%AAs)#Temas "GTK (Português)") e [Ícones#Manualmente](/index.php/%C3%8Dcones#Manualmente "Ícones").

##### Altura da barra de título

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

##### Ordem de botão de barra de título

Para definir a ordem para o gerenciador de janelas do GNOME (Mutter, Metacity):

```
$ gsettings set org.gnome.desktop.wm.preferences button-layout ':minimize,maximize,close'

```

**Dica:** O caractere de dois pontos indica em qual lado da barra de título os botões de janela aparecerão.

##### Ocultar barra de título quando maximizado

*   [Instale](/index.php/Instale "Instale") [gnome-shell-extension-no-title-bar](https://aur.archlinux.org/packages/gnome-shell-extension-no-title-bar/) ou [gnome-shell-extension-no-title-bar-git](https://aur.archlinux.org/packages/gnome-shell-extension-no-title-bar-git/). Janelas maximizadas mesclam a barra de título com a barra de atividade, salvando pixels preciosos.
*   [Instale](/index.php/Instale "Instale") [mutter-hide-legacy-decorations](https://aur.archlinux.org/packages/mutter-hide-legacy-decorations/). Isso altera a configuração padrão no gerenciador de janelas, assim como oculta automaticamente a barra de título em aplicativos legados (sem barra de título) quando eles são maximizados ou colados lado a lado na lateral.
*   [Instale](/index.php/Instale "Instale") [gnome-shell-extension-pixel-saver-git](https://aur.archlinux.org/packages/gnome-shell-extension-pixel-saver-git/) ou [gnome-shell-extension-pixel-saver](https://aur.archlinux.org/packages/gnome-shell-extension-pixel-saver/). Janelas maximizadas mesclam a barra de título com a barra de atividade, salvando pixels preciosos.

##### Temas do GNOME Shell

O tema do GNOME Shell em si é configurável. Para usar um tema de Shell, primeiro assegure-se de que você tenha o pacote [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) instalado. Então, habilite a extensão *User Themes*, pelo Ajustes do GNOME ou pela página web [GNOME Shell Extensions](https://extensions.gnome.org). Temas de shell podem então ser carregadas e selecionadas usando Ajustes do GNOME.

Há vários temas de GNOME Shell disponíveis [no AUR](https://aur.archlinux.org/packages.php?O=0&K=gnome-shell-theme&do_Search=Go&PP=50&SB=v&SO=d). Temas de shell também pode ser baixados do [gnome-look.org](http://gnome-look.org/index.php?xcontentmode=191).

##### Ícones no menu

O esquema padrão do GNOME não exibe qualquer ícone nos menus. Para exibir ícones nos menus, execute o seguinte comando.

```
$ gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/ButtonImages': <1>, 'Gtk/MenuImages': <1>}"

```

#### Pastas de grade de aplicativos

**Dica:** O scripts [gnome-catgen](https://github.com/prurigro/gnome-catgen) ([gnome-catgen-git](https://aur.archlinux.org/packages/gnome-catgen-git/)) permite que você gerencie pastas por meio da criação de arquivos em `~/.local/share/applications-categories` nomeados conforme cada categoria e contendo uma lista dos arquivos de área de trabalho pertencentes aos aplicativos que você gostaria de ter dentro. Opcionalmente, você pode fazer com que ele circule por cada aplicativo sem uma pasta e insira a categoria desejada até você `Ctrl-c` ou ficar sem aplicativos.

No **dconf-editor**, navegue para `org.gnome.desktop.app-folders` e defina o valor de `folder-children` para um vetor de nomes de pastas separados por vírgula:

```
['Utilities', 'Sundry']

```

Adicione aplicativos usando o `gsettings`:

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ apps "['alacarte.desktop', 'dconf-editor.desktop']"

```

Isso adiciona os aplicativos `alacarte.desktop` e `dconf-editor.desktop` à pastas Sundry. Isso também vai criar a pasta `org.gnome.desktop.app-folders.folders.Sundry`.

Para nomear a pasta (se ela tiver nenhum nome que apareça no tipo dos aplicativos):

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ name "Sundry"

```

Os aplicativos também podem ser ordenados por sua categoria (especificada em seu arquivo *.desktop*):

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ categories "['Office']"

```

Se determinados aplicativos que corresponderem a uma categoria não forem desejados em uma pasta, exclusões podem ser definidas:

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ excluded-apps "['libreoffice-draw.desktop']"

```

Para mais informações, veja [[4]](https://gitlab.gnome.org/GNOME/gsettings-desktop-schemas/blob/master/schemas/org.gnome.desktop.app-folders.gschema.xml.in) e [[5]](https://wiki.gentoo.org/wiki/Gnome_Applications_Folders).

#### Inicialização automática

O GNOME implementa [XDG Autostart](/index.php/XDG_Autostart_(Portugu%C3%AAs) "XDG Autostart (Português)").

O [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks) permite gerenciar entradas de "autostart".

**Dica:** Se o botão de sinal de mais na seção de inicialização do Ajustes não estiver responsivo, tente iniciá-lo a partir do terminal usando o seguinte comando: `gnome-tweaks`. Veja o seguinte [tópico de fórum](https://bbs.archlinux.org/viewtopic.php?pid=1413631#p1413631).

**Nota:** O diálogo obsoleto *gnome-session-properties* pode ser adicionado [instalando](/index.php/Instala "Instala") o pacote [gnome-session-properties](https://aur.archlinux.org/packages/gnome-session-properties/).

#### Área de trabalho

##### Ícones na área de trabalho

Até o GNOME 3.28, os ícones na área de trabalho eram fornecidos pelo [Arquivos](/index.php/GNOME/Files "GNOME/Files"), que desenhava uma janela transparente sobre a área de trabalho contendo os ícones. A partir do GNOME 3.28 essa funcionalidade foi removida e os ícones da área de trabalho não estão mais disponíveis no GNOME. Possíveis soluções incluem o uso do [Nemo](/index.php/Nemo "Nemo") (um fork do Arquivos que ainda possui a funcionalidade de ícones do desktop) ou a instalação do [gnome-shell-extension-desktop-icons](https://aur.archlinux.org/packages/gnome-shell-extension-desktop-icons/), o qual replica a funcionalidade do ícone do desktop disponível no GNOME 3.26 e anteriores, mas com pequenas diferenças. Para mais informações, consulte o seguinte [tópico no fórum do Arch](https://bbs.archlinux.org/viewtopic.php?id=235633).

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

##### Desabilitar o canto superior esquerdo ativo

A partir do GNOME 3.34, você pode desabilitá-lo desta forma:

```
$ gsettings set org.gnome.desktop.interface enable-hot-corners false

```

ou por meio de [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks), em *Barra superior > Canto ativo do panorama de atividades*

#### Extensões

O catálogo de extensões está disponível em [extensions.gnome.org](https://extensions.gnome.org). Elas podem ser instaladas e ativadas no navegador definindo o botão no canto superior esquerdo da tela para **ON** e clicando em **Install** no diálogo resultante (se a extensão em questão não estiver instalada). Extensões instaladas podem ser vistas em [extensions.gnome.org/local](https://extensions.gnome.org/local/), na qual atualizações podem ser verificadas. Extensões instaladas também podem ser habilitadas ou desabilitadas usando [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks).

**Nota:** Extensões do [extensions.gnome.org](https://extensions.gnome.org) podem ser instalados imediatamente com [gnome-software](https://www.archlinux.org/packages/?name=gnome-software). Para outros navegadores, é necessário instalar [chrome-gnome-shell](https://www.archlinux.org/packages/?name=chrome-gnome-shell) e a extensão de navegador apropriada.

O GNOME Shell pode ser personalizado com extensões por usuário ou por todo o sistema. A instalação de extensões com [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") as disponibiliza para todos os usuários do sistema e automatiza o processo de atualização. O pacote [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) fornece um conjunto de extensões mantidas como parte do projeto GNOME (muitas das extensões incluídas são usadas pela sessão do GNOME Clássico). Usuários que desejem uma barra de tarefas, mas não desejam usar a sessão do GNOME Clássico, podem querer habilitar a extensão *Window list* (fornecida pelo pacote [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions)).

Para listar as extensões atualmente habilitadas:

```
$ gsettings get org.gnome.shell enabled-extensions

```

Para mais informações sobre as extensões do shell do GNOME, veja [[6]](https://extensions.gnome.org/about/).

#### Fontes

**Dica:** Se você definiu o *Fator de escala* para um valor acima de 1.00, o menu de Acessibilidade será habilitado automaticamente.

Fontes podem ser definidas para *Títulos de janelas*, *Interface* (aplicativos), *Documentos* e *Monoespaçada*. Veja a aba Fontes no Ajustes para opções relevantes.

Para *hinting*, RGBA provavelmente é melhor por atender a maioria dos tipos de monitores. Se as fontes aparecerem bloqueadas demais, reduza *hinting* para *Slight* ou *None*.

#### Métodos de entrada

O GNOME possui suporte integrado para [métodos de entrada](/index.php/M%C3%A9todos_de_entrada "Métodos de entrada") por meio do [IBus](/index.php/IBus "IBus"), só sendo necessário instalar [ibus](https://www.archlinux.org/packages/?name=ibus) e o motor do método de entrada (ex.: [ibus-libpinyin](https://www.archlinux.org/packages/?name=ibus-libpinyin) para Intelligent Pinyin); após a instalação, o motor de método de entrada podem ser adicionados como disposição de teclado nas configurações de "Idioma & região" do GNOME.

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

##### Não suspender quando a tampa do notebook é fechada

O painel de configurações do GNOME não oferece uma opção para o usuário, para alterar a ação, quando a tampa do notebook é fechada. No entanto, [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks) pode sobrescrever a configuração aplicada por [systemd](https://www.archlinux.org/packages/?name=systemd), na aba *Geral* desative a opção *Suspender quando a tampa do notebook é fechada*. O sistema não irá, portanto, *Suspender para a RAM (S3)* no fechamento da tampa.

Para alterar a ação da opção de tampa em todo o sistema, certifique-se de que a configuração descrita acima não esteja desativada e edite as configurações do systemd em `/etc/systemd/logind.conf`. Para desativar a suspensão na tampa, defina `HandleLidSwitch=ignore`, conforme descrito em [Power management#ACPI events](/index.php/Power_management#ACPI_events "Power management").

##### Alterar ação de nível crítico da bateria

O painel de configurações não fornece uma opção para alterar a ação de nível crítico de bateria. Essas configurações foram removidas também do dconf. Eles agora são gerenciados pelo upower. Edite as configurações do upower em `/etc/UPower/UPower.conf`. Encontre essas configurações e ajuste a suas necessidades.

 `/etc/UPower/UPower.conf` 
```
PercentageLow=10
PercentageCritical=3
PercentageAction=2
CriticalPowerAction=HybridSleep
```

### Usar um gerenciador de janela diferente

GNOME Shell não oferece suporte a usar um [gerenciador de janela](/index.php/Gerenciador_de_janela "Gerenciador de janela") diferente, porém o [GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback") forence sessões para Metacity e [Compiz](/index.php/Compiz "Compiz"). Além disso, é possível definir suas próprias [sessões GNOME personalizadas](/index.php/GNOME/Tips_and_tricks#Custom_GNOME_sessions "GNOME/Tips and tricks") que usam componentes alternativos.

## Veja também

*   [Site oficial](https://www.gnome.org/)
*   [Artigo do Wikipédia](https://en.wikipedia.org/wiki/pt:GNOME "wikipedia:pt:GNOME")
*   [GNOME-Shell Extensions](https://extensions.gnome.org/)
*   [Folha de dicas do GNOME Shell](https://wiki.gnome.org/Projects/GnomeShell/CheatSheet)
*   Personalização (temas, ícones...):
    *   [Personalize GNOME](https://wiki.gnome.org/Personalization)
    *   [GNOME Look](https://www.gnome-look.org/)
*   Aplicativos do GNOME:
    *   [Índice dos aplicativos do GNOME](https://wiki.gnome.org/Apps)
    *   [Aplicativos Centrais do GNOME](https://en.wikipedia.org/wiki/GNOME_Core_Applications "wikipedia:GNOME Core Applications")
*   Código-fonte/Espelhos do GNOME:
    *   [GitLab do GNOME](https://gitlab.gnome.org/)
    *   [Espelho do GNOME no Github](https://github.com/GNOME)