**Status de tradução:** Esse artigo é uma tradução de [KDE](/index.php/KDE "KDE"). Data da última tradução: 2019-11-21\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=KDE&diff=0&oldid=589703) na versão em inglês.

Artigos relacionados

*   [Ambiente de desktop](/index.php/Ambiente_de_desktop "Ambiente de desktop")
*   [Gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição")
*   [Gerenciador de janela](/index.php/Gerenciador_de_janela "Gerenciador de janela")
*   [Qt](/index.php/Qt "Qt")
*   [SDDM](/index.php/SDDM "SDDM")
*   [Dolphin](/index.php/Dolphin "Dolphin")
*   [Carteira do KDE](/index.php/KDE_Wallet "KDE Wallet")
*   [KDevelop](/index.php/KDevelop "KDevelop")
*   [Trinity](/index.php/Trinity "Trinity")
*   [Visual uniforme para aplicativos Qt e GTK](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications")

O KDE é um projeto de software que atualmente compreende um [ambiente de desktop](/index.php/Ambiente_de_desktop "Ambiente de desktop") conhecido como Plasma, uma coleção de bibliotecas e frameworks (KDE Frameworks) e vários aplicativos (aplicativos do KDE) também. O upstream KDE tem um [wiki de UserBase](https://userbase.kde.org/Welcome_to_KDE_UserBase/pt-br) bem mantido. Informações detalhadas sobre a maioria dos aplicativos do KDE podem ser encontradas lá.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
    *   [1.1 Plasma](#Plasma)
    *   [1.2 Aplicativos do KDE](#Aplicativos_do_KDE)
    *   [1.3 Lançamentos instáveis](#Lançamentos_instáveis)
*   [2 Iniciando o Plasma](#Iniciando_o_Plasma)
    *   [2.1 Usando um gerenciador de exibição](#Usando_um_gerenciador_de_exibição)
    *   [2.2 Do console](#Do_console)
*   [3 Configuração](#Configuração)
    *   [3.1 Personalização](#Personalização)
        *   [3.1.1 Plasma desktop](#Plasma_desktop)
            *   [3.1.1.1 Temas](#Temas)
                *   [3.1.1.1.1 Aparência de aplicativos Qt e GTK](#Aparência_de_aplicativos_Qt_e_GTK)
            *   [3.1.1.2 Rosto](#Rosto)
            *   [3.1.1.3 Widgets](#Widgets)
            *   [3.1.1.4 Miniaplicativo de som de área de notificação](#Miniaplicativo_de_som_de_área_de_notificação)
            *   [3.1.1.5 Desabilitar sombra do painel](#Desabilitar_sombra_do_painel)
        *   [3.1.2 Decorações de janela](#Decorações_de_janela)
        *   [3.1.3 Temas de ícone](#Temas_de_ícone)
        *   [3.1.4 Eficiência de espaço](#Eficiência_de_espaço)
        *   [3.1.5 Geração de miniatura](#Geração_de_miniatura)
    *   [3.2 Impressão](#Impressão)
    *   [3.3 Suporte a Windows/Samba](#Suporte_a_Windows/Samba)
    *   [3.4 Atividades do ambiente KDE](#Atividades_do_ambiente_KDE)
    *   [3.5 Gerenciamento de energia](#Gerenciamento_de_energia)
    *   [3.6 Inicialização automática](#Inicialização_automática)
    *   [3.7 Phonon](#Phonon)
        *   [3.7.1 Qual backend eu devo escolher?](#Qual_backend_eu_devo_escolher?)
*   [4 Aplicativos](#Aplicativos)
    *   [4.1 Administração do sistema](#Administração_do_sistema)
        *   [4.1.1 Encerrar o servidor Xorg por meio de Configurações do Sistema KDE](#Encerrar_o_servidor_Xorg_por_meio_de_Configurações_do_Sistema_KDE)
        *   [4.1.2 KCM](#KCM)
    *   [4.2 Pesquisa do ambiente](#Pesquisa_do_ambiente)
    *   [4.3 Navegadores web](#Navegadores_web)
    *   [4.4 PIM](#PIM)
        *   [4.4.1 Akonadi](#Akonadi)
            *   [4.4.1.1 MySQL](#MySQL)
                *   [4.4.1.1.1 Instância de MySQL para todo o sistema](#Instância_de_MySQL_para_todo_o_sistema)
            *   [4.4.1.2 PostgreSQL](#PostgreSQL)
                *   [4.4.1.2.1 Instância de PostgreSQL por usuário](#Instância_de_PostgreSQL_por_usuário)
                *   [4.4.1.2.2 Instância de PostgreSQL para todo o sistema](#Instância_de_PostgreSQL_para_todo_o_sistema)
            *   [4.4.1.3 SQLite](#SQLite)
            *   [4.4.1.4 Desabilitando Akonadi](#Desabilitando_Akonadi)
    *   [4.5 KDE Telepathy](#KDE_Telepathy)
        *   [4.5.1 Usar Telegram com KDE Telepathy](#Usar_Telegram_com_KDE_Telepathy)
    *   [4.6 KDE Connect](#KDE_Connect)
*   [5 Dicas e truques](#Dicas_e_truques)
    *   [5.1 Usar um gerenciador de janela diferente](#Usar_um_gerenciador_de_janela_diferente)
        *   [5.1.1 Sessão KDE/Openbox](#Sessão_KDE/Openbox)
        *   [5.1.2 Reabilitar efeitos de composição](#Reabilitar_efeitos_de_composição)
    *   [5.2 Configurando resolução do monitor / vários monitores](#Configurando_resolução_do_monitor_/_vários_monitores)
    *   [5.3 KWin-lowlatency](#KWin-lowlatency)
    *   [5.4 Configurando perfis ICC](#Configurando_perfis_ICC)
    *   [5.5 Desabilitar a abertura do lançador de aplicativos com a tecla Super (tecla Windows)](#Desabilitar_a_abertura_do_lançador_de_aplicativos_com_a_tecla_Super_(tecla_Windows))
    *   [5.6 Desabilitar exibição de Favoritos no menu de aplicativos](#Desabilitar_exibição_de_Favoritos_no_menu_de_aplicativos)
*   [6 Solução de problemas](#Solução_de_problemas)
    *   [6.1 Fontes](#Fontes)
        *   [6.1.1 Fontes em uma sessão do Plasma têm visual ruim](#Fontes_em_uma_sessão_do_Plasma_têm_visual_ruim)
        *   [6.1.2 Fontes são gigantes ou parecem desproporcionais](#Fontes_são_gigantes_ou_parecem_desproporcionais)
    *   [6.2 Configuração relatada](#Configuração_relatada)
        *   [6.2.1 O ambiente Plasma se comporta de forma estranha](#O_ambiente_Plasma_se_comporta_de_forma_estranha)
        *   [6.2.2 Limpar cache para resolver problemas de atualização](#Limpar_cache_para_resolver_problemas_de_atualização)
        *   [6.2.3 Teclas de controle do volume, notificações e multimídia não funcionam](#Teclas_de_controle_do_volume,_notificações_e_multimídia_não_funcionam)
        *   [6.2.4 A tela de autenticação KCM não sincroniza as configurações do cursor para SDDM](#A_tela_de_autenticação_KCM_não_sincroniza_as_configurações_do_cursor_para_SDDM)
    *   [6.3 Problemas gráficos](#Problemas_gráficos)
        *   [6.3.1 Obtendo o estado atual de KWin para propósito de suporte e depuração](#Obtendo_o_estado_atual_de_KWin_para_propósito_de_suporte_e_depuração)
        *   [6.3.2 Desabilitar efeitos do ambiente manualmente ou automaticamente para aplicativos definidos](#Desabilitar_efeitos_do_ambiente_manualmente_ou_automaticamente_para_aplicativos_definidos)
        *   [6.3.3 Habilitar transparência](#Habilitar_transparência)
        *   [6.3.4 Desabilitar composição](#Desabilitar_composição)
        *   [6.3.5 Oscilação em tela cheia quando composição está habilitada](#Oscilação_em_tela_cheia_quando_composição_está_habilitada)
        *   [6.3.6 Imagem quebrada com NVIDIA](#Imagem_quebrada_com_NVIDIA)
        *   [6.3.7 O cursor do Plasma algumas vezes é mostrado incorretamente](#O_cursor_do_Plasma_algumas_vezes_é_mostrado_incorretamente)
        *   [6.3.8 Resolução de tela inutilizável definida](#Resolução_de_tela_inutilizável_definida)
        *   [6.3.9 Ícones borrados na área de notificação](#Ícones_borrados_na_área_de_notificação)
    *   [6.4 Problemas de som](#Problemas_de_som)
        *   [6.4.1 Nenhum som após a suspensão](#Nenhum_som_após_a_suspensão)
        *   [6.4.2 Arquivos MP3 não pode ser reproduzidos usando o backend GStreamer Phonon](#Arquivos_MP3_não_pode_ser_reproduzidos_usando_o_backend_GStreamer_Phonon)
    *   [6.5 Gerenciamento de energia](#Gerenciamento_de_energia_2)
        *   [6.5.1 Nenhuma opção de suspensão/hibernação](#Nenhuma_opção_de_suspensão/hibernação)
    *   [6.6 KMail](#KMail)
        *   [6.6.1 Limpar a configuração do Akonadi para corrigir o KMail](#Limpar_a_configuração_do_Akonadi_para_corrigir_o_KMail)
        *   [6.6.2 Esvaziar a caixa de entrada IMAP no KMail](#Esvaziar_a_caixa_de_entrada_IMAP_no_KMail)
        *   [6.6.3 Erros de autorização par a conta EWS no KMail](#Erros_de_autorização_par_a_conta_EWS_no_KMail)
    *   [6.7 Rede](#Rede)
        *   [6.7.1 Congela ao usar montagem automática em um volume NFS](#Congela_ao_usar_montagem_automática_em_um_volume_NFS)
    *   [6.8 Registro log agressivo do QXcbConnection](#Registro_log_agressivo_do_QXcbConnection)
    *   [6.9 Aplicativos KF5/Qt 5 não exibem ícones em i3/FVWM/awesome](#Aplicativos_KF5/Qt_5_não_exibem_ícones_em_i3/FVWM/awesome)
    *   [6.10 Problemas com salvar credenciais e ocorrendo persistentemente diálogos do KWallet](#Problemas_com_salvar_credenciais_e_ocorrendo_persistentemente_diálogos_do_KWallet)
    *   [6.11 Descoberta não mostra qualquer aplicativos](#Descoberta_não_mostra_qualquer_aplicativos)
    *   [6.12 Alto uso de CPU de kscreenlocker_greet com drivers da NVIDIA](#Alto_uso_de_CPU_de_kscreenlocker_greet_com_drivers_da_NVIDIA)
    *   [6.13 OS error 22 ao executar Akonadi no ZFS](#OS_error_22_ao_executar_Akonadi_no_ZFS)
    *   [6.14 Alguns programas não conseguem rolar o texto quando suas janelas estão inativas](#Alguns_programas_não_conseguem_rolar_o_texto_quando_suas_janelas_estão_inativas)
    *   [6.15 TeamViewer está lento](#TeamViewer_está_lento)
*   [7 Veja também](#Veja_também)

## Instalação

### Plasma

Antes de instalar o Plasma, certifique-se de ter uma instalação [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)") em funcionamento no seu sistema.

[Instale](/index.php/Instale "Instale") o meta-pacote [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) ou o grupo [plasma](https://www.archlinux.org/groups/x86_64/plasma/). Para diferenças entre [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) e [plasma](https://www.archlinux.org/groups/x86_64/plasma/), consulte [Grupo de pacotes](/index.php/Grupo_de_pacotes "Grupo de pacotes"). Como alternativa, para uma instalação mínima de Plasma, instale o pacote [plasma-desktop](https://www.archlinux.org/packages/?name=plasma-desktop).

Para habilitar o suporte a [Wayland](/index.php/Wayland_(Portugu%C3%AAs) "Wayland (Português)") no Plasma, instale também o pacote [plasma-wayland-session](https://www.archlinux.org/packages/?name=plasma-wayland-session).

### Aplicativos do KDE

Para instalar o conjunto completo de Aplicativos do KDE, instale o grupo [kde-applications](https://www.archlinux.org/groups/x86_64/kde-applications/) ou o meta-pacote [kde-applications-meta](https://www.archlinux.org/packages/?name=kde-applications-meta). Observe que isso só instalará aplicativos, não instalará nenhuma versão do Plasma.

### Lançamentos instáveis

Veja [Repositórios oficiais#kde-unstable](/index.php/Reposit%C3%B3rios_oficiais#kde-unstable "Repositórios oficiais")

## Iniciando o Plasma

**Nota:** Apesar de ser possível iniciar o Plasma no [Wayland](/index.php/Wayland_(Portugu%C3%AAs) "Wayland (Português)"), há alguns recursos em falta e alguns problemas conhecidos. Veja [Wayland Showstoppers](https://community.kde.org/Plasma/Wayland_Showstoppers) para uma lista de problemas e o [quadro de trabalho para Plasma no Wayland](https://phabricator.kde.org/project/board/99/) para o estado atual do desenvolvimento. Use [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)") para a experiência mais completa e estável.

Plasma pode ser iniciado usando um [gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição") ou o console.

### Usando um gerenciador de exibição

*   Selecione *Plasma* para iniciar uma nova sessão no [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)").
*   [Instale](/index.php/Instale "Instale") [plasma-wayland-session](https://www.archlinux.org/packages/?name=plasma-wayland-session) e selecione *Plasma (Wayland)* para iniciar uma nova sessão no [Wayland](/index.php/Wayland_(Portugu%C3%AAs) "Wayland (Português)").

### Do console

*   Para iniciar o Plasma com [xinit/startx](/index.php/Xinit_(Portugu%C3%AAs) "Xinit (Português)"), anexe `exec startplasma-x11` ao seu arquivo `.xinitrc`. Se você quiser iniciar o Xorg no login, consulte [Iniciar X no login](/index.php/Iniciar_X_no_login "Iniciar X no login").
*   Para iniciar uma sessão do Plasma no Wayland a partir de um console, execute `XDG_SESSION_TYPE=wayland dbus-run-session startplasma-wayland`.[[1]](https://community.kde.org/KWin/Wayland#Start_a_Plasma_session_on_Wayland)

## Configuração

A maioria das configurações para aplicativos do KDE é armazenada em `~/.config/`. No entanto, a configuração do KDE é feita principalmente através do aplicativo **Configurações do sistema**. Pode ser iniciado a partir de um terminal executando `systemsettings5`.

### Personalização

#### Plasma desktop

##### Temas

[Temas de Plasma](https://store.kde.org/browse/cat/104/) definem a aparência de painéis e plasmoides. Para facilitar a instalação em todo o sistema, alguns temas estão disponíveis nos repositórios oficiais e no [AUR](https://aur.archlinux.org/packages.php?K=plasma+theme).

Temas do Plasma também podem ser instalados por meio de *Configurações do sistema > Tema do Espaço de Trabalho > Tema do Plasma > Baixar novos temas da Internet*.

O [KDE-Store](https://store.kde.org/) oferece mais personalizações ao Plasma, como temas do [SDDM](/index.php/SDDM "SDDM") e telas de inicialização (*splash-screens*).

###### Aparência de aplicativos Qt e GTK

**Dica:** Para consistência no tema de Qt e GTK, veja [Aparência uniforme para aplicativos Qt e GTK](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications").

	Qt4

O Breeze não está diretamente disponível para o Qt4, já que ele não pode ser compilado sem os pacotes do KDE 4, que foram retirados do repositório extra em agosto de 2018 ([FS#59784](https://bugs.archlinux.org/task/59784)). No entanto, você pode instalar o [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk) e escolher o GTK como estilo da interface executando `qtconfig-qt4`.

	GTK

O tema recomendado para uma aparência agradável em aplicativos GTK é o [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk), um tema GTK projetado para imitar a aparência do tema Breeze do Plasma. Instale [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config) (parte do grupo [plasma](https://www.archlinux.org/groups/x86_64/plasma/)) e selecione `Breeze` ou `Breeze-Dark` como o tema GTK2/GTK3 em *Configurações do sistema > Estilo do aplicativo > Estilo dos aplicativos GNOME/GTK*.

Em alguns temas, as dicas de ferramentas nos aplicativos GTK têm texto branco em fundo branco, dificultando a leitura. Para alterar as cores nos aplicativos GTK2, encontre a seção para dicas de ferramentas no arquivo `.gtkrc-2.0` e altere-a. Para aplicativo GTK3, dois arquivos precisam ser alterados, `gtk.css` e `settings.ini`.

Alguns programas GTK2 como [vuescan-bin](https://aur.archlinux.org/packages/vuescan-bin/) ainda parecem pouco utilizáveis devido a caixas de seleção invisíveis com a capa Breeze ou Adwaita em uma sessão de Plasma. Para resolver isso, instale e selecione, por exemplo, o tema Numix-Frost-Light do [numix-frost-themes](https://aur.archlinux.org/packages/numix-frost-themes/) em *Configurações do sistema* > *Estilo dos aplicativos* > *Estilo dos aplicativos GNOME/GTK* > *Tema GTK2:*. Numix-Frost-Light se parece com o Breeze.

##### Rosto

O rosto do usuário pode ser definido por *Configurações do sistema > Detalhes da conta > Gerenciador de Usuários*.

Se *Gerenciador de Usuários* não foi encontrado, instale [user-manager](https://www.archlinux.org/packages/?name=user-manager) para obtê-lo.

##### Widgets

Plasmoides são pequenos aplicativos do KDE em scripts (scripts plasmoides) ou em códigos (binários plasmoides) projetados para melhorar a funcionalidade do seu ambiente gráfico.

A maneira mais fácil de instalar scripts plasmoides é clicando com o botão direito do mouse em um painel ou na área de trabalho e escolhendo *Adicionar widgets > Baixar novos widgets... > Baixar novos widgets do Plasma*. Isto irá apresentar um bom frontend para [https://store.kde.org/](https://store.kde.org/) que permite instalar, desinstalar ou atualizar scripts de plasmoides de terceiros com literalmente apenas um clique.

Muitos binários plasmoides estão disponíveis no [AUR](https://aur.archlinux.org/packages.php?K=plasmoid).

##### Miniaplicativo de som de área de notificação

[Instale](/index.php/Instale "Instale") [plasma-pa](https://www.archlinux.org/packages/?name=plasma-pa) ou [kmix](https://www.archlinux.org/packages/?name=kmix) (inicie Kmix a partir do Lançador de aplicativos). [plasma-pa](https://www.archlinux.org/packages/?name=plasma-pa) está agora instalado por padrão com [plasma](https://www.archlinux.org/groups/x86_64/plasma/), nenhuma outra configuração é necessária.

**Nota:** Para ajustar o [tamanho das etapas de aumento/redução do volume](https://bugs.kde.org/show_bug.cgi?id=313579#c28), adicione, por exemplo, `VolumePercentageStep=1` na seção `[Global]` de `~/.config/kmixrc`.

##### Desabilitar sombra do painel

Como o painel do Plasma está em cima de outras janelas, sua sombra é desenhada sobre elas. [[2]](https://bbs.archlinux.org/viewtopic.php?pid=1228394#p1228394) Para desabilitar esse comportamento sem afetar outras sombras, [instale](/index.php/Instale "Instale") [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) e execute:

```
$ xprop -remove _KDE_NET_WM_SHADOW

```

em seguida, selecione o painel com o cursor de tamanho maior. [[3]](https://forum.kde.org/viewtopic.php?f=285&t=121592) Para automação, instale o [xorg-xwininfo](https://www.archlinux.org/packages/?name=xorg-xwininfo) e crie o seguinte script:

 `/usr/local/bin/kde-no-shadow` 
```
#!/bin/bash
for WID in $(xwininfo -root -tree | sed '/"Plasma": ("plasmashell" "plasmashell")/!d; s/^  *\([^ ]*\) .*/\1/g'); do
   xprop -id $WID -remove _KDE_NET_WM_SHADOW
done

```

Defina permissões de execução para o script:

```
# chmod 755 /usr/local/bin/kde-no-shadow

```

O script pode ser executar ao iniciar sessão com *Adicionar script* em *Iniciar automaticamente*:

```
$ kcmshell5 autostart

```

#### Decorações de janela

[Decorações da janela](https://store.kde.org/browse/cat/114/) podem ser alteradas em *Configurações do sistema > Estilo dos aplicativos > Decorações da janela*.

Lá você também pode baixar e instalar diretamente mais temas com um clique e alguns disponíveis no [AUR](https://aur.archlinux.org/packages.php?K=kde+window+decoration).

#### Temas de ícone

Temas de ícones podem ser instalados e alterados em *Configurações do sistema > Ícones*.

**Nota:** Embora todos os ambientes modernos do Linux compartilhem o mesmo formato de tema de ícones, os ambientes como o [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)") usam menos ícones (especialmente em menus e barras de ferramentas). Os temas desenvolvidos para esses ambientes geralmente não possuem ícones exigidos pelos aplicativos Plasma e KDE. Recomenda-se a instalação de temas de ícones compatíveis com o Plasma.

**Dica:** Como alguns temas de ícones não herdam o tema de ícones padrão, alguns ícones podem estar faltando. Para herdar do Breeze, adicione `breeze` ao array `Inherits=` em `/usr/share/icon/*nome-do-tema*/index.theme`, por exemplo: `Inherits=breeze,hicolor`. Você precisa reaplicar este patch após cada atualização do tema do ícone, considere o uso de [hooks do pacman](/index.php/Hooks_do_pacman "Hooks do pacman") para automatizar o processo.

#### Eficiência de espaço

O shell Plasma Netbook foi retirado do Plasma 5, veja a seguinte [publicação do fórum do KDE](https://forum.kde.org/viewtopic.php?f=289&t=126631&p=335947&hilit=plasma+netbook#p335899). No entanto, você pode conseguir algo semelhante editando o arquivo `~/.config/kwinrc` adicionando `BorderlessMaximizedWindows=true` na seção `[Windows]`.

#### Geração de miniatura

Para permitir a geração de miniaturas para arquivos de mídia ou documentos na área de trabalho e no Dolphin, instale o [kdegraphics-thumbnailers](https://www.archlinux.org/packages/?name=kdegraphics-thumbnailers) e o [ffmpegthumbs](https://www.archlinux.org/packages/?name=ffmpegthumbs).

Em seguida, ative as categorias de miniaturas para a área de trabalho através de *clique direito* no *plano de fundo da área de trabalho* > *Configurar área de trabalho* > *Ícones* > *Mais Opções de Prévia...*.

No *Dolphin*, navegue até *Controle* > *Configurar o Dolphin...* > *Geral* > *Visualizações*.

### Impressão

**Dica:** Use a interface web do [CUPS](/index.php/CUPS "CUPS") para uma configuração mais rápida. As impressoras configuradas dessa maneira podem ser usadas nos aplicativos do KDE.

Você também pode configurar impressoras em *Configurações do sistema > Impressoras*. Para usar este método, você deve primeiro instalar [print-manager](https://www.archlinux.org/packages/?name=print-manager) e [cups](https://www.archlinux.org/packages/?name=cups). Veja [CUPS#Configuration](/index.php/CUPS#Configuration "CUPS").

### Suporte a Windows/Samba

Se você quiser ter acesso aos serviços do Windows, instale o [Samba](/index.php/Samba "Samba") (pacote [samba](https://www.archlinux.org/packages/?name=samba)).

A funcionalidade de compartilhamento do Dolphin requer o pacote [kdenetwork-filesharing](https://www.archlinux.org/packages/?name=kdenetwork-filesharing) e usershares, que o arquivo `smb.conf` não habilitou. As instruções para adicioná-las estão no [Samba#Enable Usershares](/index.php/Samba#Enable_Usershares "Samba"), após o qual o compartilhamento no Dolphin deve funcionar imediatamente após o reinício do Samba.

**Dica:** Use `*` (asterisco) para nome de usuário e senha ao acessar um compartilhamento do Windows sem autenticação no prompt do Dolphin.

Ao contrário dos navegadores de arquivos GTK que utilizam o GVfs também para o programa iniciado, abrir arquivos de compartilhamentos Samba no Dolphin via KIO faz com que o Plasma copie o arquivo inteiro para o sistema local primeiro com a maioria dos programas (VLC é uma exceção). Para resolver isso, você pode usar um navegador de arquivos baseado em GTK como [thunar](https://www.archlinux.org/packages/?name=thunar) com [gvfs](https://www.archlinux.org/packages/?name=gvfs) e [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb) (e [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring) para salvar credenciais de login) para acessar compartilhamentos SMB de uma maneira mais eficiente.

Outra possibilidade é [montar](/index.php/Mount "Mount") um compartilhamento Samba via [cifs-utils](https://www.archlinux.org/packages/?name=cifs-utils) para fazer com que pareça o Plasma como se o compartilhamento SMB fosse apenas uma pasta local normal e, portanto, pudesse ser acessado normalmente. Veja [Samba#Manual mounting](/index.php/Samba#Manual_mounting "Samba") e [Samba#Automatic mounting](/index.php/Samba#Automatic_mounting "Samba").

Uma solução de GUI está disponível com [samba-mounter-git](https://aur.archlinux.org/packages/samba-mounter-git/), que oferece basicamente a mesma funcionalidade através de uma opção fácil de usar localizada em *Configurações do sistema* > *Drivers de Rede*. No entanto, pode quebrar com novas versões do KDE Plasma.

### Atividades do ambiente KDE

[Atividades do ambiente KDE](https://userbase.kde.org/Plasma/pt-br#Atividades) são espaços especiais nos quais você pode selecionar configurações específicas para cada atividade que se aplica apenas quando você está usando aquela atividade.

### Gerenciamento de energia

[Instale](/index.php/Instale "Instale") [powerdevil](https://www.archlinux.org/packages/?name=powerdevil) para um serviço integrado de gerenciamento de energia Plasma. Este serviço oferece recursos adicionais de economia de energia, controle de brilho do monitor (se suportado) e relatório de bateria, incluindo dispositivos periféricos.

Um pacote alternativo sem dependências [NetworkManager](/index.php/NetworkManager_(Portugu%C3%AAs) "NetworkManager (Português)") e [Bluez](/index.php/Bluez "Bluez") é fornecido por [powerdevil-light](https://aur.archlinux.org/packages/powerdevil-light/).

**Nota:** O Powerdevil não pode [inibir](/index.php/Power_management#Power_managers "Power management") todas as configurações de logins (como a ação de fechamento da tampa para laptops). Nesses casos, a própria configuração do logind precisará ser alterada - consulte [Power management#Power management with systemd](/index.php/Power_management#Power_management_with_systemd "Power management").

### Inicialização automática

O Plasma pode iniciar automaticamente aplicativos e executar scripts na inicialização e no desligamento. Para iniciar automaticamente um aplicativo, navegue até *Configurações do sistema > Inicialização e desligamento > Iniciar automaticamente" e adicione o programa ou shell script de sua escolha. Para aplicativos, um arquivo* .desktop *será criado, para scripts de shell, um link simbólico será criado.*

**Nota:**

*   Os programas podem ser iniciados automaticamente somente no login, enquanto os shell scripts também podem ser executados no desligamento ou até mesmo antes do início do Plasma.
*   Os scripts do shell só serão executados se estiverem marcados com [executável](/index.php/Execut%C3%A1vel "Executável").

*   Coloque [entradas de desktop](/index.php/Entradas_de_desktop "Entradas de desktop") (p.ex., arquivos *.desktop*) no diretório de [inicialização automática XDG](/index.php/XDG_Autostart_(Portugu%C3%AAs) "XDG Autostart (Português)") apropriado.

*   Coloque ou faça link simbólico para scripts shell em um dos seguintes diretórios:

	`~/.config/plasma-workspace/env/`

	para executar scripts no login antes de iniciar o Plasma.

	`~/.config/autostart-scripts/`

	para executar scripts no login.

	`~/.config/plasma-workspace/shutdown/`

	para executar scripts no desligamento.

### Phonon

Do [Wikipedia](https://en.wikipedia.org/wiki/Phonon_(software) "wikipedia:Phonon (software)"):

	Phonon é a API multimídia fornecida pelo KDE e é a abstração padrão para lidar com fluxos multimídia no software KDE e também usada por vários aplicativos Qt.

	Phonon foi originalmente criado para permitir que o software KDE e Qt seja independente de qualquer estrutura multimídia única, como GStreamer ou xine, e fornecer uma API estável para a vida útil de uma grande versão.

O Phonon está sendo amplamente usado no KDE, tanto para áudio (por exemplo, as notificações do sistema ou aplicativos de áudio do KDE) como para vídeo (por exemplo, as miniaturas de vídeo do [Dolphin](/index.php/Dolphin "Dolphin")).

#### Qual backend eu devo escolher?

Você pode escolher entre backends baseados no [GStreamer](/index.php/GStreamer "GStreamer") e [VLC](/index.php/VLC "VLC") – cada um disponível em versões para aplicativos Qt4 e aplicativos Qt5 ([phonon-qt4-gstreamer](https://aur.archlinux.org/packages/phonon-qt4-gstreamer/), [phonon-qt5-gstreamer](https://www.archlinux.org/packages/?name=phonon-qt5-gstreamer) – [phonon-qt4-vlc](https://aur.archlinux.org/packages/phonon-qt4-vlc/), [phonon-qt5-vlc](https://www.archlinux.org/packages/?name=phonon-qt5-vlc)).

[Upstream prefere VLC](https://www.phoronix.com/scan.php?page=news_item&px=MTUwNDM), mas proeminentes distribuições Linux (Kubuntu e Fedora-KDE, por exemplo) preferem o GStreamer porque isso permite que eles deixem de fora facilmente os codecs MPEG patenteados da instalação padrão. Ambos os backends têm um conjunto de recursos um pouco diferente [[4]](https://community.kde.org/Phonon/FeatureMatrix). O backend do Gstreamer possui alguma dependência de codec opcional, instale-os conforme necessário:

*   [gst-libav](https://www.archlinux.org/packages/?name=gst-libav) — Codecs de libav.
*   [gst-plugins-good](https://www.archlinux.org/packages/?name=gst-plugins-good) — Suporte a PulseAudio e codecs adicionais.
*   [gst-plugins-ugly](https://www.archlinux.org/packages/?name=gst-plugins-ugly) — codecs adicionais.
*   [gst-plugins-bad](https://www.archlinux.org/packages/?name=gst-plugins-bad) — codecs adicionais.

No passado, outros backends também foram desenvolvidos, mas não são mais mantidos e seus pacotes AUR foram excluídos.

**Nota:**

*   Vários backends podem ser instalados de uma só vez e priorizado por meio do aplicativo *phononsettings*.
*   De acordo com os [fóruns do KDE](https://forum.kde.org/viewtopic.php?f=250&t=126476&p=335080), o backend VLC carece de suporte para [ReplayGain](https://en.wikipedia.org/wiki/ReplayGain "wikipedia:ReplayGain").
*   Se usar o backend do VLC, você poderá encontrar travamentos toda vez que o Plasma quiser lhe enviar um aviso sonoro e em vários outros casos também [[5]](https://forum.kde.org/viewtopic.php?f=289&t=135956). Uma possível correção é reconstruir o cache de plugins do VLC:

 `# /usr/lib/vlc/vlc-cache-gen /usr/lib/vlc/plugins` 

## Aplicativos

O projeto KDE fornece um conjunto de aplicativos que se integram ao desktop Plasma. Veja o grupo [kde-applications](https://www.archlinux.org/groups/x86_64/kde-applications/) para uma lista completa dos aplicativos disponíveis. Veja também [Category: KDE](/index.php/Category:KDE "Category:KDE") para páginas de aplicativos relacionadas ao KDE.

Além dos programas fornecidos nos aplicativos do KDE, há muitos outros aplicativos disponíveis que podem complementar o ambiente do Plasma. Alguns destes são discutidos abaixo.

### Administração do sistema

#### Encerrar o servidor Xorg por meio de Configurações do Sistema KDE

Navegue até o submenu *Configurações do sistema > Dispositivos de entrada > Teclado > Avançado (aba) > "Sequência de teclas para mantar o servidor X"* e verifique se a caixa de seleção está marcada.

#### KCM

KCM significa **KC**onfig **M**odule. Os KCMs podem ajudá-lo a configurar seu sistema fornecendo interfaces nas configurações do sistema, ou através da linha de comando com *kcmshell5*.

*   **sddm-kcm** — Módulo de configuração do KDE para [SDDM](/index.php/SDDM "SDDM").

	[https://cgit.kde.org/sddm-kcm.git](https://cgit.kde.org/sddm-kcm.git) || [sddm-kcm](https://www.archlinux.org/packages/?name=sddm-kcm)

*   **kde-gtk-config** — Configurador GTK2 e GTK3 para KDE.

	[https://cgit.kde.org/kde-gtk-config.git](https://cgit.kde.org/kde-gtk-config.git) || [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config)

*   **System policies** — Configuração de módulos de configuração que permite ao administrador alterar as configurações [PolicyKit](/index.php/PolicyKit "PolicyKit").

	[https://cgit.kde.org/polkit-kde-kcmodules-1.git](https://cgit.kde.org/polkit-kde-kcmodules-1.git) || [kcm-polkit-kde-git](https://aur.archlinux.org/packages/kcm-polkit-kde-git/)

*   **wacom tablet** — Interface gráfica do KDE para drivers Linux de Wacom.

	[https://www.linux-apps.com/p/1127862/](https://www.linux-apps.com/p/1127862/) || [kcm-wacomtablet](https://www.archlinux.org/packages/?name=kcm-wacomtablet)

*   **Kcmsystemd** — Módulo de controle de systemd para KDE.

	[https://github.com/rthomsen/kcmsystemd](https://github.com/rthomsen/kcmsystemd) || [systemd-kcm](https://aur.archlinux.org/packages/systemd-kcm/)

Mais KCMs podem ser encontrados em [linux-apps.com](https://www.linux-apps.com/search?projectSearchText=KCM).

### Pesquisa do ambiente

O KDE implementa a pesquisa na área de trabalho com um software chamado [Baloo](/index.php/Baloo "Baloo"), uma solução de indexação e busca de arquivos.

### Navegadores web

Os seguintes navegadores da web podem se integrar ao Plasma:

*   **[Konqueror](https://en.wikipedia.org/wiki/Konqueror "wikipedia:Konqueror")** — Parte do projeto KDE, possui suporte a dois motores de renderização – o KHTML e o Qt WebEngine baseado no [Chromium](/index.php/Chromium "Chromium").

	[https://konqueror.org/](https://konqueror.org/) || [konqueror](https://www.archlinux.org/packages/?name=konqueror)

*   **[Falkon](https://en.wikipedia.org/wiki/Falkon "wikipedia:Falkon")** — Um navegador web Qt com recursos de integração do Plasma, anteriormente conhecido como Qupzilla. Ele usa o Qt WebEngine.

	[https://userbase.kde.org/Falkon/](https://userbase.kde.org/Falkon/) || [falkon](https://www.archlinux.org/packages/?name=falkon)

*   **[Chromium](/index.php/Chromium "Chromium")** — O Chromium e sua variante proprietária, o Google Chrome, têm uma integração limitada ao Plasma. [Eles podem usar o KWallet](/index.php/KDE_Wallet#KDE_Wallet_for_Chrome_and_Chromium "KDE Wallet") e janelas de abrir/salvar do KDE.

	[https://www.chromium.org/](https://www.chromium.org/) || [chromium](https://www.archlinux.org/packages/?name=chromium)

*   **[Firefox](/index.php/Firefox "Firefox")** — Firefox pode ser configurado para melhor integrar ao Plasma. Veja [integração do Firefox com KDE](/index.php/Firefox#KDE/GNOME_integration "Firefox") para detalhes.

	[https://mozilla.org/firefox](https://mozilla.org/firefox) || [firefox](https://www.archlinux.org/packages/?name=firefox)

**Dica:** A partir do Plasma 5.13, pode-se integrar [Firefox](/index.php/Firefox "Firefox") ou [Chrome](/index.php/Chrome "Chrome") ao Plasma: fornecendo controle de reprodução de mídia a partir da área de notificação do Plasma, download de notificações e encontrar abas abertas no KRunner. [Instale](/index.php/Instale "Instale") [plasma-browser-integration](https://www.archlinux.org/packages/?name=plasma-browser-integration) e a extensão correspondente do navegador. O suporte para Chrome/Chromium já deve estar incluído, para o complemento do Firefox veja [Firefox#KDE/GNOME integration](/index.php/Firefox#KDE/GNOME_integration "Firefox").

### PIM

O KDE oferece sua própria pilha para [gerenciamento de informações pessoais](https://en.wikipedia.org/wiki/Personal_information_management "wikipedia:Personal information management") (PIM). Isso inclui e-mails, contatos, calendário, etc. Para instalar todos os pacotes PIM, você pode usar o grupo de pacotes [kdepim](https://www.archlinux.org/groups/x86_64/kdepim/) ou o metapacote [kdepim-meta](https://www.archlinux.org/packages/?name=kdepim-meta).

#### Akonadi

O Akonadi é um sistema destinado a atuar como um cache local para dados do PIM, independentemente de sua origem, que pode ser usado por outros aplicativos. Isso inclui os e-mails, contatos, calendários, eventos, diários, alarmes, notas e assim por diante do usuário. O Akonadi não armazena dados por si só: o formato de armazenamento depende da natureza dos dados (por exemplo, os contatos podem ser armazenados no formato vCard).

Instale [akonadi](https://www.archlinux.org/packages/?name=akonadi). Para extensões adicionais, instale [kdepim-addons](https://www.archlinux.org/packages/?name=kdepim-addons).

**Nota:** Se você deseja usar um mecanismo de banco de dados diferente de [MariaDB](/index.php/MariaDB "MariaDB"), quando instalar o pacote [akonadi](https://www.archlinux.org/packages/?name=akonadi), use o seguinte comando para pular a instalação das dependências [mariadb](https://www.archlinux.org/packages/?name=mariadb):
```
# pacman -S akonadi --assume-installed mariadb

```

Veja também [FS#32878](https://bugs.archlinux.org/task/32878).

##### MySQL

Por padrão, o Akonadi vai usar `/usr/bin/mysqld` ([MariaDB](/index.php/MariaDB "MariaDB") por padrão, veja [MySQL](/index.php/MySQL "MySQL") para provedores alternativos) para executar uma instância MySQL gerenciada com o banco de dados armazenado em `~/.local/share/akonadi/db_data/`.

###### Instância de MySQL para todo o sistema

O Akonadi possui suporte ao uso de [MySQL](/index.php/MySQL "MySQL") para todo sistema para seu banco de dados.[[6]](https://techbase.kde.org/KDE_PIM/Akonadi#Can_Akonadi_use_a_normal_MySQL_server_running_on_my_system.3F)

 `~/.config/akonadi/akonadiserverrc` 
```
[%General]
Driver=QMYSQL

[QMYSQL]
Host=
Name=akonadi_*usuário*
Options="UNIX_SOCKET=/run/mysqld/mysqld.sock"
StartServer=false
```

##### PostgreSQL

O Akonadi possui suporte tanto a instância existente do sistema [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), ou seja, `postgresql.service`, ou a execução de uma instância do PostgreSQL com privilégios de usuário e o banco de dados em `~/.local/share/akonadi/db_data/`.

###### Instância de PostgreSQL por usuário

[Instale](/index.php/Instale "Instale") [postgresql](https://www.archlinux.org/packages/?name=postgresql) e [postgresql-old-upgrade](https://www.archlinux.org/packages/?name=postgresql-old-upgrade).

Edite o arquivo de configuração do Akonadi para que ele tenha o seguinte conteúdo:

 `~/.config/akonadi/akonadiserverrc` 
```
[%General]
Driver=QPSQL
```

**Nota:**

*   Quando o Akonadi iniciar, ele criará a seção `[QPSQL]` e configurará as variáveis apropriadas.
*   O banco de dados será armazenado em `~/.local/share/akonadi/db_data/`.

Inicie Akonadi com `akonadictl start` e verifique seu estado: `akonadictl status`.

**Nota:**

*   A partir do [akonadi](https://www.archlinux.org/packages/?name=akonadi) 19.08.0-1, o cluster de banco de dados do PostgreSQL em `~/.local/share/akonadi/db_data/` será atualizado automaticamente quando uma atualização de versão do postgreSQL é detectada.
*   Para as versões anteriores do [akonadi](https://www.archlinux.org/packages/?name=akonadi), as principais atualizações da versão do PostgreSQL exigirão uma atualização manual do banco de dados. Siga as [instruções de atualização no KDE UserBase Wiki](https://userbase.kde.org/Akonadi/Postgres_update). Certifique-se de ajustar os caminhos dos binários do PostgreSQL para aqueles usados pelo [postgresql](https://www.archlinux.org/packages/?name=postgresql) e pelo [postgresql-old-upgrade](https://www.archlinux.org/packages/?name=postgresql-old-upgrade), veja [PostgreSQL#Upgrading PostgreSQL](/index.php/PostgreSQL#Upgrading_PostgreSQL "PostgreSQL").

###### Instância de PostgreSQL para todo o sistema

Isso requer um já configurado e executando o [PostgreSQL](/index.php/PostgreSQL "PostgreSQL").

Crie uma conta de usuário do PostgreSQL para seu usuário:

```
[postgres]$ createuser *usuário*

```

Crie um banco de dados para o Akonadi:

```
[postgres]$ createdb -O *usuário* --locale=en_US.UTF-8 -T template0 akonadi-*usuário*

```

Configure o Akonadi para usar o PostgreSQL em todo o sistema:

 `~/.config/akonadi/akonadiserverrc` 
```
[%General]
Driver=QPSQL

[QPSQL]
Host=/run/postgresql
Name=akonadi-*usuário*
StartServer=false
```

**Nota:** Porta personalizada, nome de usuário e senha podem ser especificados com opções `Port=`, `User=`, `Password=` na seção `QPSQL]`.

Inicie Akonadi com `akonadictl start` e verifique seu estado: `akonadictl status`.

##### SQLite

Para usar [SQLite](/index.php/SQLite "SQLite"), edit o arquivo de configuração do Akonadi para corresponder à configuração abaixo:

 `~/.config/akonadi/akonadiserverrc` 
```
[%General]
Driver=QSQLITE3
```

**Nota:**

*   Quando o Akonadi inicia, ele vai criar a seção `[QSQLITE3]` e definir as variáveis apropriadas nele.
*   O banco de dados será armazenado como `~/.local/share/akonadi/akonadi.db`.

##### Desabilitando Akonadi

Veja essa [seção no KDE UserBase](https://userbase.kde.org/Akonadi/pt-br#Desabilitando_o_subsistema_Akonadi).

### KDE Telepathy

[KDE Telepathy](https://community.kde.org/KTp) é um projeto com o objetivo de integrar de perto a mensageria instantânea com a área de trabalho do KDE. Ele utiliza a estrutura do Telepathy como backend e destina-se a substituir o Kopete.

Para instalar todos os protocolos Telepathy, instale o grupo [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/). Para usar o cliente KDE Telepathy, instale o pacote [telepathy-kde-meta](https://www.archlinux.org/packages/?name=telepathy-kde-meta) que inclui todos os pacotes contidos no grupo [telepathy-kde](https://www.archlinux.org/groups/x86_64/telepathy-kde/).

#### Usar Telegram com KDE Telepathy

O protocolo do [Telegram](/index.php/Telegram_(Portugu%C3%AAs) "Telegram (Português)") está disponível usando [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze), instalando [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/) ou [telegram-purple-git](https://aur.archlinux.org/packages/telegram-purple-git/) e [telepathy-morse-git](https://aur.archlinux.org/packages/telepathy-morse-git/). O nome de usuário é o número de telefone da conta Telegram (completo com o prefixo nacional `+*xx*`, por exemplo, `+49` para a Alemanha).

A configuração através da interface gráfica pode ser complicada: se o número de telefone não for aceito ao configurar uma nova conta no cliente do KDE Telepathy (com uma mensagem de erro reclamando de um parâmetro inválido que impede a criação da conta), insira entre aspas simples e depois remova as aspas manualmente do arquivo de configuração (`~/.local/share/telepathy/mission-control/accounts.cfg`) após a criação da conta (se as aspas não forem removidas depois, um erro de autenticação deve ser apresentado).

**Nota:** O arquivo de configuração deve ser editado manualmente quando o KDE Telepathy não estiver em execução, por exemplo, quando não houver sessão de área de trabalho do KDE ativa, caso contrário, as alterações manuais poderão ser substituídas pelo software.

### KDE Connect

[KDE Connect](https://community.kde.org/KDEConnect) fornece vários recursos para conectar seu telefone [Android](/index.php/Android "Android") ao seu desktop Linux:

*   Compartilhamento de arquivos e URLs para/do KDE de/para qualquer aplicativo, sem fios.
*   Emulação do touchpad: use a tela do telefone como o touchpad do seu computador.
*   Notificações sincronizadas (4.3+): leia as notificações do Android no computador.
*   Área de transferência compartilhada: copie e cole entre seu telefone e seu computador.
*   Controle remoto de multimídia: utilize o seu telefone como controle remoto para leitores multimídia do Linux.
*   Conexão WiFi: não é necessário fio USB ou Bluetooth.
*   Criptografia RSA: suas informações estão seguras.

Você precisará instalar o KDE Connect tanto no seu computador quanto no seu Android. Para o lado do PC, [instale](/index.php/Instale "Instale") o pacote [kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect). Do lado do Android, instale o KDE Connect do [Google Play](https://play.google.com/store/apps/details?id=org.kde.kdeconnect_tp) ou do [F-Droid](https://f-droid.org/packages/org.kde.kdeconnect_tp/). Se você quiser navegar pelo sistema de arquivos do seu telefone, você também precisa instalar o [sshfs](https://www.archlinux.org/packages/?name=sshfs) e configurar as exposições do sistema de arquivos em seu aplicativo Android.

É possível usar o KDE Connect mesmo que você não use ao ambiente Plasma. Para ambientes de desktop que usam AppIndicators, como o Unity, instale também o pacote [indicator-kdeconnect](https://aur.archlinux.org/packages/indicator-kdeconnect/). Para usuários do GNOME, uma melhor integração pode ser obtida instalando [gnome-shell-extension-gsconnect](https://aur.archlinux.org/packages/gnome-shell-extension-gsconnect/) em vez de [kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect).

Se você usa um [firewall](/index.php/Firewall "Firewall"), você precisa abrir as portas UDP e TCP `1714` até `1764`. Veja [https://community.kde.org/KDEConnect#Troubleshooting](https://community.kde.org/KDEConnect#Troubleshooting).

## Dicas e truques

### Usar um gerenciador de janela diferente

As configurações do seletor de componentes no Plasma não permitem mais alterar o gerenciador de janela. [[7]](https://github.com/KDE/plasma-desktop/commit/2f83a4434a888cd17b03af1f9925cbb054256ade) Para alterar o gerenciador de janela usado, você precisa definir a [variável de ambiente](/index.php/Vari%C3%A1vel_de_ambiente "Variável de ambiente") `KDEWM` antes da inicialização do KDE. [[8]](https://wiki.haskell.org/Xmonad/Using_xmonad_in_KDE) Para fazer isso, você pode criar um script chamado `set_window_manager.sh` em `~/.config/plasma-workspace/env/` e exporte a variável `KDEWM`. Por exemplo, para usar o gerenciador de janela i3:

 `~/.config/plasma-workspace/env/set_window_manager.sh`  `export KDEWM=/usr/bin/i3` 

E então torne-o executável:

 `$ chmod +x ~/.config/plasma-workspace/env/set_window_manager.sh` 
**Nota:** Ao usar o gerenciador de janela i3 com o Plasma, pode ser necessário configurar manualmente os diálogos para abrir no modo flutuante para que eles apareçam corretamente. Para mais informações, veja [I3#Correct handling of floating dialogs](/index.php/I3#Correct_handling_of_floating_dialogs "I3").

#### Sessão KDE/Openbox

O pacote [openbox](https://www.archlinux.org/packages/?name=openbox) fornece uma sessão para usar o KDE com [Openbox](/index.php/Openbox "Openbox"). Para fazer uso desta sessão, selecione *KDE/Openbox* no menu do [gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição").

Para aqueles que iniciam a sessão manualmente, adicione a seguinte linha à sua configuração do [xinit (Português)](/index.php/Xinit_(Portugu%C3%AAs) "Xinit (Português)"):

 `~/.xinitrc` 
```
exec openbox-kde-session

```

#### Reabilitar efeitos de composição

Ao substituir o Kwin por um gerenciador de janelas que não forneça um Compositor (como o Openbox), quaisquer efeitos de composição do ambiente, por exemplo, transparência será perdida. Nesse caso, instale e execute um gerenciador composto separado para fornecer os efeitos, como [Xcompmgr](/index.php/Xcompmgr "Xcompmgr") ou [Compton](/index.php/Compton "Compton").

### Configurando resolução do monitor / vários monitores

Para ativar o gerenciamento de resolução de tela e vários monitores no Plasma, instale o [kscreen](https://www.archlinux.org/packages/?name=kscreen). Isso fornece opções adicionais para *Configurações do sistema > Tela e monitor*.

### KWin-lowlatency

[KWin-lowlatency](https://github.com/tildearrow/kwin-lowlatency) é uma tentativa de reduzira a latência e falhas no popular compositor KWin e está disponível como [kwin-lowlatency](https://aur.archlinux.org/packages/kwin-lowlatency/).

### Configurando perfis ICC

Para ativar [perfis ICC](/index.php/ICC_profiles "ICC profiles") no Plasma, [instale](/index.php/Instale "Instale") [colord-kde](https://www.archlinux.org/packages/?name=colord-kde). Isso fornece opções adicionais para *Configurações do sistema > Correções de cores*.

Os perfis ICC podem ser importados usando *Adicionar perfil*.

### Desabilitar a abertura do lançador de aplicativos com a tecla Super (tecla Windows)

Para desabilitar esse recurso, você pode executar o seguinte comando:

```
$ kwriteconfig5 --file kwinrc --group ModifierOnlyShortcuts --key Meta ""

```

### Desabilitar exibição de Favoritos no menu de aplicativos

Com a integração do navegador com o Plasma instalada, o KDE mostrará favoritos no lançador de aplicativos.

Para desabilitar esse recurso, você atualmente pode executar os seguintes comandos:

```
$ mkdir ~/.local/share/kservices5
$ sed 's/EnabledByDefault=true$/EnabledByDefault=false/' /usr/share/kservices5/plasma-runner-bookmarks.desktop > ~/.local/share/kservices5/plasma-runner-bookmarks.desktop

```

## Solução de problemas

### Fontes

#### Fontes em uma sessão do Plasma têm visual ruim

Tente instalar os pacotes [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) e [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation).

Após a instalação, certifique-se de sair e voltar. Você não deve modificar nada em *Configurações do sistema > Fontes*. Se você estiver usando o [qt5ct](https://www.archlinux.org/packages/?name=qt5ct), as configurações da Qt5 Configuration Tool poderão substituir as configurações de fonte nas Configurações do sistema.

Se você configurou pessoalmente como sua [Fontes](/index.php/Fonts "Fonts") renderiza, esteja ciente de que as Configurações do sistema podem alterar sua aparência. Quando você vai *Configurações do sistema > Fontes*, Configurações do sistema provavelmente irá alterar o seu arquivo de configuração de fontes (`fonts.conf`).

Não há como evitar isso, mas, se você definir os valores para corresponder ao seu arquivo `fonts.conf`, a renderização de fonte esperada retornará (será necessário reiniciar o aplicativo ou, em alguns casos, reiniciar sua área de trabalho). Note que as preferências de fonte do GNOME também fazem isso.

#### Fontes são gigantes ou parecem desproporcionais

Tente forçar o DPI da fonte para `**96**` em *Configurações do sistema > Fontes*.

Se isso não funcionar, tente configurar o DPI diretamente na sua configuração do Xorg como documentado em [Xorg#Setting DPI manually](/index.php/Xorg#Setting_DPI_manually "Xorg").

### Configuração relatada

Muitos problemas no KDE estão relacionados à sua configuração.

#### O ambiente Plasma se comporta de forma estranha

Os problemas no Plasma são geralmente causados por *widgets de Plasma* instáveis (coloquialmente chamados de *plasmoides*) ou *temas de Plasma*. Primeiro, descubra qual foi o último widget ou tema que você instalou e desative ou desinstale-o.

Portanto, se seu ambiente exibir um "bloqueio", isso provavelmente é causado por um widget instalado defeituoso. Se você não consegue lembrar qual widget você instalou antes do problema começar (às vezes pode ser um problema irregular), tente rastreá-lo removendo cada widget até que o problema cesse. Então você pode desinstalar o widget, e preencher um relatório de erro no [rastreador de erros do KDE](https://bugs.kde.org/) **somente se for um widget oficial**. Se não for, é recomendado encontrar a entrada na [KDE Store](https://store.kde.org/) e informar o desenvolvedor do widget sobre o problema (detalhando os passos para se reproduzir, etc.).

Se você não conseguir encontrar o problema, mas não quiser que *todas* as configurações sejam perdidas, navegue até `~/.config/` e execute o seguinte comando:

```
$ for j in plasma*; do mv -- "$j" "${j%}.bak"; done

```

Este comando vai renomear **todos** os arquivos de configuração relacionados ao Plasma para **.bak* (por exemplo, `plasmarc.bak`) do seu usuário e quando você entrar no Plasma, você terá o configurações padrão de volta. Para desfazer essa ação, remova a extensão de arquivo *.bak*. Se você já tiver arquivos **.bak*, renomeie, mova ou exclua-os primeiro. É altamente recomendável que você crie backups regulares de qualquer maneira. Veja [Programas de sincronização e backup](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs") para uma lista de possíveis soluções.

#### Limpar cache para resolver problemas de atualização

O [problema](https://bbs.archlinux.org/viewtopic.php?id=135301) pode ser causado por um cache antigo. Às vezes, após uma atualização, o cache antigo pode apresentar um comportamento estranho, difícil de depurar, como shells que não podem ser encerrados, travamentos ao alterar várias configurações, sendo que o Ark não consegue extrair arquivos ou o Amarok não reconhece nenhuma de suas músicas. Esta solução também pode resolver problemas com os aplicativos do KDE e do Qt que ficam ruins após uma atualização.

Recompile o cache usando os seguintes comandos:

```
$ rm ~/.config/Trolltech.conf
$ kbuildsycoca5 --noincremental

```

Opcionalmente, esvazie o conteúdo da pasta `~/.cache/`, porém isso também vai limpar o cache de outros aplicativos:

```
$ rm -rf ~/.cache/*

```

#### Teclas de controle do volume, notificações e multimídia não funcionam

Ocultar determinados itens nas configurações da área de notificação (por exemplo, Volume do áudio, Reprodutor de mídia ou Notificações) também desativa os recursos relacionados. Ao ocultar o *Volume do áudio* desativa as teclas de controle de volume, *Reprodutor de mídia* desativa as teclas multimídia (rebobinar, parar, pausar) e ocultar *Notificações* desativa a exibição de notificações.

#### A tela de autenticação KCM não sincroniza as configurações do cursor para SDDM

A tela de autenticação do KCM lê as configurações do cursor em `~/.config/kcminputrc`, sem esse arquivo nenhuma configuração é sincronizada. A maneira mais fácil de gerar esse arquivo é alterar o tema do cursor em *Configurações do sistema > Cursores* e alterá-lo novamente para o tema preferido de cursor.

### Problemas gráficos

Certifique-se de ter o driver adequado para a sua GPU instalada. Veja [Xorg#Driver installation](/index.php/Xorg#Driver_installation "Xorg") para mais informações. Se você tiver uma placa mais antiga, poderá ajudar a [#Desabilitar efeitos do ambiente manualmente ou automaticamente para aplicativos definidos](#Desabilitar_efeitos_do_ambiente_manualmente_ou_automaticamente_para_aplicativos_definidos) ou [#Desabilitar composição](#Desabilitar_composição).

#### Obtendo o estado atual de KWin para propósito de suporte e depuração

Esse comando exibe um resumo do estado atual do KWin, incluindo opções usadas, back-end de composição usada e recursos relevantes do driver OpenGL. Veja mais no [blog do Martin](https://blog.martin-graesslin.com/blog/2012/03/on-getting-help-for-kwin-and-helping-kwin/).

```
$ qdbus org.kde.KWin /KWin supportInformation

```

#### Desabilitar efeitos do ambiente manualmente ou automaticamente para aplicativos definidos

O Plasma tem efeitos do ambiente ativados por padrão e, por exemplo, nem todo jogo irá desabilitá-los automaticamente. Você pode desativar os efeitos da área de trabalho em *Configurações do sistema > Comportamento da Área de Trabalho > Efeitos da área de trabalho* e pode alternar os efeitos da área de trabalho com `Alt+Shift+F12`.

Além disso, você pode criar regras personalizadas do KWin para desabilitar/habilitar automaticamente a composição quando um determinado aplicativo/janela é iniciado em *Configurações do sistema > Gerenciamento de Janelas > Regras das janelas*.

#### Habilitar transparência

Se você usar um fundo transparente sem habilitar o compositor, você receberá a mensagem:

```
Este esquema de cores usa um fundo transparente, que parece não ser suportado pelo seu ambiente de trabalho

```

Em *Configurações do sistema > Tela e monitor > Compositor*, marque *Ativar o compositor na inicialização* e reinicie o Plasma.

#### Desabilitar composição

Em *Configurações do sistema > Tela e monitor > Compositor*, desmarque *Ativar o compositor na inicialização* e reinicie Plasma.

#### Oscilação em tela cheia quando composição está habilitada

Em *Configurações do sistema > Tela e monitor > Compositor*, desmarque *Permitir que os aplicativos bloqueiem a composição*. Isso pode prejudicar o desempenho.

#### Imagem quebrada com NVIDIA

Veja [NVIDIA/Troubleshooting#Avoid screen tearing in KDE (KWin)](/index.php/NVIDIA/Troubleshooting#Avoid_screen_tearing_in_KDE_(KWin) "NVIDIA/Troubleshooting").

#### O cursor do Plasma algumas vezes é mostrado incorretamente

Crie o diretório `~/.icons/default` e, dentro, um arquivo chamado `index.theme` com o seguinte conteúdo:

 `~/.icons/default/index.theme` 
```
[Icon Theme]
Inherits=breeze_cursors
```

Execute o seguinte comando:

```
$ ln -s /usr/share/icons/breeze_cursors/cursors ~/.icons/default/cursors

```

#### Resolução de tela inutilizável definida

Suas configurações locais para o kscreen podem sobrescrever aquelas definidas no `xorg.conf`. Procure pelos arquivos de configuração do kscreen em `~/.local/share/kscreen/` e verifique se o modo está sendo definido para uma resolução que não é suportada pelo seu monitor.

#### Ícones borrados na área de notificação

Para adicionar ícones à área de notificação, os aplicativos geralmente fazem uso da biblioteca appindicator. Se os ícones estiverem desfocados, verifique qual versão do libappindicator você instalou. Se você só tem o [libappindicator-gtk2](https://www.archlinux.org/packages/?name=libappindicator-gtk2) instalado, você pode instalar o [libappindicator-gtk3](https://www.archlinux.org/packages/?name=libappindicator-gtk3) ou o [libappindicator-sharp](https://www.archlinux.org/packages/?name=libappindicator-sharp) como uma tentativa de obter ícones claros.

### Problemas de som

**Nota:** Primeiro, certifique-se de que você tenha [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) instalado.

#### Nenhum som após a suspensão

Se não houver som após a suspensão e se o KMix não mostrar dispositivos de áudio que deveriam estar lá, reiniciar o plasmashell e pulseaudio pode ajudar:

```
$ killall plasmashell
$ systemctl --user restart pulseaudio.service
$ plasmashell

```

Alguns aplicativos também podem precisar ser reiniciados para que o som seja reproduzido novamente.

#### Arquivos MP3 não pode ser reproduzidos usando o backend GStreamer Phonon

Isso pode ser resolvido instalando o plugin libav do GStreamer (pacote [gst-libav](https://www.archlinux.org/packages/?name=gst-libav)). Se você ainda encontrar problemas, tente alterar o backend do Phonon usado instalando outro, como [phonon-qt4-vlc](https://aur.archlinux.org/packages/phonon-qt4-vlc/) ou [phonon-qt5-vlc](https://www.archlinux.org/packages/?name=phonon-qt5-vlc).

Em seguida, certifique-se de que o backend é preferido através de *Configurações do sistema > Multimídia > Áudio e vídeo > Infraestrutura*.

### Gerenciamento de energia

#### Nenhuma opção de suspensão/hibernação

Se o seu sistema puder suspender ou hibernar usando [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)"), mas não tiver essas opções mostradas no KDE, certifique-se de que [powerdevil](https://www.archlinux.org/packages/?name=powerdevil) esteja instalado.

### KMail

#### Limpar a configuração do Akonadi para corrigir o KMail

Consulte [esse](https://docs.kde.org/trunk5/en/pim/kmail2/clean-start-after-a-failed-migration.html) documento para detalhes.

Se você quiser um backup, por favor copie o diretório de configuração em vez de excluí-lo.

```
$ cp -a ~/.local/share/akonadi ~/.local/share/akonadi-old
$ cp -a ~/.config/akonadi ~/.config/akonadi-old

```

#### Esvaziar a caixa de entrada IMAP no KMail

Para algumas contas IMAP, o KMail irá mostrar a caixa de entrada como um contentor de nível superior (por isso, não será possível ler mensagens lá) com todas as outras pastas desta conta no interior. [[9]](https://bugs.kde.org/show_bug.cgi?id=284172). Para resolver este problema, simplesmente desative as assinaturas do lado do servidor nas configurações da conta do KMail.

#### Erros de autorização par a conta EWS no KMail

Ao configurar a conta do EWS no KMail, você pode continuar recebendo erros sobre a autorização com falha, mesmo para credenciais válidas e totalmente funcionais. Isso provavelmente é causado por uma comunicação interrompida entre o [KWallet](/index.php/KWallet "KWallet") e o KMail. Para solucionar o problema, defina uma senha pelo qdbus:

```
$ qdbus org.freedesktop.Akonadi.Resource.akonadi_ews_resource_0 /Settings org.kde.Akonadi.Ews.Wallet.setPassword "XXX"

```

### Rede

#### Congela ao usar montagem automática em um volume NFS

Usar [Fstab#Automount with systemd](/index.php/Fstab#Automount_with_systemd "Fstab") em um volume [NFS](/index.php/NFS "NFS") pode causar congelamentos, veja [relatório de erro no upstream](https://bugs.kde.org/show_bug.cgi?id=354137).

### Registro log agressivo do QXcbConnection

Veja [Qt#Disable/Change Qt journal logging behaviour](/index.php/Qt#Disable/Change_Qt_journal_logging_behaviour "Qt").

### Aplicativos KF5/Qt 5 não exibem ícones em i3/FVWM/awesome

Veja [Qt#Configuration of Qt5 apps under environments other than KDE Plasma](/index.php/Qt#Configuration_of_Qt5_apps_under_environments_other_than_KDE_Plasma "Qt").

### Problemas com salvar credenciais e ocorrendo persistentemente diálogos do KWallet

Não é recomendado desativar o sistema de salvamento de senhas do [KWallet](/index.php/KWallet "KWallet") nas configurações do usuário, pois é necessário para salvar credenciais criptografadas, como senhas WiFi para cada usuário. Diálogos do KWallet aparecendo de forma persistente podem ser a consequência de desativá-lo.

Caso você ache irritantes os diálogos para desbloquear a carteira quando os aplicativos quiserem acessá-la, você pode deixar que os [gerenciadores de exibição](/index.php/Gerenciadores_de_exibi%C3%A7%C3%A3o "Gerenciadores de exibição") [SDDM](/index.php/SDDM "SDDM") e [LightDM](/index.php/LightDM "LightDM") desbloqueiem a carteira no início da sessão automaticamente, consulte [KDE Wallet#Unlock KDE Wallet automatically on login](/index.php/KDE_Wallet#Unlock_KDE_Wallet_automatically_on_login "KDE Wallet"). A primeira carteira precisa ser gerada pelo KWallet (e não gerada pelo usuário) para ser usada nas credenciais do programa do sistema.

Caso você queira que as credenciais da carteira não sejam abertas na memória para cada aplicativo, você pode restringir os aplicativos de acessá-los com o [kwalletmanager](https://www.archlinux.org/packages/?name=kwalletmanager) nas configurações do KWallet.

Se você não se importa com a criptografia de credenciais, pode simplesmente deixar os formulários de senha em branco quando o KWallet solicitar a senha durante a criação de uma carteira. Nesse caso, os aplicativos podem acessar senhas sem ter que desbloquear a carteira primeiro.

### Descoberta não mostra qualquer aplicativos

Isso pode ser resolvido instalando [packagekit-qt5](https://www.archlinux.org/packages/?name=packagekit-qt5).

### Alto uso de CPU de kscreenlocker_greet com drivers da NVIDIA

Como descrito no [Bug 347772 do KDE](https://bugs.kde.org/show_bug.cgi?id=347772), os drivers NVIDIA OpenGL e QML podem não funcionar bem junto com o Qt 5\. Isso pode levar `kscreenlocker_greet` a um alto uso da CPU após desbloquear a sessão. Para contornar esse problema, defina a [variável de ambiente](/index.php/Vari%C3%A1vel_de_ambiente "Variável de ambiente") `QSG_RENDERER_LOOP` como `basic`.

Em seguida, mate as instâncias anteriores do greeter com `killall kscreenlocker_greet`.

### OS error 22 ao executar Akonadi no ZFS

Se sua pasta pessoal está em um pool de [ZFS](/index.php/ZFS "ZFS"), crie um arquivo `~/.config/akonadi/mysql-local.conf` com o seguinte conteúdo:

```
[mysqld]
innodb_use_native_aio = 0

```

Veja [MariaDB#OS error 22 when running on ZFS](/index.php/MariaDB#OS_error_22_when_running_on_ZFS "MariaDB").

### Alguns programas não conseguem rolar o texto quando suas janelas estão inativas

Isso é causado pela maneira problemática de o GTK 3 lidar com eventos de rolagem do mouse. Uma solução para isso é definir a [variável de ambiente](/index.php/Vari%C3%A1vel_de_ambiente "Variável de ambiente") `GDK_CORE_DEVICE_EVENTS=1`. No entanto, essa solução também interrompe a rolagem suave do touchpad e a rolagem da tela sensível ao toque.

### TeamViewer está lento

Ao usar o TeamViewer, ele pode se comportar lentamente se você usar animações uniformes (como minimizar janelas). Veja [#Desabilitar composição](#Desabilitar_composição) como uma solução alternativa.

## Veja também

*   [Site do KDE](https://www.kde.org/)
*   [Rastreador de erros do KDE](https://bugs.kde.org/)
*   [Blog do Martin Graesslin](https://blog.martin-graesslin.com/blog/kategorien/kde/)