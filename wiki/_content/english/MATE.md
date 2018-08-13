Related articles

*   [GNOME](/index.php/GNOME "GNOME")
*   [Cinnamon](/index.php/Cinnamon "Cinnamon")
*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Display manager](/index.php/Display_manager "Display manager")
*   [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications")

From [MATE homepage](https://mate-desktop.org/):

	*The MATE Desktop Environment is the continuation of GNOME 2\. It provides an intuitive and attractive desktop environment using traditional metaphors for Linux and other Unix-like operating systems. MATE is [under active development](https://github.com/mate-desktop) to add support for new technologies while preserving a traditional desktop experience.*

## Contents

*   [1 Installation](#Installation)
    *   [1.1 MATE applications](#MATE_applications)
    *   [1.2 Additional MATE packages](#Additional_MATE_packages)
    *   [1.3 MATE unstable](#MATE_unstable)
*   [2 Starting MATE](#Starting_MATE)
*   [3 Configuration](#Configuration)
    *   [3.1 Accessibility](#Accessibility)
    *   [3.2 Notifications](#Notifications)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Enabling compositing](#Enabling_compositing)
    *   [4.2 Enabling new window centering](#Enabling_new_window_centering)
    *   [4.3 Enabling window snapping](#Enabling_window_snapping)
    *   [4.4 Show or hide desktop icons](#Show_or_hide_desktop_icons)
        *   [4.4.1 Hide all desktop icons](#Hide_all_desktop_icons)
        *   [4.4.2 Hide individual icons](#Hide_individual_icons)
    *   [4.5 Use a different window manager](#Use_a_different_window_manager)
    *   [4.6 Prevent Caja from managing the desktop](#Prevent_Caja_from_managing_the_desktop)
    *   [4.7 Change window decoration button order](#Change_window_decoration_button_order)
    *   [4.8 Auto open file manager after drive mount](#Auto_open_file_manager_after_drive_mount)
    *   [4.9 Screensaver](#Screensaver)
    *   [4.10 Spatial view in Caja](#Spatial_view_in_Caja)
    *   [4.11 Change font DPI setting](#Change_font_DPI_setting)
    *   [4.12 Change applications menu icon](#Change_applications_menu_icon)
    *   [4.13 Panel speed settings](#Panel_speed_settings)
    *   [4.14 Set the terminal for caja-open-terminal](#Set_the_terminal_for_caja-open-terminal)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Toggling compositing](#Toggling_compositing)
    *   [5.2 Vertical sync for compositing](#Vertical_sync_for_compositing)
    *   [5.3 Consistent cursor theme](#Consistent_cursor_theme)
    *   [5.4 Use of gradient backgrounds with LightDM](#Use_of_gradient_backgrounds_with_LightDM)
    *   [5.5 Enabling panel shadow](#Enabling_panel_shadow)
    *   [5.6 Disabling scroll in taskbar](#Disabling_scroll_in_taskbar)
    *   [5.7 Logout/shutdown delayed by at-spi-registryd](#Logout.2Fshutdown_delayed_by_at-spi-registryd)
*   [6 See also](#See_also)

## Installation

MATE is available in the [official repositories](/index.php/Official_repositories "Official repositories") and can be [installed](/index.php/Installed "Installed") with one of the following:

*   The [mate](https://www.archlinux.org/groups/x86_64/mate/) group contains the core desktop environment required for the standard MATE experience.
*   The [mate-extra](https://www.archlinux.org/groups/x86_64/mate-extra/) group contains additional utilities and applications that integrate well with the MATE desktop. Installing just the [mate-extra](https://www.archlinux.org/groups/x86_64/mate-extra/) group will not pull in the whole [mate](https://www.archlinux.org/groups/x86_64/mate/) group via dependencies. If you want to install all MATE packages then you will need to explicitly install both groups.

The base desktop consists of [marco](https://www.archlinux.org/packages/?name=marco), [mate-panel](https://www.archlinux.org/packages/?name=mate-panel) and [mate-session-manager](https://www.archlinux.org/packages/?name=mate-session-manager).

### MATE applications

MATE is largely composed of GNOME 2 applications and utilities, forked and renamed to avoid conflicting with their GNOME 3 counterparts. Below is a list of common GNOME applications which have been renamed in MATE.

| Application | GNOME 2 | MATE |
| menu editor | Alacarte | [mozo](https://www.archlinux.org/packages/?name=mozo) |
| file manager | Nautilus | [caja](https://www.archlinux.org/packages/?name=caja) |
| window manager | Metacity | [marco](https://www.archlinux.org/packages/?name=marco) |
| text editor | Gedit | [pluma](https://www.archlinux.org/packages/?name=pluma) |
| image viewer | Eye of GNOME | Eye of MATE ([eom](https://www.archlinux.org/packages/?name=eom)) |
| document viewer | Evince | [atril](https://www.archlinux.org/packages/?name=atril) |
| archive manager | File Roller | [engrampa](https://www.archlinux.org/packages/?name=engrampa) |

Other applications and core components prefixed with GNOME (such as GNOME Terminal, GNOME Panel, GNOME Menus, etc.) have had the prefix changed to MATE so they become MATE Panel, MATE Menus etc.

### Additional MATE packages

There are a number of other unofficial MATE applications that are contributed to and maintained by the MATE community and therefore not included in the [mate](https://www.archlinux.org/groups/x86_64/mate/) or [mate-extra](https://www.archlinux.org/groups/x86_64/mate-extra/) groups.

*   **Dock Applet** — Application dock for the MATE panel.

	[https://github.com/robint99/dock-applet](https://github.com/robint99/dock-applet) || [mate-applet-dock](https://www.archlinux.org/packages/?name=mate-applet-dock)

*   **Online Radio Applet** — A MATE panel applet to let you play your favourite online radio station with a single click.

	[http://www.zavedil.com/online-radio-applet/](http://www.zavedil.com/online-radio-applet/) || [mate-applet-streamer](https://www.archlinux.org/packages/?name=mate-applet-streamer)

*   **MATE Menu** — Advanced menu for MATE Panel, a fork of MintMenu.

	[https://github.com/ubuntu-mate/mate-menu](https://github.com/ubuntu-mate/mate-menu) || [mate-menu](https://www.archlinux.org/packages/?name=mate-menu)

*   **MATE Tweak** — Tweak tool for MATE, a fork of mintDesktop.

	[https://github.com/ubuntu-mate/mate-tweak](https://github.com/ubuntu-mate/mate-tweak) || [mate-tweak](https://aur.archlinux.org/packages/mate-tweak/)

*   **BriskMenu** — Modern, efficient menu for the MATE Desktop Environment from SolusOS distribution.

	[https://github.com/solus-project/brisk-menu](https://github.com/solus-project/brisk-menu) || [brisk-menu](https://aur.archlinux.org/packages/brisk-menu/)

Additional packages need to be installed to take advantage of some of Caja's advanced features - see [File manager functionality](/index.php/File_manager_functionality "File manager functionality").

### MATE unstable

Consider the following community efforts, cf. [forum](https://bbs.archlinux.org/viewtopic.php?pid=1624557#p1624557):

*   [mate-desktop-dev](https://aur.archlinux.org/packages/mate-desktop-dev/) ([https://github.com/nicman23/arch_mate](https://github.com/nicman23/arch_mate))

## Starting MATE

Choose *MATE* from the menu in a [display manager](/index.php/Display_manager "Display manager") of choice.

Alternatively, to start MATE with *startx*, append `exec mate-session` to your `~/.xinitrc` file. See [xinitrc](/index.php/Xinitrc "Xinitrc") for details, such as preserving the logind session.

## Configuration

MATE can be configured with its *Control Center* application (*mate-control-center*) provided by the [mate-control-center](https://www.archlinux.org/packages/?name=mate-control-center) package. To manage some hardware, you may need to install additional tools.

	Audio

	[ALSA](/index.php/ALSA "ALSA") and [PulseAudio](/index.php/PulseAudio "PulseAudio") backends are supported by the [mate-media](https://www.archlinux.org/packages/?name=mate-media) package.

	Bluetooth

	For [Bluetooth](/index.php/Bluetooth "Bluetooth") device support, install the [blueman](https://www.archlinux.org/packages/?name=blueman) package. See [Blueman](/index.php/Blueman "Blueman").

	Networking

	For configuring the network, install the [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) package. See [NetworkManager](/index.php/NetworkManager "NetworkManager").

	Power

	UPower backend is supported by the [mate-power-manager](https://www.archlinux.org/packages/?name=mate-power-manager) package.

	Printers

	For configuring the printers, install the [system-config-printer](https://www.archlinux.org/packages/?name=system-config-printer) package.

### Accessibility

MATE is well suited for use by individuals with sight or mobility impairment. [Install](/index.php/Install "Install") [orca](https://www.archlinux.org/packages/?name=orca), [espeak](https://www.archlinux.org/packages/?name=espeak) (Screen reader for individuals who are blind or visually impaired) and [onboard](https://www.archlinux.org/packages/?name=onboard) (On-screen keyboard useful for mobility impaired users)

Before starting MATE for the first time, enter the following command as the user who needs accessibility features:

```
$ gsettings set org.mate.interface accessibility true

```

Once you start MATE, you can configure the accessibility applications via *System > Preferences > Assistive Technologies*, although if you need Orca, you will need to run it from the `Alt-F2` run window in order to start getting speech.

### Notifications

	Battery discharge

To disable the notification on battery discharge, run:

```
$ gsettings set org.mate.power-manager.notify-discharging false

```

	Brightness

See [Backlight#Kernel command-line options](/index.php/Backlight#Kernel_command-line_options "Backlight").

## Tips and tricks

### Enabling compositing

Compositing is not enabled by default. To enable it navigate to run *System > Preferences > Look and Feel > Windows > General* and click the tick box alongside *Enable software compositing window manager*. Alternatively, you can run the following from the terminal:

```
$ gsettings set org.mate.Marco.general compositing-manager true

```

### Enabling new window centering

By default, new windows are placed in the top-left corner. To center new windows on creation navigate to run *System > Preferences > Windows > Placement* and click the tick box alongside *Center new windows*. Alternatively, you can run the following from the terminal:

```
$ gsettings set org.mate.Marco.general center-new-windows true

```

### Enabling window snapping

Window snapping is not be enabled by default, to enable it navigate to run *System > Preferences > Windows > Placement* and click the tick box alongside *Enable side by side tiling*. Alternatively, you can run the following from the terminal:

```
$ gsettings set org.mate.Marco.general allow-tiling true

```

### Show or hide desktop icons

By default, MATE shows multiple icons on the desktop: the content of your desktop directory, computer, home and network directories, the trash and mounted drives. You can show or hide them individually or all at once using `gsettings`.

#### Hide all desktop icons

```
$ gsettings set org.mate.background show-desktop-icons false

```

#### Hide individual icons

Hide computer icon:

```
$ gsettings set org.mate.caja.desktop computer-icon-visible false

```

Hide user directory icon:

```
$ gsettings set org.mate.caja.desktop home-icon-visible false

```

Hide network icon:

```
$ gsettings set org.mate.caja.desktop network-icon-visible false

```

Hide trash icon:

```
$ gsettings set org.mate.caja.desktop trash-icon-visible false

```

Hide mounted volumes:

```
$ gsettings set org.mate.caja.desktop volumes-visible false

```

Replace `false` with `true` for the icons to reappear.

### Use a different window manager

The *marco* window manager can be replaced with another window manager via either of the following methods:

	Using gsettings (recommended)

Execute the following to specify a different window manager for MATE:

```
$ gsettings set org.mate.session.required-components windowmanager *wm-name*

```

	Using MATE session autostart

You can autostart a window manager of your choice using *mate-session-properties*. This means that the autostarted window manager will replace the default window manager at login. Navigate to *System* -> *Preferences* -> *Startup Applications*. In the dialog click *Add.* The command should take the syntax `*wm-name* --replace`.

### Prevent Caja from managing the desktop

To prevent Caja from managing the desktop, execute the following:

```
$ gsettings set org.mate.background show-desktop-icons false
$ killall caja  # Caja will be restarted by session manager

```

### Change window decoration button order

You can change the button order using the graphical dconf-editor or the gsettings command line tool:

```
$ gsettings set org.mate.Marco.general button-layout 'close,maximize,minimize:'

```

and put **menu**, **close**, **minimize** and **maximize** in your desired order, separated by commas. The colon is used to specify on which side of the titlebar the window buttons will appear and must be used for the changes to apply.

### Auto open file manager after drive mount

By default, MATE automatically opens a new file manager window when a drive is mounted. To disable this:

```
$ gsettings set org.mate.media-handling automount-open false

```

And to disable automounting:

```
$ gsettings set org.mate.media-handling automount false

```

### Screensaver

MATE uses [mate-screensaver](https://www.archlinux.org/packages/?name=mate-screensaver) to lock your session. By default there are a limited number of screensavers available. To make more screensavers available, install the [mate-screensaver-hacks](https://aur.archlinux.org/packages/mate-screensaver-hacks/) package. This will allow you to use [XScreenSaver](/index.php/XScreenSaver "XScreenSaver") screensavers with [mate-screensaver](https://www.archlinux.org/packages/?name=mate-screensaver).

### Spatial view in Caja

To ensure that each new folder opens in a new window (known as spatial view), open Caja's preferences dialog, click on the behaviour tab and tick the 'Open each folder in its own window' option. Alternatively, execute the following command which achieves the same effect:

```
$ gsettings set org.mate.caja.preferences always-use-browser false

```

### Change font DPI setting

You can alter the DPI (dots per inch) of the fonts in MATE by right-clicking on the desktop and choosing *Change desktop background > Fonts > Details > Resolution*.

### Change applications menu icon

By default, the applications menu icon is set to `start-here`. To use a different icon, copy your icon to a folder such as `/usr/local/share/pixmaps` and execute the following:

```
$ gsettings set org.mate.panel.menubar icon-name *icon*

```

where *icon* is the name of your icon. Do not include the file extension in the icon name. Finally, restart MATE Panel.

### Panel speed settings

	Hide/Unhide delay

To adjust the amount of time it takes for the panel to disappear or reappear when autohide is enabled, execute the following:

```
$ dconf write /org/mate/panel/toplevels/*panel*/(un)hide-delay *time*

```

where *panel* is either *top* or *bottom* and *time* is a value in miliseconds, e.g. 300.

	Animation speed

To set the speed at which panel animations occur, execute the following:

```
$ dconf write /org/mate/panel/toplevels/*panel*/animation-speed *value*

```

where *panel* is either *top* or *bottom* and *value* is either `"'fast'"`, `"'medium'"` or `"'slow'"`.

### Set the terminal for caja-open-terminal

The `caja-open-terminal` extension uses GSettings to determine which terminal to use - *mate-terminal* is the default. To change the terminal that will be used, run the following command

```
$ gsettings set org.mate.applications-terminal exec *my-terminal*

```

where *my-terminal* is the name of the terminal executable to be launched, for example: *xterm*.

## Troubleshooting

### Toggling compositing

Some software may have issues rendering graphics when working on an environment using the nvidia proprietary drivers and a compositing window manager.

To easily toggle the compositing feature, save the following script somewhere within the Home directory, e.g. `~/.scripts/compositing.sh`:

```
#!/bin/bash
if [ "$(gsettings get org.mate.Marco.general compositing-manager)" = "true" ]
then
  gsettings set org.mate.Marco.general compositing-manager false
else
  gsettings set org.mate.Marco.general compositing-manager true
fi

```

and then create a custom keyboard shortcut that executes the file, e.g. `Ctrl+Alt+C`, to `sh ~/.scripts/compositing.sh`.

### Vertical sync for compositing

Mate's window manager, *marco*, supports tear-free software compositing via DRI3/Xpresent. [[1]](https://github.com/mate-desktop/marco/issues/326)

If your graphics driver does not support DRI3 (e.g. the Nvidia Proprietary driver), *marco* does not support vertical synchronization via *OpenGL*, which may cause video tearing with enabled compositing. [[2]](https://github.com/mate-desktop/marco/issues/91) In this case, consider a different [composite manager](/index.php/Composite_manager "Composite manager") with OpenGL support such as [Compton](/index.php/Compton "Compton").

### Consistent cursor theme

See [Cursor themes#Desktop environments](/index.php/Cursor_themes#Desktop_environments "Cursor themes").

### Use of gradient backgrounds with LightDM

If you wish to use the default MATE (1.8) *Stripes* background as the LightDM background as well so as to make for seamless transition from LightDM to MATE, you will find that it is runtime-constructed from a grayscale PNG upon which MATE layers a vertical blue-to-green gradient, something which LightDM does not currently support. If insistent, you can work around this by temporarily setting `/org/mate/desktop/background/show-desktop-icons` to `false`, either through the `dconf-editor` tool available from the `System Tools` menu or by running

```
$ gsettings set org.mate.background show-desktop-icons false

```

from the Alt-F2 `Run Application` dialog, then running `killall mate-panel` from said dialog and hitting `Print Screen` before the panel reappears. You are then presented with a `Save As` dialog for exactly that fully rendered, screen-sized PNG that you need for LightDM. Run

```
$ gsettings set org.mate.background show-desktop-icons true

```

to have your desktop icons reappear, if desired.

### Enabling panel shadow

Due to a race condition, the panel shadow does not appear after logging in to the MATE desktop, even with compositing enabled. [[3]](https://github.com/mate-desktop/mate-panel/issues/193)

Copy `/usr/share/applications/marco.desktop` and add a delay:

 `~/.local/share/applications/marco.desktop` 
```
X-MATE-Autostart-Phase=**Applications**
**X-MATE-Autostart-Delay=2**
X-MATE-Provides=windowmanager
X-MATE-Autostart-Notify=true
```

**Note:** Delays are only allowed in the applications phase, hence `X-MATE-Autostart-Phase` must be set to `Applications`.

If this has no effect, increase the delay duration.

### Disabling scroll in taskbar

A feature of the MATE panel window list is that windows can be scrolled through using the mouse or touchpad. This feature may be troublesome for some as there is potential for accidental, unintended scrolling through windows.

Whilst there is no way of disabling this feature through MATE's settings, this feature can be disabled by patching [libwnck3](https://www.archlinux.org/packages/?name=libwnck3) using the [Arch Build System](/index.php/Arch_Build_System "Arch Build System"); in this case, rebuild libwnck3 with the following [patch](https://pastebin.com/raw/q66p3dtj). For more information on rebuilding packages with patches applied, see [Patching in ABS#Applying patches](/index.php/Patching_in_ABS#Applying_patches "Patching in ABS").

### Logout/shutdown delayed by at-spi-registryd

When logging out or shutting down, you may find that you are presented with an *A program is still running: at-spi-registryd.desktop* popup. As a workaround, you can prevent *at-spi-registryd* from starting - see [GTK+#Suppress warning about accessibility bus](/index.php/GTK%2B#Suppress_warning_about_accessibility_bus "GTK+") - though this may have an effect on some accessibility features.

## See also

*   [MATE homepage](https://mate-desktop.org)
*   [MATE wiki for Arch Linux](https://wiki.mate-desktop.org/archlinux_custom_repo)
*   [*MATE desktop screenshots*](https://mate-desktop.org/gallery/1.8/)
*   [*The MATE Desktop Environment*](https://bbs.archlinux.org/viewtopic.php?pid=1018647) - Arch Linux forum discussion about MATE