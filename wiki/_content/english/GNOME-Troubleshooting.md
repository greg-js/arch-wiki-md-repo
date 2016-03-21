See [GNOME](/index.php/GNOME "GNOME") for the main article.

## Contents

*   [1 Shell freezes](#Shell_freezes)
*   [2 Incorrect application defaults](#Incorrect_application_defaults)
*   [3 Tracker & Documents do not list any local files](#Tracker_.26_Documents_do_not_list_any_local_files)
*   [4 Unable to add accounts in Empathy and GNOME Online Accounts](#Unable_to_add_accounts_in_Empathy_and_GNOME_Online_Accounts)
*   [5 Cannot change settings in dconf-editor](#Cannot_change_settings_in_dconf-editor)
*   [6 When an extension breaks the shell](#When_an_extension_breaks_the_shell)
*   [7 Extensions do not work after GNOME 3 update](#Extensions_do_not_work_after_GNOME_3_update)
*   [8 Extensions disabled at every system startup](#Extensions_disabled_at_every_system_startup)
*   [9 Keyboard shortcut do not work with only conky running](#Keyboard_shortcut_do_not_work_with_only_conky_running)
*   [10 Unable to apply stored configuration for monitors](#Unable_to_apply_stored_configuration_for_monitors)
*   [11 Consistent cursor theme](#Consistent_cursor_theme)
*   [12 Windows cannot be modified with Alt-Key + mouse-button](#Windows_cannot_be_modified_with_Alt-Key_.2B_mouse-button)
*   [13 Slow loading of system icons/slow GDM login](#Slow_loading_of_system_icons.2Fslow_GDM_login)
*   [14 Artifacts when maximizing windows](#Artifacts_when_maximizing_windows)
*   [15 Tear-free video with Intel HD Graphics](#Tear-free_video_with_Intel_HD_Graphics)
*   [16 Window opens behind other windows when using multiple monitors](#Window_opens_behind_other_windows_when_using_multiple_monitors)
*   [17 Lock button fails to re-enable touchpad](#Lock_button_fails_to_re-enable_touchpad)
*   [18 GNOME Shell keyboard sources menu not visible](#GNOME_Shell_keyboard_sources_menu_not_visible)
*   [19 Mouse cursor missing](#Mouse_cursor_missing)
*   [20 No restart button in session menu when screen is locked](#No_restart_button_in_session_menu_when_screen_is_locked)
*   [21 PulseAudio system-wide causes delay in GNOME and GDM](#PulseAudio_system-wide_causes_delay_in_GNOME_and_GDM)
*   [22 GNOME crashes when trying to reorder applications in the GNOME Shell Dash](#GNOME_crashes_when_trying_to_reorder_applications_in_the_GNOME_Shell_Dash)
*   [23 Setting global Wayland environment with an environment variable](#Setting_global_Wayland_environment_with_an_environment_variable)

## Shell freezes

In the event of a Shell freeze (which might be caused by certain appearance tweaks, malfunctioning extensions or perhaps a lack of available memory) restarting the Shell by pressing `Alt` + `F2` and then entering **r** may not be possible.

In this case, try switching to another TTY (**Ctrl** + **Alt** + **F2**) and entering the following command: `pkill -HUP gnome-shell`. It may take a few seconds before the Shell successfully restarts. Restarting the shell in this fashion should not log the user out but it is a good idea to try and ensure that all work is saved anyway.

If this fails, the [Xorg](/index.php/Xorg "Xorg") server will need to be restarted either by: `pkill X` for console logins or: `systemctl restart gdm` for GDM logins. Bear in mind that restarting the Xorg server will log the user out so try to ensure that all work is saved before attempting this.

## Incorrect application defaults

When installing applications for the first time you may find that GNOME has the wrong application associated to a certain protocols - for instance, *easytag* becomes the folder handler instead of [GNOME Files](/index.php/GNOME_Files "GNOME Files").

For GNOME Files see the following page: [GNOME Files#Files is no longer the default file manager](/index.php/GNOME_Files#Files_is_no_longer_the_default_file_manager "GNOME Files").

For Document Viewer, run the following command:

```
$ xdg-mime default evince.desktop application/pdf

```

For other applications, default handler settings are detailed on the following page: [Default applications](/index.php/Default_applications "Default applications").

Optionally, you can [install](/index.php/Install "Install") [gnome-defaults-list](https://aur.archlinux.org/packages/gnome-defaults-list/). It will place your configuration file at `/etc/gnome/defaults.list`.

## Tracker & Documents do not list any local files

In order for Tracker (and, therefore, Documents) to detect your local files, they must be stored in an [XDG compliant directory](http://standards.freedesktop.org/basedir-spec/basedir-spec-latest.html) (such as 'Documents' or 'Music'). For more information, see [Xdg user directories](/index.php/Xdg_user_directories "Xdg user directories").

You can also configure Tracker to recursively search inside specific directories such as your home directory. These settings can be made using `tracker-preferences`.

## Unable to add accounts in Empathy and GNOME Online Accounts

Empathy, the engine behind integrated messaging, GNOME Online Accounts, and all other system settings based on messaging accounts will not function correctly unless the [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/) group of packages or at least one of the backends ([telepathy-gabble](https://www.archlinux.org/packages/?name=telepathy-gabble), or [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze), for example) is [installed](/index.php/Install "Install"). View descriptions of *telepathy* components on the [freedesktop.org telepathy wiki](http://telepathy.freedesktop.org/wiki/Components).

**Note:** [Avahi](/index.php/Avahi "Avahi") daemon is required for connecting with the People Nearby account, and also in order for some desktop extensions to work correctly like [Chat Status](https://extensions.gnome.org/extension/746/chat-status/)

## Cannot change settings in dconf-editor

When one cannot set settings in [dconf](https://www.archlinux.org/packages/?name=dconf), it is possible their dconf user settings are corrupt. In this case it is best to delete the user dconf files in `~/.config/dconf/user*` and set the settings in dconf-editor after.

## When an extension breaks the shell

When enabling shell extensions causes GNOME breakage, you should first remove the *user-theme* and *auto-move-windows* extensions from their installation directory.

The installation directory could be one of `~/.local/share/gnome‑shell/extensions`, `/usr/share/gnome‑shell/extensions` or `/usr/local/share/gnome‑shell/extensions`. Removing these two extension-containing folders may fix the breakage. Otherwise, isolate the problem extension with trial‑and‑error.

Removing or adding an extension-containing folder to the aforementioned directories removes or adds the corresponding extension to your system. Details on GNOME Shell extensions are available at the [GNOME web site.](https://live.gnome.org/GnomeShell/Extensions)

If you have trouble with uninstalling an extension via [extensions.gnome.org/local](https://extensions.gnome.org/local/), then probably they have been installed as system-wide extensions with the [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) package. Removing the package again obviously affects all user accounts.

## Extensions do not work after GNOME 3 update

**Note:** Please bear in mind that whilst the methods below will allow you to **try** and activate an extension with an unsupported version of GNOME Shell, it is by no means a guarantee that the extension will work successfully. The most likely outcome of trying to activate such an extension is that GNOME Shell will crash and then restart.

Before trying the workarounds below, check if an update is available for the extension by visiting [extensions.gnome.org/local](https://extensions.gnome.org/local).

If there is no update for your current GNOME version yet, use the following command to disable version validation for extensions:

```
$ gsettings set org.gnome.shell disable-extension-version-validation true

```

Alternatively, you could modify the extension itself, changing the supported shell version to satisfy the version validation. See the method below.

Locate the folder where your extensions are installed. It might be `~/.local/share/gnome-shell/extensions` or `/usr/share/gnome-shell/extensions`.

Edit each occurrence of `metadata.json` which appears in each extension sub-folder.

| Insert: | `"shell-version": ["3.x"]` |
| Instead of (for example): | `"shell-version": ["3.4"]` |

`"3.x"` indicates the extension works with every shell version. If it breaks, you will know to change it back.

## Extensions disabled at every system startup

This is a known bug [[1]](https://bugs.launchpad.net/ubuntu/+source/gnome-shell/+bug/1236749). Until it is fixed, the following workaround can be helpful.

Get the active extensions:

```
$ gsettings get org.gnome.shell enabled-extensions

```

Create a [desktop entry](/index.php/Desktop_entry "Desktop entry") in `~/.config/autostart/restore-extensions.desktop`, replacing `active_extensions` with the output from the above command:

```
[Desktop Entry]
Type=Application
Exec=gsettings set org.gnome.shell enabled-extensions *active_extensions*
Hidden=false
NoDisplay=false
X-GNOME-Autostart-enabled=true
Name=Restore Extensions
Comment=Restore enabled extensions on login

```

## Keyboard shortcut do not work with only conky running

The GNOME shell keyboard shortcuts like `Alt+F2`, `Alt+F1`, and the media key shortcuts do not work if conky is the only program running. However, if another application like *gedit* is running, then the keyboard shortcuts work.

Solution: edit `.conkyrc`

```
own_window yes
own_window_transparent yes
own_window_argb_visual yes
own_window_type dock
own_window_class Conky
own_window_hints undecorated,below,sticky,skip_taskbar,skip_pager

```

## Unable to apply stored configuration for monitors

If you encounter this message try to disable the *xrandr* `gnome-settings-daemon plugin`:

```
$ dconf write /org/gnome/settings-daemon/plugins/xrandr/active false

```

## Consistent cursor theme

See [Cursor themes#Desktop environments](/index.php/Cursor_themes#Desktop_environments "Cursor themes").

## Windows cannot be modified with Alt-Key + mouse-button

In GNOME 3.6 and above, the mouse button modifier (the key that allows you to drag a window from a location other than the titlebar) is the `Super` key instead of the `Alt` key which was used in the past. The change was made in response to the following [bug report](https://bugzilla.gnome.org/show_bug.cgi?id=607797).

To change the mouse button modifier back to the `Alt` key, execute the following:

```
$ gsettings set org.gnome.desktop.wm.preferences mouse-button-modifier '<Alt>'  

```

**Note:** It is not possible to change this with *System settings* > *Keyboard* > *Shortcuts*

## Slow loading of system icons/slow GDM login

Problems with the loading of system icons, such the ones in the title bar of Files, might be solved by executing the following command:

```
# gdk-pixbuf-query-loaders --update-cache

```

Running the aforementioned command may also fix repeated occurrences of the "Oh no! Something has gone wrong!" error screen and/or very slow loading and login with GDM as described in the following [forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1414157).

## Artifacts when maximizing windows

Maximizing windows may cause artifacts as of GNOME 3.12.0 - see the following [forum thread](https://bbs.archlinux.org/viewtopic.php?id=183617) and [bug report](https://bugzilla.gnome.org/show_bug.cgi?id=728385). A solution is detailed in the following section: [#Tear-free video with Intel HD Graphics](#Tear-free_video_with_Intel_HD_Graphics).

## Tear-free video with Intel HD Graphics

	DRI3

According to [this bug report](https://bugzilla.gnome.org/show_bug.cgi?id=711028#c2), DRI3 includes the `buffer_age` extension that allows GNOME Shell's Mutter compositor to sync windows to vblank in an efficient way. [Enable](/index.php/Intel_Graphics#Direct_Rendering_Infrastructure_3_.28DRI3.29 "Intel Graphics") it in the Xorg driver. You can change `AccelMethod` to your preference in the configuration file created, but the line must be included when the file is created; otherwise, `gnome-session` will crash upon login in a non-Wayland session.

	Intel TearFree

Enabling the [Xorg Intel TearFree option](/index.php/Intel_Graphics#Tear-free_video "Intel Graphics") is a known workaround for tearing problems on Intel adapters. However, the way this option acts makes it redundant with the use of a compositor (it increases memory consumption and lowers performance, see [the original bug report's final comment](https://bugs.freedesktop.org/show_bug.cgi?id=37686#c123)).

	Mutter tweaks

**Note:** This workaround has been [reported](https://bugzilla.gnome.org/show_bug.cgi?id=711028#c0) to have side effects and may not fix tearing in all cases.

GNOME Shell's Mutter compositor has a tweak known to address tearing problems (see [the original suggestion for this fix](https://bugzilla.gnome.org/show_bug.cgi?id=657071#c1) and its mention in [the Freedesktop bug report](https://bugs.freedesktop.org/show_bug.cgi?id=37686#c59)). To enable this tweak, append the following line to `/etc/environment`: `CLUTTER_PAINT=disable-clipped-redraws:disable-culling`. Then restart the Xorg server.

## Window opens behind other windows when using multiple monitors

This is possibly a bug in GNOME Shell which causes new windows to open behind others. To fix this issue, one can run the following command:

```
$ gsettings set org.gnome.shell.overrides workspaces-only-on-primary false

```

## Lock button fails to re-enable touchpad

Some laptops have a touchpad lock button that disables the touchpad so that users can type without worrying about touching the touchpad. Currently, it appears that although GNOME can lock the touchpad by pressing this button, it cannot unlock it. If the touchpad gets locked you can run the following to unlock it:

```
$ xinput set-prop "SynPS/2 Synaptics TouchPad" "Device Enabled" 1

```

## GNOME Shell keyboard sources menu not visible

A menu showing the keyboard input sources (for example 'en' for an English keyboard layout) should be visible next to the status area containing icons for network, volume and power sources. If the keyboard sources menu is not visible, this is probably because you have configured your [Xorg](/index.php/Xorg "Xorg") keyboard layout in a way which GNOME does not recognise.

To ensure that the menu is visible, remove any Xorg keyboard configuration you might have created and set the keyboard locale using [localectl](/index.php/Keyboard_configuration_in_Xorg#Using_localectl "Keyboard configuration in Xorg").

Upon running the command and then logging out, you should find that the keyboard input sources menu is visible in GDM and in the GNOME Shell desktop. See [Input sources in GNOME](http://blogs.gnome.org/mclasen/2012/09/21/input-sources-in-gnome/) for more information.

## Mouse cursor missing

When using a separate [window manager](/index.php/Window_manager "Window manager") with *gnome-settings-daemon*, the mouse cursor may vanish. Run:

```
$ gsettings set org.gnome.settings-daemon.plugins.cursor active false

```

## No restart button in session menu when screen is locked

If [XScreenSaver](/index.php/XScreenSaver "XScreenSaver") is installed, ensure that it is not running at startup, see [GNOME#Startup applications](/index.php/GNOME#Startup_applications "GNOME").

## PulseAudio system-wide causes delay in GNOME and GDM

If you are running [PulseAudio](/index.php/PulseAudio "PulseAudio") in system-wide mode, the PulseAudio 7.0 upgrade breaks [GDM](/index.php/GDM "GDM") and GNOME. See [this forum post](https://bbs.archlinux.org/viewtopic.php?id=203051) for more information.

## GNOME crashes when trying to reorder applications in the GNOME Shell Dash

The dash is the "toolbar" that appears, by default, [on the left](https://en.wikipedia.org/wiki/GNOME_Shell#Design_components "wikipedia:GNOME Shell") when you click Activities. Applications can be reordered in the dash by dragging and dropping. If this fails, and/or causes GNOME to crash, try [changing your icon theme](https://bbs.archlinux.org/viewtopic.php?id=171689).

## Setting global Wayland environment with an environment variable

Setting a global Wayland environment, by running `env GDK_BACKEND=wayland gnome-session --session=gnome-wayland`, currently does not work - *gnome-session* will exit immediately. Instead, use `export GDK_BACKEND='wayland,x11'` in your bash profile, or use `env GDK_BACKEND='wayland,x11' gnome-session --session=gnome-wayland` on the command line. But in general, neither of these environment settings are necessary, and running `gnome-session` with the `--session=gnome-wayland` switch is sufficient. Without the `GDK_BACKEND` environment variable, the GNOME Application must be "Wayland aware" to run as a Wayland application, or default to running on Xwayland otherwise. See also `GDK_BACKEND` under GNOME [Environment variables](https://developer.gnome.org/gtk3/stable/gtk-running.html).