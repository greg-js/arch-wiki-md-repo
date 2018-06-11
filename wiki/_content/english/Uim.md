[uim](https://github.com/uim/uim/wiki/WhatsUim) (universal input method) is a multilingual [input method](/index.php/Input_method "Input method") framework.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [uim](https://www.archlinux.org/packages/?name=uim) package.

## Usage

Add the following to [xprofile](/index.php/Xprofile "Xprofile") or [xinitrc](/index.php/Xinitrc "Xinitrc"):

```
export GTK_IM_MODULE=uim
export QT_IM_MODULE=uim
uim-xim &
export XMODIFIERS=@im=uim

```

*uim* provides several toolbars (`uim-toolbar-*`), if you want to autostart one you can also do it here.

## Configuration

*uim* provides several GUI preference editors (`uim-pref-*`).

Choose your preferred input method as *Default input method*.

You can run `uim-xim` or restart [X](/index.php/X "X") to test your settings.

## See also

*   [GitHub wiki introduction](https://github.com/uim/uim/wiki/WhatsUim)
*   [Wikibook introduction](https://en.wikibooks.org/wiki/Uim/Introduction "wikibooks:Uim/Introduction")
*   [Wikipedia:uim](https://en.wikipedia.org/wiki/uim "wikipedia:uim")