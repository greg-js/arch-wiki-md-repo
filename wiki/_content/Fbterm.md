# Fbterm

Related articles

*   [KMSCON](/index.php/KMSCON "KMSCON")

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Fbterm#](https://wiki.archlinux.org/index.php/Talk:Fbterm))

**Fbterm** (**F**rame **b**uffer **term**inal emulator) is standalone replacement of Linux kernel terminal that can function outside of [Xorg](/index.php/Xorg "Xorg").

## Contents

*   [1 Features](#Features)
*   [2 Installation](#Installation)
*   [3 Customization](#Customization)
    *   [3.1 Fonts](#Fonts)
    *   [3.2 Input method support](#Input_method_support)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Background image](#Background_image)
    *   [4.2 White font color](#White_font_color)

## Features

From [http://code.google.com/p/fbterm/](http://code.google.com/p/fbterm/):

NaN

NaN

## Installation

Fbterm is available in the package [fbterm](https://www.archlinux.org/packages/?name=fbterm).

After installation, mind the additional instructions:

```
==> To run fbterm as a non-root user, do:
sudo gpasswd -a YOUR_USERNAME video
==> To enable keyboard shortcuts for non-root users, do:
sudo setcap 'cap_sys_tty_config+ep' /usr/bin/fbterm
or
sudo chmod u+s /usr/bin/fbterm

```

## Customization

### Fonts

Fbterm uses [fontconfig](https://en.wikipedia.org/wiki/fontconfig "wikipedia:fontconfig") for a list of fonts, trying each sequentially until it is able to render the characters.

To change the fonts that are used, use the `--font-names` option to select favorites from the list given by `fc-list`.

### Input method support

Fbterm supports diverse [input methods](https://en.wikipedia.org/wiki/Input_method "wikipedia:Input method") by acting as a client for an independent input method framework server. Several such programs are available for Arch, see [Internationalization#Input methods in Xorg](/index.php/Internationalization#Input_methods_in_Xorg "Internationalization").

## Tips and tricks

### Background image

To use a background image, Fbterm can be set to take a screen shot of the frame buffer device when it starts.

The following script (using the [fbv](https://www.archlinux.org/packages/?name=fbv) image viewer) is recommended in the man page:

```
#!/bin/bash
# fbterm-bi: a wrapper script to enable background image with fbterm
# usage: fbterm-bi /path/to/image fbterm-options
echo -ne "\e[?25l" # hide cursor
fbv -ciuker "$1" << EOF
q
EOF
shift
export FBTERM_BACKGROUND_IMAGE=1
exec /bin/fbterm "$@"

```

### White font color

By default, fbterm display the "white" text as a gray color, even using the -f 7 switch. Its possible to get real white by doing an echo once inside fbterm, like this

```
echo -en "\e]P7ffffff"

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Fbterm&oldid=403790](https://wiki.archlinux.org/index.php?title=Fbterm&oldid=403790)"