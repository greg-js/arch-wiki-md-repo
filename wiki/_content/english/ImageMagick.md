According to [Wikipedia](https://en.wikipedia.org/wiki/ImageMagick "wikipedia:ImageMagick"):

	ImageMagick is a free and open-source software suite for displaying, converting, and editing raster image and vector image files. It can read and write over 200 image file formats.

**Note:** [libmagick](https://www.archlinux.org/packages/?name=libmagick) uses [Ghostscript](/index.php/Ghostscript "Ghostscript") for PDF, EPS, PS and XPS parsing. Because their have been multiple vulnerabilities with Ghostscript[[1]](https://security.archlinux.org/package/ghostscript), these formats are now proactively disabled in `/etc/ImageMagick-7/policy.xml` with the following line:
```
<policy domain="coder" rights="none" pattern="{PS,PS2,PS3,EPS,PDF,XPS}" />

```
See also [FS#59778](https://bugs.archlinux.org/task/59778).

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Screenshot taking](#Screenshot_taking)
        *   [2.1.1 Screenshot of multiple X screens](#Screenshot_of_multiple_X_screens)
        *   [2.1.2 Screenshot of individual Xinerama heads](#Screenshot_of_individual_Xinerama_heads)
        *   [2.1.3 Screenshot of the active/focused window](#Screenshot_of_the_active/focused_window)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) package. Alternatively install [graphicsmagick](https://www.archlinux.org/packages/?name=graphicsmagick) for [GraphicsMagick](https://en.wikipedia.org/wiki/GraphicsMagick "wikipedia:GraphicsMagick"), a fork of ImageMagick, emphasizing stability of the API and command-line interface.

## Usage

See [ImageMagick(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ImageMagick.1), or [gm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gm.1) for GraphicsMagick.

Popular operations include `-append`, `-resize`, `-rotate`, `-quality` and many more. For example, to combine multiple pictures into one:

```
$ convert -append *input.pngs* *output.png*

```

**Note:** The sign before an option is important. Opposite operations can be performed by using a *plus* instead of a *minus*.

To crop part of multiple images and convert them to another format:

```
$ mogrify -crop *WIDTH***x***HEIGHT*+*X*+*Y* -format jpg *.png

```

Where *WIDTH* and *HEIGHT* is the cropped output image size, and *X* and *Y* is the offset from the input image size.

### Screenshot taking

An easy way to take a screenshot of your current system is using the [import(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/import.1) command:

```
$ import -window root screenshot.jpg

```

`import` is part of the [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) package.

Running `import` without the `-window` option allows selecting a window or an arbitrary region interactively.

**Note:** If you prefer **graphicsmagick** alternative, just prepend "gm", e.g. `$ gm import -window root screenshot.jpg`.

#### Screenshot of multiple X screens

If you run twinview or dualhead, simply take the screenshot twice and use `imagemagick` to paste them together:

```
import -window root -display :0.0 -screen /tmp/0.png
import -window root -display :0.1 -screen /tmp/1.png
convert +append /tmp/0.png /tmp/1.png screenshot.png
rm /tmp/{0,1}.png

```

#### Screenshot of individual Xinerama heads

Xinerama-based multi-head setups have only one virtual screen. If the physical screens are different in height, you will find dead space in the screenshot. In this case, you may want to take screenshot of each physical screen individually. As long as Xinerama information is available from the X server, the following will work:

```
#!/bin/sh
xdpyinfo -ext XINERAMA | sed '/^  head #/!d;s///' |
while IFS=' :x@,' read i w h x y; do
        import -window root -crop ${w}x$h+$x+$y head_$i.png
done

```

#### Screenshot of the active/focused window

The following script takes a screenshot of the currently focused window. It works with EWMH/NetWM compatible X Window Managers. To avoid overwriting previous screenshots, the current date is used as the filename.

```
#!/bin/sh
activeWinLine=$(xprop -root | grep "_NET_ACTIVE_WINDOW(WINDOW)")
activeWinId=${activeWinLine:40}
import -window "$activeWinId" /tmp/$(date +%F_%H%M%S_%N).png

```

Alternatively, the following should work regardless of EWMH support:

```
$ import -window "$(xdotool getwindowfocus -f)" /tmp/$(date +%F_%H%M%S_%N).png

```

**Note:** If screenshots of some programs (dwb and zathura) appear blank, try appending `-frame` or removing `-f` from the `xdotool` command.

## See also

*   [ImageMagick website](http://www.imagemagick.org/) for an extensive list of options and examples.
*   [List of applications/Multimedia#Image processing](/index.php/List_of_applications/Multimedia#Image_processing "List of applications/Multimedia")