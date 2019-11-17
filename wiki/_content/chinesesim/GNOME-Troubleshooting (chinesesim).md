<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Gnome Shell 界面卡死](#Gnome_Shell_界面卡死)
*   [2 Incorrect application defaults](#Incorrect_application_defaults)
*   [3 Tracker & Documents do not list any local files](#Tracker_&_Documents_do_not_list_any_local_files)
*   [4 Unable to add accounts in Empathy and GNOME Online Accounts](#Unable_to_add_accounts_in_Empathy_and_GNOME_Online_Accounts)
*   [5 Cannot change settings in dconf-editor](#Cannot_change_settings_in_dconf-editor)
*   [6 When an extension breaks the shell](#When_an_extension_breaks_the_shell)
*   [7 扩展在 GNOME 3 升级后不工作了](#扩展在_GNOME_3_升级后不工作了)
*   [8 只有 conky 运行时键盘快捷方式不工作](#只有_conky_运行时键盘快捷方式不工作)
*   [9 Unable to apply stored configuration for monitors](#Unable_to_apply_stored_configuration_for_monitors)
*   [10 一致的光标主题](#一致的光标主题)
*   [11 Windows cannot be modified with Alt-Key + mouse-button](#Windows_cannot_be_modified_with_Alt-Key_+_mouse-button)
*   [12 加载速度慢的系统图标/慢GDM登录](#加载速度慢的系统图标/慢GDM登录)
*   [13 Artifacts when maximizing windows](#Artifacts_when_maximizing_windows)
*   [14 Tear-free video with Intel HD Graphics](#Tear-free_video_with_Intel_HD_Graphics)
*   [15 Window opens behind other windows when using multiple monitors](#Window_opens_behind_other_windows_when_using_multiple_monitors)
*   [16 锁定按钮无法重新启用触摸板](#锁定按钮无法重新启用触摸板)
*   [17 GNOME Shell键盘源菜单不可见](#GNOME_Shell键盘源菜单不可见)
*   [18 鼠标指针丢失](#鼠标指针丢失)
*   [19 在会话菜单中没有重启按钮时，屏幕被锁定](#在会话菜单中没有重启按钮时，屏幕被锁定)
*   [20 pulseaudio系统原因延误GNOME和GDM](#pulseaudio系统原因延误GNOME和GDM)
*   [21 GNOME crashes when trying to reorder applications in the GNOME Shell Dash](#GNOME_crashes_when_trying_to_reorder_applications_in_the_GNOME_Shell_Dash)

### Gnome Shell 界面卡死

如果 Gnome Shell 的界面卡死了（可能是由于某些外观调整异常、某个扩展出问题，或内存不足），你可能就连按下 `Alt` + `F2` 并输入 **r** 的机会都没有。这时，请试着切换到另一个 TTY（**Ctrl** + **Alt** + **F2**） 上，并输入命令`pkill -HUP gnome-shell`。Gnome Shell 将重新启动，可能需要个几十秒。这样的重启方式不会注销已登录的用户，因此所有的程序也将继续运行。不过，保存你正在编辑文件总是个好主意。

如果这也不行，那你可能得重新启动 [Xorg](/index.php/Xorg "Xorg") 服务器。如果你通过终端登录，输入 `pkill X`；如果你通过 GDM 登录，输入 `systemctl restart gdm`。但需要注意的是，重启 Xorg 服务器会导致已登录的用户被注销，因此请确保在这之前已经设法保存你所有的文件。

### Incorrect application defaults

When installing applications for the first time you may find that GNOME has the wrong application associated to a certain protocols - for instance, *easytag* becomes the folder handler instead of [GNOME Files](/index.php/GNOME_Files "GNOME Files").

For GNOME Files see the following page: [GNOME Files#Files is no longer the default file manager](/index.php/GNOME_Files#Files_is_no_longer_the_default_file_manager "GNOME Files").

For Document Viewer, run the following command:

```
$ xdg-mime default evince.desktop application/pdf

```

For other applications, default handler settings are detailed on the following page: [Default applications](/index.php/Default_applications "Default applications").

Optionally, you can [install](/index.php/Install "Install") [gnome-defaults-list](https://aur.archlinux.org/packages/gnome-defaults-list/). It will place your configuration file at `/etc/gnome/defaults.list`.

### Tracker & Documents do not list any local files

In order for Tracker (and, therefore, Documents) to detect your local files, they must be stored in an [XDG compliant directory](http://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html) (such as 'Documents' or 'Music'). For more information, see [XDG user directories](/index.php/XDG_user_directories "XDG user directories").

You can also configure Tracker to recursively search inside specific directories such as your home directory. These settings can be made using `tracker-preferences`.

### Unable to add accounts in Empathy and GNOME Online Accounts

Empathy, the engine behind integrated messaging, GNOME Online Accounts, and all other system settings based on messaging accounts will not function correctly unless the [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/) group of packages or at least one of the backends ([telepathy-gabble](https://www.archlinux.org/packages/?name=telepathy-gabble), or [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze), for example) is [installed](/index.php/Install "Install"). View descriptions of *telepathy* components on the [freedesktop.org telepathy wiki](http://telepathy.freedesktop.org/wiki/Components).

**Note:** [Avahi](/index.php/Avahi "Avahi") daemon is required for connecting with the People Nearby account, and also in order for some desktop extensions to work correctly like [Chat Status](https://extensions.gnome.org/extension/746/chat-status/)

### Cannot change settings in dconf-editor

When one cannot set settings in [dconf](https://www.archlinux.org/packages/?name=dconf), it is possible their dconf user settings are corrupt. In this case it is best to delete the user dconf files in `~/.config/dconf/user*` and set the settings in dconf-editor after.

### When an extension breaks the shell

When enabling shell extensions causes GNOME breakage, you should first remove the *user-theme* and *auto-move-windows* extensions from their installation directory.

The installation directory could be one of `~/.local/share/gnome‑shell/extensions`, `/usr/share/gnome‑shell/extensions` or `/usr/local/share/gnome‑shell/extensions`. Removing these two extension-containing folders may fix the breakage. Otherwise, isolate the problem extension with trial‑and‑error.

Removing or adding an extension-containing folder to the aforementioned directories removes or adds the corresponding extension to your system. Details on GNOME Shell extensions are available at the [GNOME web site.](https://live.gnome.org/GnomeShell/Extensions)

If you have trouble with uninstalling an extension via [extensions.gnome.org/local](https://extensions.gnome.org/local/), then probably they have been installed as system-wide extensions with the [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) package. Removing the package again obviously affects all user accounts.

### 扩展在 GNOME 3 升级后不工作了

**Note:** Please bear in mind that whilst the methods below will allow you to **try** and activate an extension with an unsupported version of GNOME Shell, it is by no means a guarantee that the extension will work successfully. The most likely outcome of trying to activate such an extension is that GNOME Shell will crash and then restart.

Before trying the workarounds below, check if an update is available for the extension by visiting [extensions.gnome.org/local](https://extensions.gnome.org/local).

If there is no update for your current GNOME version yet, use the following command to disable version validation for extensions:

```
$ gsettings set org.gnome.shell disable-extension-version-validation true

```

Alternatively, you could modify the extension itself, changing the supported shell version to satisfy the version validation. See the method below.

找到扩展的安装目录，可能是 `~/.local/share/gnome-shell/extensions` 或 `/usr/share/gnome-shell/extensions`.

编辑扩展子文件夹中的每一个 **`metadata.json`**

| Insert: | `"shell-version": ["3.x"]` |
| Instead of (for example): | `"shell-version": ["3.4"]` |

`"3.x"` 是最好的选择，这个表示扩展能在所有 ***3.x*** GNOME Shell版本下工作。

### 只有 conky 运行时键盘快捷方式不工作

gnome-shell 键盘快捷方式(如 Alt+F2,Alt+F1 和多媒体键快捷方式)当只有 conky 运行时不会工作。然而如果另一个程序(例如 gedit)在运行，键盘快捷方式就可以工作了。

解决方式：编辑 .conkyrc

```
own_window yes
own_window_transparent yes
own_window_argb_visual yes
own_window_type dock
own_window_class Conky
own_window_hints undecorated,below,sticky,skip_taskbar,skip_pager

```

### Unable to apply stored configuration for monitors

If you encounter this message try to disable the *xrandr* `gnome-settings-daemon plugin`:

```
$ dconf write /org/gnome/settings-daemon/plugins/xrandr/active false

```

### 一致的光标主题

See [Cursor themes#Desktop environments](/index.php/Cursor_themes#Desktop_environments "Cursor themes").

### Windows cannot be modified with Alt-Key + mouse-button

In GNOME 3.6 and above, the mouse button modifier (the key that allows you to drag a window from a location other than the titlebar) is the `Super` key instead of the `Alt` key which was used in the past. The change was made in response to the following [bug report](https://bugzilla.gnome.org/show_bug.cgi?id=607797).

To change the mouse button modifier back to the `Alt` key, execute the following:

```
$ gsettings set org.gnome.desktop.wm.preferences mouse-button-modifier '<Alt>'  

```

**Note:** It is not possible to change this with *System settings* > *Keyboard* > *Shortcuts*

### 加载速度慢的系统图标/慢GDM登录

Problems with the loading of system icons, such the ones in the title bar of Files, might be solved by [installing](/index.php/Pacman#Installing_specific_packages "Pacman") (or re-installing) the [gdk-pixbuf2](https://www.archlinux.org/packages/?name=gdk-pixbuf2) package.

Re-installing the aforementioned package may also fix repeated occurrences of the "Oh no! Something has gone wrong!" error screen and/or very slow loading and login with GDM as described in the following [forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1414157).

### Artifacts when maximizing windows

Maximizing windows may cause artifacts as of GNOME 3.12.0 - see the following [forum thread](https://bbs.archlinux.org/viewtopic.php?id=183617) and [bug report](https://bugzilla.gnome.org/show_bug.cgi?id=728385). A solution is detailed in the following section: [#Tear-free video with Intel HD Graphics](#Tear-free_video_with_Intel_HD_Graphics).

### Tear-free video with Intel HD Graphics

	Intel TearFree

Enabling the [Xorg Intel TearFree option](/index.php/Intel_graphics#Tear-free_video "Intel graphics") is a known workaround for tearing problems on Intel adapters. However, the way this option acts makes it redundant with the use of a compositor (it increases memory consumption and lowers performance, see [the original bug report's final comment](https://bugs.freedesktop.org/show_bug.cgi?id=37686#c123)).

	DRI3

According to [this bug report](https://bugzilla.gnome.org/show_bug.cgi?id=711028#c2), DRI3 includes the `buffer_age` extension that allows GNOME Shell's Mutter compositor to sync windows to vblank in an efficient way. DRI3 support is not compiled in to the mesa package, so you have to recompile [mesa](https://www.archlinux.org/packages/?name=mesa) with `--enable-dri3` in the `./configure` flags (see [ABS](/index.php/ABS "ABS")). Then enable it in the Xorg driver:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
   Identifier  "Intel Graphics"
   Driver      "intel"
   Option      "DRI"    "3"
EndSection
```

	Mutter tweaks

**Note:** This workaround has been [reported](https://bugzilla.gnome.org/show_bug.cgi?id=711028#c0) to have side effects and may not fix tearing in all cases.

GNOME Shell's Mutter compositor has a tweak known to address tearing problems (see [the original suggestion for this fix](https://bugzilla.gnome.org/show_bug.cgi?id=657071#c1) and its mention in [the Freedesktop bug report](https://bugs.freedesktop.org/show_bug.cgi?id=37686#c59)). To enable this tweak, append the following line to `/etc/environment`: `CLUTTER_PAINT=disable-clipped-redraws:disable-culling`. Then restart the Xorg server.

### Window opens behind other windows when using multiple monitors

This is possibly a bug in GNOME Shell which causes new windows to open behind others. To fix this issue, one can run the following command:

```
$ gsettings set org.gnome.shell.overrides workspaces-only-on-primary false

```

### 锁定按钮无法重新启用触摸板

Some laptops have a touchpad lock button that disables the touchpad so that users can type without worrying about touching the touchpad. Currently, it appears that although GNOME can lock the touchpad by pressing this button, it cannot unlock it. If the touchpad gets locked you can run the following to unlock it:

```
$ xinput set-prop "SynPS/2 Synaptics TouchPad" "Device Enabled" 1

```

### GNOME Shell键盘源菜单不可见

A menu showing the keyboard input sources (for example 'en' for an English keyboard layout) should be visible next to the status area containing icons for network, volume and power sources. If the keyboard sources menu is not visible, this is probably because you have configured your [Xorg](/index.php/Xorg "Xorg") keyboard layout in a way which GNOME does not recognise.

To ensure that the menu is visible, remove any Xorg keyboard configuration you might have created and set the keyboard locale using [localectl](/index.php/Keyboard_configuration_in_Xorg#Using_localectl "Keyboard configuration in Xorg").

Upon running the command and then logging out, you should find that the keyboard input sources menu is visible in GDM and in the GNOME Shell desktop. See [Input sources in GNOME](http://blogs.gnome.org/mclasen/2012/09/21/input-sources-in-gnome/) for more information.

### 鼠标指针丢失

When using a separate [window manager](/index.php/Window_manager "Window manager") with *gnome-settings-daemon*, the mouse cursor may vanish. Run:

```
$ gsettings set org.gnome.settings-daemon.plugins.cursor active false

```

### 在会话菜单中没有重启按钮时，屏幕被锁定

If [XScreenSaver](/index.php/XScreenSaver "XScreenSaver") is installed, ensure that it is not running at startup, see [GNOME#Startup applications](/index.php/GNOME#Startup_applications "GNOME").

### pulseaudio系统原因延误GNOME和GDM

If you are running [PulseAudio](/index.php/PulseAudio "PulseAudio") in system-wide mode, the PulseAudio 7.0 upgrade breaks [GDM](/index.php/GDM "GDM") and GNOME. See [this forum post](https://bbs.archlinux.org/viewtopic.php?id=203051) for more information.

### GNOME crashes when trying to reorder applications in the GNOME Shell Dash

The dash is the "toolbar" that appears, by default, [on the left](https://en.wikipedia.org/wiki/GNOME_Shell#Design_components "wikipedia:GNOME Shell") when you click Activities. Applications can be reordered in the dash by dragging and dropping. If this fails, and/or causes GNOME to crash, try [changing your icon theme](https://bbs.archlinux.org/viewtopic.php?id=171689).