Related articles

*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [GNOME](/index.php/GNOME "GNOME")
*   [Compiz](/index.php/Compiz "Compiz")

[Unity](http://unity.ubuntu.com/) is a desktop shell for the [GNOME](/index.php/GNOME "GNOME") desktop environment developed by [Canonical Ltd](http://www.canonical.com/about) for [Ubuntu](http://www.ubuntu.com). Unity is implemented as a plugin of the [Compiz](/index.php/Compiz "Compiz") [window manager](/index.php/Window_manager "Window manager").

**Note:** Unity was discontinued by Canonical on April 6, 2017 and is no longer being developed.[[1]](https://insights.ubuntu.com/2017/04/05/growing-ubuntu-for-cloud-and-iot-rather-than-phone-and-convergence/) If you are already using it, a follow-on project to follow may be [UBports' Unity8](https://unity8.io/).

Not to be confused with [Unity3D](/index.php/Unity3D "Unity3D").

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Updating](#Updating)
    *   [1.2 Standard and extended functionality](#Standard_and_extended_functionality)
*   [2 Tips and tricks](#Tips_and_tricks)
    *   [2.1 Customize LightDM wallpaper and appearance](#Customize_LightDM_wallpaper_and_appearance)
    *   [2.2 Autostart programs on login](#Autostart_programs_on_login)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Cannot right click on desktop](#Cannot_right_click_on_desktop)
    *   [3.2 Unity stops working after update](#Unity_stops_working_after_update)
    *   [3.3 Some GTK+ themes look ugly since GNOME 3.6](#Some_GTK+_themes_look_ugly_since_GNOME_3.6)
    *   [3.4 Workspace switcher widget disappeared](#Workspace_switcher_widget_disappeared)
    *   [3.5 No skype or other applications appear in indicator tray](#No_skype_or_other_applications_appear_in_indicator_tray)
*   [4 Known issues](#Known_issues)
    *   [4.1 Indicator-messages does not work properly](#Indicator-messages_does_not_work_properly)
    *   [4.2 Pidgin-libnotify-ubuntu has unresolvable dependency](#Pidgin-libnotify-ubuntu_has_unresolvable_dependency)
*   [5 See also](#See_also)

## Installation

**Warning:** Installing Unity means that many official packages will be replaced with patched Ubuntu versions. Be careful to check the resulting package conflicts.

PKGBUILDs for the Unity desktop are available on GitHub, where [Unity-For-Arch](https://github.com/chenxiaolong/Unity-for-Arch) provides a minimal working Unity shell, and [Unity-For-Arch-Extra](https://github.com/chenxiaolong/Unity-for-Arch-Extra) provides some additional applications, including [lightdm-ubuntu](https://aur.archlinux.org/packages/lightdm-ubuntu/) ([LightDM](/index.php/LightDM "LightDM") with Ubuntu patches), [ubuntu-themes](https://aur.archlinux.org/packages/ubuntu-themes/), *unity-tweak-tool* (a popular Unity configuration tool) and more.

[Install](/index.php/Install "Install") [git](https://www.archlinux.org/packages/?name=git) and navigate to a directory in which the sources can be built, then do:

```
$ git clone [https://github.com/chenxiaolong/Unity-for-Arch.git](https://github.com/chenxiaolong/Unity-for-Arch.git)

```

Open the `README` and build the packages according to the ordered list (see: [Makepkg#Usage](/index.php/Makepkg#Usage "Makepkg")):

```
$ cd *<package name>*
$ makepkg -sci

```

**Tip:** To use [LightDM](/index.php/LightDM "LightDM"), follow the same steps mentioned above to install [lightdm-ubuntu](https://aur.archlinux.org/packages/lightdm-ubuntu/) and [lightdm-unity-greeter](https://aur.archlinux.org/packages/lightdm-unity-greeter/) from the [Unity-For-Arch-Extra](https://github.com/chenxiaolong/Unity-for-Arch-Extra) repository.

#### Updating

Navigate to the original directory and pull all changes:

```
$ git pull

```

Then, check, if any packages need updating:

```
$ ./"What_can_I_update?.py"

```

**Note:** Sometimes, if a certain crucial package is updated, those depending on it will also need to be recompiled. For example, if *unity* is updated, *nux* might need to be re-compiled as well.

### Standard and extended functionality

The following section lists packages that, whilst not required for the Unity shell to function, do serve to enhance the user experience:

| Functionality | Package(s) |
| Notifications | [notify-osd](https://www.archlinux.org/packages/?name=notify-osd) |
| Screen locking | *gnome-screensaver-ubuntu* |
| Online accounts | [signon-keyring-extension](https://aur.archlinux.org/packages/signon-keyring-extension/), [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring), [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/) |
| SSH | [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring) |
| HUD & menubar integration | [appmenu-qt4](https://www.archlinux.org/packages/?name=appmenu-qt4), [firefox-ubuntu](https://aur.archlinux.org/packages/firefox-ubuntu/), [thunderbird-ubuntu](https://aur.archlinux.org/packages/thunderbird-ubuntu/) |
| File and Folder lens | *zeitgeist-ubuntu* |
| Configuration | [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool), *unity-tweak-tool* |
| Pidgin integration | *pidgin-indicator* |

## Tips and tricks

### Customize LightDM wallpaper and appearance

See [LightDM#Changing background images/colors](/index.php/LightDM#Changing_background_images/colors "LightDM").

### Autostart programs on login

See [GNOME#Autostart](/index.php/GNOME#Autostart "GNOME").

## Troubleshooting

### Cannot right click on desktop

Other issues that this fix addresses:

*   Title bar at the top doesn't display *Arch Linux Desktop*
*   Shortcut keys, such as `Super` and `Alt` do not work when there are no active windows

Execute the following: `gsettings set org.gnome.desktop.background show-desktop-icons true`

### Unity stops working after update

Run `compiz.reset` and then log out and log back into the Unity session.

If Unity still is not working, report an issue on [github](https://github.com/chenxiaolong/Unity-for-Arch/issues?state=open) or discuss it in this [forum thread](https://bbs.archlinux.org/viewtopic.php?id=125423&p=1) on the Arch Linux Forums.

### Some GTK+ themes look ugly since GNOME 3.6

This affects the unity default theme and light themes. Use:

 `~/.config/gtk3.0/gtk.css` 
```
GtkLabel {
  background-color: @transparent;
}

```

### Workspace switcher widget disappeared

In *ccsm* (the Compiz Configuration Settings Manager), ensure that the following option is checked: *Settings > Appearance > Behaviour > Enable workspaces*.

### No skype or other applications appear in indicator tray

Using Skype as an example; Append *Skype* to the `systray-whitelist` list in `com.canonical.Unity.Panel` using [dconf-editor](https://www.archlinux.org/packages/?name=dconf-editor) or the gsettings command. Reboot or logout afterwards.

Alternatively, replace the contents of `systray-whitelist` with *all*.

## Known issues

See [Github Issues](https://github.com/chenxiaolong/Unity-for-Arch/issues) for known problems.

### Indicator-messages does not work properly

Pidgin and a number of other applications can not be integrated into *indicator-messages* due to its API changes. Users will have to wait for upstream to release software updates for the affected applications.

### Pidgin-libnotify-ubuntu has unresolvable dependency

As of February 2015, the required package *perlxml* is unavailable, try *pidgin-indicator*.

## See also

*   [Unity home page](http://unity.ubuntu.com/)
*   [Unity in Launchpad](https://launchpad.net/unity)