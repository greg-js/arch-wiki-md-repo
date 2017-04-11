[Pantheon](http://elementary.io/) is the default desktop environment originally created for the elementary OS distribution. It is written from scratch using Vala and the GTK3 toolkit. With regards to usability and appearance, the desktop has some similarities with [GNOME](/index.php/GNOME "GNOME") Shell and MacOS.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Desktop Environment](#Desktop_Environment)
    *   [1.2 Services and Configuration](#Services_and_Configuration)
    *   [1.3 Theme](#Theme)
    *   [1.4 Applications](#Applications)
*   [2 Launching Pantheon](#Launching_Pantheon)
    *   [2.1 Via Display Manager](#Via_Display_Manager)
    *   [2.2 Via xinit](#Via_xinit)
        *   [2.2.1 Autostart applications with ~/.xinitrc](#Autostart_applications_with_.7E.2F.xinitrc)
*   [3 Configuration](#Configuration)
    *   [3.1 Plank](#Plank)
        *   [3.1.1 Adding new application icons](#Adding_new_application_icons)
    *   [3.2 Pantheon Files](#Pantheon_Files)
        *   [3.2.1 Enable context menu entries](#Enable_context_menu_entries)
    *   [3.3 Terminal](#Terminal)
        *   [3.3.1 Opacity (transparency)](#Opacity_.28transparency.29)
*   [4 Known Issues](#Known_Issues)
    *   [4.1 Gala crashes on start](#Gala_crashes_on_start)
    *   [4.2 I do not have any mouse cursor](#I_do_not_have_any_mouse_cursor)
    *   [4.3 Indicators not appearing in wingpanel](#Indicators_not_appearing_in_wingpanel)
        *   [4.3.1 Third-party indicators](#Third-party_indicators)
    *   [4.4 Indicator-session menus not responsive](#Indicator-session_menus_not_responsive)
    *   [4.5 Cannot interact with the LightDM Pantheon greeter](#Cannot_interact_with_the_LightDM_Pantheon_greeter)
    *   [4.6 Appearance Issues](#Appearance_Issues)
        *   [4.6.1 How can I change the default appearance such as GTK theme, font size, etc?](#How_can_I_change_the_default_appearance_such_as_GTK_theme.2C_font_size.2C_etc.3F)
        *   [4.6.2 Pantheon-terminal transparency](#Pantheon-terminal_transparency)
        *   [4.6.3 Wingpanel transparency](#Wingpanel_transparency)
        *   [4.6.4 GTK+ applications surrounded by awful black shadow box](#GTK.2B_applications_surrounded_by_awful_black_shadow_box)
        *   [4.6.5 White icons in pantheon-files](#White_icons_in_pantheon-files)
        *   [4.6.6 Corrupted graphics in Ayatana indicators](#Corrupted_graphics_in_Ayatana_indicators)

## Installation

**Note:** Although their release schedule and toolchain are bound to [Ubuntu's](/index.php/Arch_compared_to_other_distributions#Ubuntu "Arch compared to other distributions"), [elementary OS development](https://plus.google.com/communities/104613975513761463450) moves quickly. The *-[bzr](/index.php/Bazaar "Bazaar") packages contain the most recent updates and are *less* likely to have obsolete dependencies in Archlinux, but occasionally have stability or build issues and may not be compatible with the standard releases.

Some Pantheon packages are available from the [community](/index.php/Community "Community") repository, but [Alucryd's unofficial repo](https://github.com/alucryd/aur-alucryd/tree/master/pantheon) contains more and more up-to-date packages. To use it add the following lines at the top of your sources in `/etc/pacman.conf`:

```
[pantheon]
SigLevel = Optional
Server = https://pkgbuild.com/~alucryd/$repo/$arch

```

**Note:** The PKGBUILDs for these packages are also available in the [AUR](/index.php/AUR "AUR").

### Desktop Environment

To get the minimal Pantheon desktop interface, start by installing [pantheon-session-bzr](https://aur.archlinux.org/packages/pantheon-session-bzr/), which pulls--among other dependencies--the core components:

*   [cerbere-bzr](https://aur.archlinux.org/packages/cerbere-bzr/): Watchdog service to keep core Pantheon apps running
*   [gala-bzr](https://aur.archlinux.org/packages/gala-bzr/): Window Manager
*   [wingpanel](https://www.archlinux.org/packages/?name=wingpanel): Top panel (release version)
*   [slingshot-launcher](https://www.archlinux.org/packages/?name=slingshot-launcher): Application launcher (release version)

You may additionally install these packages as well:

*   [plank-bzr](https://aur.archlinux.org/packages/plank-bzr/): MacOS-like Dock
*   [wingpanel-bzr](https://aur.archlinux.org/packages/wingpanel-bzr/): Top panel (bzr version)
*   [slingshot-launcher-bzr](https://aur.archlinux.org/packages/slingshot-launcher-bzr/): Application launcher (bzr version)

### Services and Configuration

These packages provide background services and default settings for Pantheon and elementary OS applications:

*   [pantheon-default-settings-bzr](https://aur.archlinux.org/packages/pantheon-default-settings-bzr/): Default desktop appearance, behavior, and application configuration; pulls in theme packages [elementary-icon-theme](https://www.archlinux.org/packages/?name=elementary-icon-theme), [gtk-theme-elementary-bzr](https://aur.archlinux.org/packages/gtk-theme-elementary-bzr/), [pantheon-backgrounds-bzr](https://aur.archlinux.org/packages/pantheon-backgrounds-bzr/), and [plank-theme-pantheon-bzr](https://aur.archlinux.org/packages/plank-theme-pantheon-bzr/).
*   [contractor-bzr](https://aur.archlinux.org/packages/contractor-bzr/): Service for sharing data between apps
*   [gnome-settings-daemon-elementary](https://aur.archlinux.org/packages/gnome-settings-daemon-elementary/): A patch against [gnome-settings-daemon-ubuntu](https://aur.archlinux.org/packages/gnome-settings-daemon-ubuntu/) to support [elementary-dpms-helper-bzr](https://aur.archlinux.org/packages/elementary-dpms-helper-bzr/) and [wingpanel-indicator-power-bzr](https://aur.archlinux.org/packages/wingpanel-indicator-power-bzr/)
*   [pantheon-print-bzr](https://aur.archlinux.org/packages/pantheon-print-bzr/): Print settings dialog
*   [pantheon-agent-polkit-bzr](https://aur.archlinux.org/packages/pantheon-agent-polkit-bzr/): Polkit authentication agent

### Theme

These packages contribute to the look and feel of the desktop:

*   [elementary-icon-theme-bzr](https://aur.archlinux.org/packages/elementary-icon-theme-bzr/): Icon theme designed to be smooth, sexy, clear, and efficient (bzr version)
*   [lightdm-pantheon-greeter-bzr](https://aur.archlinux.org/packages/lightdm-pantheon-greeter-bzr/): LightDM greeter

It is also recommended to install the following fonts:

*   [ttf-opensans](https://aur.archlinux.org/packages/ttf-opensans/): Open Sans Fonts
*   [ttf-raleway](https://aur.archlinux.org/packages/ttf-raleway/): Raleway Font
*   [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu): Font family based on the Bitstream Vera Fonts
*   [ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid): General-purpose fonts released by Google as part of Android
*   [ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont): Set of free outline fonts covering the Unicode character set
*   [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation): Red Hats Liberation fonts

### Applications

These packages are the original, patched, and selected applications that comprise the elementary OS software suite:

*   [pantheon-files-bzr](https://aur.archlinux.org/packages/pantheon-files-bzr/): File explorer based on Marlin
*   [pantheon-terminal-bzr](https://aur.archlinux.org/packages/pantheon-terminal-bzr/): Terminal emulator
*   [scratch-text-editor-bzr](https://aur.archlinux.org/packages/scratch-text-editor-bzr/): Text editor
*   [pantheon-calculator-bzr](https://aur.archlinux.org/packages/pantheon-calculator-bzr/): Calculator
*   [noise-player-bzr](https://aur.archlinux.org/packages/noise-player-bzr/): Audio player
*   [audience-bzr](https://aur.archlinux.org/packages/audience-bzr/): Video player
*   [maya-calendar-bzr](https://aur.archlinux.org/packages/maya-calendar-bzr/): Calendar
*   [midori-granite-bzr](https://aur.archlinux.org/packages/midori-granite-bzr/): Web browser (recently replaced by a patched version of [Epiphany](https://www.archlinux.org/packages/?name=Epiphany))
*   [pantheon-mail-bzr](https://aur.archlinux.org/packages/pantheon-mail-bzr/): Email client based on [Geary](https://www.archlinux.org/packages/?name=Geary)
*   [screenshot-tool-bzr](https://aur.archlinux.org/packages/screenshot-tool-bzr/): Screenshot tool
*   [eidete-bzr](https://aur.archlinux.org/packages/eidete-bzr/): Simple screencaster
*   [pantheon-photos-bzr](https://aur.archlinux.org/packages/pantheon-photos-bzr/): Photo manager based on [Slingshot](https://www.archlinux.org/packages/?name=Slingshot)
*   [snap-photobooth-bzr](https://aur.archlinux.org/packages/snap-photobooth-bzr/): Webcam app (recently developed into pantheon-camera)
*   [elementary-scan-bzr](https://aur.archlinux.org/packages/elementary-scan-bzr/): Simple scan utility (does not build)
*   [pantheon-notes-bzr](https://aur.archlinux.org/packages/pantheon-notes-bzr/): Note taking app, replacing [footnote-bzr](https://aur.archlinux.org/packages/footnote-bzr/)
*   [switchboard-bzr](https://aur.archlinux.org/packages/switchboard-bzr/): Pluggable settings manager

## Launching Pantheon

**Note:** Either install [cerbere-bzr](https://aur.archlinux.org/packages/cerbere-bzr/) or add 'gala' to `org.pantheon.desktop.cerbere.monitored-processes` in [cerbere](https://aur.archlinux.org/packages/cerbere/)'s [dconf](http://s0.uploads.im/AvOIT.png) to avoid errors such as no visible mouse cursor, failure to start, etc.

### Via [Display Manager](/index.php/Display_Manager "Display Manager")

[pantheon-session-bzr](https://aur.archlinux.org/packages/pantheon-session-bzr/) provides a [gnome-session](https://www.archlinux.org/packages/?name=gnome-session) entry for display managers such as [gdm](https://www.archlinux.org/packages/?name=gdm) or [lightdm](https://www.archlinux.org/packages/?name=lightdm).

### Via [xinit](/index.php/Xinit "Xinit")

Alternatively, you can use `~/.xinitrc` to launch the Pantheon shell, such as:

```
#!/bin/sh

if [ -d /etc/X11/xinit/xinitrc.d ]; then
  for f in /etc/X11/xinit/xinitrc.d/*; do
    [ -x "$f" ] && . "$f"
  done
  unset f
fi

gsettings-data-convert &
xdg-user-dirs-gtk-update &
/usr/lib/polkit-gnome/polkit-gnome-authentication-agent-1 &
/usr/lib/gnome-settings-daemon/gnome-settings-daemon &
/usr/lib/gnome-user-share/gnome-user-share &
eval $(gnome-keyring-daemon --start --components=pkcs11,secrets,ssh,gpg)
export GNOME_KEYRING_CONTROL GNOME_KEYRING_PID GPG_AGENT_INFO SSH_AUTH_SOCK
exec cerbere

```

#### Autostart applications with `~/.xinitrc`

This method does not support [XDG](/index.php/XDG_support "XDG support") autostart. However, there are 3 other ways to achieve this for applications which do not provide a [systemd unit](/index.php/Systemd#Using_units "Systemd"):

*   You may add any program to your `~/.xinitrc`, preferably right before the `exec cerbere` line. This is the better choice for one-shot programs.
*   Or you may edit the `org.pantheon.desktop.cerbere.monitored-processes` key using *dconf-editor* and add the programs of your choice. This method is best for applications which keep running in the background.
*   Or you may use a program like [dapper](https://aur.archlinux.org/packages/dapper/), [dex-git](https://aur.archlinux.org/packages/dex-git/), or [fbautostart](https://aur.archlinux.org/packages/fbautostart/) to add support for XDG autostart in your `~/.xinitrc`.

**Note:** Keep in mind that applications started via *cerbere* cannot be terminated, they will keep respawning up to `org.pantheon.desktop.cerbere.max-crashes`

## Configuration

Configuring Pantheon is done via [switchboard-bzr](https://aur.archlinux.org/packages/switchboard-bzr/) and its plugs, most of which are available in the [AUR](/index.php/AUR "AUR") and [Alucryd's repo](#Installation) as *switchboard-plug-*-bzr*. All pantheon settings, except [plank's](/index.php/Plank "Plank"), can also be altered via *dconf* and are located in the `org.pantheon` key. Use *dconf-editor* for easy editing.

**Note:** The intent is to replace [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center), but not all of its settings have been ported. You may prefer to use [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) itself and [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool) instead.

**Note:** Although it seems to have been abandoned, [switchboard-plug-elementary-tweaks-bzr](https://aur.archlinux.org/packages/switchboard-plug-elementary-tweaks-bzr/) remains a useful tool for configuring many aspects of the pantheon desktop, including [plank](/index.php/Plank "Plank").

### Plank

#### Adding new application icons

Either drag and drop a desktop file on to the dock, or right click on a running application and select "Keep in dock". You can then reorder icons by drag and drop.

**Note:** Plank has its own plaintext configuration files in `~/.config/plank/`

### Pantheon Files

#### Enable context menu entries

If you want to enable context menu entries such as for [file-roller](https://www.archlinux.org/packages/?name=file-roller) to extract/compress archives, then you have to additionally install [contractor-bzr](https://aur.archlinux.org/packages/contractor-bzr/).

### Terminal

#### Opacity (transparency)

You can set a certain opacity to make Pantheon Terminal (semi-)transparent. Open `dconf-editor` and go to `org.pantheon.terminal.settings.opacity` to set your desired opacity.

**Note:** For [pantheon-terminal-bzr](https://aur.archlinux.org/packages/pantheon-terminal-bzr/), the background color and transparency are set by `org.pantheon.terminal.settings.background`

## Known Issues

### Gala crashes on start

It appears that unconfigured gala tries to use default gnome wallpaper as a background. However, the corresponding file is absent unless you have [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard) installed. Thus, install [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard) to workaround the crash. It is safe to remove this package after you configure pantheon in a way you want.

### I do not have any mouse cursor

The 'gala' window manager is most likely [not running](#Launching_Pantheon). Add 'gala' to the list of cerbere's monitored processes.

### Indicators not appearing in wingpanel

Wingpanel does not come with any indicators, they must be installed individually.

**Note:** [wingpanel](https://aur.archlinux.org/packages/wingpanel/) and [wingpanel-bzr](https://aur.archlinux.org/packages/wingpanel-bzr/) implement different kinds of indicators. The standard release wingpanel--poorly--supports the same kind of indicators as [Unity](/index.php/Unity "Unity"), while there are native indicators for the bzr version available in the [AUR](/index.php/AUR "AUR") and [Alucryd's repo](#Installation) as *wingpanel-indicator-*-bzr*.

#### Third-party indicators

If you launch pantheon from a [display manager](#Via_a_Display_Manager), make sure third-party indicators' `/etc/xdg/autostart/indicator-*.desktop` files contain *Pantheon* in `OnlyShowIn=`, eg:

```
OnlyShowIn=Unity;XFCE;GNOME;Pantheon;

```

If you launch pantheon by [~/.xinitrc](#Via_.xinitrc), you need to add third-party indicators to one of the three start-up methods described above.

Additionally, indicators designed for [Unity](/index.php/Unity "Unity") require [wingpanel-indicator-ayatana-bzr](https://aur.archlinux.org/packages/wingpanel-indicator-ayatana-bzr/) to appear in [wingpanel-bzr](https://aur.archlinux.org/packages/wingpanel-bzr/).

### Indicator-session menus not responsive

*   [indicator-session](https://aur.archlinux.org/packages/indicator-session/)

This version of indicator-session relies on dbus methods provided by [Unity](/index.php/Unity "Unity") for most of its functions and fails to fallback to gnome or systemd methods in its absence.

*   [wingpanel-indicator-session-bzr](https://aur.archlinux.org/packages/wingpanel-indicator-session-bzr/)

For *Lock* to function (and "Ctrl+L" hotkey), install [light-locker](/index.php/Light-locker "Light-locker") or [xscreensaver-dbus-screenlock](https://aur.archlinux.org/packages/xscreensaver-dbus-screenlock/).

### Cannot interact with the LightDM Pantheon greeter

You need to delete `/var/lib/lightdm/.pam_environment`. Do note however that this file is a workaround for the following LightDM bug: [https://bugs.launchpad.net/ubuntu/+source/unity-greeter/+bug/1024482](https://bugs.launchpad.net/ubuntu/+source/unity-greeter/+bug/1024482)

### Appearance Issues

#### How can I change the default appearance such as GTK theme, font size, etc?

Install [switchboard-plug-elementary-tweaks-bzr](https://aur.archlinux.org/packages/switchboard-plug-elementary-tweaks-bzr/). Alternatively, use [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool) or see [GTK+](/index.php/GTK%2B "GTK+").

#### Pantheon-terminal transparency

Transparency in pantheon-terminal is not yet fully functional with GTK themes other than the elmentary OS theme. Either use [gtk-theme-elementary](https://aur.archlinux.org/packages/gtk-theme-elementary/), [gtk-theme-elementary-bzr](https://aur.archlinux.org/packages/gtk-theme-elementary-bzr/) or add [this](http://bazaar.launchpad.net/~elementary-design/egtk/4.x/revision/210) code to your theme or the override file in `~/.config/gtk-3.0/gtk.css`.

#### Wingpanel transparency

Wingpanel is transparent by design when using [gtk-theme-elementary](https://aur.archlinux.org/packages/gtk-theme-elementary/) or [gtk-theme-elementary-bzr](https://aur.archlinux.org/packages/gtk-theme-elementary-bzr/), and becomes opaque when a maximized window occupies your screen. However, using other GTK themes will produce a solid panel most of the time.

To achieve the former behavior within other themes, add the following lines to the end of its css or the override file in `~/.config/gtk-3.0/gtk.css`:

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

#### GTK+ applications surrounded by awful black shadow box

The Elementary GTK theme seems to be using its own files and ignoring the `~/.config/gtk-3.0/gtk.css` user-override config file. This has been reported on [https://bugs.launchpad.net/elementaryos/+bug/1592441](https://bugs.launchpad.net/elementaryos/+bug/1592441). To work around the issue, go to the file `/usr/share/themes/elementary/gtk-3.0/gtk-widgets.css` and look for the following (around line 3669):

```
decoration,
.window-frame {
    border-radius: 4px 4px 0 0;
    box-shadow: 0 0 0 1px alpha (#000, 0.3),
                0 14px 28px rgba(0,0,0,0.35),
                0 10px 10px rgba(0,0,0,0.22);
    margin: 12px;
}

```

Replace the above by the the code below

```
decoration,
.window-frame {
    box-shadow: none;
    border: none;
    padding: 0;
    margin: 0;
}

```

#### White icons in pantheon-files

Currently there seems to be a bug which displays the view icons in the top location in a white colour instead of black. This can be fixed by installing [gtk-theme-elementary-bzr](https://aur.archlinux.org/packages/gtk-theme-elementary-bzr/) or adding the following line to `gtk-widgets.css` or `gtk-widgets.css` of your [gtk-theme-elementary](https://aur.archlinux.org/packages/gtk-theme-elementary/) theme:

```
GtkToolItem { color: @text_color; }

```

#### Corrupted graphics in Ayatana indicators

Indicators behave incorrectly with every theme I have tried. They are very ancient, all of them date back to 2012 because the newer indicators depend on Ubuntu patches, and they should be killed with fire anyway. Wingpanel is doing just that and I hope the next major release will ship their new plugin system.