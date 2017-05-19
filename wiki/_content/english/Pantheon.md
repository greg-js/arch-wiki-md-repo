[Pantheon](http://elementary.io/) is the default desktop environment originally created for the elementary OS distribution. It is written from scratch using Vala and the GTK3 toolkit. With regards to usability and appearance, the desktop has some similarities with [GNOME](/index.php/GNOME "GNOME") Shell and MacOS.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Desktop Environment](#Desktop_Environment)
    *   [1.2 Services and Configuration](#Services_and_Configuration)
    *   [1.3 Theme](#Theme)
    *   [1.4 Applications](#Applications)
*   [2 Launching Pantheon](#Launching_Pantheon)
    *   [2.1 Via Display manager](#Via_Display_manager)
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
    *   [4.1 Usability](#Usability)
        *   [4.1.1 Cannot interact with the LightDM Pantheon greeter](#Cannot_interact_with_the_LightDM_Pantheon_greeter)
        *   [4.1.2 Gala crashes on start](#Gala_crashes_on_start)
        *   [4.1.3 No mouse cursor after login](#No_mouse_cursor_after_login)
    *   [4.2 Indicators](#Indicators)
        *   [4.2.1 Indicators not appearing in wingpanel](#Indicators_not_appearing_in_wingpanel)
        *   [4.2.2 Third-party indicators](#Third-party_indicators)
        *   [4.2.3 Indicator-session menus not responsive](#Indicator-session_menus_not_responsive)
    *   [4.3 Appearance](#Appearance)
        *   [4.3.1 Pantheon-terminal transparency](#Pantheon-terminal_transparency)
        *   [4.3.2 Wingpanel transparency](#Wingpanel_transparency)
        *   [4.3.3 GTK+ applications surrounded by awful black shadow box](#GTK.2B_applications_surrounded_by_awful_black_shadow_box)
        *   [4.3.4 White icons in pantheon-files](#White_icons_in_pantheon-files)

## Installation

**Note:** Although their release schedule and toolchain are bound to [Ubuntu's](/index.php/Arch_compared_to_other_distributions#Ubuntu "Arch compared to other distributions") LTS release cycle, [elementary OS development](https://plus.google.com/communities/104613975513761463450) moves quickly. The *-[bzr](/index.php/Bzr "Bzr") and *-[git](/index.php/Git "Git") packages contain the most recent updates and are *less* likely to have obsolete dependencies in Archlinux, but occasionally have stability or build issues and may not be compatible with the standard releases.

[Alucryd's unofficial repo](https://github.com/alucryd/aur-alucryd/tree/master/pantheon) contains more and more up-to-date packages than the few available in [community](/index.php/Community "Community"). To use it add the following lines at the top of your sources in `/etc/pacman.conf`:

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
*   [wingpanel](https://aur.archlinux.org/packages/wingpanel/): Top panel (release version)
*   [slingshot-launcher](https://aur.archlinux.org/packages/slingshot-launcher/): Application launcher (release version)

You may additionally install these packages as well:

*   [plank](https://www.archlinux.org/packages/?name=plank) or [plank-bzr](https://aur.archlinux.org/packages/plank-bzr/): MacOS-like Dock
*   [wingpanel-git](https://aur.archlinux.org/packages/wingpanel-git/): Top panel (development version)
*   [slingshot-launcher-bzr](https://aur.archlinux.org/packages/slingshot-launcher-bzr/): Application launcher (development version)

### Services and Configuration

These packages provide background services and default settings for Pantheon and elementary OS applications:

*   [pantheon-default-settings-bzr](https://aur.archlinux.org/packages/pantheon-default-settings-bzr/): Default desktop appearance, behavior, and application configuration; pulls in theme packages [elementary-icon-theme](https://www.archlinux.org/packages/?name=elementary-icon-theme), [gtk-theme-elementary-bzr](https://aur.archlinux.org/packages/gtk-theme-elementary-bzr/), [pantheon-backgrounds-bzr](https://aur.archlinux.org/packages/pantheon-backgrounds-bzr/), and [plank-theme-pantheon-bzr](https://aur.archlinux.org/packages/plank-theme-pantheon-bzr/).
*   [contractor](https://www.archlinux.org/packages/?name=contractor) or [contractor-git](https://aur.archlinux.org/packages/contractor-git/): Service for sharing data between apps
*   [gnome-settings-daemon-elementary](https://aur.archlinux.org/packages/gnome-settings-daemon-elementary/): A patch against [gnome-settings-daemon-ubuntu](https://aur.archlinux.org/packages/gnome-settings-daemon-ubuntu/) to support [elementary-dpms-helper-bzr](https://aur.archlinux.org/packages/elementary-dpms-helper-bzr/) and [wingpanel-indicator-power-git](https://aur.archlinux.org/packages/wingpanel-indicator-power-git/)
*   [pantheon-print-git](https://aur.archlinux.org/packages/pantheon-print-git/): Print settings dialog
*   [pantheon-agent-polkit-bzr](https://aur.archlinux.org/packages/pantheon-agent-polkit-bzr/): Polkit authentication agent

### Theme

These packages contribute to the look and feel of the desktop:

*   [elementary-icon-theme](https://www.archlinux.org/packages/?name=elementary-icon-theme) or [elementary-icon-theme-git](https://aur.archlinux.org/packages/elementary-icon-theme-git/): Icon theme designed to be smooth, sexy, clear, and efficient
*   [lightdm-pantheon-greeter](https://aur.archlinux.org/packages/lightdm-pantheon-greeter/) or [lightdm-pantheon-greeter-git](https://aur.archlinux.org/packages/lightdm-pantheon-greeter-git/): LightDM greeter

It is also recommended to install the following fonts:

*   [ttf-opensans](https://aur.archlinux.org/packages/ttf-opensans/): Open Sans Fonts
*   [ttf-raleway](https://aur.archlinux.org/packages/ttf-raleway/): Raleway Font
*   [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu): Font family based on the Bitstream Vera Fonts
*   [ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid): General-purpose fonts released by Google as part of Android
*   [ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont): Set of free outline fonts covering the Unicode character set
*   [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation): Red Hats Liberation fonts

### Applications

These are some of the original, patched, and selected packages that comprise the elementary OS software suite:

*   [pantheon-files](https://www.archlinux.org/packages/?name=pantheon-files) or [pantheon-files-bzr](https://aur.archlinux.org/packages/pantheon-files-bzr/): File explorer based on Marlin
*   [pantheon-terminal](https://www.archlinux.org/packages/?name=pantheon-terminal) or [pantheon-terminal-git](https://aur.archlinux.org/packages/pantheon-terminal-git/): Terminal emulator
*   [scratch-text-editor](https://www.archlinux.org/packages/?name=scratch-text-editor) or [scratch-text-editor-git](https://aur.archlinux.org/packages/scratch-text-editor-git/): Text editor
*   [pantheon-calculator](https://aur.archlinux.org/packages/pantheon-calculator/) or [pantheon-calculator-git](https://aur.archlinux.org/packages/pantheon-calculator-git/): Calculator
*   [pantheon-music-git](https://aur.archlinux.org/packages/pantheon-music-git/): Audio player developed from [noise-player](https://www.archlinux.org/packages/?name=noise-player)
*   [pantheon-videos-git](https://aur.archlinux.org/packages/pantheon-videos-git/): Video player developed from [audience](https://www.archlinux.org/packages/?name=audience)
*   [pantheon-calendar-git](https://aur.archlinux.org/packages/pantheon-calendar-git/): Calendar developed from [maya-calendar](https://aur.archlinux.org/packages/maya-calendar/)
*   [midori-granite](https://aur.archlinux.org/packages/midori-granite/) or [midori-granite-bzr](https://aur.archlinux.org/packages/midori-granite-bzr/): Web browser, replaced by a customized [epiphany](https://www.archlinux.org/packages/?name=epiphany) (not yet packaged for Archlinux).
*   [pantheon-mail-git](https://aur.archlinux.org/packages/pantheon-mail-git/): Email client based on [geary](https://www.archlinux.org/packages/?name=geary)
*   [screenshot-tool-bzr](https://aur.archlinux.org/packages/screenshot-tool-bzr/): Screenshot tool
*   [eidete-bzr](https://aur.archlinux.org/packages/eidete-bzr/): Simple screencaster
*   [pantheon-photos](https://www.archlinux.org/packages/?name=pantheon-photos) or [pantheon-photos-git](https://aur.archlinux.org/packages/pantheon-photos-git/): Photo manager based on [shotwell](https://www.archlinux.org/packages/?name=shotwell)
*   [pantheon-camera-git](https://aur.archlinux.org/packages/pantheon-camera-git/): Webcam app developed from [snap-photobooth](https://aur.archlinux.org/packages/snap-photobooth/)
*   [elementary-scan-bzr](https://aur.archlinux.org/packages/elementary-scan-bzr/): Simple scan utility (does not build)
*   [pantheon-notes-bzr](https://aur.archlinux.org/packages/pantheon-notes-bzr/): Note taking app, replacing [footnote-bzr](https://aur.archlinux.org/packages/footnote-bzr/)
*   [switchboard](https://aur.archlinux.org/packages/switchboard/) or [switchboard-git](https://aur.archlinux.org/packages/switchboard-git/): Pluggable settings manager similar to [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center)

## Launching Pantheon

### Via [Display manager](/index.php/Display_manager "Display manager")

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

Configure Pantheon via [switchboard](https://aur.archlinux.org/packages/switchboard/) and its plugs (*switchboard-plug-**), which must be installed separately. The intent is to replace [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center), but not all settings--particularly not third-party applications' settings--have been ported. In some cases, you may prefer to use [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) or [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool) instead. All Pantheon settings, except [plank's](/index.php/Plank "Plank"), can also be altered via *dconf* and are located in the `org.pantheon` key. Use [dconf-editor](https://www.archlinux.org/packages/?name=dconf-editor) for easy editing.

**Note:** Although abandoned, [switchboard-plug-elementary-tweaks-bzr](https://aur.archlinux.org/packages/switchboard-plug-elementary-tweaks-bzr/) remains a useful tool for configuring many aspects of Pantheon, including [plank](/index.php/Plank "Plank").

### Plank

#### Adding new application icons

Either drag and drop a desktop file on to the dock, or right click on a running application and select "Keep in dock". You can then reorder icons by drag and drop.

**Note:** Plank stores its configuration files in `~/.config/plank/`

### Pantheon Files

#### Enable context menu entries

If you want to enable context menu entries such as for [file-roller](https://www.archlinux.org/packages/?name=file-roller) to extract/compress archives, then you have to additionally install [contractor](https://www.archlinux.org/packages/?name=contractor).

### Terminal

#### Opacity (transparency)

To make [pantheon-terminal](https://www.archlinux.org/packages/?name=pantheon-terminal) (semi-)transparent, open [dconf-editor](https://www.archlinux.org/packages/?name=dconf-editor) and go to `org.pantheon.terminal.settings.opacity` to set your desired opacity. For [pantheon-terminal-git](https://aur.archlinux.org/packages/pantheon-terminal-git/), the background color and transparency are set by `org.pantheon.terminal.settings.background`.

## Known Issues

### Usability

#### Cannot interact with the LightDM Pantheon greeter

You need to delete `/var/lib/lightdm/.pam_environment`. Do note however that this file is a workaround for the following LightDM bug: [https://bugs.launchpad.net/ubuntu/+source/unity-greeter/+bug/1024482](https://bugs.launchpad.net/ubuntu/+source/unity-greeter/+bug/1024482)

#### Gala crashes on start

Unconfigured gala tries to use default gnome wallpaper, which is absent unless you have the package [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard) installed. Install it workaround the crash; it is safe to remove after you configure another wallpaper.

#### No mouse cursor after login

The Gala window manager is most likely not running. Either install [cerbere-git](https://aur.archlinux.org/packages/cerbere-git/) or add `gala` to the list of cerbere's [monitored processes](#Via_xinit).

### Indicators

#### Indicators not appearing in wingpanel

Wingpanel does not come with any indicators; they must be installed separately.

**Note:** [wingpanel](https://aur.archlinux.org/packages/wingpanel/) supports [Ayatana indicators](/index.php/Unity "Unity"), while [wingpanel-git](https://aur.archlinux.org/packages/wingpanel-git/) has native indicators (*wingpanel-indicator-*-git*).

#### Third-party indicators

*   If launched by a [display manager](#Via_Display_manager), append `Pantheon` to `OnlyShowIn=` in third-party indicators' [*.desktop files](/index.php/Desktop_entries#Autostart "Desktop entries")

*   If launched by [~/.xinitrc](#Via_xinit), add third-party indicators to one of the start-up methods described [above](#Launching_Pantheon).

*   For [wingpanel-git](https://aur.archlinux.org/packages/wingpanel-git/), indicators designed for [Unity](/index.php/Unity "Unity") require [wingpanel-indicator-ayatana-bzr](https://aur.archlinux.org/packages/wingpanel-indicator-ayatana-bzr/).

#### Indicator-session menus not responsive

*   [indicator-session](https://aur.archlinux.org/packages/indicator-session/) relies on dbus methods provided by [Unity](/index.php/Unity "Unity") for most of its functions and fails to fallback to gnome or systemd methods in its absence.

*   [wingpanel-indicator-session-git](https://aur.archlinux.org/packages/wingpanel-indicator-session-git/) needs [light-locker](/index.php/Light-locker "Light-locker") or [xscreensaver-dbus-screenlock](https://aur.archlinux.org/packages/xscreensaver-dbus-screenlock/) installed for the `Lock` menu item.

### Appearance

#### Pantheon-terminal transparency

Transparency in pantheon-terminal is not yet fully functional with GTK themes other than the elmentary OS theme. Either use [gtk-theme-elementary](https://aur.archlinux.org/packages/gtk-theme-elementary/), [gtk-theme-elementary-git](https://aur.archlinux.org/packages/gtk-theme-elementary-git/) or add [this](http://bazaar.launchpad.net/~elementary-design/egtk/4.x/revision/210) code to your theme or the override file in `~/.config/gtk-3.0/gtk.css`.

#### Wingpanel transparency

Wingpanel is transparent by design when using [gtk-theme-elementary](https://aur.archlinux.org/packages/gtk-theme-elementary/) or [gtk-theme-elementary-git](https://aur.archlinux.org/packages/gtk-theme-elementary-git/), and becomes opaque when a maximized window occupies your screen. However, using other GTK themes will produce a solid panel most of the time.

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

Currently there seems to be a bug which displays the view icons in the top location in a white colour instead of black. This can be fixed by installing [gtk-theme-elementary-git](https://aur.archlinux.org/packages/gtk-theme-elementary-git/) or, for [gtk-theme-elementary](https://aur.archlinux.org/packages/gtk-theme-elementary/), add the following line to `gtk-widgets.css`:

```
GtkToolItem { color: @text_color; }

```