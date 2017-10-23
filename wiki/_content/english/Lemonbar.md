[lemonbar](https://github.com/LemonBoy/bar) is a lightweight bar based on XCB. It provides foreground/background color switching along with text alignment and colored under/overlining of text, full UTF-8 support and reduced memory footprint. Nothing less and nothing more.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 Colors](#Colors)
    *   [3.2 Text alignment](#Text_alignment)
    *   [3.3 Examples](#Examples)
    *   [3.4 XFT fonts](#XFT_fonts)
        *   [3.4.1 Font Awesome icons](#Font_Awesome_icons)

## Installation

[Install](/index.php/Install "Install") the [lemonbar](https://aur.archlinux.org/packages/lemonbar/) package, or [lemonbar-git](https://aur.archlinux.org/packages/lemonbar-git/) for the development version.

## Configuration

Configuration of lemonbar is now completely done via `screenrc`-like format strings and command line options as opposed to older versions, where configuration took place at compile-time.

See the man page for a short overview of those configuration options.

## Usage

`lemonbar` prints no information on its own. To get any text into `lemonbar` you need to pipe text into it. The following example would write the text "Hello World" into your bar.

```
#!/bin/bash

# Echo the text
echo "Hello World"

```

If you want the text in `lemonbar` to update through a script, you need to add the `-p` option. This prevents `lemonbar` from exiting after stdin is closed.

#### Colors

`lemonbar` uses the following commands to color the text, background or the under/overline. Colors can be specified via the formats `#RRGGBB`, `#AARRGGBB` (with an alpha channel; this requires a compositor to be running), or even `#RGB`.

The special color `-` indicates the default color (which is set by command-line flags, or is otherwise the default white text on a black background).

| Command | Meaning |
| `%{F*color*}` | Use *color* as the foreground/font color |
| `%{B*color*}` | Use *color* as the background |
| `%{U*color*}` | Use *color* for under/overlining the text |

#### Text alignment

`lemonbar` also supports alignment of text. It uses the following commands to align the text

| Command | Meaning |
| `%{l}` | Aligns the text to the left |
| `%{c}` | Aligns the text to the center |
| `%{r}` | Aligns the text to the right |

#### Examples

The following example prints the date and time in the middle of the bar, the font's color being `yellow` and the background `blue` and changes the font/background color back to the default color afterwards. Run it with `/path/to/script/example.sh | lemonbar -p`

 `example.sh` 
```
#!/usr/bin/bash

# Define the clock
Clock() {
        DATETIME=$(date "+%a %b %d, %T")

        echo -n "$DATETIME"
}

# Print the clock

while true; do
        echo "%{c}%{F#FFFF00}%{B#0000FF} $(Clock) %{F-}%{B-}"
        sleep 1
done

```

Another example showing the battery percentage. To use this script you need to install [acpi](https://www.archlinux.org/packages/?name=acpi).

 `example.sh` 
```
#!/usr/bin/bash

#Define the battery
Battery() {
        BATPERC=$(acpi --battery | cut -d, -f2)
        echo "$BATPERC"
}

# Print the percentage
while true; do
        echo "%{r}$(Battery)"
        sleep 1;
done

```

#### XFT fonts

The default lemonbar version does not support XFT fonts. To get support for XFT fonts, you need to install [lemonbar-xft-git](https://aur.archlinux.org/packages/lemonbar-xft-git/), which replaces [lemonbar](https://aur.archlinux.org/packages/lemonbar/).

To use different font with lemonbar, you need to pass `-f` option when starting lemonbar e.g. `lemonbar -f "Roboto Medium"`.

##### Font Awesome icons

With XFT support, you can also add [font-awesome icons](http://fontawesome.io/) to your bar. You need to install [ttf-font-awesome](https://aur.archlinux.org/packages/ttf-font-awesome/) before using the icons and pass `-f "Font Awesome"` to lemonbar. Please note, that you also need to specify one more font (e.g. `-f "Roboto Medium"`) to be used for other symbols than font awesome icons if you want something else visible in your lemonbar as font awesome does not contain other symbols.

Before adding an icon to lemonbar, you need to look up its unicode id on the [icon list](http://fontawesome.io/icons/) and pass it to lemonbar string. Here is a script that displays icon with unicode id `f242` in lemonbar:

 `fontawesome.sh` 
```
#!/usr/bin/bash
echo -e "\uf242 Battery: 0"

```

Pay extra attention to `echo -e` flag, as it is necessary to properly use echo with escape sequences.

And corresponding lemonbar command: `lemonbar -f "Roboto Medium" -f "Font Awesome"`