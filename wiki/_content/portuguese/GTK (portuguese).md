**Status de tradução:** Esse artigo é uma tradução de [GTK](/index.php/GTK "GTK"). Data da última tradução: 2019-08-16\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=GTK&diff=0&oldid=580079) na versão em inglês.

Artigos relacionados

*   [Visual uniforme para aplicativos Qt e GTK](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications")
*   [Qt](/index.php/Qt "Qt")
*   [Projeto GNU](/index.php/Projeto_GNU "Projeto GNU")
*   [GTK/Desenvolvimento](/index.php/GTK/Development "GTK/Development")

Do [site do GTK](https://www.gtk.org/):

	GTK, ou o GIMP Toolkit, é um kit de ferramentas multiplataforma para criar interfaces gráficas com o usuário. Oferecendo um conjunto completo de widgets, o GTK é adequado para projetos que variam de pequenas ferramentas únicas a conjuntos completos de aplicativos.

O GTK, o GIMP Toolkit, foi criado inicialmente pelo [Projeto GNU](/index.php/Projeto_GNU "Projeto GNU") para o [GIMP](/index.php/GIMP "GIMP"), mas agora é um kit de ferramentas muito popular com vinculações para várias linguagens. Este artigo explorará as ferramentas usadas para configurar o tema, o estilo, o ícone, a fonte e o tamanho da fonte do GTK, além de detalhar a configuração manual.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Temas](#Temas)
    *   [2.1 GTK e Qt](#GTK_e_Qt)
*   [3 Ferramentas de configuração](#Ferramentas_de_configuração)
*   [4 Configuração](#Configuração)
    *   [4.1 Configuração básica de tema](#Configuração_básica_de_tema)
    *   [4.2 Variante escura de tema](#Variante_escura_de_tema)
    *   [4.3 Atalhos de teclado](#Atalhos_de_teclado)
        *   [4.3.1 Vinculações de teclas Emacs](#Vinculações_de_teclas_Emacs)
    *   [4.4 Atraso no menu do GNOME](#Atraso_no_menu_do_GNOME)
    *   [4.5 Reduzir tamanhos de widgets](#Reduzir_tamanhos_de_widgets)
    *   [4.6 Ocultar botões de CSD](#Ocultar_botões_de_CSD)
    *   [4.7 Desabilitar colagem com mouse](#Desabilitar_colagem_com_mouse)
    *   [4.8 Localização inicial do seletor de arquivos](#Localização_inicial_do_seletor_de_arquivos)
    *   [4.9 Comportamento de rolagem legada](#Comportamento_de_rolagem_legada)
    *   [4.10 Desabilitar barras de rolagem de sobreposição](#Desabilitar_barras_de_rolagem_de_sobreposição)
        *   [4.10.1 Remover indicadores de rolagem de sobreposição](#Remover_indicadores_de_rolagem_de_sobreposição)
    *   [4.11 Exemplos](#Exemplos)
*   [5 Backend do GDK](#Backend_do_GDK)
    *   [5.1 Backend do Broadway](#Backend_do_Broadway)
    *   [5.2 Backend do Wayland](#Backend_do_Wayland)
*   [6 Solução de problemas](#Solução_de_problemas)
    *   [6.1 Temas diferentes entre aplicativos GTK 2 e GTK 3](#Temas_diferentes_entre_aplicativos_GTK_2_e_GTK_3)
    *   [6.2 Tema não aplicado para aplicativos de root](#Tema_não_aplicado_para_aplicativos_de_root)
    *   [6.3 Decorações do lado do cliente](#Decorações_do_lado_do_cliente)
    *   [6.4 Cedilha ç/Ç em vez de ć/Ć](#Cedilha_ç/Ç_em_vez_de_ć/Ć)
    *   [6.5 Suprimir aviso sobre barramento de acessibilidade](#Suprimir_aviso_sobre_barramento_de_acessibilidade)
    *   [6.6 Incompatibilidade de cor de fundo da barra de título](#Incompatibilidade_de_cor_de_fundo_da_barra_de_título)
    *   [6.7 Eventos de foco incorretos com gerenciadores de janela tiling](#Eventos_de_foco_incorretos_com_gerenciadores_de_janela_tiling)
    *   [6.8 Suporte a miniaturas para diálogo de arquivos GTK 2](#Suporte_a_miniaturas_para_diálogo_de_arquivos_GTK_2)
    *   [6.9 Botão e ícones de menu](#Botão_e_ícones_de_menu)
    *   [6.10 GTK 3 sem polkit](#GTK_3_sem_polkit)
    *   [6.11 Alguns temas de GTK 2 só alteram a paleta de cores da UI](#Alguns_temas_de_GTK_2_só_alteram_a_paleta_de_cores_da_UI)
    *   [6.12 Aplicando patch no seletor de arquivos GTK para usar a digitação adiantada normal](#Aplicando_patch_no_seletor_de_arquivos_GTK_para_usar_a_digitação_adiantada_normal)
*   [7 Veja também](#Veja_também)

## Instalação

As duas versões do GTK estão atualmente disponíveis nos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais"). Elas podem ser [instaladas](/index.php/Instala "Instala") com os seguintes pacotes:

*   **GTK 3.x** está disponível com o pacote [gtk3](https://www.archlinux.org/packages/?name=gtk3).
*   **GTK 2.x** está disponível com o pacote [gtk2](https://www.archlinux.org/packages/?name=gtk2).

**GTK 1.x** está disponível com o pacote [gtk](https://aur.archlinux.org/packages/gtk/).

## Temas

No GTK 2, o tema padrão é o Raleigh, mas o Arch Linux tem um arquivo de configuração personalizado em `/usr/share/gtk-2.0/gtkrc`, que define o tema padrão como Adwaita. No GTK 3, o tema padrão é Adwaita, mas os temas HighContrast, HighContrastInverse e Raleigh também estão incluídos.

Para forçar um tema específico, defina as seguintes [variáveis de ambiente](/index.php/Vari%C3%A1veis_de_ambiente "Variáveis de ambiente"):

*   Para GTK 2, use `GTK2_RC_FILES`. Por exemplo, para iniciar o [GIMP](/index.php/GIMP "GIMP") com o tema Raleigh:

```
$ GTK2_RC_FILES=/usr/share/themes/Raleigh/gtk-2.0/gtkrc gimp

```

**Dica:** `gtkrc` também pode ser um arquivo personalizado em seu diretório home criado por qualquer uma das [#Ferramentas de configuração](#Ferramentas_de_configuração). Veja [#Exemplos](#Exemplos).

*   Para GTK 3, use `GTK_THEME`. Por exemplo, para iniciar a Calculadora do GNOME com a variante escura do Adwaita:

```
$ GTK_THEME=Adwaita:dark gnome-calculator

```

**Nota:** Para aplicar o acima aos atalhos da área de trabalho (ou lançadores), consulte [Desktop entries#Modify environment variables](/index.php/Desktop_entries#Modify_environment_variables "Desktop entries").

Mais temas podem ser instalados a partir dos repositórios oficiais ou do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"). Temas extraídos manualmente vão nos diretórios `~/.themes/` ou `~/.local/share/themes/`.

**GTK 2 e GTK 3.20 ou mais novos tem suporte em:**

*   **Adapta** — Um tema GTK adaptivo baseado em Material Design Guidelines. Inclui: Adapta, Adapta-Eta, Adapta-Nokto, Adapta-Nokto-Eta

	[https://github.com/tista500/Adapta](https://github.com/tista500/Adapta) || [adapta-gtk-theme](https://www.archlinux.org/packages/?name=adapta-gtk-theme)

*   **Arc** — Um tema plano com um visual moderno e elementos transparentes. Inclui: Arc, Arc-Dark, Arc-Darker

	[https://github.com/nicohood/arc-theme](https://github.com/nicohood/arc-theme) || com transparência: [arc-gtk-theme](https://www.archlinux.org/packages/?name=arc-gtk-theme), sem transparência: [arc-solid-gtk-theme](https://www.archlinux.org/packages/?name=arc-solid-gtk-theme)

*   **Bluebird** — Blue Desktop Suite para o Xfce.

	[https://github.com/shimmerproject/Bluebird](https://github.com/shimmerproject/Bluebird) || [xfce-theme-bluebird](https://aur.archlinux.org/packages/xfce-theme-bluebird/)

*   **Breeze** — A versão GTK do tema de widgets padrão do KDE. Inclui: Breeze, Breeze-Dark

	[https://cgit.kde.org/breeze-gtk.git](https://cgit.kde.org/breeze-gtk.git) || [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk)

*   **Deepin** — Tema padrão para o ambiente Deepin. Inclui: deepin, deepin-dark

	[https://github.com/linuxdeepin/deepin-gtk-theme](https://github.com/linuxdeepin/deepin-gtk-theme) || [deepin-gtk-theme](https://www.archlinux.org/packages/?name=deepin-gtk-theme)

*   **GNOME Extra Themes** — Temas extras para o ambiente GNOME. Inclui: Adwaita, Adwaita-dark, HighContrast

	[https://gitlab.gnome.org/GNOME/gnome-themes-extra](https://gitlab.gnome.org/GNOME/gnome-themes-extra) || [gnome-themes-extra](https://www.archlinux.org/packages/?name=gnome-themes-extra)

*   **Greybird** — Um tema cinza e azul para o Xfce, usado por padrão no Xubuntu 12.04.

	[https://github.com/shimmerproject/Greybird](https://github.com/shimmerproject/Greybird) || [xfce-theme-greybird](https://aur.archlinux.org/packages/xfce-theme-greybird/)

*   **Materia** — Um tema plano semelhante ao Material Design para GTK3, GTK2 e GNOME-Shell.

	[https://github.com/nana-4/materia-theme](https://github.com/nana-4/materia-theme) || [materia-gtk-theme](https://www.archlinux.org/packages/?name=materia-gtk-theme)

*   **MATE Themes** — Temas padrão para o ambiente MATE. Inclui: BlackMATE, Blue-Submarine, BlueMenta, ContrastHighInverse, Green-Submarine, GreenLaguna, Menta, TraditionalGreen, TraditionalOk

	[https://github.com/mate-desktop/mate-themes](https://github.com/mate-desktop/mate-themes) || [mate-themes](https://www.archlinux.org/packages/?name=mate-themes)

*   **Numix** — Um tema plano e leve com um visual moderno (GNOME, Openbox, Unity, Xfce). Inclui: Numix

	[https://github.com/numixproject/numix-gtk-theme](https://github.com/numixproject/numix-gtk-theme) || [numix-gtk-theme-git](https://aur.archlinux.org/packages/numix-gtk-theme-git/)

*   **Vertex** — Tema para GTK 3, GTK 2, Gnome-Shell e Cinnamon.

	[https://github.com/horst3180/vertex-theme](https://github.com/horst3180/vertex-theme) || [vertex-themes](https://aur.archlinux.org/packages/vertex-themes/)

*   **Zuki** — Tema para GTK, gnome-shell e mais.

	[https://github.com/lassekongo83/zuki-themes](https://github.com/lassekongo83/zuki-themes) || [zuki-themes](https://aur.archlinux.org/packages/zuki-themes/)

Há vários temas GTK adicionais no AUR. Por exemplo, [pesquise por gtk-theme](https://aur.archlinux.org/packages.php?K=gtk-theme).

**Nota:** Porque o GTK 3 muda rapidamente, temas GTK 3 geralmente exigem retrabalhos após um lançamento do GTK 3\. Por este motivo, nem todos os temas para GTK 3 podem parecer como pretendidos quando usados com a versão mais recente do GTK 3.

### GTK e Qt

Se você tem aplicativos GTK e Qt (KDE) em sua área de trabalho, sabe que sua aparência não combina bem. Se você deseja fazer seus estilos de GTK combinarem com seus estilos de Qt, por favor, leia [Aparência uniforme para aplicativos em Qt e GTK](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications").

## Ferramentas de configuração

A maioria dos grandes [ambientes de desktop](/index.php/Ambientes_de_desktop "Ambientes de desktop") fornecem ferramentas para configurar o tema GTK, ícones, fonte e tamanho da fonte, e gerenciar essas configurações por [XSettings](https://specifications.freedesktop.org/xsettings-spec/xsettings-spec-0.5.html):

*   Se você usa [Cinnamon](/index.php/Cinnamon "Cinnamon"), use a ferramenta Temas (*cinnamon-settings themes*): vá em *Configurações do sistema > Temas*.
*   Se você usa [Enlightenment](/index.php/Enlightenment "Enlightenment"): vá em *Definições > Tudo > Aparência > Tema das aplicações*.
*   Se você usa [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)"), use Ajustes do GNOME (*gnome-tweaks*): instale [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks).
*   Se você usa [MATE](/index.php/MATE "MATE"), use a ferramenta Appearance Preferences (*mate-appearance-properties*): vá em *Sistema > Configurações > Aparência*.
*   Se você usa [Xfce](/index.php/Xfce_(Portugu%C3%AAs) "Xfce (Português)"), use a ferramenta Appearance: vá em *Configurações > Aparência*.

Outras ferramentas GUI geralmente sobrescrevem os [arquivos de configuração](#Configuração).

**Suporte a GTK 2 e GTK 3:**

*   **KDE GTK Configurator** — Aplicativo que permite que você altere o estilo e fonte de aplicativos GTK 2 e GTK 3.

	[https://cgit.kde.org/kde-gtk-config.git](https://cgit.kde.org/kde-gtk-config.git) || [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config)

	Após a instalação, `kde-gtk-config` também pode ser encontrado em *Configurações do sistema > Estilo dos aplicativos > GNOME/GTK Application Style*.

*   **LXAppearance** — Ferramenta de configuração de estilo independente para GTK 2 e GTK 3 do projeto LXDE (não requer outras partes da área de trabalho do LXDE).

	[http://wiki.lxde.org/en/LXAppearance](http://wiki.lxde.org/en/LXAppearance) || [lxappearance](https://www.archlinux.org/packages/?name=lxappearance)

*   **Oo-mox** — Aplicativo gráfico para gerar diferentes variações de cores dos temas dos temas Numix e Flat-Plat (GTK 2 e 3), Archdroid e Gnome-Colors. Também permite gerar temas GTK 2 pré-dimensionados para telas HiDPI.

	[https://github.com/actionless/oomox](https://github.com/actionless/oomox) || [oomox](https://aur.archlinux.org/packages/oomox/)

**Suporte apenas a GTK 2:**

*   **GTK Change Theme** — Um programa pequeno que permite que você altere seu tema GTK 2.0 (considerado uma alternativa melhor ao *switch2*).

	[http://plasmasturm.org/code/gtk-chtheme/](http://plasmasturm.org/code/gtk-chtheme/) || [gtk-chtheme](https://www.archlinux.org/packages/?name=gtk-chtheme)

*   **GTK Preference Tool** — Seletor de temas GTK e alternador de fontes.

	[http://gtk-win.sourceforge.net/home/index.php/Main/GTKPreferenceTool](http://gtk-win.sourceforge.net/home/index.php/Main/GTKPreferenceTool) || [gtk2_prefs](https://aur.archlinux.org/packages/gtk2_prefs/)

*   **GTK Theme Switch** — Alternador de temas GTK simples.

	[http://muhri.net/nav.php3?node=gts](http://muhri.net/nav.php3?node=gts) || [gtk-theme-switch2](https://www.archlinux.org/packages/?name=gtk-theme-switch2)

## Configuração

As configurações do GTK podem ser especificadas manualmente nos arquivos de configuração, mas os ambientes e aplicativos de desktop podem substituir essas configurações. Dependendo da versão do GTK, esses arquivos estão localizados em:

*   específico de usuário no GTK 2: `~/.gtkrc-2.0`
*   todo o sistema no GTK 2: `/etc/gtk-2.0/gtkrc`
*   específico de usuário no GTK 3: `$XDG_CONFIG_HOME/gtk-3.0/settings.ini`, ou `$HOME/.config/gtk-3.0/settings.ini` se `$XDG_CONFIG_HOME` não estiver definido
*   todo o sistema no GTK 3: `/etc/gtk-3.0/settings.ini`

**Nota:**

*   Veja as [propriedades de *GtkSettings* do GTK 3](https://developer.gnome.org/gtk3/stable/GtkSettings.html#GtkSettings.properties) (e as [propriedades do GTK 2](https://developer.gnome.org/gtk2/stable/GtkSettings.html#GtkSettings.properties)) no manual de referência de programação do GTK para a lista completa as opções de configuração de GTK atualmente válidas.
*   Algumas das configurações descritas abaixo (como `gtk-icon-size`) são obsoletas e ignoradas desde o GTK 3.10.
*   Se você editar seus arquivos de configuração do GTK, apenas os aplicativos recém-iniciados exibirão as alterações.

### Configuração básica de tema

Para alterar manualmente o tema, os ícones, a fonte e o tamanho da fonte do GTK, adicione o seguinte aos arquivos de configuração, por exemplo:

*   GTK 2:

 `~/.gtkrc-2.0` 
```
gtk-icon-theme-name = "Adwaita"
gtk-theme-name = "Adwaita"
gtk-font-name = "DejaVu Sans 11"
```

*   GTK 3:

 `$XDG_CONFIG_HOME/gtk-3.0/settings.ini` 
```
[Settings]
gtk-icon-theme-name = Adwaita
gtk-theme-name = Adwaita
gtk-font-name = DejaVu Sans 11
```

**Nota:** O nome do tema do ícone é o nome de seu diretório, *não* a propriedade de nome em seu `index.theme`.

### Variante escura de tema

Alguns temas do GTK 3 contêm uma variante de tema escuro, mas ela é usada apenas por padrão quando o aplicativo solicita isso explicitamente. Para usar a variante do tema escuro com todos os aplicativos GTK 3, defina:

```
gtk-application-prefer-dark-theme = true

```

### Atalhos de teclado

Os atalhos de teclado (também conhecidos como *aceleradores* no GTK) podem ser alterados passando o mouse sobre o respectivo item de menu e pressionando a combinação de teclas desejada. Para ativar esse recurso, defina:

```
gtk-can-change-accels = 1

```

#### Vinculações de teclas Emacs

Para ter associações de teclas do tipo Emacs em aplicativos de GTK, adicione o seguinte:

 `~/.gtkrc-2.0`  `gtk-key-theme-name = "Emacs"`  `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-key-theme-name = Emacs
```

Para GTK 3, também execute:

```
$ gsettings set org.gnome.desktop.interface gtk-key-theme "Emacs"

```

XFCE possui uma configuração similar:

```
$ xfconf-query -c xsettings -p /Gtk/KeyThemeName -s Emacs

```

Os arquivos de configuração em `/usr/share/themes/Emacs/` determinam quais são as ligações do Emacs e podem ser alteradas. Copiar seções para o arquivo `~/.gtkrc-2.0` permite alterações por usuário.

### Atraso no menu do GNOME

Essa configuração controla o atraso entre apontar o mouse em um menu e a abertura do menu. Esse atraso é medido em milissegundos.

```
gtk-menu-popup-delay = 0

```

### Reduzir tamanhos de widgets

Se você tem uma tela pequena ou simplesmente não gosta de grandes ícones e widgets, pode redimensionar as coisas facilmente.

Para ter ícones sem texto nas barras de ferramentas ([valores válidos](https://developer.gnome.org/gtk3/stable/gtk3-Standard-Enumerations.html#GtkToolbarStyle)), use

```
gtk-toolbar-style = GTK_TOOLBAR_ICONS

```

Para ícones menores, use uma linha como essa:

```
gtk-icon-sizes = "panel-menu=16,16:panel=16,16:gtk-menu=16,16:gtk-large-toolbar=16,16\
:gtk-small-toolbar=16,16:gtk-button=16,16"

```

Ou para remover ícones de botões completamente:

```
gtk-button-images = 0

```

Você também pode remover ícones de menus:

```
gtk-menu-images = 0

```

Veja também [[1]](http://martin.ankerl.com/2008/10/10/how-to-make-a-compact-gnome-theme/) e [[2]](http://gnome-look.org/content/show.php/Simple+eGTK?content=119812).

### Ocultar botões de CSD

Para remover os botões minimizar e maximizar das janelas em *gtk3*:

```
gtk-decoration-layout=menu:close

```

See [[3]](https://developer.gnome.org/gtk3/3.22/GtkSettings.html#GtkSettings--gtk-decoration-layout).

### Desabilitar colagem com mouse

Para desaligar colagem ao clicar com o botão do meio do mouse (também conhecido como PRIMARY):

```
gtk-enable-primary-paste=false

```

### Localização inicial do seletor de arquivos

Abra o seletor de arquivos dentro do **diretório de trabalho atual** e não o local **recentes**. Normalmente o **diretório de trabalho atual** é a pasta pessoal.

**GTK 3**

Altere a [configuração](/index.php/GNOME_(Portugu%C3%AAs)#Configuração "GNOME (Português)") com o seguinte comando:

```
$ gsettings set org.gtk.Settings.FileChooser startup-mode cwd

```

**GTK 2**

Adicione o seguinte para `~/.config/gtk-2.0/gtkfilechooser.ini`:

```
StartupMode=cwd

```

### Comportamento de rolagem legada

**Nota:** Essa configuração não é obedecida por todos os aplicativos GTK.

**Dica:** Comportamento de rolagem legado pode ser alcançado de forma confiável simplesmente usando o botão direito em vez de clicar com o botão esquerdo do mouse.

Antes do GTK 3.6, clicar em um dos lados do controle deslizante na barra de rolagem moveria a barra de rolagem na direção do clique em aproximadamente uma página. Desde o GTK 3.6, o controle deslizante se moverá diretamente para a posição do clique. Esse comportamento pode ser revertido em alguns aplicativos, criando o arquivo com o conteúdo abaixo:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-primary-button-warps-slider = false

```

### Desabilitar barras de rolagem de sobreposição

Desde o GTK 3.15, as barras de rolagem de sobreposição são ativadas por padrão, o que significa que as barras de rolagem serão mostradas apenas ao passar o mouse nas aplicações do GTK 3\. Esse comportamento pode ser revertido pela configuração da seguinte variável de ambiente: `GTK_OVERLAY_SCROLLING=0`. Veja [Variáveis de ambiente#Ambiente gráfico](/index.php/Vari%C3%A1veis_de_ambiente#Ambiente_gráfico "Variáveis de ambiente").

O GTK 4 deixará de dar suporte a `GTK_OVERLAY_SCROLLING`. Ele já foi [retirado](https://github.com/GNOME/gtk/commit/e49615184a9d85bb0bb4e289b3ee8252adee3813#diff-3cf94c6e1eb009e20985034bc2210bfd) do ramo mestre. A partir do GTK 4, a natureza de sobreposição das barras de rolagem é parte do kit de ferramentas. A alternância geral foi removida para impedir que os desenvolvedores quebrem aplicativos que não foram testados com ambas as combinações. Para permitir que os desenvolvedores de aplicativos decidam como devem ser seus aplicativos, o kit de ferramentas fornece um mecanismo para desativar ou adicionar uma configuração aos usuários. A função [gtk_scrolled_window_set_overlay_scrolling()](https://developer.gnome.org/gtk3/stable/GtkScrolledWindow.html#gtk-scrolled-window-set-overlay-scrolling) pode ser usada para ativar/desativar a sobreposição de rolagem em uma base *por aplicativo*. Os desenvolvedores de aplicativos podem, opcionalmente, usar o [GSettings](https://blog.gtk.org/2017/05/01/first-steps-with-gsettings/) para ter uma configuração de usuário vinculada à propriedade.

#### Remover indicadores de rolagem de sobreposição

As posições das barras de rolagem de sobreposição são indicadas por linhas tracejadas finas na janela do aplicativo. Essas linhas tracejadas estarão presentes mesmo quando a rolagem de overlay estiver desabilitada usando a variável de ambiente discutida na seção acima. Para remover as linhas do indicador, crie o seguinte arquivo:

 `~/.config/gtk-3.0/gtk.css` 
```
/* Remover linhas tracejadas de aplicativos GTK 3 */
undershoot.top, undershoot.right, undershoot.bottom, undershoot.left { background-image: none; }

```

### Exemplos

Exemplo de configurações do GTK:

**Nota:** Pode ser ignorado para alguns [ambientes de desktop](/index.php/Ambientes_de_desktop "Ambientes de desktop") (p.ex., [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)")).
 `~/.gtkrc-2.0` 
```
gtk-theme-name="Arc-Dark"
gtk-icon-theme-name="breeze-dark"
gtk-font-name="Sans 11"
gtk-cursor-theme-name="Breeze_Amber"
gtk-cursor-theme-size=0
gtk-toolbar-style=GTK_TOOLBAR_BOTH_HORIZ
gtk-toolbar-icon-size=GTK_ICON_SIZE_SMALL_TOOLBAR
gtk-button-images=0
gtk-menu-images=0
gtk-enable-event-sounds=0
gtk-enable-input-feedback-sounds=0
gtk-xft-antialias=1
gtk-xft-hinting=1
gtk-xft-hintstyle="hintslight"
gtk-xft-rgba="rgb"
```
 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-theme-name=Arc-Dark
gtk-icon-theme-name=breeze-dark
gtk-font-name=Sans 11
gtk-cursor-theme-name=Breeze_Amber
gtk-cursor-theme-size=0
gtk-toolbar-style=GTK_TOOLBAR_BOTH_HORIZ
gtk-toolbar-icon-size=GTK_ICON_SIZE_SMALL_TOOLBAR
gtk-button-images=0
gtk-menu-images=0
gtk-enable-event-sounds=0
gtk-enable-input-feedback-sounds=0
gtk-xft-antialias=1
gtk-xft-hinting=1
gtk-xft-hintstyle=hintslight
gtk-xft-rgba=rgb
# gtk-decoration-layout=menu:close
# gtk-application-prefer-dark-theme=1
```

## Backend do GDK

O GDK (a camada de abstração subjacente do GTK) possui suporte a vários backends para exibir aplicativos GTK. O backend padrão é *x11*.

### Backend do Broadway

O backend do GDK Broadway fornece suporte para a exibição de aplicativos GTK em um navegador da Web, usando HTML5 e soquetes da web. [[4]](https://developer.gnome.org/gtk3/3.8/gtk-broadway.html)

Ao usar *broadwayd*, especifique o número de exibição a ser usado, prefixado com caractere de dois pontos, semelhante a X. O número de exibição padrão é 1.

```
$ display_number=:5

```

Inicie-o.

```
$ broadwayd $display_number

```

Porta usada por padrão

```
port = 8080 + $display_number

```

Aponte seu navegador para [http://127.0.0.1:port](http://127.0.0.1:port)

Para iniciar aplicativos

```
$ GDK_BACKEND=broadway BROADWAY_DISPLAY=$display_number *<<app>>*

```

Alternativamente, você pode definir endereço e porta

```
$ broadwayd --port $port_number --address $address $display_number

```

### Backend do Wayland

O backend GDK do [Wayland](/index.php/Wayland "Wayland") pode ser ativado definindo a variável de ambiente `GDK_BACKEND=wayland`.

**Dica:** Para desabilitar as decorações de janela do GTK no Wayland, [instale](/index.php/Instale "Instale") o pacote [gtk3-optional-csd](https://aur.archlinux.org/packages/gtk3-optional-csd/) e defina a variável de ambiente `GTK_CSD=0`.

## Solução de problemas

### Temas diferentes entre aplicativos GTK 2 e GTK 3

Em geral, se um tema selecionado tiver suporte ao GTK 2 e ao GTK 3, o tema será aplicado a todos os aplicativos GTK 2 e GTK 3\. Se um tema selecionado tiver suporte apenas ao GTK 2, ele será usado para aplicativos do GTK 2 e o tema padrão do GTK será usado para aplicativos do GTK 3\. Se o tema selecionado tiver suporte apenas ao GTK 3, ele será usado para aplicativos do GTK 3 e o tema padrão do GTK será usado para aplicativos do GTK 2\. Assim, para a consistência do tema da aplicação, é melhor usar um tema que tenha suporte ao GTK 2 e o GTK 3.

Você poderia encontrar quais temas instalados em seu sistema possuem uma versão GTK 2 e GTK 3 usando este comando (não funciona com nomes que contenham espaços):

```
find $(find ~/.themes /usr/share/themes/ -wholename "*/gtk-3.0" | sed -e "s/^\(.*\)\/gtk-3.0$/\1/") -wholename "*/gtk-2.0" | sed -e "s/.*\/\(.*\)\/gtk-2.0/\1"/

```

### Tema não aplicado para aplicativos de root

Como arquivos de tema de usuário (`$XDG_CONFIG_HOME/gtk-3.0/settings.ini`, `~/.gtkrc-2.0`) não são lidos por outras contas, o tema selecionado não será aplicado a [aplicativos X sendo executados como root](/index.php/Executando_aplicativos_GUI_como_root "Executando aplicativos GUI como root"). Possíveis soluções incluem:

*   Criar links simbólicos, p.ex.:

```
# ln -s /home/[username]/.gtkrc-2.0 /etc/gtk-2.0/gtkrc
# ln -s /home/[username]/.config/gtk-3.0/settings.ini /etc/gtk-3.0/settings.ini

```

*   Configurar arquivos de temas para todo sistema: `/etc/gtk-3.0/settings.ini` (GTK 3) ou `/etc/gtk-2.0/gtkrc` (GTK 2)
*   Ajustar o tema como root

```
# sudo lxappearance

```

*   Usar o daemon de configurações (é isso que a maioria dos ambientes desktop fazem). Uma variante agnóstica a desktop usando [XSettings](https://specifications.freedesktop.org/xsettings-spec/xsettings-spec-0.5.html) está disponível sob nome [xsettingsd-git](https://aur.archlinux.org/packages/xsettingsd-git/).

### Decorações do lado do cliente

O GTK 3.12 introduziu [decorações para cliente](https://blogs.gnome.org/mclasen/2013/12/05/client-side-decorations-in-themes/), que move a barra de cabeçalho para fora do gerenciador de janela. Isso pode apresentar problemas como [barras de título duplas](http://redmine.audacious-media-player.org/boards/1/topics/1135), nenhuma barra de título ou [sombras duplas](https://github.com/chjj/compton/issues/189) com composição habilitada.

Para remover a sombra e o espaço em torno das janelas (por exemplo, em combinação com um gerenciador de janela de *tiling*), crie o seguinte arquivo:

 `~/.config/gtk-3.0/gtk.css` 
```
.window-frame, .window-frame:backdrop {
 box-shadow: 0 0 0 black;
 border-style: none;
 margin: 0;
 border-radius: 0;
}

.titlebar {
 border-radius: 0;
}

.window-frame.csd.popup {
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2), 0 0 0 1px rgba(0, 0, 0, 0.13);
}

.header-bar {
  background-image: none;
  background-color: #ededed;
  box-shadow: none;
}
/* You may want to use this if you don't like the double title.
GtkLabel.title {
    opacity: 0;
}*/

```

Para ajustar os botões na barra de cabeçalho, use a configuração `gtk-decoration-layout`[[5]](https://developer.gnome.org/gtk3/stable/GtkSettings.html#GtkSettings--gtk-decoration-layout). Os exemplos abaixo removem todos os botões:

 `~/.config/gtk-3.0/settings.ini`  `gtk-decoration-layout=menu:` 

### Cedilha ç/Ç em vez de ć/Ć

Veja [[6]](https://bugs.launchpad.net/ubuntu/+source/ibus/+bug/518056) e [[7]](https://bugs.launchpad.net/ubuntu/+source/ibus/+bug/518056/comments/37) para uma a solução de contorno usando Xcompose (layout EUA internacional).

### Suprimir aviso sobre barramento de acessibilidade

Se você não usa nenhuma recurso do [Acesso Universal do GNOMe](https://wiki.gnome.org/Accessibility), você pode receber avisos com:

```
WARNING **: Couldn't connect to accessibility bus:

```

Para suprimir esses avisos, execute programas com `NO_AT_BRIDGE=1` ou defina isso como uma [variável de ambiente](/index.php/Vari%C3%A1vel_de_ambiente "Variável de ambiente") global.

### Incompatibilidade de cor de fundo da barra de título

Se você estiver usando um [gerenciador de janela](/index.php/Gerenciador_de_janela "Gerenciador de janela") que usa um tema de decoração de janelas que imita a cor de fundo do tema GTK, você pode descobrir que a cor da barra de título não combina mais com a cor do aplicativo em alguns aplicativos do GTK 3\. Como solução alternativa, crie o seguinte arquivo:

 `~/.config/gtk-3.0/gtk.css` 
```
/* Sempre usa cor de plano de fundo */
GtkWindow {
    background-color: @theme_bg_color;
}

/* Corrige substituição de plano de fundo da dica de ferramenta */
.tooltip {
    background-color: rgba(0, 0, 0, 0.8);
}

.tooltip * {
    background-color: transparent;
}

/* Corrige substituição de plano de fundo da janela da área de trabalho do Nautilus */
NautilusWindow {
     background-color: transparent;
}

```

### Eventos de foco incorretos com gerenciadores de janela tiling

**Nota:** Isso desabilita suporte a touchscreen e rolagem suave para aplicativos GTK3\. [[8]](https://bugzilla.gnome.org/show_bug.cgi?id=677329#c14)

[Defina](/index.php/Defina "Defina") `GDK_CORE_DEVICE_EVENTS=1` para usar entrada no estilo GTK2 em vez de xinput2\. [[9]](https://bugzilla.gnome.org/show_bug.cgi?id=677329#c10)

### Suporte a miniaturas para diálogo de arquivos GTK 2

Instale [gtk2-patched-filechooser-icon-view](https://aur.archlinux.org/packages/gtk2-patched-filechooser-icon-view/) para ter a opção para ver arquivos como miniaturas em vez de lista no seletor de arquivos GTK.

### Botão e ícones de menu

Para algumas aplicações na sessão Wayland do GNOME. Seu arquivo `~/.config/gtk-3.0/settings.ini` está desconfigurado. Isso pode acontecer se você tentar outros ambientes de área de trabalho baseados em GTK. Estes são os valores ofensivos:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-button-images=1
gtk-menu-images=1
```

Basta defini-los como 0 ou remover o arquivo inteiro para usar os padrões do GNOME.

### GTK 3 sem polkit

O GTK 3 depende do polkit através do colord, que é necessário para impressão. No entanto, a impressão funciona bem sem o polkit instalado; pelo menos com uma impressora monocromática e versões de pacote gtk3-print-backends=3.22.19-2 e colord=1.4.1-1.

### Alguns temas de GTK 2 só alteram a paleta de cores da UI

Dependendo do tema de escolha do suporte para o GTK 2, os controles da interface do usuário ainda podem ter a aparência padrão do Raleigh, possivelmente com uma paleta de cores diferente. Isso se deve a esses temas que exigem o mecanismo Murrine GTK 2, que está faltando (programas GTK 2 devem reclamar sobre isso em sua saída de erro padrão). Instale o pacote [gtk-engine-murrine](https://www.archlinux.org/packages/?name=gtk-engine-murrine).

### Aplicando patch no seletor de arquivos GTK para usar a digitação adiantada normal

O seletor de arquivos GTK usa o mesmo recurso de busca por digitação antecipada do [GNOME/Files](/index.php/GNOME/Files "GNOME/Files"). Isso pode ser muito chocante e não se encaixa muito bem com outros ambientes de desktop.

Alguns aplicativos possuem suporte ao XDG-desktop-portal, que permite que o aplicativo use o seletor de arquivo nativo. Se isso não funcionar, você pode restaurar a funcionalidade de digitação antecipada usando um GTK com patch aplicado como, por exemplo, [gtk3-mushrooms](https://aur.archlinux.org/packages/gtk3-mushrooms/).

## Veja também

*   [O site oficial do GTK](https://www.gtk.org/)
*   [Artigo do Wikipédia sobre o GTK](https://en.wikipedia.org/wiki/GTK "wikipedia:GTK")