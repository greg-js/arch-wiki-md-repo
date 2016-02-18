[lemonbar](https://github.com/LemonBoy/bar) is a lightweight bar based on XCB. It provides foreground/background color switching along with text alignment and colored under/overlining of text, full utf8 support and reduced memory footprint. Nothing less and nothing more.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 Colors](#Colors)
    *   [3.2 Text alignment](#Text_alignment)
    *   [3.3 Examples](#Examples)

## Installation

[lemonbar-git](https://aur.archlinux.org/packages/lemonbar-git/) is available in the AUR and can be installed manually or through the use of a AUR helper of your choice.

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