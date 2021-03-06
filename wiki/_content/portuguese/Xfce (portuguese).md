Artigos relacionados

*   [Ambiente de desktop](/index.php/Ambiente_de_desktop "Ambiente de desktop")
*   [Gerenciador de janela](/index.php/Gerenciador_de_janela "Gerenciador de janela")
*   [Xfwm](/index.php/Xfwm "Xfwm")
*   [Thunar](/index.php/Thunar "Thunar")
*   [LXDE](/index.php/LXDE "LXDE")
*   [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)")

[Xfce](http://www.xfce.org) é um [ambiente de desktop](/index.php/Ambiente_de_desktop "Ambiente de desktop") leve e modular atualmente baseado no GTK 2 e GTK 3\. Para fornecer uma experiência de usuário completa, ele inclui um gerenciador de janela, um gerenciador de arquivos, área de trabalho e painel.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Iniciando](#Iniciando)
*   [3 Configuração](#Configuração)
    *   [3.1 Menu](#Menu)
        *   [3.1.1 Menu whisker](#Menu_whisker)
        *   [3.1.2 Editar entradas](#Editar_entradas)
    *   [3.2 Área de trabalho](#Área_de_trabalho)
        *   [3.2.1 Plano de fundo transparente para títulos de ícones](#Plano_de_fundo_transparente_para_títulos_de_ícones)
        *   [3.2.2 Remover ícones da área de trabalho](#Remover_ícones_da_área_de_trabalho)
        *   [3.2.3 Um papel de parede entre vários monitores](#Um_papel_de_parede_entre_vários_monitores)
        *   [3.2.4 Atalho para matar janelas](#Atalho_para_matar_janelas)
    *   [3.3 Sessão](#Sessão)
        *   [3.3.1 Inicialização automática](#Inicialização_automática)
        *   [3.3.2 Bloquear a tela](#Bloquear_a_tela)
        *   [3.3.3 Suspensão](#Suspensão)
        *   [3.3.4 Desabilitar sessões salvas](#Desabilitar_sessões_salvas)
        *   [3.3.5 Usar um gerenciador de janela diferente](#Usar_um_gerenciador_de_janela_diferente)
    *   [3.4 Temas](#Temas)
    *   [3.5 Som](#Som)
        *   [3.5.1 Temas de som](#Temas_de_som)
        *   [3.5.2 Botões de volume do teclado](#Botões_de_volume_do_teclado)
            *   [3.5.2.1 Atalhos](#Atalhos)
    *   [3.6 Atalhos de teclado](#Atalhos_de_teclado)
    *   [3.7 Agente de autenticação polkit](#Agente_de_autenticação_polkit)
    *   [3.8 Piscar da tela](#Piscar_da_tela)
*   [4 Dicas e truques](#Dicas_e_truques)
    *   [4.1 Ocultar partições do thunar e do xfdesktop](#Ocultar_partições_do_thunar_e_do_xfdesktop)
    *   [4.2 Capturas de tela](#Capturas_de_tela)
    *   [4.3 Desabilitar atalhos F1 e F11 do terminal](#Desabilitar_atalhos_F1_e_F11_do_terminal)
    *   [4.4 Temas ou paletas de cores do terminal](#Temas_ou_paletas_de_cores_do_terminal)
        *   [4.4.1 Alternando o tema de cores padrão](#Alternando_o_tema_de_cores_padrão)
        *   [4.4.2 Tema de cores tango do terminal](#Tema_de_cores_tango_do_terminal)
    *   [4.5 Abrir URLs com o botão do meio do mouse no terminal](#Abrir_URLs_com_o_botão_do_meio_do_mouse_no_terminal)
    *   [4.6 Gerenciador de cores](#Gerenciador_de_cores)
    *   [4.7 Vários monitores](#Vários_monitores)
    *   [4.8 Agentes SSH](#Agentes_SSH)
    *   [4.9 Rolar uma janela de plano de fundo sem mudar o foco nela](#Rolar_uma_janela_de_plano_de_fundo_sem_mudar_o_foco_nela)
    *   [4.10 Modificador de botão do mouse](#Modificador_de_botão_do_mouse)
    *   [4.11 Definir o clique com dois dedos para clique com botão do meio para um touchpad](#Definir_o_clique_com_dois_dedos_para_clique_com_botão_do_meio_para_um_touchpad)
    *   [4.12 Limitar o brilho mínimo do brightness-slider](#Limitar_o_brilho_mínimo_do_brightness-slider)
    *   [4.13 Adicionar imagens de perfil](#Adicionar_imagens_de_perfil)
    *   [4.14 Rótulo do plugin de gerenciamento de energia](#Rótulo_do_plugin_de_gerenciamento_de_energia)
*   [5 Solução de problemas](#Solução_de_problemas)
    *   [5.1 Ícones da área de trabalho se reorganizam sozinhos](#Ícones_da_área_de_trabalho_se_reorganizam_sozinhos)
    *   [5.2 Temas GTK não funcionam com vários monitores](#Temas_GTK_não_funcionam_com_vários_monitores)
    *   [5.3 Ícones não aparecem nos menus de clique de botão direito](#Ícones_não_aparecem_nos_menus_de_clique_de_botão_direito)
    *   [5.4 NVIDIA e xfce4-sensors-plugin](#NVIDIA_e_xfce4-sensors-plugin)
    *   [5.5 Telas pretas na inicialização com NVIDIA e vários monitores](#Telas_pretas_na_inicialização_com_NVIDIA_e_vários_monitores)
    *   [5.6 Miniaplicativos de painéis sendo alinhados à esquerda](#Miniaplicativos_de_painéis_sendo_alinhados_à_esquerda)
    *   [5.7 A preferência de aplicativos preferidos não têm efeito](#A_preferência_de_aplicativos_preferidos_não_têm_efeito)
    *   [5.8 Restaurar configurações padrão](#Restaurar_configurações_padrão)
    *   [5.9 Falha de sessão](#Falha_de_sessão)
    *   [5.10 Fontes no título da janela travando o xfce4-title](#Fontes_no_título_da_janela_travando_o_xfce4-title)
    *   [5.11 Configurações de tampa do laptop ignoradas](#Configurações_de_tampa_do_laptop_ignoradas)
    *   [5.12 O botão de ação de troca de usuário está acinzentada](#O_botão_de_ação_de_troca_de_usuário_está_acinzentada)
    *   [5.13 Macros em .Xresources não funcionam](#Macros_em_.Xresources_não_funcionam)
    *   [5.14 Tema do cursor não muda ao iniciar a sessão](#Tema_do_cursor_não_muda_ao_iniciar_a_sessão)
*   [6 Veja também](#Veja_também)

## Instalação

[Install](/index.php/Install "Install") the [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/) group. You may also wish to install the [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/) group which includes extra plugins and a number of useful utilities such as the [mousepad](https://www.archlinux.org/packages/?name=mousepad) editor. Xfce uses the [Xfwm](/index.php/Xfwm "Xfwm") window manager by default.

## Iniciando

Choose *Xfce Session* from the menu in a [display manager](/index.php/Display_manager "Display manager") of choice, or add `exec startxfce4` to [Xinitrc](/index.php/Xinitrc "Xinitrc").

**Note:** Do not call the `xfce4-session` executable directly; `startxfce4` is the correct command which, in turn, calls the former when appropriate.

## Configuração

Xfce stores configuration options in [Xfconf](http://docs.xfce.org/xfce/xfconf/start). There are several ways to modify these options:

*   In the main menu, select [Settings](http://docs.xfce.org/xfce/xfce4-settings/start) and the category you want to customize. Categories are programs usually located in `/usr/bin/xfce4-*` and `/usr/bin/xfdesktop-settings`.
*   `xfce4-settings-editor` can see and modify all settings. Options modified here will take effect immediately. Use `xfconf-query` to change settings from the commandline; see [the documentation](http://docs.xfce.org/xfce/xfconf/xfconf-query) for details.
*   Settings are stored in XML files in `~/.config/xfce4/xfconf/xfce-perchannel-xml/` which can be edited by hand. However, changes made here will *not* take effect immediately.

### Menu

See [Xdg-menu](/index.php/Xdg-menu "Xdg-menu") for more info on using the Free Desktop menu system.

#### Menu whisker

[xfce4-whiskermenu-plugin](https://www.archlinux.org/packages/?name=xfce4-whiskermenu-plugin) (also part of [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/)) is an alternative application launcher. It shows a list of favorites, browses through all installed applications through category buttons, and supports fuzzy searching. After package being installed, it can replace *Applications Menu* as first item in Panel 1 (in *Settings > Panel > Items* add *Whisker Menu*).

#### Editar entradas

A number of graphical tools are available for this task:

*   **MenuLibre** — An advanced menu editor that provides modern features in a clean, easy-to-use interface.

	[https://launchpad.net/menulibre](https://launchpad.net/menulibre) || [menulibre](https://aur.archlinux.org/packages/menulibre/).

*   **Alacarte** — Menu editor for GNOME

	[http://www.gnome.org/](http://www.gnome.org/) || [alacarte](https://www.archlinux.org/packages/?name=alacarte)

*   **XAME (XFCE Applications Menu Editor)** — GUI tool written in Gambas designed specifically for editing menu entries in Xfce, it will not work in other environments. (Discontinued)

	[http://redsquirrel87.altervista.org/doku.php/xfce-applications-menu-editor](http://redsquirrel87.altervista.org/doku.php/xfce-applications-menu-editor) || [xame](https://aur.archlinux.org/packages/xame/)

Alternatively, create the file `~/.config/menus/xfce-applications.menu` manually. See the example configuration below:

```
<!DOCTYPE Menu PUBLIC "-//freedesktop//DTD Menu 1.0//EN"
  "[http://www.freedesktop.org/standards/menu-spec/1.0/menu.dtd](http://www.freedesktop.org/standards/menu-spec/1.0/menu.dtd)">

<Menu>
    <Name>Xfce</Name>
    <MergeFile type="parent">/etc/xdg/menus/xfce-applications.menu</MergeFile>

    <Exclude>
        <Filename>xfce4-run.desktop</Filename>
        <Filename>exo-terminal-emulator.desktop</Filename>
        <Filename>exo-file-manager.desktop</Filename>
        <Filename>exo-mail-reader.desktop</Filename>
        <Filename>exo-web-browser.desktop</Filename>
        <Filename>xfce4-about.desktop</Filename>
        <Filename>xfhelp4.desktop</Filename>
    </Exclude>

    <Layout>
        <Merge type="all"/>
        <Separator/>
        <Menuname>Settings</Menuname>
        <Separator/>
        <Filename>xfce4-session-logout.desktop</Filename>
    </Layout>
</Menu>

```

The `<MergeFile>` tag includes the default Xfce menu.

The `<Exclude>` tag excludes applications which we do not want to appear in the menu. Here we excluded some Xfce default shortcuts, but you can exclude `firefox.desktop` or any other application.

The `<Layout>` tag defines the layout of the menu. The applications can be organized in folders or however we wish. For more details see the [Xfce wiki](http://wiki.xfce.org/howto/customize-menu).

You can also make changes to the Xfce menu by editing the `.desktop` files themselves. To hide entries, see [Entradas de desktop#Ocultar entradas de desktop](/index.php/Entradas_de_desktop#Ocultar_entradas_de_desktop "Entradas de desktop"). You can edit the application's category by modifying the `Categories=` line of the desktop entry, see [Entradas de desktop#Exemplo de arquivo](/index.php/Entradas_de_desktop#Exemplo_de_arquivo "Entradas de desktop").

### Área de trabalho

#### Plano de fundo transparente para títulos de ícones

To change the default white background of desktop icon titles to something more suitable, create or edit `~/.gtkrc-2.0`:

```
style "xfdesktop-icon-view" {
    XfdesktopIconView::label-alpha = 10
    base[NORMAL] = "#000000"
    base[SELECTED] = "#71B9FF"
    base[ACTIVE] = "#71B9FF"
    fg[NORMAL] = "#fcfcfc"
    fg[SELECTED] = "#ffffff"
    fg[ACTIVE] = "#ffffff"
}
widget_class "*XfdesktopIconView*" style "xfdesktop-icon-view"

```

#### Remover ícones da área de trabalho

Issue the following command:

```
$ xfconf-query -c xfce4-desktop -v --create -p /desktop-icons/style -t int -s 0

```

To reinstate icons on the desktop, issue the same command with a value of 2.

#### Um papel de parede entre vários monitores

Open `xfce4-settings-editor` and create a new property with the following settings:

```
Property: /backdrop/screen0/xinerama-stretch
Type: Boolean
Value: TRUE|1|Enabled

```

#### Atalho para matar janelas

Xfce does not have a shortcut to kill a window, for example when a program freezes.

With [xorg-xkill](https://www.archlinux.org/packages/?name=xorg-xkill), use `xkill` to interactively kill a window. For the currently active window, use [xdotool](https://www.archlinux.org/packages/?name=xdotool):

```
$ xdotool getwindowfocus windowkill

```

Alternatively:

```
$ sh -c "xkill -id $(xprop -root -notype | sed -n '/^_NET_ACTIVE_WINDOW/ s/^.*# *\|\,.*$//g p')"

```

To add the shortcut, use *Settings > Keyboard* or an application like [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys).

### Sessão

#### Inicialização automática

To launch custom applications when Xfce starts up, click the *Applications Menu > Settings > Settings Manager* and then choose the *Session and Startup* option and click the tab *Application Autostart*. You will see a list of programs that get launched on startup. To add an entry, click the *Add* button and fill out the form, specifying the path to an executable you want to run.

Autostart applications are stored as `*name*.desktop` in `~/.config/autostart/`.

Alternatively, add the commands you wish to run (including setting environment variables) to [xinitrc](/index.php/Xinitrc "Xinitrc") (or [xprofile](/index.php/Xprofile "Xprofile") when a [display manager](/index.php/Display_manager "Display manager") is being used).

**Tip:** Sometimes it might be useful to **delay the startup of an application**. Note that specifying under *Application > Autostart* a command such as `sleep 3 && *command*` does not work; a workaround is to use the syntax `sh -c "sleep 3 && *command*"`

#### Bloquear a tela

*xflock4* is the reference Bash script which is used to lock an Xfce session.

It tries to lock the screen with either [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver), [gnome-screensaver](https://www.archlinux.org/packages/?name=gnome-screensaver), [slock](https://www.archlinux.org/packages/?name=slock) or [xlockmore](https://www.archlinux.org/packages/?name=xlockmore). It consecutively looks for the corresponding binary or exits with return code 1 if it fails to find any of these four.

The [List of applications/Security#Screen lockers](/index.php/List_of_applications/Security#Screen_lockers "List of applications/Security") contains a short description of these four screen lockers together with other popular applications. There is in this list an alternative locker, [light-locker](https://www.archlinux.org/packages/?name=light-locker), which integrates particularly well with [xfce4-power-manager](https://www.archlinux.org/packages/?name=xfce4-power-manager). Once it is installed, Xfce Power Manager's setting gains an additional *Security* tab to configure *light-locker* and the existing *Lock screen when system is going for sleep* setting is relocated under this tab. In this new GUI it is possible to set whether the session should be locked upon screensaver activity or whenever the system goes to sleep.

To have *xflock4* run *light-locker* or any custom session locker, not among the four cited above, one must set `LockCommand` in the session's xfconf channel to the command line to be used (the command inside the quotes in the following example can be adapted accordingly for other screen lockers):

 `$ xfconf-query -c xfce4-session -p /general/LockCommand -s "*light-locker-command --lock*" --create -t string` 

The panel lock button in the *Action Buttons* panel simply executes `/usr/bin/xflock4`. It should work as expected as long as *xflock4* is functioning i.e. one of the native lockers is installed or a custom locker is configured to integrate with it as proposed above.

#### Suspensão

Whenever asked to suspend, Xfce executes the [xfce4-session-logout(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xfce4-session-logout.1) command with the `suspend` option:

```
$ xfce4-session-logout --suspend

```

Whether or not the session is systematically locked on *suspend* can be configured through the xfconf properties or from the GUI.

To control this state using the CLI: there are two settings that are used, `LockScreen` and `lock-screen-suspend-hibernate`, in respectively the session and the power manager xfconf channels. To prevent locking on suspend, turn them to `false`:

```
$ xfconf-query -c xfce4-session -p /shutdown/LockScreen -s **false**
$ xfconf-query -c xfce4-power-manager -p /xfce4-power-manager/lock-screen-suspend-hibernate -s **false**

```

Similarly, turn them to `true` to lock the session on suspend.

The setting can also be controlled from the GUI: open the *Session and Startup* application and turn the flag *Advanced > Lock screen before sleep* on or off.

Whenever the suspend keyboard button is pressed, it can be handled by either Xfce's power manager or by *systemd-logind*. To give precedence to logind, the following xfconf setting must be set to `true`:

```
$ xfconf-query -c xfce4-power-manager -p /xfce4-power-manager/logind-handle-suspend-key -n -t bool -s **true**

```

**Note:** To check how *systemd-logind* handles events whenever it has precedence over Xfce, check [logind.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/logind.conf.5)

#### Desabilitar sessões salvas

Per user, saved sessions can be disabled by executing the following:

```
$ xfconf-query -c xfce4-session -p /general/SaveOnExit -s false

```

Then navigate to *Applications > Settings > Session and Startup > Sessions* and press the *Clear saved sessions* button to remove all previously saved sessions.

**Tip:** If the command above does not change the setting persistently, use the following command instead: `xfconf-query -c xfce4-session -p /general/SaveOnExit -n -t bool -s false`

Alternatively, Xfce [kiosk mode](https://wiki.xfce.org/howto/kiosk_mode) can be used to disable the saving of sessions systemwide. To disable sessions, create or edit the file `/etc/xdg/xfce4/kiosk/kioskrc` and add the following:

```
[xfce4-session]
SaveSession=NONE

```

If kiosk mode is not working, the user can set read only permissions for the sessions directory:

```
$ rm ~/.cache/sessions/* && chmod 500 ~/.cache/sessions

```

This will prevent Xfce from saving any sessions despite any configuration that specifies otherwise.

#### Usar um gerenciador de janela diferente

**Note:** For the changes to take effect, you will need to clear the saved sessions and ensure that session saving is disabled when logging out for the first time. Once the window manager of choice is running, session saving can be enabled again.

The files specifying the default window manager are found in the following locations:

*   `~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml` - per user
*   `/etc/xdg/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml` - systemwide

The default window manager for the user can be set easily using *xfconf-query*:

```
$ xfconf-query -c xfce4-session -p /sessions/Failsafe/Client0_Command -t string -sa *wm_name*

```

If you want to start the window manager with command line options, see the command below:

```
$ xfconf-query -c xfce4-session -p /sessions/Failsafe/Client0_Command -t string -t string -s *wm_name* -s *--wm-option*

```

If you need more command line options, simply add more `-t string` and `-s *--wm-option*` arguments to the command.

If you want to change the default window manager systemwide, edit the file specified above manually, changing *xfwm4* to the preferred window manager and adding more `<value type="string" value="*--wm-option*"/>` lines for extra command line options if needed.

You can also change the window manager by autostarting `*wm_name* --replace` using the autostart facility or by running `*wm_name* --replace &` in a terminal and making sure the session is saved on logout. Be aware though that this method does not truly change the default manager, it merely replaces it at login. Note that if you are using the autostart facility, you should disable saved sessions as this could lead to the new window manager being started twice after the default window manager.

### Temas

XFCE themes are available at [xfce-look.org](http://www.xfce-look.org). *Xfwm* themes are stored in `/usr/share/themes/xfce4`, and set in *Settings > Window Manager*. [GTK](/index.php/GTK "GTK") themes are set in *Settings > Appearance*.

To achieve a uniform look for all applications, see [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications").

See also [temas de cursor](/index.php/Temas_de_cursor "Temas de cursor"), [Icons](/index.php/Icons "Icons"), and [Font configuration](/index.php/Font_configuration "Font configuration").

### Som

#### Temas de som

XFCE4 supports [freedesktop system sounds](https://www.freedesktop.org/wiki/Specifications/sound-theme-spec/), but it is not configured out of the box.

To enable a sound theme:

1.  Install [libcanberra](https://www.archlinux.org/packages/?name=libcanberra) and [libcanberra-pulse](https://www.archlinux.org/packages/?name=libcanberra-pulse) for [PulseAudio](/index.php/PulseAudio "PulseAudio") support;
2.  "canberra-gtk-module" should be in the GTK_MODULES environment variable (re-login may be required);
3.  Check "Enable event sounds" in Settings Manager → Appearance → Settings tab;
4.  In the Settings Editor set "xsettings/Net/SoundThemeName" to a sound theme located in `/usr/share/sounds/`;
5.  Turn on "System Sounds" in audio mixer (e.g. pavucontrol).

[sound-theme-freedesktop](https://www.archlinux.org/packages/?name=sound-theme-freedesktop) provides a compatible sound theme, but it lacks many required events. A better choice is [sound-theme-smooth](https://aur.archlinux.org/packages/sound-theme-smooth/) (SoundThemeName should be "Smooth").

#### Botões de volume do teclado

[xfce4-pulseaudio-plugin](https://www.archlinux.org/packages/?name=xfce4-pulseaudio-plugin) provides a panel applet which has support for keyboard volume control and volume notifications. As an alternative, you can install [xfce4-volumed-pulse](https://aur.archlinux.org/packages/xfce4-volumed-pulse/), which also provides keybinding and notification control, but without an icon sitting in the panel. This is handy, for example, when using [pasystray](https://www.archlinux.org/packages/?name=pasystray) at the same time for a finer control.

Alternatively, [xfce4-mixer](https://aur.archlinux.org/packages/xfce4-mixer/) also provides a panel applet and keyboard shortcuts which supports Alsa as well. Note however, that it is based on a feature of GStreamer 0.10 which has been abandoned in 1.0.

For non desktop environment specific alternatives, see [List of applications/Multimedia#Volume control](/index.php/List_of_applications/Multimedia#Volume_control "List of applications/Multimedia").

##### Atalhos

If you are not using an applet or daemon that controls the volume keys, you can map volume control commands to your volume keys manually using Xfce's keyboard settings. For the sound system you are using, see the sections linked to below for the appropriate commands.

*   ALSA: see [Advanced Linux Sound Architecture#Keyboard volume control](/index.php/Advanced_Linux_Sound_Architecture#Keyboard_volume_control "Advanced Linux Sound Architecture").
*   PulseAudio: see [PulseAudio#Keyboard volume control](/index.php/PulseAudio#Keyboard_volume_control "PulseAudio")
*   OSS: see [OSS#Using multimedia keys with OSS](/index.php/OSS#Using_multimedia_keys_with_OSS "OSS").

### Atalhos de teclado

Keyboard shortcuts are defined in two places: *Settings > Window Manager > Keyboard*, and *Settings > Keyboard > Shortcuts*.

### Agente de autenticação polkit

The [polkit-gnome](https://www.archlinux.org/packages/?name=polkit-gnome) agent will be installed along with [xfce4-session](https://www.archlinux.org/packages/?name=xfce4-session) and autostarted automatically; no user intervention is required. For more information, see [Polkit#Authentication agents](/index.php/Polkit#Authentication_agents "Polkit").

A third party polkit authentication agent for Xfce is also available, see [xfce-polkit](https://aur.archlinux.org/packages/xfce-polkit/) or [xfce-polkit-git](https://aur.archlinux.org/packages/xfce-polkit-git/).

### Piscar da tela

Some programs that are commonly used with Xfce will control monitor blanking and [DPMS](/index.php/DPMS "DPMS") (monitor powersaving) settings. They are discussed below.

	Xfce Power Manager

*Xfce Power Manager* controls blanking and DPMS settings. These settings can be configured in the *Power Manager* GUI within the *Display* tab.

Note that when *Display power management* is turned off, DPMS is fully disabled, it does not mean that *Power Manager* will simply stop controlling DPMS. It does not disable screen blanking either. To disable both blanking and DPMS, right click on the power manager system tray icon or left click on the panel applet and make sure that the option labelled *Presentation mode* is ticked.

	XScreenSaver

If [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver) is installed and runs alongside Xfce Power Manager, it may not be clear which application is in control of blanking and DPMS as both are competing for control of the same settings. Therefore, in a situation where it is important that the monitor not be blanked (when watching a video for instance), it is advisable to disable blanking and DPMS through both applications. To know more about *XScreenSaver* options, see [XScreenSaver#DPMS and blanking settings](/index.php/XScreenSaver#DPMS_and_blanking_settings "XScreenSaver").

	xset

If neither of the above applications are running, then blanking and DPMS settings can be controlled using the *xset* command, see [DPMS#Modify DPMS and screensaver settings with a command](/index.php/DPMS#Modify_DPMS_and_screensaver_settings_with_a_command "DPMS").

**Note:** There are some issues associated with blanking and resuming from blanking in some configurations. See [[1]](https://bbs.archlinux.org/viewtopic.php?id=194313&p=2)[[2]](https://bugzilla.xfce.org/show_bug.cgi?id=11107).

## Dicas e truques

### Ocultar partições do thunar e do xfdesktop

If your installation partitions are shown as mounted devices on the desktop and in Thunar, try to install [gvfs](https://www.archlinux.org/packages/?name=gvfs). See [Udisks#Hide selected partitions](/index.php/Udisks#Hide_selected_partitions "Udisks") for more advanced configuration options.

### Capturas de tela

Xfce has its own screenshot tool, [xfce4-screenshooter](https://www.archlinux.org/packages/?name=xfce4-screenshooter). It is part of the [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/) group.

Go to *Applications > Settings > Keyboard*, *Application Shortcuts*. Add the `xfce4-screenshooter -f` (or `-w` for the active window) command to use the `Print` key in order to take fullscreen screenshots. See screenshooter's man page for other optional arguments.

Alternatively, an independent screenshot program like [scrot](/index.php/Taking_a_screenshot#scrot "Taking a screenshot") can be used.

### Desabilitar atalhos F1 e F11 do terminal

The xfce terminal binds F1 and F11 to help and fullscreen, respectively, which can make using programs like htop difficult. To disable those shortcuts, create or edit its configuration file, then log out and log back in. F10 can disabled in the Preferences menu.

 `~/.config/xfce4/terminal/accels.scm` 
```
(gtk_accel_path "<Actions>/terminal-window/fullscreen" "")
(gtk_accel_path "<Actions>/terminal-window/contents" "")

```

### Temas ou paletas de cores do terminal

Terminal color themes or palettes can be changed in GUI under Appearance tab in Preferences. These are the colors that are available to most console applications like [Emacs](/index.php/Emacs "Emacs"), [Vi](/index.php/Vi "Vi") and so on. Their settings are stored individually for each system user in `~/.config/xfce4/terminal/terminalrc` file. There are also so many other themes to choose from. Check forum thread [Terminal Colour Scheme Screenshots](https://bbs.archlinux.org/viewtopic.php?id=51818) for hundreds of available choices and themes.

#### Alternando o tema de cores padrão

Xfce's `extra/terminal` package comes with a darker colour palette. To change this, append the following in your terminalrc file for a lighter color theme, that is always visible in darker Terminal backgrounds.

 `~/.config/xfce4/terminal/terminalrc` 
```
ColorPalette5=#38d0fcaaf3a9
ColorPalette4=#e013a0a1612f
ColorPalette2=#d456a81b7b42
ColorPalette6=#ffff7062ffff
ColorPalette3=#7ffff7bd7fff
ColorPalette13=#82108210ffff
```

#### Tema de cores tango do terminal

To switch to tango color theme, open with your favorite editor

```
~/.config/xfce4/terminal/terminalrc

```

And add(replace) these lines:

```
ColorForeground=White
ColorBackground=#323232323232
ColorPalette1=#2e2e34343636
ColorPalette2=#cccc00000000
ColorPalette3=#4e4e9a9a0606
ColorPalette4=#c4c4a0a00000
ColorPalette5=#34346565a4a4
ColorPalette6=#757550507b7b
ColorPalette7=#060698989a9a
ColorPalette8=#d3d3d7d7cfcf
ColorPalette9=#555557575353
ColorPalette10=#efef29292929
ColorPalette11=#8a8ae2e23434
ColorPalette12=#fcfce9e94f4f
ColorPalette13=#72729f9fcfcf
ColorPalette14=#adad7f7fa8a8
ColorPalette15=#3434e2e2e2e2
ColorPalette16=#eeeeeeeeecec

```

### Abrir URLs com o botão do meio do mouse no terminal

On update to version 0.8 open URL with middle mouse turned off by default and just paste clip to cursor. To enable old behavior fix next option in `${XDG_CONFIG_HOME}/xfce4/terminal/terminalrc` (`XDG_CONFIG_HOME=${HOME}/.config` by default)

 `${XDG_CONFIG_HOME}/xfce4/terminal/terminalrc` 
```
[Configuration]
MiscMiddleClickOpensUri=TRUE
```

### Gerenciador de cores

Xfce has no native support for colour management. [[3]](https://bugzilla.xfce.org/show_bug.cgi?id=8559) See [ICC profiles](/index.php/ICC_profiles "ICC profiles") for alternatives.

### Vários monitores

Xfce has support for multiple monitors. Settings can be configured in the *Applications > Settings > Display* dialog. For more information, see the [display](http://docs.xfce.org/xfce/xfce4-settings/display) article from the Xfce documentation.

XFCE's display configuration is not persistent so you may find yourself needing to use the display tool a lot, especially if you use multiple displays. One workaround for this is to use [arandr](https://www.archlinux.org/packages/?name=arandr) to easily configure your display configurations in the form of xrandr commands which you can assign to be executed as XFCE keyboard shortcuts.

### Agentes SSH

By default Xfce 4.10 will try to load gpg-agent or ssh-agent in that order during session initialization. To disable this, create an xfconf key using the following command:

```
xfconf-query -c xfce4-session -p /startup/ssh-agent/enabled -n -t bool -s false

```

To force using ssh-agent even if gpg-agent is installed, run the following instead:

```
xfconf-query -c xfce4-session -p /startup/ssh-agent/type -n -t string -s ssh-agent

```

To use [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring"), simply tick the checkbox *Launch GNOME services on startup* in the *Advanced* tab of *Session and Startup* in Xfce's settings. This will also disable gpg-agent and ssh-agent.

Source: [http://docs.xfce.org/xfce/xfce4-session/advanced](http://docs.xfce.org/xfce/xfce4-session/advanced)

### Rolar uma janela de plano de fundo sem mudar o foco nela

Go to *Main Menu > Settings > Window Manager Tweaks > Accessibility* tab. Uncheck *Raise windows when any mouse button is pressed*.

### Modificador de botão do mouse

By default, the mouse button modifier in Xfce is set to `Alt`. This can be changed with *xfconf-query*. For instance, the following command will set the `Super` key as the mouse button modifier:

```
$ xfconf-query -c xfwm4 -p /general/easy_click -n -t string -s "Super"

```

Strictly speaking, using multiple modifiers is not supported. However, as a workaround, multiple modifiers can be specified if the key names are separated with `><`. For instance, to set `Ctrl+Alt` as the mouse button modifier, you can use the following command:

```
$ xfconf-query -c xfwm4 -p /general/easy_click -n -t string -s "Ctrl><Alt"

```

### Definir o clique com dois dedos para clique com botão do meio para um touchpad

If you want the 2 finger click on the touchpad to do a middle click, create or edit the following file:

 `~/.config/xfce4/xfconf/xfce-perchannel-xml/pointers.xml` 
```
<channel name="pointers" version="1.0">
  <property name="SynPS2_Synaptics_TouchPad" type="empty">
    <property name="Properties" type="empty">
      <property name="Synaptics_Tap_Action" type="array">
        <value type="int" value="0"/>
        <value type="int" value="0"/>
        <value type="int" value="0"/>
        <value type="int" value="0"/>
        <value type="int" value="1"/>
        <value type="int" value="2"/>
        <value type="int" value="3"/>
      </property>
    </property>
  </property>
</channel>

```

The 2 in the array is the middle click.

### Limitar o brilho mínimo do brightness-slider

Limiting the minimum brightness can be useful for displays which turn off backlight on a brightness level of 0\. In `xfce4-power-manager 1.3.2` a new hidden option had been introduced to set a minimum brightness value with a xfconf4-property. Add `brightness-slider-min-level` as an int property in xfconf4\. Adjust the int value to get a suitable minimum brightness level.

### Adicionar imagens de perfil

To add profile pictures for each user to be displayed in the whisker-menu, simply place a 96x96 PNG file in the respective user's home directory with the name `.face`. For example the PNG file `/home/*bob*/.face` for user *bob*.

Image editing programs like [GIMP](/index.php/GIMP "GIMP") can be used to convert and scale your favourite images down to 96x96.

### Rótulo do plugin de gerenciamento de energia

The xfconf option `show-panel-label` of type `int` controls the label of the power manager, it can be configured for different label formats: it can be set to 0 (no label), 1 (percentage), 2 (remaining time) or 3 (both).

It is also accessible through the power manager plugin GUI in *Properties > Show label*

## Solução de problemas

### Ícones da área de trabalho se reorganizam sozinhos

At certain events (such as opening the panel settings dialog) icons on the desktop rearrange themselves. This is because icon positions are determined by files in the `~/.config/xfce4/desktop/` directory. Each time a change is made to the desktop (icons are added or removed or change position) a new file is generated in this directory and these files can conflict.

To solve the problem, navigate to the directory and delete all the files other than the one which correctly defines the icon positions. You can determine which file defines the correct icon positions by opening it and examining the locations of the icons. The topmost row is defined as `row 0` and the leftmost column is defined by `col 0`. Therefore an entry of:

```
[Firefox]
row=3
col=0

```

means that the Firefox icon will be located on the 4th row of the leftmost column.

### Temas GTK não funcionam com vários monitores

Some configuration tools may corrupt displays.xml, which results in GTK themes under *Applications Menu > Settings > Appearance* ceasing to work. To fix the issue, delete `~/.config/xfce4/xfconf/xfce-perchannel-xml/displays.xml` and reconfigure your screens.

### Ícones não aparecem nos menus de clique de botão direito

**Note:** Despite the deprecation of GConf, this method does still work.

Users may find that icons do not appear when right-clicking options within some applications, including those made with [Qt](/index.php/Qt "Qt"). This problem only appears to happen within Xfce. Run these two commands:

```
$ gconftool-2 --type boolean --set /desktop/gnome/interface/buttons_have_icons true
$ gconftool-2 --type boolean --set /desktop/gnome/interface/menus_have_icons true

```

### NVIDIA e xfce4-sensors-plugin

To detect and use sensors of nvidia gpu you need to install [libxnvctrl](https://www.archlinux.org/packages/?name=libxnvctrl) and then rebuild [xfce4-sensors-plugin](https://www.archlinux.org/packages/?name=xfce4-sensors-plugin) with [ABS](/index.php/ABS "ABS"). You also have the option of using [xfce4-sensors-plugin-nvidia](https://aur.archlinux.org/packages/xfce4-sensors-plugin-nvidia/) which replaces [xfce4-sensors-plugin](https://www.archlinux.org/packages/?name=xfce4-sensors-plugin).

### Telas pretas na inicialização com NVIDIA e vários monitores

Using [NVIDIA](/index.php/NVIDIA "NVIDIA"), multiple monitors and [NVIDIA/Troubleshooting#Avoid screen tearing](/index.php/NVIDIA/Troubleshooting#Avoid_screen_tearing "NVIDIA/Troubleshooting") may result as a black screen when booting Xfce. The screens' position conflict into the files `/etc/X11/xorg.conf` and `~/.config/xfce4/xfconf/xfce-perchannel-xml/displays.xml`. Deleting the `displays.xml` file fixes the behavior.

```
$ rm ~/.config/xfce4/xfconf/xfce-perchannel-xml/displays.xml

```

### Miniaplicativos de painéis sendo alinhados à esquerda

Add a separator someplace before the right end and set its "expand" property. [[4]](https://forums.linuxmint.com/viewtopic.php?f=110&t=155602})

### A preferência de aplicativos preferidos não têm efeito

Most applications rely on [xdg-open](/index.php/Xdg-open "Xdg-open") for opening a preferred application for a given file or URL.

In order for xdg-open and xdg-settings to detect and integrate with the Xfce desktop environment correctly, you need to [install](/index.php/Install "Install") the [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) package.

If you do not do that, your preferred applications preferences (set by exo-preferred-applications) will not be obeyed. Installing the package and allowing *xdg-open* to detect that you are running Xfce makes it forward all calls to *exo-open* instead, which correctly uses all your preferred applications preferences.

To make sure xdg-open integration is working correctly, ask *xdg-settings* for the default web browser and see what the result is:

```
# xdg-settings get default-web-browser

```

If it replies with:

```
xdg-settings: unknown desktop environment

```

it means that it has failed to detect Xfce as your desktop environment, which is likely due to a missing [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) package.

### Restaurar configurações padrão

If for any reason you need to revert back: to the default settings, rename `~/.config/xfce4-session/` and `~/.config/xfce4/`

```
$ mv ~/.config/xfce4-session/ ~/.config/xfce4-session-bak
$ mv ~/.config/xfce4/ ~/.config/xfce4-bak

```

Relogin for changes to take effect. If you get `Unable to load a failsafe session` upon login, see the [#Session failure](#Session_failure) section.

### Falha de sessão

Symptoms include:

*   The mouse is an X and/or does not appear at all;
*   Window decorations have disappeared and windows cannot be closed;
*   (`xfwm4-settings`) will not start, reporting `These settings cannot work with your current window manager (unknown)`;
*   Errors reported by a [display manager](/index.php/Display_manager "Display manager") such as `No window manager registered on screen 0`.
*   Unable to load a failsafe session:

```
Unable to load a failsafe session.
Unable to determine failsafe session name.  Possible causes: xfconfd isn't running (D-Bus setup problem); environment variable $XDG_CONFIG_DIRS is set incorrectly (must include "/etc"), or xfce4-session is installed incorrectly. 

```

Restarting Xfce or rebooting your system may solve the problem, but a corrupt session could also be the cause. Delete the session folder:

```
$ rm -r ~/.cache/sessions/

```

Also make sure that the relevant folders in `$HOME` are owned by the user starting `xfce4`. See [Chown](/index.php/Chown "Chown").

### Fontes no título da janela travando o xfce4-title

Install [ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid) and [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu). See also [FS#44382](https://bugs.archlinux.org/task/44382).

### Configurações de tampa do laptop ignoradas

You may find that the lid close settings in Xfce4 Power Manager are ignored, meaning that the laptop will always suspend on lid close, no matter what settings are chosen in the power manager. This is because the power manager is not set to handle lid close events by default. Instead, *systemd-logind* handles the lid close event. To change this behavior so that the power manager handles lid close events, execute the following command:

```
$ xfconf-query -c xfce4-power-manager -p /xfce4-power-manager/logind-handle-lid-switch -s false

```

**Note:** Under some circumstances, the `logind-handle-lid-switch` setting will get set to true when changes are made to the laptop lid actions or the lock on suspend setting. See [[5]](https://bugzilla.xfce.org/show_bug.cgi?id=12756#c2). In this case, you will need to toggle `logind-handle-lid-switch` to false again.

### O botão de ação de troca de usuário está acinzentada

The *Switch User* action button assumes that the *gdmflexiserver* executable (provided by [GDM](/index.php/GDM "GDM")) exists. Thus, if GDM is not being used then the button will be greyed out. See the [upstream bug report](https://bugzilla.xfce.org/show_bug.cgi?id=9307).

A possible workaround is to create an executable script called *gdmflexiserver* in `/usr/bin` or `/usr/local/bin` which calls the greeter switch command provided by the [display manager](/index.php/Display_manager "Display manager") which is being used.

*   For LXDM - [LXDM#Simultaneous users and switching users](/index.php/LXDM#Simultaneous_users_and_switching_users "LXDM").
*   For LightDM - [LightDM#User switching](/index.php/LightDM#User_switching "LightDM").

### Macros em .Xresources não funcionam

Xfce loads `$HOME/.Xresources` file using `xrdb`, but with `-nocpp` option to skip preprocessing. For macros to work properly, copy `/etc/xdg/xfce4/xinitrc` to `$HOME/.config/xfce4` directory and remove `-nocpp` option to `xrdb` from the resulting file. See [this thread](https://bbs.archlinux.org/profile.php?id=104121).

### Tema do cursor não muda ao iniciar a sessão

Ensure the systemwide XDG cursor is set to your desired cursor theme - see [temas de cursor#Especificação XDG](/index.php/Temas_de_cursor#Especificação_XDG "Temas de cursor").

## Veja também

*   [Xfce - Documentation](http://docs.xfce.org/)
*   [Xfce - Wiki](http://wiki.xfce.org)
*   [Xfce - About](http://www.xfce.org/about/)
*   [Xfce - Tour](https://xfce.org/about/tour)
*   [Wikipedia:Xfce](https://en.wikipedia.org/wiki/Xfce "wikipedia:Xfce")
*   [Xfce-Look](http://www.xfce-look.org/) - Themes, wallpapers, and more.
*   [Xfce Wikia](http://xfce.wikia.com/wiki/Main_Page)