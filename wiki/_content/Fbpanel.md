# Fbpanel

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

fbpanel is a lightweight NETWM compliant desktop panel. This article describes the installation and configuration of fbpanel.

## Contents

*   [1 Installing](#Installing)
*   [2 Starting](#Starting)
*   [3 Configuration](#Configuration)
    *   [3.1 wincmd plugin (show desktop button)](#wincmd_plugin_.28show_desktop_button.29)
*   [4 See also](#See_also)

## Installing

[Install](/index.php/Pacman "Pacman") the [fbpanel](https://www.archlinux.org/packages/?name=fbpanel) package from the [official repositories](/index.php/Official_repositories "Official repositories").

## Starting

If you want to start fbpanel with your X session, add the following line to your .xinitrc, before the line where you start your window manager.

```
fbpanel &

```

## Configuration

You can find the configuration file in `~/.config/fbpanel`

If it doesn't exist, copy over the default configuration file:

```
# mkdir ~/.config/fbpanel
# cp /usr/share/fbpanel/default ~/.config/fbpanel

```

### wincmd plugin (show desktop button)

This plugin is enabled by default, but it might not show up because it cannot find an existing icon. In that case, change the icon path to one that points to an existing icon. You can also use an image as its icon. In that case, replace the "icon" key with "image".

```
Plugin {
   type = wincmd
   config {
       image = ~/images/my_image.png
       tooltip = Left click to iconify all windows. Middle click to shade them.
   }
}

```

## See also

*   [Official Website](http://fbpanel.sourceforge.net/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Fbpanel&oldid=290315](https://wiki.archlinux.org/index.php?title=Fbpanel&oldid=290315)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Application launchers](/index.php/Category:Application_launchers "Category:Application launchers")
*   [Eye candy](/index.php/Category:Eye_candy "Category:Eye candy")
*   [Status monitoring and notification](/index.php/Category:Status_monitoring_and_notification "Category:Status monitoring and notification")