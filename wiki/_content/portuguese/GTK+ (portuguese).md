Artigos relacionados

*   [Visual uniforme para aplicativos Qt e GTK](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications")
*   [Qt](/index.php/Qt "Qt")
*   [Projeto GNU](/index.php/Projeto_GNU "Projeto GNU")
*   [GTK+/Desenvolvimento](/index.php/GTK%2B/Development "GTK+/Development")

Do [site do GTK+](https://www.gtk.org/):

	GTK+, ou o GIMP Toolkit, é um kit de ferramentas multiplataforma para criar interfaces gráficas com o usuário. Oferecendo um conjunto completo de widgets, o GTK + é adequado para projetos que variam de pequenas ferramentas únicas a conjuntos completos de aplicativos.

O GTK+, o GIMP Toolkit, foi criado inicialmente pelo [Projeto GNU](/index.php/Projeto_GNU "Projeto GNU") para o [GIMP](/index.php/GIMP "GIMP"), mas agora é um kit de ferramentas muito popular com vinculações para várias linguagens. Este artigo explorará as ferramentas usadas para configurar o tema, o estilo, o ícone, a fonte e o tamanho da fonte do GTK+, além de detalhar a configuração manual.

## Contents

*   [1 Instalação](#Instalação)
*   [2 Temas](#Temas)
    *   [2.1 GTK+ e Qt](#GTK+_e_Qt)
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
    *   [6.1 Temas diferentes entre aplicativos GTK+ 2 e GTK+ 3](#Temas_diferentes_entre_aplicativos_GTK+_2_e_GTK+_3)
    *   [6.2 Tema não aplicado para aplicativos de root](#Tema_não_aplicado_para_aplicativos_de_root)
    *   [6.3 Decorações do lado do cliente](#Decorações_do_lado_do_cliente)
    *   [6.4 Cedilha ç/Ç em vez de ć/Ć](#Cedilha_ç/Ç_em_vez_de_ć/Ć)
    *   [6.5 Suprimir aviso sobre barramento de acessibilidade](#Suprimir_aviso_sobre_barramento_de_acessibilidade)
    *   [6.6 Incompatibilidade de cor de fundo da barra de título](#Incompatibilidade_de_cor_de_fundo_da_barra_de_título)
    *   [6.7 Eventos de foco incorretos com gerenciadores de janela tiling](#Eventos_de_foco_incorretos_com_gerenciadores_de_janela_tiling)
    *   [6.8 Suporte a miniaturas para diálogo de arquivos GTK+ 2](#Suporte_a_miniaturas_para_diálogo_de_arquivos_GTK+_2)
    *   [6.9 Botão e ícones de menu](#Botão_e_ícones_de_menu)
    *   [6.10 GTK+ 3 sem polkit](#GTK+_3_sem_polkit)
    *   [6.11 Alguns temas de GTK+ 2 só alteram a paleta de cores da UI](#Alguns_temas_de_GTK+_2_só_alteram_a_paleta_de_cores_da_UI)
*   [7 Veja também](#Veja_também)

## Instalação

As duas versões do GTK+ estão atualmente disponíveis nos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais"). Elas podem ser [instaladas](/index.php/Instala "Instala") com os seguintes pacotes:

*   **GTK+ 3.x** está disponível com o pacote [gtk3](https://www.archlinux.org/packages/?name=gtk3).
*   **GTK+ 2.x** está disponível com o pacote [gtk2](https://www.archlinux.org/packages/?name=gtk2).
*   **GTK+ 1.x** está disponível com o pacote [gtk](https://aur.archlinux.org/packages/gtk/).

## Temas

No GTK+ 2, o tema padrão é o Raleigh, mas o Arch Linux tem um arquivo de configuração personalizado em `/usr/share/gtk-2.0/gtkrc`, que define o tema padrão como Adwaita. No GTK+ 3, o tema padrão é Adwaita, mas os temas HighContrast, HighContrastInverse e Raleigh também estão incluídos.

Para forçar um tema específico, defina as seguintes [variáveis de ambiente](/index.php/Vari%C3%A1veis_de_ambiente "Variáveis de ambiente"):

*   Para GTK+ 2, use `GTK2_RC_FILES`. Por exemplo, para iniciar o [GIMP](/index.php/GIMP "GIMP") com o tema Raleigh:

```
$ GTK2_RC_FILES=/usr/share/themes/Raleigh/gtk-2.0/gtkrc gimp

```

**Dica:** `gtkrc` também pode ser um arquivo personalizado em seu diretório home criado por qualquer uma das [#Ferramentas de configuração](#Ferramentas_de_configuração). Veja [#Exemplos](#Exemplos).

*   Para GTK+ 3, use `GTK_THEME`. Por exemplo, para iniciar a Calculadora do GNOME com a variante escura do Adwaita:

```
$ GTK_THEME=Adwaita:dark gnome-calculator

```

**Nota:** Para aplicar o acima aos atalhos da área de trabalho (ou lançadores), consulte [Desktop entries#Modify environment variables](/index.php/Desktop_entries#Modify_environment_variables "Desktop entries").

Mais temas podem ser instalados a partir dos repositórios oficiais ou do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"). Temas extraídos manualmente vão nos diretórios `~/.themes/` ou `~/.local/share/themes/`.

**GTK+ 2 e GTK+ 3.20 ou mais novos tem suporte em:**

*   **Adapta** — Um tema Gtk+ adaptivo baseado em Material Design Guidelines. Inclui: Adapta, Adapta-Eta, Adapta-Nokto, Adapta-Nokto-Eta

	[https://github.com/tista500/Adapta](https://github.com/tista500/Adapta) || [adapta-gtk-theme](https://www.archlinux.org/packages/?name=adapta-gtk-theme)

*   **Arc** — Um tema plano com um visual moderno e elementos transparentes. Inclui: Arc, Arc-Dark, Arc-Darker

	[https://github.com/nicohood/arc-theme](https://github.com/nicohood/arc-theme) || com transparência: [arc-gtk-theme](https://www.archlinux.org/packages/?name=arc-gtk-theme), sem transparência: [arc-solid-gtk-theme](https://www.archlinux.org/packages/?name=arc-solid-gtk-theme)

*   **Bluebird** — Blue Desktop Suite para o Xfce.

	[https://github.com/shimmerproject/Bluebird](https://github.com/shimmerproject/Bluebird) || [xfce-theme-bluebird](https://aur.archlinux.org/packages/xfce-theme-bluebird/)

*   **Breeze** — A versão GTK+ do tema de widgets padrão do KDE. Inclui: Breeze, Breeze-Dark

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

	[https://github.com/shimmerproject/Numix](https://github.com/shimmerproject/Numix) || [numix-gtk-theme](https://www.archlinux.org/packages/?name=numix-gtk-theme)

*   **Vertex** — Tema para GTK 3, GTK 2, Gnome-Shell e Cinnamon.

	[https://github.com/horst3180/vertex-theme](https://github.com/horst3180/vertex-theme) || [vertex-themes](https://aur.archlinux.org/packages/vertex-themes/)

*   **Zuki** — Tema para GTK, gnome-shell e mais.

	[https://github.com/lassekongo83/zuki-themes](https://github.com/lassekongo83/zuki-themes) || [zuki-themes](https://aur.archlinux.org/packages/zuki-themes/)

Há vários temas GTK+ adicionais no AUR. Por exemplo, [pesquise por gtk-theme](https://aur.archlinux.org/packages.php?K=gtk-theme).

**Nota:** Porque o GTK+ 3 muda rapidamente, temas GTK+ 3 geralmente exigem retrabalhos após um lançamento do GTK+ 3\. Por este motivo, nem todos os temas para GTK+ 3 podem parecer como pretendidos quando usados com a versão mais recente do GTK+ 3.

### GTK+ e Qt

Se você tem aplicativos GTK+ e Qt (KDE) em sua área de trabalho, sabe que sua aparência não combina bem. Se você deseja fazer seus estilos de GTK+ combinarem com seus estilos de Qt, por favor, leia [Aparência uniforme para aplicativos em Qt e GTK](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications").

## Ferramentas de configuração

A maioria dos grandes [ambientes de desktop](/index.php/Ambientes_de_desktop "Ambientes de desktop") fornecem ferramentas para configurar o tema GTK+, ícones, fonte e tamanho da fonte, e gerenciar essas configurações por [XSettings](https://specifications.freedesktop.org/xsettings-spec/xsettings-spec-0.5.html):

*   Se você usa [Cinnamon](/index.php/Cinnamon "Cinnamon"), use a ferramenta Temas (*cinnamon-settings themes*): vá em *Configurações do sistema > Temas*.
*   Se você usa [Enlightenment](/index.php/Enlightenment "Enlightenment"): vá em *Definições > Tudo > Aparência > Tema das aplicações*.
*   Se você usa [GNOME](/index.php/GNOME "GNOME"), use Ajustes do GNOME (*gnome-tweaks*): instale [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks).
*   Se você usa [MATE](/index.php/MATE "MATE"), use a ferramenta Appearance Preferences (*mate-appearance-properties*): vá em *Sistema > Configurações > Aparência*.
*   Se você usa [Xfce](/index.php/Xfce "Xfce"), use a ferramenta Appearance: vá em *Configurações > Aparência*.

Outras ferramentas GUI geralmente sobrescrevem os [arquivos de configuração](#Configuração).

**Suporte a GTK+ 2 e GTK+ 3:**

*   **KDE GTK Configurator** — Aplicativo que permite que você altere o estilo e fonte de aplicativos GTK+ 2 e GTK+ 3.

	[https://cgit.kde.org/kde-gtk-config.git](https://cgit.kde.org/kde-gtk-config.git) || [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config)

	Após a instalação, `kde-gtk-config` também pode ser encontrado em *Configurações do sistema > Estilo dos aplicativos > GTK*.

*   **LXAppearance** — Ferramenta de configuração de estilo independente para GTK+ 2 e GTK+ 3 do projeto LXDE (não requer outras partes da área de trabalho do LXDE).

	[http://wiki.lxde.org/en/LXAppearance](http://wiki.lxde.org/en/LXAppearance) || [lxappearance](https://www.archlinux.org/packages/?name=lxappearance)

*   **Oo-mox** — Aplicativo gráfico para gerar diferentes variações de cores dos temas dos temas Numix e Flat-Plat (GTK+ 2 e 3), Archdroid e Gnome-Colors. Também permite gerar temas GTK+ 2 pré-dimensionados para telas HiDPI.

	[https://github.com/actionless/oomox](https://github.com/actionless/oomox) || [oomox](https://aur.archlinux.org/packages/oomox/)

**Suporte apenas a GTK+ 2:**

*   **GTK+ Change Theme** — Um programa pequeno que permite que você altere seu tema GTK+ 2.0 (considerado uma alternativa melhor ao *switch2*).

	[http://plasmasturm.org/code/gtk-chtheme/](http://plasmasturm.org/code/gtk-chtheme/) || [gtk-chtheme](https://www.archlinux.org/packages/?name=gtk-chtheme)

*   **GTK+ Preference Tool** — Seletor de temas GTK+ e alternador de fontes.

	[http://gtk-win.sourceforge.net/home/index.php/Main/GTKPreferenceTool](http://gtk-win.sourceforge.net/home/index.php/Main/GTKPreferenceTool) || [gtk2_prefs](https://aur.archlinux.org/packages/gtk2_prefs/)

*   **GTK+ Theme Switch** — Alternador de temas GTK+ simples.

	[http://muhri.net/nav.php3?node=gts](http://muhri.net/nav.php3?node=gts) || [gtk-theme-switch2](https://www.archlinux.org/packages/?name=gtk-theme-switch2)

## Configuração

GTK+ settings can be specified manually in configuration files, but desktop environments and applications can override these settings. Depending on GTK+ version, these files are located at:

*   GTK+ 2 user specific: `~/.gtkrc-2.0`
*   GTK+ 2 system wide: `/etc/gtk-2.0/gtkrc`
*   GTK+ 3 user specific: `$XDG_CONFIG_HOME/gtk-3.0/settings.ini`, or `$HOME/.config/gtk-3.0/settings.ini` if `$XDG_CONFIG_HOME` is not set
*   GTK+ 3 system wide: `/etc/gtk-3.0/settings.ini`

**Note:**

*   See the [GTK+ 3 *GtkSettings* properties](https://developer.gnome.org/gtk3/stable/GtkSettings.html#GtkSettings.properties) (and [GTK+ 2 properties](https://developer.gnome.org/gtk2/stable/GtkSettings.html#GtkSettings.properties)) in the GTK+ programming reference manual for the full list of currently supported GTK+ configuration options.
*   Some of the settings described below (such as `gtk-icon-sizes`) are deprecated and ignored since GTK+ 3.10.
*   If you edit your GTK+ configuration files, only newly started applications will display the changes.

### Configuração básica de tema

To manually change the GTK+ theme, icons, font and font size, add the following to the configuration files, for example:

*   GTK+ 2:

 `~/.gtkrc-2.0` 
```
gtk-icon-theme-name = "Adwaita"
gtk-theme-name = "Adwaita"
gtk-font-name = "DejaVu Sans 11"
```

*   GTK+ 3:

 `$XDG_CONFIG_HOME/gtk-3.0/settings.ini` 
```
[Settings]
gtk-icon-theme-name = Adwaita
gtk-theme-name = Adwaita
gtk-font-name = DejaVu Sans 11
```

**Note:** The icon theme name is the name defined in the theme's index file, *not* the name of its directory.

### Variante escura de tema

Some GTK+ 3 themes contain a dark theme variant, but it's only used by default when the application requests it explicitly. To use dark theme variant with all GTK+ 3 applications, set:

```
gtk-application-prefer-dark-theme = true

```

### Atalhos de teclado

Keyboard shortcuts (otherwise known as *accelerators* in GTK+) may be changed by hovering the mouse over the respective menu item, and pressing the desired key combination. To enable this feature, set:

```
gtk-can-change-accels = 1

```

#### Vinculações de teclas Emacs

To have Emacs-like key bindings in GTK+ applications add the following:

 `~/.gtkrc-2.0`  `gtk-key-theme-name = "Emacs"`  `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-key-theme-name = Emacs
```

For GTK+3 also run:

```
$ gsettings set org.gnome.desktop.interface gtk-key-theme "Emacs"

```

XFCE has a similar setting:

```
$ xfconf-query -c xsettings -p /Gtk/KeyThemeName -s Emacs

```

The config files in `/usr/share/themes/Emacs/` determine what the Emacs bindings are, and can be changed. Copying sections to the users `~/.gtkrc-2.0` file allows for changes on a per user basis.

### Atraso no menu do GNOME

This setting controls the delay between pointing the mouse at a menu and that menu opening. This delay is measured in milliseconds.

```
gtk-menu-popup-delay = 0

```

### Reduzir tamanhos de widgets

If you have a small screen or you just do not like big icons and widgets, you can resize things easily.

To have icons without text in toolbars ([valid values](https://developer.gnome.org/gtk3/stable/gtk3-Standard-Enumerations.html#GtkToolbarStyle)), use

```
gtk-toolbar-style = GTK_TOOLBAR_ICONS

```

To use smaller icons, use a line like this:

```
gtk-icon-sizes = "panel-menu=16,16:panel=16,16:gtk-menu=16,16:gtk-large-toolbar=16,16\
:gtk-small-toolbar=16,16:gtk-button=16,16"

```

Or to remove icons from buttons completely:

```
gtk-button-images = 0

```

You can also remove icons from menus:

```
gtk-menu-images = 0

```

See also [[1]](http://martin.ankerl.com/2008/10/10/how-to-make-a-compact-gnome-theme/) and [[2]](http://gnome-look.org/content/show.php/Simple+eGTK?content=119812).

### Ocultar botões de CSD

To remove the minimize and maximize buttons from *gtk3* windows:

```
gtk-decoration-layout=menu:close

```

See [[3]](https://developer.gnome.org/gtk3/3.22/GtkSettings.html#GtkSettings--gtk-decoration-layout).

### Desabilitar colagem com mouse

To turn off pasting on middle mouse button click (aka PRIMARY):

```
gtk-enable-primary-paste=false

```

### Localização inicial do seletor de arquivos

Open the file-chooser within the **current working directory** and not the **recent** location. Normally the **current working directory** is the *Home* directory.

**GTK+ 3**

Change [setting](/index.php/GNOME#Configuration "GNOME") with the following command:

```
$ gsettings set org.gtk.Settings.FileChooser startup-mode cwd

```

**GTK+ 2**

Add the following to `~/.config/gtk-2.0/gtkfilechooser.ini`:

```
StartupMode=cwd

```

### Comportamento de rolagem legada

**Note:** This setting is not obeyed by all GTK+ applications.

**Tip:** Legacy scrolling behaviour can be achieved reliably simply by using right click instead of left click.

Prior to GTK+ 3.6, clicking on either side of the slider in the scrollbar would move the scrollbar in the direction of the click by approximately one page. Since GTK+ 3.6, the slider will move directly to the position of the click. This behaviour can be reverted in some applications by creating the file with the content below:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-primary-button-warps-slider = false

```

### Desabilitar barras de rolagem de sobreposição

Since GTK+ 3.15, overlay scrollbars are enabled by default, meaning that scrollbars will be shown only on mouseover in GTK+ 3 applications. This behavior can be reverted by setting the following environment variable: `GTK_OVERLAY_SCROLLING=0`. See [Environment variables#Graphical applications](/index.php/Environment_variables#Graphical_applications "Environment variables").

GTK+ 4 will no longer support `GTK_OVERLAY_SCROLLING`. It has already been [dropped](https://github.com/GNOME/gtk/commit/e49615184a9d85bb0bb4e289b3ee8252adee3813#diff-3cf94c6e1eb009e20985034bc2210bfd) from master. As of GTK+ 4, the overlay nature of the scrollbars is part of the toolkit. The blanket toggle has been removed to prevent developers from breaking applications that haven't been tested with both combinations. To allow application developers to decide what their applications should look like, the toolkit instead provides a mechanism to opt-out or add a setting for users. The function [gtk_scrolled_window_set_overlay_scrolling()](https://developer.gnome.org/gtk3/stable/GtkScrolledWindow.html#gtk-scrolled-window-set-overlay-scrolling) can be used to enable/disable overlay scrolling on a *per-application* basis. Application developers can optionally use [GSettings](https://blog.gtk.org/2017/05/01/first-steps-with-gsettings/) to have a user setting bound to the property.

#### Remover indicadores de rolagem de sobreposição

The positions of the overlay scrollbars are indicated by thin dashed lines in the application window. These dashed lines will be present even when overlay scrolling is disabled using the environment variable discussed in the section above. To remove the indicator lines, create the following file:

 `~/.config/gtk-3.0/gtk.css` 
```
/* Remove dotted lines from GTK+ 3 applications */
undershoot.top, undershoot.right, undershoot.bottom, undershoot.left { background-image: none; }

```

### Exemplos

GTK+ example configurations:

**Note:** May be ignored by some [desktop environments](/index.php/Desktop_environments "Desktop environments") (e.g. [GNOME](/index.php/GNOME "GNOME")).
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

GDK (the underlying abstraction layer of GTK+) supports multiple backends to display GTK+ applications. The default backend is *x11*.

### Backend do Broadway

The GDK Broadway backend provides support for displaying GTK+ applications in a web browser, using HTML5 and web sockets. [[4]](https://developer.gnome.org/gtk3/3.8/gtk-broadway.html)

When using broadwayd, specify the display number to use, prefixed with a colon, similar to X. The default display number is 1.

```
$ display_number=:5

```

Start it.

```
$ broadwayd $display_number 

```

Port Used on default

```
port = 8080 + $display_number

```

Point your browser to [http://127.0.0.1:port](http://127.0.0.1:port)

To Start apps

```
$ GDK_BACKEND=broadway BROADWAY_DISPLAY=$display_number *<<app>>*

```

Alternatively can set address and port

```
$ broadwayd --port $port_number --address $address $display_number

```

### Backend do Wayland

The GDK [Wayland](/index.php/Wayland "Wayland") backend can be enabled by setting the `GDK_BACKEND=wayland` environment variable.

**Tip:** To disable GTK window decorations in Wayland, [install](/index.php/Install "Install") the [gtk3-optional-csd](https://aur.archlinux.org/packages/gtk3-optional-csd/) package and set the environment variable `GTK_CSD=0`.

## Solução de problemas

### Temas diferentes entre aplicativos GTK+ 2 e GTK+ 3

In general, if a selected theme has support for both GTK+ 2 and GTK+ 3, the theme will be applied to all GTK+ 2 and GTK+ 3 applications. If a selected theme has support for only GTK+ 2, it will be used for GTK+ 2 applications and the default GTK+ theme will be used for GTK+ 3 applications. If the selected theme has support for only GTK+ 3, it will be used for GTK+ 3 applications and the default GTK+ theme will be used for GTK+ 2 applications. Thus for application theme consistency, it is best to use a theme which has support for both GTK+ 2 and GTK+ 3.

You could find what themes installed on your system have both an GTK+ 2 and GTK+ 3 version by using this command (does not work with names containing spaces):

```
find $(find ~/.themes /usr/share/themes/ -wholename "*/gtk-3.0" | sed -e "s/^\(.*\)\/gtk-3.0$/\1/") -wholename "*/gtk-2.0" | sed -e "s/.*\/\(.*\)\/gtk-2.0/\1"/

```

### Tema não aplicado para aplicativos de root

As user theme files (`$XDG_CONFIG_HOME/gtk-3.0/settings.ini`, `~/.gtkrc-2.0`) are not read by other accounts, the selected theme will not apply to [X applications run as root](/index.php/Running_X_apps_as_root "Running X apps as root"). Possible solutions include:

*   Create symlinks, e.g

```
# ln -s /home/[username]/.gtkrc-2.0 /etc/gtk-2.0/gtkrc
# ln -s /home/[username]/.config/gtk-3.0/settings.ini /etc/gtk-3.0/settings.ini

```

*   Configure system-wide theme files: `/etc/gtk-3.0/settings.ini` (GTK+ 3) or `/etc/gtk-2.0/gtkrc` (GTK+ 2)
*   Adjust the theme as root

```
# sudo lxappearance

```

*   Use a settings daemon (this is what most desktop environments do). A desktop-agnostic variant using [XSettings](https://specifications.freedesktop.org/xsettings-spec/xsettings-spec-0.5.html) is available in the [AUR](/index.php/AUR "AUR") under [xsettingsd-git](https://aur.archlinux.org/packages/xsettingsd-git/).

### Decorações do lado do cliente

GTK 3.12 introduced [client-side decorations](https://blogs.gnome.org/mclasen/2013/12/05/client-side-decorations-in-themes/), which move the title-bar away from the window manager. This may present issues such as [double title-bars](http://redmine.audacious-media-player.org/boards/1/topics/1135), no title-bar at all or [double shadows](https://github.com/chjj/compton/issues/189) with compositing enabled.

To remove the shadow and gap around windows (for example in combination with a tiling window manager), create the following file:

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

To adjust the buttons in the header bar, use the `gtk-decoration-layout` setting. [[5]](https://developer.gnome.org/gtk3/stable/GtkSettings.html#GtkSettings--gtk-decoration-layout) The below examples removes all buttons:

 `~/.config/gtk-3.0/settings.ini`  `gtk-decoration-layout=menu:` 

### Cedilha ç/Ç em vez de ć/Ć

See [[6]](https://bugs.launchpad.net/ubuntu/+source/ibus/+bug/518056), and [[7]](https://bugs.launchpad.net/ubuntu/+source/ibus/+bug/518056/comments/37) for a workaround using Xcompose (US international layout).

### Suprimir aviso sobre barramento de acessibilidade

If you do not use any [Gnome Accessibility](https://wiki.gnome.org/Accessibility) features, you may receive warnings like:

```
WARNING **: Couldn't connect to accessibility bus:

```

To suppress these warnings, execute programs with `NO_AT_BRIDGE=1` or set that as a global [environment variable](/index.php/Environment_variable "Environment variable").

### Incompatibilidade de cor de fundo da barra de título

If you are using a [window manager](/index.php/Window_manager "Window manager") which uses a window decoration theme that mimics the GTK+ theme background color, you may find that the titlebar color no longer completely matches the application color in some GTK+ 3 applications. As a workaround, create the following file:

 `~/.config/gtk-3.0/gtk.css` 
```
/* Always use background color */
GtkWindow {
    background-color: @theme_bg_color;
}

/* Fix tooltip background override */
.tooltip {
    background-color: rgba(0, 0, 0, 0.8);
}

.tooltip * {
    background-color: transparent;
}

/* Fix Nautilus desktop window background override */
NautilusWindow {
     background-color: transparent; 
}

```

### Eventos de foco incorretos com gerenciadores de janela tiling

**Note:** This disables touchscreen support for GTK3 applications. [[8]](https://bugzilla.gnome.org/show_bug.cgi?id=677329#c14)

[Define](/index.php/Define "Define") `GDK_CORE_DEVICE_EVENTS=1` to use GTK2 style input, instead of xinput2\. [[9]](https://bugzilla.gnome.org/show_bug.cgi?id=677329#c10)

### Suporte a miniaturas para diálogo de arquivos GTK+ 2

Install [gtk2-patched-filechooser-icon-view](https://aur.archlinux.org/packages/gtk2-patched-filechooser-icon-view/) to have the option to view files as thumbnails instead of list in the GTK+ file chooser.

### Botão e ícones de menu

For some applications in GNOME's Wayland session. Your `~/.config/gtk-3.0/settings.ini` file is misconfigured. This can happen if you try other GTK+ based desktop environments. These are the offending values:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-button-images=1
gtk-menu-images=1
```

Simply set them to 0 or remove the whole file to use GNOME defaults.

### GTK+ 3 sem polkit

GTK+3 depends on polkit through colord, which is required for printing. However printing works fine without polkit installed; at least with a monochrome printer and package versions gtk3-print-backends=3.22.19-2 and colord=1.4.1-1.

### Alguns temas de GTK+ 2 só alteram a paleta de cores da UI

Depending on the theme of choice's support for GTK+ 2, UI controls may still have the default Raleigh appearance, possibly with a different color palette. This is due to these themes requiring the GTK+ 2 Murrine engine, which is missing (GTK+ 2 programs should complain about it on their standard error output). Install the [gtk-engine-murrine](https://www.archlinux.org/packages/?name=gtk-engine-murrine) package.

## Veja também

*   [The official GTK+ website](https://www.gtk.org/)
*   [Wikipedia article about GTK+](https://en.wikipedia.org/wiki/GTK%2B "wikipedia:GTK+")