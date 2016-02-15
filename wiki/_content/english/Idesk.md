Idesk is a simple program for adding icons to your X desktop. It can also manage your wallpaper with a built in changer similar to that found in Windows 7.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Background options](#Background_options)
    *   [2.2 Icons](#Icons)
    *   [2.3 Idesktool](#Idesktool)

## Installation

[Install](/index.php/Install "Install") [idesk](https://www.archlinux.org/packages/?name=idesk) from the official repositories. Then copy the necessary configuration files to your home directory as shown below:

```
$ mkdir ~/.idesktop
$ cp /usr/share/idesk/dot.ideskrc ~/.ideskrc

```

optional:

```
$ cp /usr/share/idesk/default.lnk ~/.idesktop/

```

(This adds the default icon which just runs Xdialog to display a welcome message. It can be used as a template for other icons.)

## Configuration

The [idesk](https://www.archlinux.org/packages/?name=idesk) package does not come with a man page, but it does come with a readme file: `/usr/share/idesk/README`. There is also documentation on [**SourceForge.net**](http://idesk.sourceforge.net/html/usage.html) however most of the configuration options should be self-explanatory.

### Background options

If you are using another wallpaper setter such as [Feh](/index.php/Feh "Feh") or [Nitrogen](/index.php/Nitrogen "Nitrogen"), Idesk's background settings do not need to be modified.

If you are using Idesk's own background setter, supported wallpaper formats include JPEG, PNG, GIF, and XPM. Using either `Background.File` or `Background.Source`, specify the path to the image file you wish to use as a wallaper.

**Tip:** `Background.Source` seems to take precedence over `Background.File`; however, it is ignored if `Background.Delay` is set to 0.

### Icons

Idesk looks in `~/.idesktop` for files which names end with `.lnk` for icons. Each file should define one icon If you attempt to define a second icon it will be silently ignored. Aside from ending with `.lnk`, the files' names are not important.

Example for Chromium:

 `chromium.lnk` 

```
table Icon
  Caption: Chromium
  ToolTip.Caption: Google's OSS Web Browser
  Icon: /usr/share/icons/hicolor/32x32/apps/chromium.png
  Width: 32
  Height: 32
  X: 977
  Y: 369
  Command[0]: chromium
end
```

`Width` and `Height` should match the actual dimensions of the icon. `X` and `Y` will be modified by idesk to reflect the icon's actual position.

**Tip:**

*   Most system icons can be found in the following locations: `/usr/share/icons/hicolor`, `/usr/share/icons/gnome` and `/usr/share/pixmaps`.
*   Many icon themes provide a variety of different sizes of icon - 48x48 is a commonly used size for desktop icons.

### Idesktool

The [idesk-extras](https://aur.archlinux.org/packages/idesk-extras/) package in the [AUR](/index.php/AUR "AUR") provides a graphical configuration tool for Idesk. It can be started by running the `idesktool` command. Users can use Idesktool to create and remove icons, modify settings and restart Idesk.