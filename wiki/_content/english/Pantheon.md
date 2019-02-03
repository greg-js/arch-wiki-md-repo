[Pantheon](https://bbs.archlinux.org/viewtopic.php?id=152930) is the desktop environment originally created for the [elementary OS](http://elementary.io/) distribution. It is written from scratch in [Vala](https://en.wikipedia.org/wiki/Vala_(programming_language) "wikipedia:Vala (programming language)"), using [GTK3](/index.php/GTK%2B "GTK+") and [Granite](https://github.com/elementary/granite). With regards to usability and appearance, the desktop has some similarities with [GNOME Shell](/index.php/GNOME_Shell "GNOME Shell") and [macOS](https://en.wikipedia.org/wiki/MacOS "wikipedia:MacOS").

## Contents

*   [1 Project Status](#Project_Status)
*   [2 Installation](#Installation)
    *   [2.1 Packages](#Packages)
        *   [2.1.1 Unofficial repository](#Unofficial_repository)
        *   [2.1.2 AUR](#AUR)
    *   [2.2 Desktop Environment](#Desktop_Environment)
    *   [2.3 Services and Configuration](#Services_and_Configuration)
    *   [2.4 Theme](#Theme)
    *   [2.5 Applications](#Applications)
*   [3 Launching Pantheon](#Launching_Pantheon)
    *   [3.1 Via Display manager](#Via_Display_manager)
        *   [3.1.1 Autostart applications with a display manager](#Autostart_applications_with_a_display_manager)
    *   [3.2 Via xinit](#Via_xinit)
        *   [3.2.1 Autostart applications with *xinit*](#Autostart_applications_with_xinit)
*   [4 Configuration](#Configuration)
    *   [4.1 Wingpanel](#Wingpanel)
        *   [4.1.1 Third-party indicators](#Third-party_indicators)
        *   [4.1.2 Indicator-session menus unresponsive](#Indicator-session_menus_unresponsive)
    *   [4.2 Plank](#Plank)
        *   [4.2.1 Adding new application icons](#Adding_new_application_icons)
    *   [4.3 Pantheon Files](#Pantheon_Files)
        *   [4.3.1 Enable context menu entries](#Enable_context_menu_entries)
    *   [4.4 Terminal](#Terminal)
        *   [4.4.1 Opacity](#Opacity)
*   [5 Known Issues](#Known_Issues)
    *   [5.1 Appearance](#Appearance)
        *   [5.1.1 Pantheon-terminal transparency](#Pantheon-terminal_transparency)
        *   [5.1.2 Wingpanel transparency](#Wingpanel_transparency)

## Project Status

Although the [elementary OS](https://elementary.io/) release schedule and toolchain are bound to [Ubuntu's](/index.php/Arch_compared_to_other_distributions#Ubuntu "Arch compared to other distributions") LTS release cycle, [development](https://plus.google.com/communities/104613975513761463450) moves quickly and has recently moved to [github](https://github.com/elementary).

## Installation

### Packages

#### Unofficial repository

Alucryd's unofficial repository contains more and more [up-to-date](https://github.com/alucryd/aur-alucryd/tree/master/pantheon) packages than the few available in the [community repository](/index.php/Community_repository "Community repository"). To use it add the following lines at the top of your sources in `/etc/pacman.conf`:

```
[extra-alucryd]
Server = https://pkgbuild.com/~alucryd/$repo/$arch

```

Do note that some packages are missing from the repository due to [issues](https://github.com/alucryd/aur-alucryd/issues/88#issuecomment-434606676) with upstream. You will have to supplement the repo with locally compiled packages.

#### AUR

Alternatively, the [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") for the pantheon packages are also available in the [AUR](/index.php/AUR "AUR").

As of 6 November 2018, [gala-git](https://aur.archlinux.org/packages/gala-git/) will fail to build with the current version of [mutter](https://www.archlinux.org/packages/?name=mutter), and will require a [downgrade](/index.php/Downgrade "Downgrade") to the latest compatible version (3.28). (This is the reason why some packages are missing from the [unofficial repo](https://github.com/alucryd/aur-alucryd/tree/master/pantheon).) You can either downgrade, package [mutter](https://www.archlinux.org/packages/?name=mutter) 3.28 separately (do consider submitting to AUR if you do), or wait until upstream decides to adapt the most recent version. [gala-git](https://aur.archlinux.org/packages/gala-git/) is a dependency for a lot of packages; you need to take care of this for a lot of the applications.

### Desktop Environment

For the minimal Pantheon shell, install [pantheon-session-git](https://aur.archlinux.org/packages/pantheon-session-git/), which pulls--among other dependencies--the core components:

*   [cerbere-git](https://aur.archlinux.org/packages/cerbere-git/): Watchdog service; restarts core components if they crash.
*   [gala-git](https://aur.archlinux.org/packages/gala-git/): Window and composting manager
*   [wingpanel-git](https://aur.archlinux.org/packages/wingpanel-git/): Top panel (holds the launcher, clock, and indicators)
*   [pantheon-applications-menu-git](https://aur.archlinux.org/packages/pantheon-applications-menu-git/): Application launcher formerly known as "Slingshot"
*   [plank](https://www.archlinux.org/packages/?name=plank): macOS-style Dock

### Services and Configuration

These optional packages provide background services and default settings for Pantheon and elementary OS applications:

*   [pantheon-default-settings-git](https://aur.archlinux.org/packages/pantheon-default-settings-git/): Default appearance, behavior, and configuration; pulls in theme packages [elementary-icon-theme](https://www.archlinux.org/packages/?name=elementary-icon-theme), [gtk-theme-elementary-git](https://aur.archlinux.org/packages/gtk-theme-elementary-git/), and [elementary-wallpapers-git](https://aur.archlinux.org/packages/elementary-wallpapers-git/)
*   [gnome-settings-daemon-elementary](https://aur.archlinux.org/packages/gnome-settings-daemon-elementary/): A patched [gnome-settings-daemon-ubuntu](https://aur.archlinux.org/packages/gnome-settings-daemon-ubuntu/) required by [pantheon-dpms-helper-git](https://aur.archlinux.org/packages/pantheon-dpms-helper-git/) and [wingpanel-indicator-power-git](https://aur.archlinux.org/packages/wingpanel-indicator-power-git/)
*   [pantheon-print-git](https://aur.archlinux.org/packages/pantheon-print-git/): Print settings dialog
*   [pantheon-polkit-agent-git](https://aur.archlinux.org/packages/pantheon-polkit-agent-git/): Polkit authentication agent

### Theme

These optional packages contribute to the look and feel of the desktop:

*   [elementary-icon-theme](https://www.archlinux.org/packages/?name=elementary-icon-theme) or [elementary-icon-theme-git](https://aur.archlinux.org/packages/elementary-icon-theme-git/): Icon theme designed to be smooth, sexy, clear, and efficient
*   [lightdm-pantheon-greeter](https://aur.archlinux.org/packages/lightdm-pantheon-greeter/) or [lightdm-pantheon-greeter-git](https://aur.archlinux.org/packages/lightdm-pantheon-greeter-git/): LightDM greeter

It is also recommended to install the following fonts:

*   [ttf-opensans](https://www.archlinux.org/packages/?name=ttf-opensans): Open Sans Fonts
*   [ttf-raleway](https://aur.archlinux.org/packages/ttf-raleway/): Raleway Font
*   [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu): Font family based on the Bitstream Vera Fonts
*   [ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid): General-purpose fonts released by Google as part of Android
*   [ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont): Set of free outline fonts covering the Unicode character set
*   [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation): Red Hats Liberation fonts

### Applications

These are some of the original, patched, and selected packages that comprise the optional elementary OS software suite:

*   [pantheon-files](https://www.archlinux.org/packages/?name=pantheon-files) or [pantheon-files-git](https://aur.archlinux.org/packages/pantheon-files-git/): File explorer developed from Marlin
*   [pantheon-terminal](https://www.archlinux.org/packages/?name=pantheon-terminal) or [pantheon-terminal-git](https://aur.archlinux.org/packages/pantheon-terminal-git/): Terminal emulator
*   [pantheon-code](https://www.archlinux.org/packages/?name=pantheon-code) or [pantheon-code-git](https://aur.archlinux.org/packages/pantheon-code-git/): Text editor formerly known as "Scratch"
*   [pantheon-calculator](https://aur.archlinux.org/packages/pantheon-calculator/) or [pantheon-calculator-git](https://aur.archlinux.org/packages/pantheon-calculator-git/): Calculator
*   [pantheon-music](https://www.archlinux.org/packages/?name=pantheon-music) or [pantheon-music-git](https://aur.archlinux.org/packages/pantheon-music-git/): Audio player formerly known as "Noise"
*   [pantheon-videos](https://www.archlinux.org/packages/?name=pantheon-videos) or [pantheon-videos-git](https://aur.archlinux.org/packages/pantheon-videos-git/): Video player formerly known as "Audience"
*   [pantheon-calendar-git](https://aur.archlinux.org/packages/pantheon-calendar-git/): Calendar application formerly known as "Maya", integrates with [wingpanel-indicator-datetime-git](https://aur.archlinux.org/packages/wingpanel-indicator-datetime-git/)
*   [epiphany-pantheon](https://aur.archlinux.org/packages/epiphany-pantheon/): Web browser replacing [midori-granite](https://aur.archlinux.org/packages/midori-granite/)
*   [pantheon-mail-git](https://aur.archlinux.org/packages/pantheon-mail-git/): Email client developed from [geary](https://www.archlinux.org/packages/?name=geary)
*   [pantheon-screenshot](https://aur.archlinux.org/packages/pantheon-screenshot/) or [pantheon-screenshot-git](https://aur.archlinux.org/packages/pantheon-screenshot-git/): Screenshot tool
*   [eidete-bzr](https://aur.archlinux.org/packages/eidete-bzr/): Simple screencaster
*   [pantheon-photos](https://www.archlinux.org/packages/?name=pantheon-photos) or [pantheon-photos-git](https://aur.archlinux.org/packages/pantheon-photos-git/): Photo manager developed from [shotwell](https://www.archlinux.org/packages/?name=shotwell)
*   [pantheon-camera-git](https://aur.archlinux.org/packages/pantheon-camera-git/): Webcam app developed from [snap-photobooth](https://aur.archlinux.org/packages/snap-photobooth/)
*   [elementary-scan-bzr](https://aur.archlinux.org/packages/elementary-scan-bzr/): Simple scan utility (does not build)
*   [switchboard](https://www.archlinux.org/packages/?name=switchboard) or [switchboard-git](https://aur.archlinux.org/packages/switchboard-git/): Pluggable settings manager similar to [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center)

## Launching Pantheon

### Via [Display manager](/index.php/Display_manager "Display manager")

[pantheon-session-git](https://aur.archlinux.org/packages/pantheon-session-git/) provides a [gnome-session](https://www.archlinux.org/packages/?name=gnome-session) entry for display managers such as [gdm](https://www.archlinux.org/packages/?name=gdm) or [lightdm](https://www.archlinux.org/packages/?name=lightdm).

#### Autostart applications with a display manager

As a gnome-session, Pantheon implements [XDG Autostart](/index.php/GNOME#Autostart "GNOME").

### Via [xinit](/index.php/Xinit "Xinit")

Alternatively, you can use `~/.xinitrc` to launch the Pantheon shell, by adding `exec cerbere` to the end of the file.

#### Autostart applications with *xinit*

For applications which do not provide a [systemd unit](/index.php/Systemd#Using_units "Systemd"), consider these options:

*   Run once when X starts:

	Add it to your [`~/.xinitrc`](#Via_xinit) [Shell](/index.php/Shell "Shell") script, before the `exec cerbere` line.

*   Keep running in the background:

	Add it to the [dconf key](#Configuration) `org.pantheon.desktop.cerbere.monitored-processes`.

	Should the process stop, [cerbere](https://aur.archlinux.org/packages/cerbere/) will respawn it.

*   Launch from a [.desktop](/index.php/.desktop ".desktop") file:

	Use a program like [dapper](https://aur.archlinux.org/packages/dapper/), [dex-git](https://aur.archlinux.org/packages/dex-git/), or [fbautostart](https://aur.archlinux.org/packages/fbautostart/) to implement [XDG Autostart](/index.php/XDG_Autostart "XDG Autostart").

## Configuration

Configure Pantheon via [switchboard](https://www.archlinux.org/packages/?name=switchboard) or [switchboard-git](https://aur.archlinux.org/packages/switchboard-git/) and its plugs (*switchboard-plug-**), which must be installed separately. Not all of [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center)'s settings panels have been ported. In addition, except [plank](/index.php/Plank "Plank"), all the Pantheon components store their configuration in the `org.pantheon` or `io.elementary` [gsettings keys](/index.php/GNOME#Configuration "GNOME"), which can be edited with [dconf-editor](https://www.archlinux.org/packages/?name=dconf-editor).

**Note:** [switchboard-plug-elementary-tweaks-git](https://aur.archlinux.org/packages/switchboard-plug-elementary-tweaks-git/) provides easy access to [customizations for various aspects of the Pantheon desktop and applications](https://raw.githubusercontent.com/elementary-tweaks/elementary-tweaks/master/docs/screenshot.png), similar to [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks).

### Wingpanel

Wingpanel does not come with any indicators; they must be installed separately.

At the minimum, you'll probably want to install:

*   [slingshot-launcher](https://aur.archlinux.org/packages/slingshot-launcher/) or [pantheon-applications-menu-git](https://aur.archlinux.org/packages/pantheon-applications-menu-git/): Applications menu and "Run" dialog
*   [wingpanel-indicator-datetime](https://aur.archlinux.org/packages/wingpanel-indicator-datetime/) or [wingpanel-indicator-datetime-git](https://aur.archlinux.org/packages/wingpanel-indicator-datetime-git/): Clock and calendar widget
*   [wingpanel-indicator-session](https://aur.archlinux.org/packages/wingpanel-indicator-session/) or [wingpanel-indicator-session-git](https://aur.archlinux.org/packages/wingpanel-indicator-session-git/): User and session menu (Switch user, Logout, Shutdown, etc.)

**Note:** [wingpanel](https://aur.archlinux.org/packages/wingpanel/) supports [Ayatana indicators](/index.php/Unity "Unity"), while [wingpanel-git](https://aur.archlinux.org/packages/wingpanel-git/) has native indicators (*wingpanel-indicator-*-git*).

#### Third-party indicators

*   If launched by a [display manager](#Via_Display_manager), append `Pantheon;` to `OnlyShowIn=` in third-party indicators' [*.desktop files](/index.php/XDG_Autostart "XDG Autostart")

*   If launched by [~/.xinitrc](#Via_xinit), add third-party indicators to one of the start-up methods described [above](#Launching_Pantheon).

*   [Ayatana Indicators](/index.php/Unity "Unity") require [wingpanel-indicator-ayatana](https://aur.archlinux.org/packages/wingpanel-indicator-ayatana/) or [wingpanel-indicator-ayatana-git](https://aur.archlinux.org/packages/wingpanel-indicator-ayatana-git/) to appear in [wingpanel-git](https://aur.archlinux.org/packages/wingpanel-git/).

#### Indicator-session menus unresponsive

*   [indicator-session](https://aur.archlinux.org/packages/indicator-session/) relies on dbus methods provided by [Unity](/index.php/Unity "Unity") for most of its functions and fails to fallback to gnome or systemd methods in its absence.

*   [wingpanel-indicator-session-git](https://aur.archlinux.org/packages/wingpanel-indicator-session-git/) needs [light-locker](/index.php/Light-locker "Light-locker") or [xscreensaver-dbus-screenlock](https://aur.archlinux.org/packages/xscreensaver-dbus-screenlock/) installed for the `Lock` menu item.

### Plank

#### Adding new application icons

Either drag and drop a desktop file on to the dock, or right click on a running application and select "Keep in dock". You can then reorder icons by drag and drop.

**Note:** Plank stores .dockitem launchers in `~/.config/plank/` and configuration in the gsettings key `net.launchpad.plank`

### Pantheon Files

#### Enable context menu entries

If you want to enable context menu entries such as for [file-roller](https://www.archlinux.org/packages/?name=file-roller) to extract/compress archives, then you have to additionally install [contractor](https://www.archlinux.org/packages/?name=contractor) or [contractor-git](https://aur.archlinux.org/packages/contractor-git/).

### Terminal

#### Opacity

To make [pantheon-terminal](https://www.archlinux.org/packages/?name=pantheon-terminal) (semi-)transparent, [set the dconf key](#Configuration) `org.pantheon.terminal.settings.opacity` to your desired opacity; for [pantheon-terminal-git](https://aur.archlinux.org/packages/pantheon-terminal-git/), the background color and transparency are set by `io.elementary.terminal.settings.background`.

## Known Issues

### Appearance

#### Pantheon-terminal transparency

Transparency in pantheon-terminal is not yet fully functional with GTK themes other than the elmentary OS theme. Either use [gtk-theme-elementary](https://aur.archlinux.org/packages/gtk-theme-elementary/), [gtk-theme-elementary-git](https://aur.archlinux.org/packages/gtk-theme-elementary-git/) or add the following code to your theme's css or the override file in `~/.config/gtk-3.0/gtk.css`:

```
/************
 * Terminal *
 ***********/

PantheonTerminalPantheonTerminalWindow.background {
   background-color: transparent;
}

```

#### Wingpanel transparency

Wingpanel is transparent by design when using [gtk-theme-elementary](https://aur.archlinux.org/packages/gtk-theme-elementary/) or [gtk-theme-elementary-git](https://aur.archlinux.org/packages/gtk-theme-elementary-git/), and becomes opaque when a maximized window occupies your screen. However, using other GTK themes will produce a solid panel most of the time.

To achieve the former behavior within another theme, add the following code to its css or the override file in `~/.config/gtk-3.0/gtk.css`:

```
/*********************
 * wingpanel support *
 ********************/

.panel {
    background-color: transparent;
    transition: all 1s ease-in-out;
}

.panel.maximized {
    background-color: #000;
}

```