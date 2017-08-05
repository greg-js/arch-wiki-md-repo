[llpp](http://repo.or.cz/w/llpp.git) is a lightweight, fast and featureful PDF, EPUB, XPS and CBZ viewer based on [MuPDF](/index.php/MuPDF "MuPDF").

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
    *   [3.1 UI Font](#UI_Font)
    *   [3.2 Custom key bindings](#Custom_key_bindings)
    *   [3.3 Save annotations to pdf](#Save_annotations_to_pdf)
*   [4 Tips and Tricks](#Tips_and_Tricks)
    *   [4.1 Reload File](#Reload_File)
    *   [4.2 Remote Interface](#Remote_Interface)
    *   [4.3 Clean up history](#Clean_up_history)
    *   [4.4 Inverse search using Synctex and Vim](#Inverse_search_using_Synctex_and_Vim)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [llpp](https://aur.archlinux.org/packages/llpp/) package, or [llpp-git](https://aur.archlinux.org/packages/llpp-git/) for the development version.

## Usage

llpp uses keyboard shortcuts and the mouse to navigate through a document. By default, pressing `F1` or `h` will bring up a help page where all other key bindings are described.

Check out the following page for a complete list of the [key and mouse bindings](http://repo.or.cz/w/llpp.git/blob_plain/master:/KEYS).

## Configuration

llpp uses a configuration file to store settings: `$XDG_CONFIG_HOME/llpp.conf` or `~/.config/llpp.conf`. This file stores: 1) application defaults, and 2) file-by-file user preferences (e.g. the last page viewed).

### UI Font

One can set the font used by llpp by indicating the size and filename in the config. For example:

```
<llppconfig>
  <ui-font size='16'><![CDATA[/usr/share/fonts/TTF/DejaVuSansMono.ttf]]></ui-font>
  <defaults ... >
  ...
  </defaults>
</llppconfig>

```

### Custom key bindings

It is possible to configure key bindings. For example, to disable `Esc` exiting llpp, add the `keymap` element in between the `defaults` tags as follows:

```
<llppconfig>
  <defaults ... >
    <keymap mode='view'>
      <map in='esc' out=*/>*
    </keymap>
  </defaults>
</llppconfig>

```

More examples can be found in llpp's example file [keys.txt](http://repo.or.cz/w/llpp.git/blob/HEAD:/misc/keys.txt). For vi-like key bindings, see [this example](https://gist.github.com/Earnestly/7608794).

**Tip:** Bindings can be set for particular modes, including `birdseye`, `global`, `help`, `info`, `listview`, `outline`, and `view`. Example [here](https://gist.github.com/holomorph/9d8e5f483465d92ee69c).

### Save annotations to pdf

You can annotate a pdf with `Shift + Right Click`. To allow saving of annotations add

```
   savepath-command='echo %s'

```

to your `llpp.conf`. After annotating the file save the changes by pressing `W`. This `echo`s the current pdf path to the option savepath-mmand

## Tips and Tricks

### Reload File

A document can be reloaded in three ways:

*   Pressing the `r` key
*   Sending a HUP signal to the llpp process

```
$ killall -SIGHUP llpp

```

*   Using the "remote" interface (see below)

### Remote Interface

The following commands will setup the remote interface and use it to reload the file "image.pdf".

```
$ mkfifo /tmp/llpp.remote
$ llpp -remote /tmp/llpp.remote image.pdf & disown
$ sleep 1
$ echo reload >/tmp/llpp.remote

```

There are eight remote commands:

*   `reload` - reload
*   `quit` - quit
*   `goto <page-number> <x-coordinate> <y-coordinate>` - goto
*   `goto1 <page-number> <relative-y-coordinate>` - goto
*   `gotor <file-name> <page-number>` - goto other document
*   `gotord <file-name> <remote-destination>` - goto named destination within the other document
*   `rect <pageno> <color> <x0> <y0> <x1> <y1>` - draw a rectangle
*   `activatewin` - raise and switch to llpp's window

### Clean up history

Files that no longer exist can be cleaned from llpp's history by using a "garbage collecting" script, such as the upstream python2 script [here](http://repo.or.cz/w/llpp.git/blob/HEAD:/misc/gc.py). Use the `-gc` flag:

```
$ llpp -gc /path/to/script
gc.py done.

```

### Inverse search using Synctex and Vim

To use the synctex capability of llpp, add the line bellow to your <tt>~/.config/llpp.conf</tt> under the <tt>defaults</tt> tag:

```
<defaults
    ...
    synctex-command='SyncTeX-inverse.sh'
    ...>
    ...
</defaults>

```

where <tt>SyncTeX-inverse.sh</tt> is the script bellow

```
#!/bin/bash
pdf_file=$1
page=$(($2 + 1)) # The page number star at zero in llpp
x=$3
y=$4

synctex edit -o "$page:$x:$y:$pdf_file" \
       -x "gvim --servername synctex --remote-wait-silent +%{line} %{input}"

```

Make sure <tt>SyncTeX-inverse.sh</tt> is an executable script and add it to your <tt>PATH</tt> environment variable. To use the <tt>synctex</tt> command you will need [texlive-bin](https://www.archlinux.org/packages/?name=texlive-bin) package from the official Arch repositories.

## See also

*   [llpp git repo](http://repo.or.cz/w/llpp.git)