[Pantheon](http://elementary.io/) is the default desktop environment originally created for the elementary OS distribution. It is written from scratch using Vala and the GTK3 toolkit. With regards to usability and appearance, the desktop has some similarities with [GNOME](/index.php/GNOME "GNOME") Shell and macOS.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Additional Info](#Additional_Info)
        *   [1.1.1 Packages based on older evolution-data-server](#Packages_based_on_older_evolution-data-server)
*   [2 Launching Pantheon](#Launching_Pantheon)
    *   [2.1 Via a Display Manager](#Via_a_Display_Manager)
    *   [2.2 Via .xinitrc](#Via_.xinitrc)
    *   [2.3 Autostart applications](#Autostart_applications)
*   [3 Configuration](#Configuration)
    *   [3.1 Pantheon Files](#Pantheon_Files)
        *   [3.1.1 Enable context menu entries](#Enable_context_menu_entries)
    *   [3.2 Terminal](#Terminal)
        *   [3.2.1 Opacity (transparency)](#Opacity_.28transparency.29)
*   [4 Known Issues](#Known_Issues)
    *   [4.1 Indicators not working in wingpanel](#Indicators_not_working_in_wingpanel)
    *   [4.2 Indicator-session menus not working](#Indicator-session_menus_not_working)
    *   [4.3 No transparency in pantheon-terminal](#No_transparency_in_pantheon-terminal)
    *   [4.4 White icons in pantheon-files](#White_icons_in_pantheon-files)
    *   [4.5 Wingpanel is transparent](#Wingpanel_is_transparent)
    *   [4.6 Corrupted graphics in canonical indicators](#Corrupted_graphics_in_canonical_indicators)
    *   [4.7 Cannot interact with the LightDM Pantheon greeter](#Cannot_interact_with_the_LightDM_Pantheon_greeter)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Gala crashes on start](#Gala_crashes_on_start)
    *   [5.2 How can I add new applications to the dock?](#How_can_I_add_new_applications_to_the_dock.3F)
    *   [5.3 How can I change the default appearance such as GTK theme, font size, etc?](#How_can_I_change_the_default_appearance_such_as_GTK_theme.2C_font_size.2C_etc.3F)
    *   [5.4 I do not have any mouse cursor](#I_do_not_have_any_mouse_cursor)
    *   [5.5 Wingpanel is empty except for Applications](#Wingpanel_is_empty_except_for_Applications)

## Installation

Pantheon is split into several packages which are available in an unofficial repository which is daily updated with recent changes from upstream. To use the repository add the following lines at the top of your sources in `/etc/pacman.conf`:

```
[pantheon]
SigLevel = Optional
Server = http://pkgbuild.com/~alucryd/$repo/$arch

```

**Note:** All Pantheon related PKGBUILDs can be found in [Alucryd's GitHub repository](https://github.com/alucryd/aur-alucryd/tree/master/pantheon).

Alternatively, all packages provided by the repository are also available in the [AUR](/index.php/AUR "AUR") for those who prefer to build the packages from source.

To get a minimal desktop interface, you may start by installing [pantheon-session-bzr](https://aur.archlinux.org/packages/pantheon-session-bzr/). This will pull the following core components:

*   [cerbere-bzr](https://aur.archlinux.org/packages/cerbere-bzr/): Watchdog service to keep core Pantheon apps running
*   [gala-bzr](https://aur.archlinux.org/packages/gala-bzr/): Window Manager
*   [wingpanel-bzr](https://aur.archlinux.org/packages/wingpanel-bzr/): Top panel
*   [slingshot-launcher-bzr](https://aur.archlinux.org/packages/slingshot-launcher-bzr/): Application launcher
*   [plank-bzr](https://aur.archlinux.org/packages/plank-bzr/): Dock

However,it is recommended to install the following packages to get a fully working Pantheon Shell:

**Note:** Problems can occur when using (non)-mixed bzr packages! You can install the latest release, by adding -bzr to its install package-name.

*   [audience-bzr](https://aur.archlinux.org/packages/audience-bzr/): Video player
*   [contractor-bzr](https://aur.archlinux.org/packages/contractor-bzr/): Service for sharing data between apps
*   [dexter-contacts-bzr](https://aur.archlinux.org/packages/dexter-contacts-bzr/): Contacts manager (does not build)
*   [eidete-bzr](https://aur.archlinux.org/packages/eidete-bzr/): Simple screencaster
*   [elementary-icon-theme-bzr](https://aur.archlinux.org/packages/elementary-icon-theme-bzr/): elementary icons
*   [elementary-scan-bzr](https://aur.archlinux.org/packages/elementary-scan-bzr/): Simple scan utility (does not build)
*   [elementary-wallpapers-bzr](https://aur.archlinux.org/packages/elementary-wallpapers-bzr/): elementary wallpaper collection
*   [gtk-theme-elementary-bzr](https://aur.archlinux.org/packages/gtk-theme-elementary-bzr/): elementary GTK theme
*   [feedler-bzr](https://aur.archlinux.org/packages/feedler-bzr/): RSS feeds reader (does not build)
*   [footnote-bzr](https://aur.archlinux.org/packages/footnote-bzr/): Note taking app
*   [geary](https://www.archlinux.org/packages/?name=geary): Email client
*   [indicator-pantheon-session-bzr](https://aur.archlinux.org/packages/indicator-pantheon-session-bzr/): Session indicator
*   [lightdm-pantheon-greeter-bzr](https://aur.archlinux.org/packages/lightdm-pantheon-greeter-bzr/): LightDM greeter
*   [maya-calendar-bzr](https://aur.archlinux.org/packages/maya-calendar-bzr/): Calendar
*   [midori-granite-bzr](https://aur.archlinux.org/packages/midori-granite-bzr/): Web browser
*   [noise-player-bzr](https://aur.archlinux.org/packages/noise-player-bzr/): Audio player
*   [pantheon-backgrounds-bzr](https://aur.archlinux.org/packages/pantheon-backgrounds-bzr/): Wallpaper collection
*   [pantheon-calculator-bzr](https://aur.archlinux.org/packages/pantheon-calculator-bzr/): Calculator
*   [pantheon-default-settings-bzr](https://aur.archlinux.org/packages/pantheon-default-settings-bzr/): Pantheon default's settings (appearance, etc.)
*   [pantheon-files-bzr](https://aur.archlinux.org/packages/pantheon-files-bzr/): File explorer
*   [pantheon-notify-bzr](https://aur.archlinux.org/packages/pantheon-notify-bzr/): Notification daemon
*   [pantheon-print-bzr](https://aur.archlinux.org/packages/pantheon-print-bzr/): Print settings
*   [pantheon-terminal-bzr](https://aur.archlinux.org/packages/pantheon-terminal-bzr/): Terminal emulator
*   [plank-theme-pantheon-bzr](https://aur.archlinux.org/packages/plank-theme-pantheon-bzr/): Pantheon theme for plank
*   [scratch-text-editor-bzr](https://aur.archlinux.org/packages/scratch-text-editor-bzr/): Text editor
*   [snap-photobooth-bzr](https://aur.archlinux.org/packages/snap-photobooth-bzr/): Webcam app
*   [switchboard-bzr](https://aur.archlinux.org/packages/switchboard-bzr/): Settings manager

**Note:** You will also need to install plugs, look for "switchboard-plug-*" in the [AUR](https://aur.archlinux.org/packages/?O=0&K=switchboard-plug) or in [Alucryd's GitHub repository](https://github.com/alucryd/aur-alucryd/tree/master/pantheon).

It is also recommended to install the following fonts:

*   [ttf-opensans](https://aur.archlinux.org/packages/ttf-opensans/): Open Sans Fonts
*   [ttf-raleway-font-family](https://aur.archlinux.org/packages/ttf-raleway-font-family/): Raleway Font Family
*   [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu): Font family based on the Bitstream Vera Fonts
*   [ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid): General-purpose fonts released by Google as part of Android
*   [ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont): Set of free outline fonts covering the Unicode character set
*   [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation): Red Hats Liberation fonts

### Additional Info

#### Packages based on older evolution-data-server

[dexter-contacts-bzr](https://aur.archlinux.org/packages/dexter-contacts-bzr/) and [feedler-bzr](https://aur.archlinux.org/packages/feedler-bzr/) do not build because they are based on evolution-data-server 3.2\. Arch Linux provides version 3.10 which uses a different Vala API.

## Launching Pantheon

### Via a Display Manager

[pantheon-session-bzr](https://aur.archlinux.org/packages/pantheon-session-bzr/) provides a session entry for display managers such as [gdm](https://www.archlinux.org/packages/?name=gdm) or [lightdm](https://www.archlinux.org/packages/?name=lightdm).

**Note:** Either use the bzr version of *cerbere* or add 'gala' to the monitored processes for this to work.

### Via .xinitrc

You can also use `~/.xinitrc` to launch the Pantheon shell. The following code will successfully launch a Pantheon session:

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

**Note:** Pantheon may refuse to start correctly, resulting in errors such as no visible mouse cursor and others. In this case you have to add the window manager 'gala' to the list of monitored processes of cebere. This can be done in `dconf-editor` and should look like [this](http://s0.uploads.im/AvOIT.png). Remember do not run dconf-editor as root, use your local username.

### Autostart applications

Pantheon, when launched via `~/.xinitrc`, does not support XDG autostart. However, there are 3 other ways to achieve this for applications which do not provide a systemd unit:

*   You may add any program to your `~/.xinitrc`, preferably right before the *exec cerbere* line. This is the better choice for one-shot programs.
*   Or you may edit the `org.pantheon.cerbere.monitored-processes` key using *dconf-editor* and add the programs of your choice. This method is best for applications which keep running in the background.
*   Or you may use a program like [dapper](https://aur.archlinux.org/packages/dapper/), [dex-git](https://aur.archlinux.org/packages/dex-git/), or [fbautostart](https://aur.archlinux.org/packages/fbautostart/) to add support for XDG autostart in your `~/.xinitrc`.

**Note:** Keep in mind that applications started via *cerbere* cannot be terminated, they will keep respawning.

## Configuration

Configuring Pantheon is done via [switchboard-bzr](https://aur.archlinux.org/packages/switchboard-bzr/) and its plugs, most are available in the AUR and the custom repo. All pantheon settings can also be altered via *dconf*, they are located in the `org.pantheon` key. Use *dconf-editor* for easy editing.

Part of the configuration is handled by [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) via a dedicated plug, which unfortunately only supports GNOME up to 3.6\. Use [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) itself and [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool) instead.

### Pantheon Files

#### Enable context menu entries

If you want to enable context menu entries such as for [file-roller](https://www.archlinux.org/packages/?name=file-roller) to extract/compress archives, then you have to additionally install [contractor-bzr](https://aur.archlinux.org/packages/contractor-bzr/).

### Terminal

#### Opacity (transparency)

You can set a certain opacity to make Pantheon Terminal (semi-)transparent. Open `dconf-editor` and go to `org.pantheon.terminal.settings.opacity` to set your desired opacity.

## Known Issues

### Indicators not working in wingpanel

Make sure the /etc/xdg/autostart/indicator-[name].desktop file contains Pantheon inside OnlyShowIn=

```
OnlyShowIn=Unity;XFCE;GNOME;Pantheon;

```

**Note:**

*   Indicator support itself is a complex issue, due to discrepancies between Ubuntu and Gnome's differing implementations of KDE's status notification indicators.
*   The pantheon devs now have [their own standard indicators](https://launchpad.net/~wingpanel-devs) for wingpanel.

### Indicator-session menus not working

*   [indicator-session-bzr](https://aur.archlinux.org/packages/indicator-session-bzr/)

This version of indicator-session relies on dbus methods native to Unity for most of its fuctions; it can be made to work by patching out the use of Unity dialogs, such as in [indicator-session-pantheon-bzr](https://github.com/quequotion/pantheon-bzr-qq/tree/master/REDUNDANT/indicator-session-pantheon-bzr)

*   [indicator-session](https://aur.archlinux.org/packages/indicator-session/)

This version of indicator-session fails to interact with the session manager somehow; a (crudely hacked) version that uses systemd/logind instead is available [indicator-session-systemd](https://aur.archlinux.org/packages/indicator-session-systemd/)

*About This Computer*, *Lock* and *Sound Settings* ([indicator-sound](https://aur.archlinux.org/packages/indicator-sound/) or [indicator-sound-pantheon-bzr](https://github.com/quequotion/pantheon-bzr-qq/tree/master/REDUNDANT/indicator-session-pantheon-bzr)) rely on gnome components that may not be installed, such as gnome-control-center and gnome-screensaver.

For *Lock* functionality (including "Ctrl+L" hotkey), replace gnome-screensaver with [light-locker](/index.php/Light-locker "Light-locker") or [XScreenSaver](/index.php/XScreenSaver "XScreenSaver") and [a script that emulates the gnome-screensaver dbus](https://github.com/quequotion/pantheon-bzr-qq/tree/master/EXTRAS/xscreensaver-dbus-screenlock).

### No transparency in pantheon-terminal

Transparency in pantheon-terminal is not yet fully functional with GTK themes other than the elmentaryOS theme. Either use [gtk-theme-elementary](https://aur.archlinux.org/packages/gtk-theme-elementary/) or add [this](http://bazaar.launchpad.net/~elementary-design/egtk/4.x/revision/210) code to your theme.

### White icons in pantheon-files

Currently there seems to be a bug which displays the view icons in the top location in a white colour instead of black. This can be fixed by installing [gtk-theme-elementary-bzr](https://aur.archlinux.org/packages/gtk-theme-elementary-bzr/) or adding the following line to `gtk-widgets.css` or `gtk-widgets.css` of your [gtk-theme-elementary](https://aur.archlinux.org/packages/gtk-theme-elementary/) theme:

```
GtkToolItem { color: @text_color; }

```

### Wingpanel is transparent

Wingpanel is transparent by design when using the elementary GTK theme. It becomes black when a maximized window occupies your screen. However, using other GTK themes will produce a solid panel most of the time.

To achieve the former behavior within other themes just add the following lines to the end of it's css. It is mostly found within `/usr/share/themes/<theme-name>` or `~/.themes/<theme-name>`. Depending on your theme the filename may be `apps.css` or `gtk.css`:

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

### Corrupted graphics in canonical indicators

Indicators behave incorrectly with every theme I have tried. They are very ancient, all of them date back to 2012 because the newer indicators depend on Ubuntu patches, and they should be killed with fire anyway. Wingpanel is doing just that and I hope the next major release will ship their new plugin system.

### Cannot interact with the LightDM Pantheon greeter

You need to delete `/var/lib/lightdm/.pam_environment`. Do note however that this file is a workaround for the following LightDM bug: [https://bugs.launchpad.net/ubuntu/+source/unity-greeter/+bug/1024482](https://bugs.launchpad.net/ubuntu/+source/unity-greeter/+bug/1024482)

## Troubleshooting

### Gala crashes on start

It appears that unconfigured gala tries to use default gnome wallpaper as a background. However, the corresponding file is absent unless you have [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard) installed. Thus, install [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard) to workaround the crash. It is safe to remove this package after you configure pantheon in a way you want.

### How can I add new applications to the dock?

Either drag and drop a desktop file on it, or right click on a running application and select "Keep in dock". You can then reorder icons by drag and drop.

### How can I change the default appearance such as GTK theme, font size, etc?

Install [switchboard-plug-elementary-tweaks-bzr](https://aur.archlinux.org/packages/switchboard-plug-elementary-tweaks-bzr/). Alternatively, use [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool) or see [GTK+](/index.php/GTK%2B "GTK+").

### I do not have any mouse cursor

The 'gala' window manager is most likely not running. [#Via .xinitrc](#Via_.xinitrc) Add 'gala' to the list of cerbere's monitored processes.

### Wingpanel is empty except for Applications

The indicators that are displayed in the wingpanel are split into separate packages. [#Installation](#Installation) Install additional indicators such as [wingpanel-indicator-datetime-bzr](https://aur.archlinux.org/packages/wingpanel-indicator-datetime-bzr/), [indicator-power](https://aur.archlinux.org/packages/indicator-power/) or [indicator-sound](https://aur.archlinux.org/packages/indicator-sound/).