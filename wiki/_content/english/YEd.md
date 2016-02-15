[yEd](http://www.yworks.com/en/products_yed_about.html) is a powerful graph editor, written in Java, that can be used to generate diagrams. Diagrams can be created manually, or be imported from external data for analysis. An automatic layout algorithm arranges the data sets if needed.

## Installation

[Install](/index.php/Install "Install") [yed](https://aur.archlinux.org/packages/yed/), which is available in the [AUR](/index.php/AUR "AUR"). It requires an installed Java runtime environment, such as [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) or [jre](https://aur.archlinux.org/packages/jre/).

Once installed, yEd can be run using the `yed` command.

## Tips & Tricks

### Font issues

If you encounter font issues, such as [glitchy fonts](http://i.imgur.com/mcvU014.png), try using the proprietary [jre](https://aur.archlinux.org/packages/jre/) instead of OpenJDK and add the following line to your shell's rc file:

```
export _JAVA_OPTIONS='-Dawt.useSystemAAFontSettings=lcd_hrgb'

```