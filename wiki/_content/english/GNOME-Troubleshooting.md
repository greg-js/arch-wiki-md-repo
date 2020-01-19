See [GNOME](/index.php/GNOME "GNOME") for the main article.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Shell freezes](#Shell_freezes)
*   [2 Shell segfaults](#Shell_segfaults)
*   [3 Incorrect application defaults](#Incorrect_application_defaults)
*   [4 Tracker & Documents do not list any local files](#Tracker_&_Documents_do_not_list_any_local_files)
*   [5 Unable to add accounts in Empathy and GNOME Online Accounts](#Unable_to_add_accounts_in_Empathy_and_GNOME_Online_Accounts)
*   [6 Empathy does not use GNOME Online Accounts](#Empathy_does_not_use_GNOME_Online_Accounts)
*   [7 GNOME Online Accounts settings page does not show properly](#GNOME_Online_Accounts_settings_page_does_not_show_properly)
*   [8 Cannot change settings in dconf-editor](#Cannot_change_settings_in_dconf-editor)
*   [9 When an extension breaks the shell](#When_an_extension_breaks_the_shell)
*   [10 Extensions do not work after GNOME 3 update](#Extensions_do_not_work_after_GNOME_3_update)
*   [11 Keyboard shortcut do not work with only conky running](#Keyboard_shortcut_do_not_work_with_only_conky_running)
*   [12 Unable to apply stored configuration for monitors](#Unable_to_apply_stored_configuration_for_monitors)
*   [13 Consistent cursor theme](#Consistent_cursor_theme)
*   [14 Windows cannot be modified with Alt-Key + mouse-button](#Windows_cannot_be_modified_with_Alt-Key_+_mouse-button)
*   [15 Slow loading of system icons/slow GDM login](#Slow_loading_of_system_icons/slow_GDM_login)
*   [16 Artifacts when maximizing windows](#Artifacts_when_maximizing_windows)
*   [17 Tear-free video with Intel HD Graphics](#Tear-free_video_with_Intel_HD_Graphics)
*   [18 Window opens behind other windows when using multiple monitors](#Window_opens_behind_other_windows_when_using_multiple_monitors)
*   [19 Lock button fails to re-enable touchpad](#Lock_button_fails_to_re-enable_touchpad)
*   [20 GNOME Shell keyboard sources menu not visible](#GNOME_Shell_keyboard_sources_menu_not_visible)
*   [21 Mouse cursor missing](#Mouse_cursor_missing)
*   [22 No restart button in session menu when screen is locked](#No_restart_button_in_session_menu_when_screen_is_locked)
*   [23 PulseAudio system-wide causes delay in GNOME and GDM](#PulseAudio_system-wide_causes_delay_in_GNOME_and_GDM)
*   [24 GNOME crashes when trying to reorder applications in the GNOME Shell Dash](#GNOME_crashes_when_trying_to_reorder_applications_in_the_GNOME_Shell_Dash)
*   [25 Gnome Crashes while installing gnome-extra](#Gnome_Crashes_while_installing_gnome-extra)
*   [26 No H264 Video in Gnome Video Player (Totem)](#No_H264_Video_in_Gnome_Video_Player_(Totem))
*   [27 No suspend on LID closure](#No_suspend_on_LID_closure)
*   [28 gnome-shell / gnome-session crashes on session startup](#gnome-shell_/_gnome-session_crashes_on_session_startup)
*   [29 Low OpenGL performance and stuttering](#Low_OpenGL_performance_and_stuttering)
*   [30 GNOME Wayland session not available](#GNOME_Wayland_session_not_available)
*   [31 gnome-control-center is empty and does not list any categories](#gnome-control-center_is_empty_and_does_not_list_any_categories)
*   [32 Gnome freezes for a second after using a Function (Fn) key shortcut](#Gnome_freezes_for_a_second_after_using_a_Function_(Fn)_key_shortcut)
*   [33 Zoom in/out keyboard shortcuts don't work on some apps](#Zoom_in/out_keyboard_shortcuts_don't_work_on_some_apps)

## Shell freezes

In the event of a Shell freeze (which might be caused by certain appearance tweaks, malfunctioning extensions or perhaps a lack of available memory) restarting the Shell by pressing `Alt` + `F2` and then entering **r** may not be possible.

In this case, try switching to another TTY (**Ctrl** + **Alt** + **F2**) and entering the following command: `pkill -HUP gnome-shell`. It may take a few seconds before the Shell successfully restarts. On X11 restarting the shell in this fashion should not log the user out but it is a good idea to try and ensure that all work is saved anyway; on Wayland (currently the default) restarting the shell kills the whole session, so everything will be lost.

If this fails, the [Xorg](/index.php/Xorg "Xorg") server will need to be restarted either by: `pkill X` for console logins or: `systemctl restart gdm` for GDM logins. Bear in mind that restarting the Xorg server will log the user out so try to ensure that all work is saved before attempting this.

## Shell segfaults

If you experience gnome-shell disappearing and reappearing, it means that it has segfaulted (probably because of an extension). Gnome-shell extensions use javascript; to enable debugging of extensions, it is necessary to

1) rebuild [gjs](https://www.archlinux.org/packages/?name=gjs) with the following changes to the PKGBUILD:

```
--- PKGBUILD (old)
+++ PKGBUILD (new)
@@ -29,10 +29,13 @@
 build() {
   cd $pkgname
+  export CXXFLAGS='-g -O0'
+  export CPPFLAGS='-D_FORITFY_SOURCE=0'
   ./configure \
+    --enable-debug-symbols=-gdwarf-2 \
     --prefix=/usr \
     --libexecdir=/usr/lib \
     --disable-static \
     --enable-compile-warnings=yes \
     --with-xvfb-tests
   sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool
   make
 }
```

2) rebuild [js52](https://www.archlinux.org/packages/?name=js52) with the following changes to the PKGBUILD:

```
--- PKGBUILD (old)
+++ PKGBUILD (new)
@@ -24,0 +25 @@
+options=(debug)
@@ -36,11 +37,9 @@
 build() {
   unset CPPFLAGS
   CFLAGS+=' -fno-delete-null-pointer-checks -fno-strict-aliasing -fno-tree-vrp -flto=3'
   CXXFLAGS+=' -fno-delete-null-pointer-checks -fno-strict-aliasing -fno-tree-vrp -flto=3'
   export CC=gcc CXX=g++ PYTHON=/usr/bin/python2

   cd mozilla-unified/js/src
   sh configure \
     --prefix=/usr \
-    --disable-debug \
-    --disable-debug-symbols \
```

Once the gjs and js52 packages are installed and gnome-shell restarted (`Alt`+ `F2` + `r`), whenever gnome-shell crashes the debug symbols will be available.

After the crash:

 `$ coredumpctl -1` 
```
TIME                            PID   UID   GID SIG COREFILE  EXE
Mon 2017-07-17 15:34:49 CEST  27368  1000  1000  11 present   /usr/bin/gnome-shell
$ coredumpctl gdb 27368
(gdb) bt
#0  0x00007fbc7b997945 in js::GCMethods<JSObject*>::needsPostBarrier(JSObject*) (v=0x7fbc0a9548c0) at /usr/include/mozjs-38/js/RootingAPI.h:663
#1  0x00007fbc7b997945 in JS::Heap<JSObject*>::set(JSObject*) (newPtr=0x0, this=0x254c260) at /usr/include/mozjs-38/js/RootingAPI.h:296
#2  0x00007fbc7b997945 in JS::Heap<JSObject*>::operator=(JSObject* const&) (p=<optimized out>, this=0x254c260) at /usr/include/mozjs-38/js/RootingAPI.h:266
#3  0x00007fbc7b997945 in GjsMaybeOwned<JSObject*>::reset() (this=0x254c250) at ./gjs/jsapi-util-root.h:267
#4  0x00007fbc7b997945 in closure_clear_idle(void*) (data=0x254c220) at gi/closure.cpp:133
#5  0x00007fbc79abd8c5 in g_main_context_dispatch () at /usr/lib/libglib-2.0.so.0
#6  0x00007fbc79abdc88 in  () at /usr/lib/libglib-2.0.so.0
#7  0x00007fbc79abdfa2 in g_main_loop_run () at /usr/lib/libglib-2.0.so.0
#8  0x00007fbc7b27508c in meta_run () at /usr/lib/libmutter-0.so.0
#9  0x0000000000401ff7 in main ()
```

You can then report the bug on the [project page](https://gitlab.gnome.org/GNOME/gnome-shell/issues) at GNOME GitLab.

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

In order for Tracker (and, therefore, Documents) to detect your local files, they must be stored in an [XDG compliant directory](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html) (such as 'Documents' or 'Music'). For more information, see [XDG user directories](/index.php/XDG_user_directories "XDG user directories").

You can also configure Tracker to recursively search inside specific directories such as your home directory. These settings can be made using `tracker-preferences`.

## Unable to add accounts in Empathy and GNOME Online Accounts

Empathy, the engine behind integrated messaging, GNOME Online Accounts, and all other system settings based on messaging accounts will not function correctly unless the [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/) group of packages or at least one of the backends ([telepathy-gabble](https://www.archlinux.org/packages/?name=telepathy-gabble), or [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze), for example) is [installed](/index.php/Install "Install"). View descriptions of *telepathy* components on the [freedesktop.org telepathy wiki](https://telepathy.freedesktop.org/wiki/Components/).

**Note:** [Avahi](/index.php/Avahi "Avahi") daemon is required for connecting with the People Nearby account, and also in order for some desktop extensions to work correctly like [Chat Status](https://extensions.gnome.org/extension/746/chat-status/)

## Empathy does not use GNOME Online Accounts

After adding a Gnome Online Account, it may be necessary to log out and log back in for it to be used by Empathy.

## GNOME Online Accounts settings page does not show properly

In some cases, due to interactions with Alacarte (menu editor), Gnome Online accounts settings page would not show. If that happens, "Restore System Configuration" in Alacarte can restore missing functions to gnome-control-center. (See [https://bugzilla.redhat.com/show_bug.cgi?id=1520431](https://bugzilla.redhat.com/show_bug.cgi?id=1520431).)

## Cannot change settings in dconf-editor

When one cannot set settings in [dconf](https://www.archlinux.org/packages/?name=dconf), it is possible their dconf user settings are corrupt. In this case it is best to delete the user dconf files in `~/.config/dconf/user*` and set the settings in dconf-editor after.

## When an extension breaks the shell

When enabling shell extensions causes GNOME breakage, you should first remove the *user-theme* and *auto-move-windows* extensions from their installation directory.

The installation directory could be one of `~/.local/share/gnome‑shell/extensions`, `/usr/share/gnome‑shell/extensions` or `/usr/local/share/gnome‑shell/extensions`. Removing these two extension-containing folders may fix the breakage. Otherwise, isolate the problem extension with trial‑and‑error.

Removing or adding an extension-containing folder to the aforementioned directories removes or adds the corresponding extension to your system. Details on GNOME Shell extensions are available at the [GNOME web site.](https://wiki.gnome.org/Projects/GnomeShell/Extensions)

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

According to [this bug report](https://bugzilla.gnome.org/show_bug.cgi?id=711028#c2), DRI3 includes the `buffer_age` extension that allows GNOME Shell's Mutter compositor to sync windows to vblank in an efficient way. Since version `1:2.99.917+682+g4eaab17-1`, DRI3 is enabled by default in [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) [[1]](https://git.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/xf86-video-intel&id=cd3de9bb45a9ab84383541ed45ee6f0c10ea8798).

	Intel TearFree

Enabling the [Xorg Intel TearFree option](/index.php/Intel_graphics#Tearing "Intel graphics") is a known workaround for tearing problems on Intel adapters. However, the way this option acts increases memory consumption and lowers performance, see [the original bug report's final comment](https://bugs.freedesktop.org/show_bug.cgi?id=37686#c123).

	Mutter tweaks

**Note:** This workaround has been [reported](https://bugzilla.gnome.org/show_bug.cgi?id=711028#c0) to have side effects and may not fix tearing in all cases.

GNOME Shell's Mutter compositor has a tweak known to address tearing problems (see [the original suggestion for this fix](https://bugzilla.gnome.org/show_bug.cgi?id=657071#c1) and its mention in [the Freedesktop bug report](https://bugs.freedesktop.org/show_bug.cgi?id=37686#c59)). To enable this tweak, append the following line to `/etc/environment`: `CLUTTER_PAINT=disable-clipped-redraws:disable-culling`. Then restart the Xorg server.

	Disable Fullscreen Unredirect

Gnome Shell does by default unredirect fullscreen applications. This may result in tearing. You can disable this with the gnome shell extension [gnome-shell-extension-disable-unredirect](https://aur.archlinux.org/packages/gnome-shell-extension-disable-unredirect/).

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

Upon running the command and then logging out, you should find that the keyboard input sources menu is visible in GDM and in the GNOME Shell desktop. See [Input sources in GNOME](https://blogs.gnome.org/mclasen/2012/09/21/input-sources-in-gnome/) for more information.

## Mouse cursor missing

When using a separate [window manager](/index.php/Window_manager "Window manager") with *gnome-settings-daemon*, the mouse cursor may vanish. Run:

```
$ gsettings set org.gnome.settings-daemon.plugins.cursor active false

```

## No restart button in session menu when screen is locked

If [XScreenSaver](/index.php/XScreenSaver "XScreenSaver") is installed, ensure that it is not running at startup, see [GNOME#Autostart](/index.php/GNOME#Autostart "GNOME").

## PulseAudio system-wide causes delay in GNOME and GDM

If you are running [PulseAudio](/index.php/PulseAudio "PulseAudio") in system-wide mode, the PulseAudio 7.0 upgrade breaks [GDM](/index.php/GDM "GDM") and GNOME. See [this forum post](https://bbs.archlinux.org/viewtopic.php?id=203051) for more information.

## GNOME crashes when trying to reorder applications in the GNOME Shell Dash

The dash is the "toolbar" that appears, by default, [on the left](https://en.wikipedia.org/wiki/GNOME_Shell#Design_components "wikipedia:GNOME Shell") when you click Activities. Applications can be reordered in the dash by dragging and dropping. If this fails, and/or causes GNOME to crash, try [changing your icon theme](https://bbs.archlinux.org/viewtopic.php?id=171689).

## Gnome Crashes while installing gnome-extra

Attempting to install the gnome-extra group while a gnome environment is running will crash gnome while installing gnome-getting-started-docs. X will continue to run, but gnome will not work until fixed. To fix, simply install gnome-extra from a terminal rather than inside gnome. When complete, gnome should work again.

## No H264 Video in Gnome Video Player (Totem)

[See Codecs](/index.php/Codecs#Tips_and_tricks "Codecs")

## No suspend on LID closure

GNOME defaults to this behaviour about suspension:

*   No external monitor attached, computer goes in suspension when LID closes.
*   External monitor attached, computer does not go in suspension when LID closes.

Currently [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks) is not able to modify the behaviour on the second case, when a monitor is connected to the computer. While it can inhibit suspension with no monitor attached.

**Note:** Behaviour on LID closure is controlled also by systemd. See [Power management#Power management with systemd](/index.php/Power_management#Power_management_with_systemd "Power management").

## gnome-shell / gnome-session crashes on session startup

Sometimes `gnome-session` crashes immediately after login. This might be more visible on wayland and it might seem as if every second login attempt fails. The problem can be temporarily worked around by removing the files in `~/.config/gnome-session/saved-session`. A more lasting work-around is to disable the session manager's `auto-save-session` feature:

```
$ gsettings set org.gnome.SessionManager auto-save-session false

```

## Low OpenGL performance and stuttering

*   With proprietary NVIDIA driver

[This](https://bugzilla.gnome.org/show_bug.cgi?id=781835) bug is much likely the cause of it. You should revert `383ba566bd7c2a76d0856015a66e47caedef06b6` commit in [mutter](https://www.archlinux.org/packages/?name=mutter). Use [ABS](/index.php/ABS "ABS") for this and add `git revert -n 383ba566bd7c2a76d0856015a66e47caedef06b6` to the `prepare()` function in the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") or simply install [mutter-performance](https://aur.archlinux.org/packages/mutter-performance/) instead.

*   With free drivers

If video playback stutters (a bit), try *GNOME on Xorg* instead of Wayland.

## GNOME Wayland session not available

GNOME Wayland does not support more than one GPU for output yet, [falling back](https://bugzilla.gnome.org/show_bug.cgi?id=771442) on GNOME X11.

If your displays are only connected to one of your video devices, add this to your [system environment variables](/index.php/Environment_variables#Using_pam_env "Environment variables"):

```
MUTTER_ALLOW_HYBRID_GPUS=1

```

To avoid [problems](https://bbs.archlinux.org/viewtopic.php?pid=1744592#p1744592) with some chipsets enable [Early KMS](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting").

## gnome-control-center is empty and does not list any categories

Under alternative window managers (i3 for example), *gnome-control-center* starts as an empty window. You need to set the variable `XDG_CURRENT_DESKTOP` to `GNOME` to start it (either in a script or exporting the variable in `~/.profile`).

```
 export XDG_CURRENT_DESKTOP=GNOME
 gnome-control-center &

```

## Gnome freezes for a second after using a Function (Fn) key shortcut

This is a problem with the brazilian portuguese ABNT 2 keyboard. If you have the brazilian portuguese enabled, GNOME might experience this problem. To fix this issue and keep using this keyboard layout, un-map the scroll lock button by commenting this line at `/usr/share/X11/xkb/symbols/br`:

```
 modifier_map Mod3   { Scroll_Lock };

```

And restart the session (log out and in).

## Zoom in/out keyboard shortcuts don't work on some apps

`Ctrl` + `+` and `Ctrl` + `-` keyboard shourtcuts for zoom in/out functions don't work out of the box on some Gnome apps, such as Files and Gnome-Terminal.

In such cases, open up GNOME Tweaks ([gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks)) and navigate to Keyboard & Mouse > Additional Layout Options button > Layout of numeric keypad. Change the `Disabled` value to `Hexadecimal`.