# Lemonbar

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[lemonbar](https://github.com/LemonBoy/bar) is a lightweight bar based on XCB. It provides foreground/background color switching along with text alignment and colored under/overlining of text, full utf8 support and reduced memory footprint. Nothing less and nothing more.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 Colors](#Colors)
    *   [3.2 Text alignment](#Text_alignment)
    *   [3.3 Examples](#Examples)

## Installation

[lemonbar-git](https://aur.archlinux.org/packages/lemonbar-git/)<sup><small>AUR</small></sup> is available in the AUR and can be installed manually or through the use of a AUR helper of your choice.

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

`lemonbar` uses the following commands to color the text, background or the under/overline. Colors are to be specified via their symbolic names or in #AARRGGBB notation.

<table border="1">

<tbody>

<tr>

<th>Command</th>

<th>Meaning</th>

</tr>

<tr>

<td>`%{F#}`</td>

<td>Uses the # color as the font's color</td>

</tr>

<tr>

<td>`%{B#}`</td>

<td>Uses the # color as the background</td>

</tr>

<tr>

<td>`%{U#}`</td>

<td>Uses the # color for under/overlining the text</td>

</tr>

</tbody>

</table>

#### Text alignment

`lemonbar` also supports alignment of text. It uses the following commands to align the text

<table border="1">

<tbody>

<tr>

<th>Command</th>

<th>Meaning</th>

</tr>

<tr>

<td>`%{l}`</td>

<td>Aligns the text to the left</td>

</tr>

<tr>

<td>`%{c}`</td>

<td>Aligns the text to the center</td>

</tr>

<tr>

<td>`%{r}`</td>

<td>Aligns the text to the right</td>

</tr>

</tbody>

</table>

#### Examples

The following example prints the date and time in the middle of the bar, the font's color being `yellow` and the background `blue` and changes the font's color back to the default color afterwards. Run it with `/path/to/script/example.sh | lemonbar -p`

 `example.sh` 

```
#!/usr/bin/bash

# Define the clock
Clock() {
        DATE=$(date "+%a %b %d, %T")

        echo -n "$DATE"
}

# Print the clock

while true; do
        echo "%{c}%{Fyellow}%{Bblue} $(Clock)%{F-}"
        sleep 1;
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

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lemonbar&oldid=410613](https://wiki.archlinux.org/index.php?title=Lemonbar&oldid=410613)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Eye candy](/index.php/Category:Eye_candy "Category:Eye candy")