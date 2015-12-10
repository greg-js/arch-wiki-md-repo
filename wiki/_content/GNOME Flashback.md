# GNOME Flashback

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [GNOME](/index.php/GNOME "GNOME")
*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Window manager](/index.php/Window_manager "Window manager")

[GNOME Flashback](https://wiki.gnome.org/Projects/GnomeFlashback) (previously called _GNOME fallback mode_) is a shell for GNOME 3\. The desktop layout and the underlying technology is similar to GNOME 2\. It doesn't use 3D acceleration at all, so it's generally faster and less CPU intensive than GNOME Shell with llvmpipe.

## Contents

*   [1 Installation](#Installation)
*   [2 Starting](#Starting)
    *   [2.1 Graphical log-in](#Graphical_log-in)
    *   [2.2 Manually](#Manually)
*   [3 Configuration](#Configuration)
    *   [3.1 Customizing GNOME Panel](#Customizing_GNOME_Panel)
    *   [3.2 Alternative window manager](#Alternative_window_manager)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Panel speed settings](#Panel_speed_settings)
    *   [4.2 Replace applications menu icon](#Replace_applications_menu_icon)
*   [5 See also](#See_also)

## Installation

GNOME Flashback can be [installed](/index.php/Installed "Installed") from the [gnome-flashback](https://www.archlinux.org/packages/?name=gnome-flashback) package. It's recommended to install its optional dependencies also to get a more complete desktop environment.

You can also install the following packages which provide some additional applets for the GNOME Panel:

*   **GNOME Applets** — Small applications for the GNOME panel

[https://wiki.gnome.org/Projects/GnomeApplets](https://wiki.gnome.org/Projects/GnomeApplets) || [gnome-applets](https://www.archlinux.org/packages/?name=gnome-applets)

*   **Byzanz Applet** — Record what's happening on your desktop

[https://git.gnome.org/browse/byzanz/](https://git.gnome.org/browse/byzanz/) || [byzanz](https://aur.archlinux.org/packages/byzanz/)<sup><small>AUR</small></sup>

*   **Command Runner Applet** — Applet for GNOME Flashback panel which periodically displays a command output

[https://github.com/porridge/command-runner-applet](https://github.com/porridge/command-runner-applet) || [command-runner-applet](https://aur.archlinux.org/packages/command-runner-applet/)<sup><small>AUR</small></sup>

*   **Pomodoro Applet** — GNOME Panel applet for timing the intervals used in the Pomodoro Techinique(tm)

[https://github.com/stump/pomodoro-applet](https://github.com/stump/pomodoro-applet) || [pomodoro-applet](https://aur.archlinux.org/packages/pomodoro-applet/)<sup><small>AUR</small></sup>

*   **Sensors Applet** — Applet for GNOME Flashback panel to display readings from hardware sensors, including CPU temperature, fan speeds and voltage readings

[http://sensors-applet.sourceforge.net/](http://sensors-applet.sourceforge.net/) || [sensors-applet](https://www.archlinux.org/packages/?name=sensors-applet)

It's recommended to install the [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group, which contains applications required for the standard GNOME experience.

## Starting

### Graphical log-in

Choose _GNOME Flashback (Metacity)_ from the menu in a [display manager](/index.php/Display_manager "Display manager") of choice.

Those who wish to use [Compiz](/index.php/Compiz "Compiz") with GNOME Flashback should select _GNOME Flashback (Compiz)_ instead.

### Manually

*   For the **GNOME Flashback (Metacity)** session, add the following to the `~/.xinitrc` file:

    ```
    export XDG_CURRENT_DESKTOP=GNOME-Flashback:GNOME
    exec gnome-session --session=gnome-flashback-metacity
    ```

*   For the **GNOME Flashback (Compiz)** session, add the following to the `~/.xinitrc` file:

    ```
    export XDG_CURRENT_DESKTOP=GNOME-Flashback:GNOME
    exec gnome-session --session=gnome-flashback-compiz
    ```

After editing `.xinitrc`, GNOME Flashback can be launched with _startx_. See [xinitrc](/index.php/Xinitrc "Xinitrc") for details.

## Configuration

GNOME Flashback shares most of its settings with GNOME. See [GNOME#Configuration](/index.php/GNOME#Configuration "GNOME") for more details.

### Customizing GNOME Panel

*   To configure the panel, hold down the `Alt` key, and right-click on it in an empty area.
*   To move an applet on the panel, hold down the `Alt` key, and grab it with middle-button.

**Note:** If the Alt+right-click combination does not work, try Super+Alt+right-click instead.

### Alternative window manager

You can use an alternative [window manager](/index.php/Window_manager "Window manager") with GNOME Flashback by creating a custom GNOME session with the following components:

```
`RequiredComponents=gnome-flashback-init;gnome-flashback;gnome-panel;**window-manager**;gnome-settings-daemon;nautilus-classic;`

```

where **window-manager** is the window manager you wish to use. See [GNOME#Custom GNOME sessions](/index.php/GNOME#Custom_GNOME_sessions "GNOME").

Also see [this article](http://makandra.com/notes/1367-running-the-awesome-window-manager-within-gnome) on running awesome as the window manager in GNOME.

## Tips and tricks

### Panel speed settings

Hide/Unhide delay

To adjust the amount of time it takes for the panel to disappear or reappear when autohide is enabled, execute the following:

```
$ gsettings set org.gnome.gnome-panel.toplevel:/org/gnome/gnome-panel/layout/toplevels/_panel_/ hide-delay _time_
$ gsettings set org.gnome.gnome-panel.toplevel:/org/gnome/gnome-panel/layout/toplevels/_panel_/ unhide-delay _time_

```

where _panel_ is either _top-panel_ or _bottom-panel_ and _time_ is a value in miliseconds, e.g. 300.

Animation speed

To set the speed at which panel animations occur, execute the following:

```
$ gsettings set org.gnome.gnome-panel.toplevel:/org/gnome/gnome-panel/layout/toplevels/_panel_/ animation-speed _value_

```

where _panel_ is either _top-panel_ or _bottom-panel_ and _value_ is either `"'fast'"`, `"'medium'"` or `"'slow'"`.

### Replace applications menu icon

**Note:** This change will be overwritten on updating your icon theme package.

Replace `/usr/share/icons/_icon-theme_/16x16/places/start-here.png` with your own icon (where _icon-theme_ is the name of your icon theme).

After making the change, restart GNOME Panel: `gnome-panel --replace`.

## See also

*   [GnomeFlashback - GNOME Wiki](https://wiki.gnome.org/Projects/GnomeFlashback)

Retrieved from "[https://wiki.archlinux.org/index.php?title=GNOME_Flashback&oldid=409323](https://wiki.archlinux.org/index.php?title=GNOME_Flashback&oldid=409323)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [GNOME](/index.php/Category:GNOME "Category:GNOME")