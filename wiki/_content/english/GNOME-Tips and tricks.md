See [GNOME](/index.php/GNOME "GNOME") for the main article.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Keyboard](#Keyboard)
    *   [1.1 Turn on NumLock on login](#Turn_on_NumLock_on_login)
    *   [1.2 Hotkey alternatives](#Hotkey_alternatives)
    *   [1.3 Keyboard switch with command](#Keyboard_switch_with_command)
    *   [1.4 XkbOptions keyboard options](#XkbOptions_keyboard_options)
    *   [1.5 De-bind Windows key](#De-bind_Windows_key)
*   [2 Disks](#Disks)
*   [3 Hiding applications from the menu](#Hiding_applications_from_the_menu)
*   [4 Screencast recording](#Screencast_recording)
*   [5 Screenshot](#Screenshot)
*   [6 Log out delay](#Log_out_delay)
*   [7 Disable animations](#Disable_animations)
*   [8 Retina (HiDPI) display support](#Retina_(HiDPI)_display_support)
*   [9 Passwords and keys (PGP Keys)](#Passwords_and_keys_(PGP_Keys))
*   [10 Terminal](#Terminal)
    *   [10.1 Change default terminal size](#Change_default_terminal_size)
    *   [10.2 New terminals adopt current directory](#New_terminals_adopt_current_directory)
    *   [10.3 Pad the terminal](#Pad_the_terminal)
    *   [10.4 Disable blinking cursor](#Disable_blinking_cursor)
    *   [10.5 Disable confirmation window when closing Terminal](#Disable_confirmation_window_when_closing_Terminal)
*   [11 Middle mouse button](#Middle_mouse_button)
*   [12 Enable button and menu icons](#Enable_button_and_menu_icons)
*   [13 Use custom colours and gradients for desktop background](#Use_custom_colours_and_gradients_for_desktop_background)
*   [14 Transitioning backgrounds](#Transitioning_backgrounds)
*   [15 Custom GNOME sessions](#Custom_GNOME_sessions)
*   [16 Redirect certain URLs to specific web browsers](#Redirect_certain_URLs_to_specific_web_browsers)
*   [17 Removing film holes/film strip from video thumbnails in Nautilus](#Removing_film_holes/film_strip_from_video_thumbnails_in_Nautilus)
*   [18 Prevent GNOME Software from downloading updates](#Prevent_GNOME_Software_from_downloading_updates)
*   [19 Increase volume above and beyond 100%](#Increase_volume_above_and_beyond_100%)
*   [20 Adjust volume in smaller steps](#Adjust_volume_in_smaller_steps)
*   [21 Show volume sound percentage next to top panel icon](#Show_volume_sound_percentage_next_to_top_panel_icon)
*   [22 Hybrid Sleep on laptop lid closing action](#Hybrid_Sleep_on_laptop_lid_closing_action)

## Keyboard

### Turn on NumLock on login

See [Activating Numlock on Bootup#GNOME](/index.php/Activating_Numlock_on_Bootup#GNOME "Activating Numlock on Bootup")

### Hotkey alternatives

A lot of hotkeys can be changed via system settings menu. For example, to re-enable the show desktop keybinding:

*System settings* > *Keyboard* > *Shortcuts* > *Navigation* > *Hide all normal windows*

However, certain hotkeys cannot be changed directly via system settings. In order to change these keys, use *dconf-editor*. An example of particular note is the hotkey `Alt-` + ``` (the key above `Tab` on US keyboard layouts). In GNOME Shell it is pre-configured to cycle through windows of an application, however it is also a hotkey often used in the [Emacs](/index.php/Emacs "Emacs") editor. It can be changed by opening *dconf-editor* and modifying the *switch-group* key found in `org.gnome.desktop.wm.keybindings`.

It is possible to manually change the keys via an application's so-called **accel** map file. Where it is to be found is up to the application: For instance, Thunar's is at `~/.config/Thunar/accels.scm`, whereas Files's is located at `~/.config/nautilus/accels` and `~/.gnome2/accels/nautilus` on old release.

The file should contain a list of possible hotkeys, each unchanged line commented out with a leading ";" that has to be removed for a change to become active. For example to replace the hotkey used by Files to move files to the trash folder, change the line:

```
; (gtk_accel_path "<Actions>/DirViewActions/Trash" "<Primary>Delete")

```

to this:

```
(gtk_accel_path "<Actions>/DirViewActions/Trash" "Delete")

```

The file is regenerated regularly so do not comment the file. The uncommented line will stay but every comment you add will be lost.

### Keyboard switch with command

To change the default keyboard shortcut **Win** + **Space** to another hot key:

For example to change to *Alt*+*Shift*: open Gnome-Tweak-Tool (or Keyboard Settings, in GNOME 3.16) and set *Typing* > *Modifiers-only input sources* > *select Alt-shift*. For more information see also the forum [thread](https://bbs.archlinux.org/viewtopic.php?id=152127).

### XkbOptions keyboard options

Using the **dconf-editor**, navigate to the key named `org.gnome.desktop.input-sources.xkb-options` and add desired XkbOptions (e.g. *caps:swapescape*) to the list.

See `/usr/share/X11/xkb/rules/xorg` for all XkbOptions and `/usr/share/X11/xkb/symbols/*` for the respective descriptions.

**Note:** To enable the `Ctrl+Alt+Backspace` combination to terminate Xorg, use [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks). Within the **Tweak Tool**, navigate to *Typing > Key sequence to kill the X server* and select the option `Ctrl+Alt+Backspace` from the dropdown menu.

### De-bind Windows key

By default, the 'Windows key' will open the GNOME Shell overview mode. You can unbind this key by running the command below

```
$ gsettings set org.gnome.mutter overlay-key 'Foo'

```

## Disks

GNOME provides a disk utility to manipulate storage drive settings. These are some of its features:

*   **Enable write cache** is a feature that most hard drives provide. Data is cached and allocated at chosen times to improve system performance. Not recommended unless the computer has a backup battery pack or is a laptop as data would be lost on power failure.

	*Settings* > *Drive Settings* > *Write Cache* > **On**

*   **Automatic Mount Options** can mount drives and partitions that are GPT based - will use default, recommended options.

**Warning:** This setting erases related [fstab](/index.php/Fstab "Fstab") entries

	*Partition Settings* > *Edit Mount Options* > *Automatic Mount Options* > **On**

## Hiding applications from the menu

**Tip:**

*   Desktop entries can be hidden by editing the `.desktop` files themselves. See [Desktop entries#Hide desktop entries](/index.php/Desktop_entries#Hide_desktop_entries "Desktop entries").
*   [Menulibre](https://aur.archlinux.org/packages/Menulibre/) provides a menu editor without GNOME dependencies.

Use the *Main Menu* application (provided by the [alacarte](https://www.archlinux.org/packages/?name=alacarte) package) to hide any applications you do not wish to show in the menu.

## Screencast recording

GNOME features built-in screencast recording with the `Ctrl+Shift+Alt+r` key combination. A red circle is displayed in the bottom right corner of the screen when the recording is in progress. After the recording is finished, a file named `Screencast from %d%u-%c.webm` is saved in the `Videos` directory. In order to use the screencast feature the gst plugins need to be installed.

**Note:** The recording filename may translated depending on your system's language.

## Screenshot

[gnome-screenshot](https://www.archlinux.org/packages/?name=gnome-screenshot) by default saves the image in the directory of the last save, which you can query:

```
$ gsettings get org.gnome.gnome-screenshot last-save-directory

```

Instead of using the above directory, you can set an auto save directory. e.g. for automatically saving screenshots to the `*user*`'s desktop directory:

```
$ gsettings set org.gnome.gnome-screenshot auto-save-directory file:///home/*user*/Desktop

```

Check the [gnome-screenshot(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gnome-screenshot.1) man page for more options.

## Log out delay

To eliminate the default 60 second delay when logging out:

```
$ gsettings set org.gnome.SessionManager logout-prompt false

```

## Disable animations

To disable Shell animations (such as "Show Applications" and the wave animation in the top left activities hot corner), run:

```
$ gsettings set org.gnome.desktop.interface enable-animations false

```

or via [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks), in *General* tab, switch *Animations* to off.

## Retina (HiDPI) display support

GNOME introduced HiDPI support in version 3.10\. If your display does not provide the correct screen size through EDID, this can lead to incorrectly scaled UI elements. As a workaround you can open *dconf-editor* and find the key `scaling-factor` in `org.gnome.desktop.interface`. Set it to `1` to get the standard scale.

Also see [HiDPI](/index.php/HiDPI "HiDPI").

## Passwords and keys (PGP Keys)

You can use the Passwords and Keys program [seahorse](https://www.archlinux.org/packages/?name=seahorse) to create a PGP key as it is a front end for [GnuPG](/index.php/GnuPG "GnuPG") and installs it as dependency. This may be useful in the future (for instance if to encrypt a file). Create a key as shown below (the process may take about 10 minutes):

*File* > *New* > *PGP Key* > *Name* > *Email* > *Defaults* > *Passphrase*.

## Terminal

### Change default terminal size

The default size of a new terminal can be adjusted in the menu *Edit > Profile preferences* .

### New terminals adopt current directory

By default new terminals open in the `$HOME` directory. To have new terminals adopt the current working directory: `source /etc/profile.d/vte.sh`. Add the command to the shell configuration to retain the behaviour. [[1]](http://unix.stackexchange.com/questions/93476/gnome-terminal-keep-track-of-directory-in-new-tab)

### Pad the terminal

To pad the terminal (create a small, invisible border between the window edges and the terminal contents) create the file below:

 `~/.config/gtk-3.0/gtk.css` 
```
vte-terminal,
terminal-window {
    padding: 10px 10px 10px 10px;
    -vte-terminal-inner-border: 10px 10px 10px 10px;
}
```

### Disable blinking cursor

To disable the blinking cursor in GNOME 3.8 and above use:

```
$ gsettings set org.gnome.desktop.interface cursor-blink false

```

To disable the blinking cursor in Terminal only use:

```
$ gsettings set org.gnome.Terminal.Legacy.Profile:/org/gnome/terminal/legacy/profiles:/:$(gsettings get org.gnome.Terminal.ProfilesList default | tr -d \')/ cursor-blink-mode off

```

Note that `gnome-settings-daemon`, from the package of the same name, must be running for this and other settings changes to take effect in GNOME applications - see [GNOME#Configuration](/index.php/GNOME#Configuration "GNOME").

### Disable confirmation window when closing Terminal

The Terminal will always display a confirmation window when trying to close the window while one is logged in as root. To avoid this, execute the following:

```
$ gsettings set org.gnome.Terminal.Legacy.Settings confirm-close false

```

## Middle mouse button

By default, GNOME 3 disables middle mouse button emulation regardless of [Xorg](/index.php/Xorg "Xorg") settings (**Emulate3Buttons**). To enable middle mouse button emulation use:

```
$ gsettings set org.gnome.settings-daemon.peripherals.mouse middle-button-enabled true

```

## Enable button and menu icons

Since GTK 3.10, the GSettings key 'menus-have-icons' has been deprecated. Icons in buttons and menus can still be enabled by setting the following overrides:

```
$ gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/ButtonImages': <1>, 'Gtk/MenuImages': <1>}"

```

## Use custom colours and gradients for desktop background

To use custom colours and gradients for your desktop background, you will first need to set either a transparent picture or else a non-existent picture as your desktop background. For instance, the command below will set a non-existent picture as the background.

```
$ gsettings set org.gnome.desktop.background picture-uri none

```

At this point, the desktop background should be a flat colour - the default colour setting is for a deep blue.

For a different flat colour you need only change the primary colour setting:

```
$ gsettings set org.gnome.desktop.background primary-color <my color>

```

where <my color> is a hex value (such as *ffffff* for white).

For a colour gradient, you will also need to change secondary colour setting `org.gnome.desktop.background secondary-color` and select a shading type. For instance, if you want a horizontal gradient, execute the following:

```
$ gsettings set org.gnome.desktop.background color-shading-type horizontal

```

If you are using a transparent picture as your background, you can set the opacity by executing the following:

```
$ gsettings set org.gnome.desktop.background picture-opacity <value>

```

where value is a number between 1 and 100 (100 for maximum opacity).

## Transitioning backgrounds

GNOME can transition between different wallpapers at specific time intervals. This is done by creating an XML file specifying the pictures to be used and the time interval. For more information on creating such files, see the following [article](http://www.linuxjournal.com/content/create-custom-transitioning-background-your-gnome-228-desktop).

Alternatively, a number of tools are available to automate the process:

*   **mkwlppr** — This script creates XML files that can act as dynamic wallpapers for GNOME by referring to multiple wallpapers.

	[http://pastebin.com/019G2rCy](http://pastebin.com/019G2rCy) || see [mkwlppr](http://pastebin.com/019G2rCy)

For setting the XML file as the default background, see [GNOME#Lock screen and background](/index.php/GNOME#Lock_screen_and_background "GNOME").

## Custom GNOME sessions

It is possible to create custom GNOME sessions which use the GNOME session manager but start different sets of components ([Openbox](/index.php/Openbox "Openbox") with [tint2](/index.php/Tint2 "Tint2") instead of GNOME Shell for example).

Two files are required for a custom GNOME session: a session file in `/usr/share/gnome-session/sessions/` which defines the components to be started and a [desktop entry](/index.php/Desktop_entry "Desktop entry") in `/usr/share/xsessions` which is read by the [display manager](/index.php/Display_manager "Display manager"). An example session file is provided below:

 `/usr/share/gnome-session/sessions/gnome-openbox.session` 
```
[GNOME Session]
Name=GNOME Openbox
RequiredComponents=openbox;tint2;gnome-settings-daemon;

```

And an example desktop file:

 `/usr/share/xsessions/gnome-openbox.desktop` 
```
[Desktop Entry]
Name=GNOME Openbox
Exec=gnome-session --session=gnome-openbox

```

**Note:** GNOME Session calls upon the `.desktop` files of each of the components to be started. If a component you wish to start does not provide a `.desktop` file, you must create a suitable desktop entry in a directory such as `/usr/local/share/applications`.

## Redirect certain URLs to specific web browsers

This shows how to use [Chromium](/index.php/Chromium "Chromium") for certain types of URLs while maintaining [Firefox](/index.php/Firefox "Firefox") as default browser for all other tasks.

Make sure [pcre](https://www.archlinux.org/packages/?name=pcre) is [installed](/index.php/Install "Install"), to use *pcregrep*.

Setup custom *xdg-open*:

 `/usr/local/bin/xdg-open` 
```
#!/bin/bash
DOMAIN_LIST_FILE=~/'domains.txt'
OTHER_BROWSER='/usr/bin/chromium-browser'
BROWSER_OPTIONS='' # Optional, for command line options passed to browser
XDG_OPEN='/usr/bin/xdg-open'
DEFAULT_BROWSER='/usr/bin/firefox'

if echo "$1" | pcregrep -q '^https?://'; then
    matching=0
    while read domain; do
	if echo "$1" | pcregrep -q "^https?://${domain}"; then
	    matching=1
	    break
	fi
    done < "$DOMAIN_LIST_FILE"

    if [[ $matching -eq 1 ]]; then
	"$OTHER_BROWSER" $BROWSER_OPTIONS ${*}
	exit 0
    fi

    "$DEFAULT_BROWSER" ${*}
    exit 0
else
    "$XDG_OPEN" ${*}
fi

```

Configure domains for redirect to *Chromium*:

 `$HOME/domains.txt` 
```
stackexchange.com
stackoverflow.com
superuser.com
www.youtube.com
github.com

```

Setup *xdg-open web* as desktop application:

 `$HOME/.local/share/applications/xdg-open-web.desktop` 
```
[Desktop Entry]
Version=1.0
Name=xdg-open web
GenericName=Web Browser
Exec=xdg-open %u
Terminal=false
Type=Application
MimeType=text/html;text/xml;application/xhtml+xml;application/vnd.mozilla.xul+xml;text/mml;x-scheme-handler/http;x-scheme-handler/https;
StartupNotify=true
Categories=Network;WebBrowser;
Keywords=web;browser;internet;
Actions=new-window;new-private-window;

```

```
$ update-desktop-database $HOME/.local/share/applications/

```

Set *xdg-open web* as default Web application in GNOME settings: Go to *GNOME Settings > Details > Default Applications* and set *Web* to *xdg-open web*.

## Removing film holes/film strip from video thumbnails in Nautilus

Nautilus (Files) overlays the film holes/film strip effect on video thumbnails since Gnome 3.12\. To remove or override this effect, the environment variable `G_RESOURCE_OVERLAYS` can be used to reference the path of a compiled resource (in this instance `filmholes.png`) and specify the path for the relevant overlay. This environment variable has only been available since GLib 2.50 and will have no effect on versions before this.

Extract `filmholes.png` from Nautilus.

```
gresource extract /usr/bin/nautilus /org/gnome/nautilus/icons/filmholes.png > filmholes.png

```

Edit `filmholes.png` using your preferred editor and remove the film effect from the image, leaving the transparency and dimensions intact, then overwriting the extracted image.

Copy or move the extracted image where desired, such as `/usr/share/icons/` and edit `~/.profile`, adding the following export, changing `/usr/share/icons/` as needed to the location you placed the file.

```
export G_RESOURCE_OVERLAYS=/org/gnome/nautilus/icons/filmholes.png=/usr/share/icons/filmholes.png

```

If [ffmpegthumbnailer](https://www.archlinux.org/packages/?name=ffmpegthumbnailer) has been installed as a dependency for another file manager that may generate thumbnails, the `Exec` line in `/usr/share/thumbnailers/ffmpegthumbnailer.thumbnailer` should be modified removing the `-f` flag.

To ensure that no thumbnails remain that may already have the film effect embedded, remove the thumbnail cache.

```
rm -r ~/.cache/thumbnails

```

Log out and back in to your session and you should no longer have the film holes/film strip effect on your thumbnails in Nautilus.

## Prevent GNOME Software from downloading updates

By default [gnome-software](https://www.archlinux.org/packages/?name=gnome-software) will download updated packages from the Arch Linux repositories. This forces GNOME Software to refresh the package lists for *pacman* automatically. This is the equivalent to `pacman -Sy`. If the user ignores the GNOME software update prompt, but does install a new package, that will result in [partial upgrades](/index.php/Partial_upgrades "Partial upgrades"), which are **unsupported**. To prevent GNOME Software from refreshing the package lists set the following dconf setting:

```
$ gsettings set org.gnome.software download-updates false

```

## Increase volume above and beyond 100%

Install the extension [volume mixer](https://extensions.gnome.org/extension/858/volume-mixer/). Then use the mouse to scroll above the volume icon in the top panel to increase the volume above and beyond 100%.

## Adjust volume in smaller steps

By default, pressing the keyboard's volume keys adjusts the volume by 6%. If smaller steps are desired, the shortcut *Shift + Volume Key Up/Down* adjusts volume in 2% steps.

## Show volume sound percentage next to top panel icon

Install the extension [sound percentage](https://github.com/maoschanz/sound-percentage-gs-extension) to display the current output volume level next to the sound icon in the top panel.

## Hybrid Sleep on laptop lid closing action

Follow below commands to trigger [Hybrid Sleep](/index.php/Power_management/Suspend_and_hibernate "Power management/Suspend and hibernate") when closing the lid of the laptop. Read [here](https://www.reddit.com/r/gnome/comments/97688y/can_gnome_trigger_hybrid_sleep_on_laptop_lid/) for further information.

```
   mkdir --parents /etc/systemd/logind.conf.d
   printf '%s
' '[Login]' 'HandleLidSwitch=hybrid-sleep' >/etc/systemd/logind.conf.d/50-local.conf
   systemctl restart systemd-logind.conf

```