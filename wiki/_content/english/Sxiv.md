[sxiv](https://github.com/muennich/sxiv), Simple [X](/index.php/Xorg "Xorg") Image Viewer is a lightweight and scriptable image viewer written in C.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Assigning keyboard shortcuts](#Assigning_keyboard_shortcuts)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Browse through images in directory after opening a single file](#Browse_through_images_in_directory_after_opening_a_single_file)
    *   [3.2 Showing the image size in the status bar](#Showing_the_image_size_in_the_status_bar)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [sxiv](https://www.archlinux.org/packages/?name=sxiv) package, or [sxiv-git](https://aur.archlinux.org/packages/sxiv-git/) for the development version.

## Usage

### Assigning keyboard shortcuts

sxiv supports external key events. First you have to press `Ctrl-x` to send the next key to the external key-handler. The external key-handler requires an executable file `~/.config/sxiv/exec/key-handler` and passes the key combination pressed via argument as well the names of the currently marked images as stdin (or, if none are marked, the currently selected image).

In this example, we will add the bindings `Ctrl+d` to execute `mv *filename* ~/.trash`, `Ctrl+c` to copy the current images' names to the clipboard with [xclip](https://www.archlinux.org/packages/?name=xclip), and `Ctrl+w` to set the current wallpaper with [nitrogen](/index.php/Nitrogen "Nitrogen"). Obviously, some commands may only make sense with a single image as an argument, so you may want to revise this to handle cases when those are passed more than one.

 `~/.config/sxiv/exec/key-handler` 
```
#!/bin/sh
while read file
do
        case "$1" in
        "C-d")
                mv "$file" ~/.trash ;;
        "C-r")
                convert -rotate 90 "$file" "$file" ;;
        "C-c")
                echo -n "$file" | xclip -selection clipboard ;;
        "C-w")
                nitrogen --save --set-zoom-fill "$file" ;;
        esac
done

```

Be sure to mark the script as executable

```
$ chmod +x ~/.config/sxiv/exec/key-handler

```

Create `.trash` folder if it does not exist:

```
$ mkdir ~/.trash

```

**Tip:** You may want to use a [standards-compliant trashcan](https://freedesktop.org/wiki/Specifications/trash-spec/) (like [trash-cli](https://www.archlinux.org/packages/?name=trash-cli) or [bashtrash](https://aur.archlinux.org/packages/bashtrash/)) rather than `mv "$2" ~/.trash`.

## Tips and tricks

### Browse through images in directory after opening a single file

Place [this script](https://github.com/ranger/ranger/blob/master/examples/rifle_sxiv.sh) in `/usr/local/bin` and call it like this:

```
$ *scriptname* a_single_image.jpg

```

Alternatively you can also install the script as a package from the AUR: [sxiv-rifle](https://aur.archlinux.org/packages/sxiv-rifle/).

As indicated in the comments of the script, it may be used to have this behavior when opening images from within [ranger](/index.php/Ranger "Ranger").

### Showing the image size in the status bar

Place the following executable script in `~/.config/sxiv/exec/image-info` and make sure that you have the [exiv2](https://www.archlinux.org/packages/?name=exiv2) package installed:

 `~/.config/sxiv/exec/image-info` 
```
#!/bin/sh

# Example for ~/.config/sxiv/exec/image-info
# Called by sxiv(1) whenever an image gets loaded,
# with the name of the image file as its first argument.
# The output is displayed in sxiv's status bar.

s=" | " # field separator

filename=$(basename "$1")
filesize=$(du -Hh "$1" | cut -f 1)

# The '[0]' stands for the first frame of a multi-frame file, e.g. gif.
geometry=$(identify -format '%wx%h' "$1[0]")

tags=$(exiv2 -q pr -pi "$1" | awk '$1~"Keywords" { printf("%s,", $4); }')
tags=${tags%,}

echo "${filesize}${s}${geometry}${tags:+$s}${tags}${s}${filename}"

```

## See also

*   Arch Linux [forum thread](https://bbs.archlinux.org/viewtopic.php?id=112643).
*   Sxiv for keyboard layout [bépo](https://en.wikipedia.org/wiki/Keyboard_layout#B.C3.89PO "wikipedia:Keyboard layout") (keyboard layout in the spirit of [Dvorak](https://en.wikipedia.org/wiki/Dvorak_Simplified_Keyboard "wikipedia:Dvorak Simplified Keyboard") for French speakers) : [Sxiv bépo](https://bepo.fr/wiki/Vim#Visionneuse_d.27image_Sxiv).