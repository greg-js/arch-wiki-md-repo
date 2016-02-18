From [MATE homepage](http://mate-desktop.org/):

	*The MATE Desktop Environment is the continuation of GNOME 2\. It provides an intuitive and attractive desktop environment using traditional metaphors for Linux and other Unix-like operating systems. MATE is [under active development](https://github.com/mate-desktop) to add support for new technologies while preserving a traditional desktop experience.*

## Contents

*   [1 MATE applications](#MATE_applications)
*   [2 Installation](#Installation)
    *   [2.1 Additional MATE packages](#Additional_MATE_packages)
    *   [2.2 GTK+ 3 version](#GTK.2B_3_version)
*   [3 Starting MATE](#Starting_MATE)
*   [4 Configuration](#Configuration)
    *   [4.1 Accessibility](#Accessibility)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Enabling compositing](#Enabling_compositing)
    *   [5.2 Enabling new window centering](#Enabling_new_window_centering)
    *   [5.3 Enabling window snapping](#Enabling_window_snapping)
    *   [5.4 Show or hide desktop icons](#Show_or_hide_desktop_icons)
        *   [5.4.1 Hide all desktop icons](#Hide_all_desktop_icons)
        *   [5.4.2 Hide individual icons](#Hide_individual_icons)
    *   [5.5 Use a different window manager with MATE](#Use_a_different_window_manager_with_MATE)
    *   [5.6 Prevent Caja from managing the desktop](#Prevent_Caja_from_managing_the_desktop)
    *   [5.7 Change window decoration button order](#Change_window_decoration_button_order)
    *   [5.8 Auto open file manager after drive mount](#Auto_open_file_manager_after_drive_mount)
    *   [5.9 Screensaver](#Screensaver)
    *   [5.10 Lock screen and default background image](#Lock_screen_and_default_background_image)
    *   [5.11 Spatial view in Caja](#Spatial_view_in_Caja)
    *   [5.12 Change font DPI setting](#Change_font_DPI_setting)
    *   [5.13 Change applications menu icon](#Change_applications_menu_icon)
    *   [5.14 Panel speed settings](#Panel_speed_settings)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Toggling compositing](#Toggling_compositing)
    *   [6.2 Vertical sync for compositing](#Vertical_sync_for_compositing)
    *   [6.3 Consistent cursor theme](#Consistent_cursor_theme)
    *   [6.4 Use of gradient backgrounds with LightDM](#Use_of_gradient_backgrounds_with_LightDM)
    *   [6.5 Enabling panel shadow](#Enabling_panel_shadow)
    *   [6.6 Disabling scroll in taskbar](#Disabling_scroll_in_taskbar)
*   [7 See also](#See_also)

## MATE applications

MATE is largely composed of GNOME 2 applications and utilities, forked and renamed to avoid conflicting with their GNOME 3 counterparts. Below is a list of common GNOME applications which have been renamed in MATE.

| Application | GNOME 2 | MATE |
| menu editor | Alacarte | Mozo |
| file manager | Nautilus | Caja |
| window manager | Metacity | Marco |
| text editor | Gedit | Pluma |
| image viewer | Eye of GNOME | Eye of MATE |
| document viewer | Evince | Atril |
| archive manager | File Roller | Engrampa |

Other applications and core components prefixed with GNOME (such as GNOME Terminal, GNOME Panel, GNOME Menus, etc.) have had the prefix changed to MATE so they become MATE Panel, MATE Menus etc.

## Installation

MATE is available in the [official repositories](/index.php/Official_repositories "Official repositories") and can be [installed](/index.php/Installed "Installed") with one of the following:

*   The [mate](https://www.archlinux.org/groups/x86_64/mate/) group contains the core desktop environment required for the standard MATE experience.
*   The [mate-extra](https://www.archlinux.org/groups/x86_64/mate-extra/) group contains additional utilities and applications that integrate well with the MATE desktop. Installing just the [mate-extra](https://www.archlinux.org/groups/x86_64/mate-extra/) group will not pull in the whole [mate](https://www.archlinux.org/groups/x86_64/mate/) group via dependencies. If you want to install all MATE packages then you will need to explicitly install both groups.

The base desktop consists of [marco](https://www.archlinux.org/packages/?name=marco), [mate-panel](https://www.archlinux.org/packages/?name=mate-panel) and [mate-session-manager](https://www.archlinux.org/packages/?name=mate-session-manager),

### Additional MATE packages

There are additional official packages not included in the [mate](https://www.archlinux.org/groups/x86_64/mate/) or [mate-extra](https://www.archlinux.org/groups/x86_64/mate-extra/) groups because they are not necessarily useful to everyone.

*   **GNOME Main Menu** — A MATE panel applet similar to the traditional main-menu, but with a few additions.

	[http://mate-desktop.org](http://mate-desktop.org) || [gnome-main-menu](https://www.archlinux.org/packages/?name=gnome-main-menu)

*   **MATE Netbook** — This applet will automatically maximize all windows and provides an application switcher applet.

	[http://mate-desktop.org](http://mate-desktop.org) || [mate-netbook](https://www.archlinux.org/packages/?name=mate-netbook)

There are also a number of other unofficial MATE applications that are contributed to and maintained by the MATE community and therefore not included in the [mate](https://www.archlinux.org/groups/x86_64/mate/) or [mate-extra](https://www.archlinux.org/groups/x86_64/mate-extra/) groups.

*   **MATE AccountsDialog** — An application to view and modify user accounts information for MATE.

	[https://github.com/NiceandGently/mate-accountsdialog](https://github.com/NiceandGently/mate-accountsdialog) || [mate-accountsdialog](https://www.archlinux.org/packages/?name=mate-accountsdialog)

*   **Lock Keys Applet** — A MATE panel applet that shows which of the CapsLock, NumLock and ScrollLock keys are on and which are off.

	[http://www.zavedil.com/mate-lock-keys-applet/](http://www.zavedil.com/mate-lock-keys-applet/) || [mate-applet-lockkeys](https://www.archlinux.org/packages/?name=mate-applet-lockkeys)

*   **Online Radio Applet** — A MATE panel applet to let you play your favourite online radio station with a single click.

	[http://www.zavedil.com/online-radio-applet/](http://www.zavedil.com/online-radio-applet/) || [mate-applet-streamer](https://www.archlinux.org/packages/?name=mate-applet-streamer)

*   **MATE Color Manager** — Color management application for MATE.

	[https://github.com/NiceandGently/mate-color-manager](https://github.com/NiceandGently/mate-color-manager) || [mate-color-manager](https://www.archlinux.org/packages/?name=mate-color-manager)

*   **MATE Disk Utility** — Disk management application for MATE.

	[https://github.com/NiceandGently/mate-disk-utility](https://github.com/NiceandGently/mate-disk-utility) || [mate-disk-utility](https://www.archlinux.org/packages/?name=mate-disk-utility)

*   **MATE Screensaver Hacks** — Enable screensavers from xscreensaver for MATE.

	[http://www.jwz.org/xscreensaver/](http://www.jwz.org/xscreensaver/) || [mate-screensaver-hacks](https://www.archlinux.org/packages/?name=mate-screensaver-hacks)

*   **Variety** — Variety changes the wallpaper on a regular interval using user-specified or automatically downloaded images.

	[http://peterlevi.com/variety/](http://peterlevi.com/variety/) || [variety](https://www.archlinux.org/packages/?name=variety)

The followings are also available via the AUR and integrate with MATE but the packages are not maintained by the MATE team.

*   **MATE Menu** — Advanced menu for MATE Panel, a fork of MintMenu.

	[https://bitbucket.org/ubuntu-mate/mate-menu](https://bitbucket.org/ubuntu-mate/mate-menu) || [mate-menu](https://aur.archlinux.org/packages/mate-menu/)

*   **MATE Tweak** — Tweak tool for MATE, a fork of mintDesktop.

	[https://bitbucket.org/ubuntu-mate/mate-tweak](https://bitbucket.org/ubuntu-mate/mate-tweak) || [mate-tweak](https://aur.archlinux.org/packages/mate-tweak/)

Additional packages need to be installed to take advantage of some of Caja's advanced features - see [File manager functionality](/index.php/File_manager_functionality "File manager functionality").

### GTK+ 3 version

An experimental GTK+ 3 build of MATE can be installed with [mate-gtk3](https://www.archlinux.org/groups/x86_64/mate-gtk3/) and [mate-extra-gtk3](https://www.archlinux.org/groups/x86_64/mate-extra-gtk3/) groups. While it works mostly, there are some known issues with [caja](https://github.com/mate-desktop/caja/milestones/Gtk+3), [eom](https://github.com/mate-desktop/eom/milestones/Gtk+3), [marco](https://github.com/mate-desktop/marco/milestones/Gtk+3), [mate-applets](https://github.com/mate-desktop/mate-applets/milestones/Gtk+3), [mate-control-center](https://github.com/mate-desktop/mate-control-center/milestones/Gtk+3), [mate-netbook](https://github.com/mate-desktop/mate-netbook/milestones/Gtk+3), [mate-notification-daemon](https://github.com/mate-desktop/mate-notification-daemon/milestones/Gtk+3), [mate-panel](https://github.com/mate-desktop/mate-panel/milestones/Gtk+3) and [pluma](https://github.com/mate-desktop/pluma/milestones/Gtk+3).

## Starting MATE

Choose *MATE* from the menu in a [display manager](/index.php/Display_manager "Display manager") of choice. The MATE team recommends [LightDM](/index.php/LightDM "LightDM") as the display manager.

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
gsettings set org.mate.interface accessibility true

```

Once you start MATE, you can configure the accessibility applications via *System > Preferences > Assistive Technologies*, although if you need Orca, you will need to run it from the `Alt-F2` run window in order to start getting speech.

## Tips and tricks

### Enabling compositing

Compositing is not enabled by default. To enable it navigate to run `System -> Preferences -> Windows` and click the tick box alongside **Enable software compositing window manager** in the `General` tab. Alternatively, you can run the following from the terminal:

```
$ dconf write /org/mate/marco/general/compositing-manager true

```

### Enabling new window centering

By default, new windows are placed in the top-left corner. To center new windows on creation navigate to run `System -> Preferences -> Windows` and click the tick box alongside **Center new windows** in the `Placement` tab. Alternatively, you can run the following from the terminal:

```
$ dconf write /org/mate/marco/general/center-new-windows true

```

### Enabling window snapping

Window snapping is not be enabled by default, to enable it navigate to run `System -> Preferences -> Windows` and click the tick box alongside **Enable side by side tiling** in the `Placement` tab. Alternatively, you can run the following from the terminal:

```
$ dconf write /org/mate/marco/general/side-by-side-tiling true 

```

### Show or hide desktop icons

By default, MATE shows multiple icons on the desktop: The content of your desktop directory, computer, home and network directories, the trash and mounted drives. You can show or hide them individually or all at once using `dconf`.

#### Hide all desktop icons

```
$ dconf write /org/mate/desktop/background/show-desktop-icons false

```

#### Hide individual icons

Hide computer icon:

```
$ dconf write /org/mate/caja/desktop/computer-icon-visible false

```

Hide user directory icon:

```
$ dconf write /org/mate/caja/desktop/home-icon-visible false

```

Hide network icon:

```
$ dconf write /org/mate/caja/desktop/network-icon-visible false

```

Hide trash icon:

```
$ dconf write /org/mate/caja/desktop/trash-icon-visible false

```

Hide mounted volumes:

```
$ dconf write /org/mate/caja/desktop/volumes-visible false

```

Replace `false` with `true` for the icons to reappear.

### Use a different window manager with MATE

The *marco* window manager can be replaced with another window manager via either of the following methods:

	Using DConf (recommended)

Execute the following to specify a different window manager for MATE:

```
$ dconf write /org/mate/desktop/session/required-components/windowmanager *wm-name*

```

	Using MATE session autostart

You can autostart a window manager of your choice using *mate-session-properties*. This means that the autostarted window manager will replace the default window manager at login. Navigate to *System* -> *Preferences* -> *Startup Applications*. In the dialog click *Add.* The command should take the syntax `*wm-name* --replace`.

### Prevent Caja from managing the desktop

To prevent Caja from managing the desktop, execute the following:

```
$ gsettings set org.mate.background show-desktop-icons false
$ killall caja # caja will be restarted by session manager

```

### Change window decoration button order

You can change the button using dconf. The key is in org.mate.marco.general.button-layout. Use the graphical dconf-editor or the dconf command line tool to change it:

```
$ dconf write /org/mate/marco/general/button-layout "'close,maximize,minimize:'"

```

and put **menu**, **close**, **minimize** and **maximize** in your desired order, separated by commas. The colon is used to specify on which side of the titlebar the window buttons will appear and must be used for the changes to apply.

### Auto open file manager after drive mount

By default, MATE automatically opens a new file manager window when a drive is mounted. To disable this, change the following key in dconf:

```
$ dconf write /org/mate/desktop/media-handling/automount-open false

```

### Screensaver

MATE uses [mate-screensaver](https://www.archlinux.org/packages/?name=mate-screensaver) to lock your session. By default there are a limited number of screensavers available. To make more screensavers available, install the [mate-screensaver-hacks](https://www.archlinux.org/packages/?name=mate-screensaver-hacks) package. This will allow you to use [XScreenSaver](/index.php/XScreenSaver "XScreenSaver") screensavers with [mate-screensaver](https://www.archlinux.org/packages/?name=mate-screensaver).

### Lock screen and default background image

The full list of configuration options can be found in `/usr/share/glib-2.0/schemas/org.mate.background.gschema.xml`, they are overridden by creating the file `/usr/share/glib-2.0/schemas/mate-background.gschema.override`.

**Note:** The values on the right must be enclosed in single quotes ('') otherwise an error will occur during re-compile.

Example #1: Change the background image of the lock screen:

 `/usr/share/glib-2.0/schemas/mate-background.gschema.override` 
```
[org.mate.background]
picture-filename='/path/to/the/background.jpg'
```

Example #2: Change the lock screen to use a gradient:

 `/usr/share/glib-2.0/schemas/mate-background.gschema.override` 
```
[org.mate.background]
color-shading-type='vertical-gradient'
picture-options='scaled'
picture-filename=''
primary-color='#152233'
secondary-color='#000000'
```

Re-compile the schemas:

```
# glib-compile-schemas /usr/share/glib-2.0/schemas/

```

Finally, restart your X session for the change to effect.

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

## Troubleshooting

### Toggling compositing

Some software may have issues rendering graphics when working on an environment using the nvidia proprietary drivers and a compositing window manager.

To easily toggle the compositing feature, save the following script somewhere within the Home directory, e.g. `~/.scripts/compositing.sh`:

```
#!/bin/bash
if $(dconf read /org/mate/marco/general/compositing-manager) == "true"
then
  dconf write /org/mate/marco/general/compositing-manager false
else
  dconf write /org/mate/marco/general/compositing-manager true
fi

```

and then create a custom keyboard shortcut that executes the file, e.g. `Ctrl+Alt+C`, to `sh ~/.scripts/compositing.sh`.

### Vertical sync for compositing

*marco* does not support vertical synchronization via *OpenGL*, which may cause video tearing with enabled compositing. [[1]](https://github.com/mate-desktop/marco/issues/91) Consider a different [composite manager](/index.php/Composite_manager "Composite manager") with OpenGL support such as [Compton](/index.php/Compton "Compton").

### Consistent cursor theme

See [Cursor themes#Desktop environments](/index.php/Cursor_themes#Desktop_environments "Cursor themes").

### Use of gradient backgrounds with LightDM

If you wish to use the default MATE (1.8) *Stripes* background as the LightDM background as well so as to make for seamless transition from LightDM to MATE, you will find that it is runtime-constructed from a grayscale PNG upon which MATE layers a vertical blue-to-green gradient, something which LightDM does not currently support. If insistent, you can work around this by temporarily setting `/org/mate/desktop/background/show-desktop-icons` to `false`, either through the `dconf Editor` tool available from the `System Tools` menu or by running

```
dconf write /org/mate/desktop/background/show-desktop-icons false

```

from the Alt-F2 `Run Application` dialog, then running `killall mate-panel` from said dialog and hitting `Print Screen` before the panel reappears. You are then presented with a `Save As` dialog for exactly that fully rendered, screen-sized PNG that you need for LightDM. Run

```
dconf reset /org/mate/desktop/background/show-desktop-icons

```

to have your desktop icons reappear.

### Enabling panel shadow

Due to a race condition, the panel shadow does not appear after logging in to the MATE desktop, even with compositing enabled. [[2]](https://github.com/mate-desktop/mate-panel/issues/193)

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

Whilst there is no way of disabling this feature through MATE's settings, this feature can be disabled by patching [libwnck](https://www.archlinux.org/packages/?name=libwnck) using the [Arch Build System](/index.php/Arch_Build_System "Arch Build System"); in this case, rebuild libwnck with the following [patch](http://pastebin.com/raw.php?i=Bj0AnH1c). For more information on rebuilding packages with patches applied, see [Patching in ABS#Applying patches](/index.php/Patching_in_ABS#Applying_patches "Patching in ABS").

## See also

*   [MATE homepage](http://mate-desktop.org)
*   [MATE wiki for Arch Linux](http://wiki.mate-desktop.org/archlinux_custom_repo)
*   [*MATE desktop screenshots*](http://mate-desktop.org/gallery/1.8/)
*   [*The MATE Desktop Environment*](https://bbs.archlinux.org/viewtopic.php?pid=1018647) - Arch Linux forum discussion about MATE