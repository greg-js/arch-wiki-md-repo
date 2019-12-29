Related articles

*   [X resources](/index.php/X_resources "X resources")

[Xsettingsd](https://github.com/derat/xsettingsd) is a lightweight xsettings daemon which provides settings to [Xorg](/index.php/Xorg "Xorg") applications via the [XSETTINGS specification](https://specifications.freedesktop.org/xsettings-spec/xsettings-latest.html) when not running one (like when using [KDE](/index.php/KDE "KDE")). Some applications like [Java](/index.php/Java "Java") or [Wine](/index.php/Wine "Wine") does not get the font settings through [fontconfig](https://www.archlinux.org/packages/?name=fontconfig) so this is necessary to provide setting like anti-aliasing and font hinting.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
*   [4 See also](#See_also)

## Installation

Install [xsettingsd](https://www.archlinux.org/packages/?name=xsettingsd) or [xsettingsd-git](https://aur.archlinux.org/packages/xsettingsd-git/).

## Configuration

See [https://github.com/derat/xsettingsd/wiki/Settings](https://github.com/derat/xsettingsd/wiki/Settings) for detailed syntax.

An example configuration to provide better font rendering:

 `~/.xsettingsd` 
```
Xft/Hinting 1
Xft/HintStyle "hintslight"
Xft/Antialias 1
Xft/RGBA "rgb"

```

## Usage

Configure setting in [#Configuration](#Configuration) and append `xsettingsd &` to `~/.xinitrc` if you are using [xinit](/index.php/Xinit "Xinit") or `~/.xprofile` if you are using a [Display manager](/index.php/Display_manager "Display manager") (see [Autostarting](/index.php/Autostarting "Autostarting") for more details).

## See also

*   [xsettingsd wiki](https://github.com/derat/xsettingsd/wiki)