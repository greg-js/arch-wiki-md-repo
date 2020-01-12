[fbpanel](http://aanatoly.github.io/fbpanel/) is a lightweight [NETWM](https://www.freedesktop.org/wiki/Specifications/wm-spec/) compliant desktop panel. This article describes the installation and configuration of fbpanel.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installing](#Installing)
*   [2 Starting](#Starting)
*   [3 Configuration](#Configuration)
    *   [3.1 wincmd plugin (show desktop button)](#wincmd_plugin_(show_desktop_button))

## Installing

[Install](/index.php/Install "Install") the [fbpanel](https://aur.archlinux.org/packages/fbpanel/) package.

## Starting

If you want to start fbpanel with your X session, add the following line to your .xinitrc, before the line where you start your window manager.

```
fbpanel &

```

## Configuration

You can find the configuration file in `~/.config/fbpanel`

If it doesn't exist, copy over the default configuration file:

```
$ mkdir ~/.config/fbpanel
$ cp /usr/share/fbpanel/default ~/.config/fbpanel

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