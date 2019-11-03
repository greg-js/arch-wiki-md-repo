[Ripcord](https://cancel.fm/ripcord/) is a lightweight desktop chat client for group-centric services like [Slack](/index.php/Slack "Slack") and [Discord](/index.php/Discord "Discord") built upon the [Qt](/index.php/Qt "Qt") toolkit. It is proprietary, closed-source software released under a [shareware license](https://cancel.fm/ripcord/shareware-redistribution/) which allows the Discord module to be used free of charge while locking Slack usage behind purchase.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Custom themes](#Custom_themes)
*   [3 Emoji glitch](#Emoji_glitch)
*   [4 Using system libraries](#Using_system_libraries)
*   [5 IME](#IME)

## Installation

Install the [ripcord](https://aur.archlinux.org/packages/ripcord/) package.

## Custom themes

See the following [guide](https://dev.cancel.fm/wiki?name=Custom_Themes). The directory containing `settings.ini` is `$HOME/.local/share/Ripcord`.

## Emoji glitch

There is a bug with some emoji fonts (known: [noto-fonts-emoji](https://www.archlinux.org/packages/?name=noto-fonts-emoji), [ttf-joypixels](https://www.archlinux.org/packages/?name=ttf-joypixels), [ttf-twemoji](https://aur.archlinux.org/packages/ttf-twemoji/)) which generates rendering glitches, currently not fixed.

Emoji fonts known to behave well include [ttf-twemoji-color](https://aur.archlinux.org/packages/ttf-twemoji-color/) and [ttf-symbola](https://aur.archlinux.org/packages/ttf-symbola/), so it is recommended to use one of them. Otherwise, the Experimental tab of the Preferences window offers an option to override the system font for Ripcord only.

Some users have reported that [using system libraries](#Using_system_libraries) solves the issue.

For further updates and information, see the relevant [ticket](https://dev.cancel.fm/tktview?name=d2dc78360c) on the issue tracker.

## Using system libraries

**Warning:** The following hack is not supported or guaranteed to work in any way.

The Ripcord AppImage bundles its own copy of required libraries, which are also used by the AUR package. It is however possible to force the program to load libraries preexisting in the system. The main advantage of this is better integration with the [desktop environment](/index.php/Desktop_environment "Desktop environment") and Arch as a whole. The main disadvantage is that system libraries might be incompatible with the Ripcord release in use.

Proceed as follows:

*   Install packages [qt5-base](https://www.archlinux.org/packages/?name=qt5-base), [qt5-imageformats](https://www.archlinux.org/packages/?name=qt5-imageformats), [qt5-multimedia](https://www.archlinux.org/packages/?name=qt5-multimedia), [qt5-svg](https://www.archlinux.org/packages/?name=qt5-svg), [qt5-websockets](https://www.archlinux.org/packages/?name=qt5-websockets) and [qt5-x11extras](https://www.archlinux.org/packages/?name=qt5-x11extras) (more may be necessary, if you find so please amend this list).
*   Reach directory `/usr/lib/ripcord` or, if you'd rather not touch managed files, download the AppImage, run it with `--appimage-extract` and cd to `squashfs-root`.
*   Wipe or better move to a backup location the contents of the `lib` folder you find there, leaving the folder itself intact.
*   Run `ln -s /usr/lib/libsodium.so lib/libsodium.so.18`.
*   Delete or move to a backup location the whole `plugins` folder.
*   Set environment variable `QT_QPA_PLATFORM_PLUGIN_PATH=/usr/lib/qt/plugins`.

**Note:** A recent update in some Qt component makes Ripcord versions 0.4 to 0.4.15 (included) crash when using Phantom, their own default style engine. To run those versions of the software, the following additional steps are necessary.

*   Set environment variable `RIPCORD_STYLE_ENGINE=wrong` and run the executable. The program will crash, but a list of QStyle engines available to use should still get printed to terminal. **Choose one that isn't Phantom.**
*   Set environment variable `RIPCORD_STYLE_ENGINE` to the one you chose, e.g. `RIPCORD_STYLE_ENGINE=Fusion`.

Finally, run the executable.

## IME

If you need to use an [input method](/index.php/Input_method "Input method") framework, [IBus](/index.php/IBus "IBus") is known to behave well out of the box, while [Fcitx](/index.php/Fcitx "Fcitx") seems to require using [using system libraries](#Using_system_libraries).