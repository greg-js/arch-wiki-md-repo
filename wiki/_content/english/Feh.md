Related articles

*   [Nitrogen](/index.php/Nitrogen "Nitrogen")
*   [sxiv](/index.php/Sxiv "Sxiv")

[feh](http://feh.finalrewind.org/) is a lightweight and powerful image viewer that can also be used to manage the desktop wallpaper for standalone window managers lacking such features.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Browse images](#Browse_images)
    *   [2.2 Set the wallpaper](#Set_the_wallpaper)
    *   [2.3 Open SVG images](#Open_SVG_images)
    *   [2.4 Random background image](#Random_background_image)

## Installation

[Install](/index.php/Install "Install") the [feh](https://www.archlinux.org/packages/?name=feh) package.

## Usage

feh is highly configurable. For a full list of options, run `feh --help` or see the [feh(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/feh.1) [man page](/index.php/Man_page "Man page").

### Browse images

To quickly browse images in a specific directory, you can launch feh with the following arguments:

```
$ feh -g 640x480 -d -S filename /path/to/directory

```

*   The `-g` flag forces the images to appear no larger than 640x480
*   The `-d` flag draws the file name
*   The `-S filename` flag sorts the images by file name

This is just one example; there are many more options available should you desire more flexibility.

**Tip:** The `--start-at` option will display a selected image in feh while allowing to browse all other images in the directory as well, in their default order, i.e. as if you had run "feh *" and cycled through to the selected image. For example, `feh --start-at ./foo.jpg .` views all images in the current directory, starting with `*foo*.jpg`.

If you are browsing photos from a modern camera with EXIF data, it is interesting to use the `--auto-rotate` option to automatically rotate images. This does not alter the file.

### Set the wallpaper

`feh` can be used to set the desktop wallpaper, for example for [window managers](/index.php/Window_manager "Window manager") without this feature such as [Openbox](/index.php/Openbox "Openbox"), [Fluxbox](/index.php/Fluxbox "Fluxbox"), and [xmonad](/index.php/Xmonad "Xmonad").

The following command is an example of how to set the initial background:

```
$ feh --bg-scale /path/to/image.file

```

Other scaling options include:

```
--bg-tile FILE
--bg-center FILE
--bg-max FILE
--bg-fill FILE

```

To restore the background on the next session, add the following to your startup file (e.g. `~/.xinitrc`, `~/.config/openbox/autostart`, etc.):

```
~/.fehbg &

```

To change the background image, edit the file `~/.fehbg` which gets created after running the command `feh --bg-scale /path/to/image.file` mentioned above.

One can explicitly disable the creation of the `~/.fehbg`, by passing the `--no-fehbg` flag as well.

To setup different wallpapers for different monitors one should pass as many file paths as many monitors are available. For example, for a dual monitor setup it would be:

```
$ feh --bg-center path/to/file/for/first/monitor path/to/file/for/second/monitor

```

### Open SVG images

 `$ feh --magick-timeout 1 file.svg` 

Note that this requires the [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) package.

### Random background image

You can have feh set a random wallpaper using the `--randomize` option with one of the `--bg-foo` options, for example:

 `$ feh --randomize --bg-fill ~/.wallpaper/*` 

The above command tells feh to randomize the list of files in the `~/.wallpaper/` directory and set the backgrounds for all available desktops to whichever images are at the front of the randomized list (one unique image for each desktop). You can also do this recursively, if you have your wallpapers divided into subfolders:

 `$ feh --recursive --randomize --bg-fill ~/.wallpaper` 

To set a different random wallpaper from `~/.wallpaper` each session, add the following to your `.xinitrc`:

 `$ feh --bg-max --randomize ~/.wallpaper/* &` 

Another way to set a random wallpaper on each x.org session is to edit your `.fehbg` as following.

 `$HOME/.fehbg` 
```
 feh --bg-max --randomize --no-fehbg ~/.wallpaper/* 

```

**Tip:** To change wallpapers periodically, use a script (see [while loop](https://mywiki.wooledge.org/BashGuide/TestsAndConditionals#Conditional_Loops_.28while.2C_until_and_for.29 "gregswiki:BashGuide/TestsAndConditionals")), [cron](/index.php/Cron "Cron") job, or [systemd timer](/index.php/Systemd/Timers "Systemd/Timers") to execute the command at the desired interval.