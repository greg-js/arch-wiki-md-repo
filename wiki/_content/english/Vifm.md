Related articles

*   [nnn](/index.php/Nnn "Nnn")
*   [ranger](/index.php/Ranger "Ranger")

From the [Vifm](http://vifm.info/) home page:

	Vifm is an ncurses based file manager with vi like keybindings/modes/options/commands/configuration, which also borrows some useful ideas from [mutt](/index.php/Mutt "Mutt").

If you use [vi](/index.php/Vi "Vi"), Vifm gives you complete keyboard control over your files without having to learn a new set of commands.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Help file](#Help_file)
*   [3 Customizing Vifm](#Customizing_Vifm)
    *   [3.1 Color schemes](#Color_schemes)
    *   [3.2 Key mapping](#Key_mapping)
    *   [3.3 Opening filetypes in vifm](#Opening_filetypes_in_vifm)
        *   [3.3.1 Browse images in current directory with Feh](#Browse_images_in_current_directory_with_Feh)
    *   [3.4 User commands](#User_commands)
        *   [3.4.1 Creating symbolic links](#Creating_symbolic_links)
        *   [3.4.2 Torrent creation](#Torrent_creation)
    *   [3.5 Marks](#Marks)
    *   [3.6 Previews](#Previews)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Useful key mappings](#Useful_key_mappings)
    *   [4.2 Non-vim Users](#Non-vim_Users)
    *   [4.3 Total size of selected files](#Total_size_of_selected_files)
    *   [4.4 Use output of external program in status line](#Use_output_of_external_program_in_status_line)

## Installation

[Install](/index.php/Install "Install") the [vifm](https://www.archlinux.org/packages/?name=vifm) package.

## Help file

Basic information about vifm is given in the help file. You can view it by opening vifm and typing

```
:h

```

Another good source of information is the man page.

## Customizing Vifm

Vifm creates and populates a .vifm folder in your home directory containing the following:

*   vifmrc - a well commented configuration file that can be edited to suit your working style.
*   vifm-help.txt - the help text
*   vifminfo - bookmarks and trash contents - it is not recommended to edit this file by hand
*   Trash/ directory - self explanatory
*   colors/ directory - color schemes
    *   Default - well commented default color scheme - can be copied to create user-created color schemes

To get started, read the information avaliable in:

*   `/usr/share/vifm/vifm.txt`
*   `/usr/share/vifm/vifm-help.txt`

### Color schemes

The `~/.vifm/colors` directory contains the color schemes. The format is outlined in the file and follows vi/vim syntax highlight format. It is basically:

```
highlight *group* cterm=*attribute* ctermfg=*color* ctermbg=*color*

```

An example colorscheme looks like:

```
highlight Win cterm=none ctermfg=white ctermbg=black
highlight Directory cterm=bold ctermfg=cyan ctermbg=none
highlight Link cterm=bold ctermfg=yellow ctermbg=none
highlight BrokenLink cterm=bold ctermfg=red ctermbg=none
highlight Socket cterm=bold ctermfg=magenta ctermbg=none
highlight Device cterm=bold ctermfg=red ctermbg=none
highlight Fifo cterm=bold ctermfg=cyan ctermbg=none
highlight Executable cterm=bold ctermfg=green ctermbg=none
highlight Selected cterm=bold ctermfg=magenta ctermbg=none
highlight CurrLine cterm=bold ctermfg=none ctermbg=blue
highlight TopLine cterm=none ctermfg=black ctermbg=white
highlight TopLineSel cterm=bold ctermfg=black ctermbg=none
highlight StatusLine cterm=bold ctermfg=black ctermbg=white
highlight WildMenu cterm=underline,reverse ctermfg=white ctermbg=black
highlight CmdLine cterm=none ctermfg=white ctermbg=black
highlight ErrorMsg cterm=none ctermfg=red ctermbg=black
highlight Border cterm=none ctermfg=black ctermbg=white

```

You can also highlight different filetypes using regular expressions:

```
highlight /^.*\.(mp3|ogg|oga|flac|m4a)$/ ctermfg=magenta
highlight /^.*\.(jpg|jpeg|png|gif|tiff|webp|bmp|svg|svgz)$/ ctermfg=yellow
highlight /^.*\.(zip|gz|bz2|xz|tar|tgz|tbz2|7z|rar|iso|rpm|deb)$/ ctermfg=red

```

### Key mapping

As of 0.6.2 you can customize key bindings in Vifm. These can be set from the command mode using the map command, like so:

```
:map ] :s

```

However, these mappings will not be saved between sessions. To map a key permanently, place them in `~/.vifm/vifmrc`. More sample mappings can be seen at the end of that file.

### Opening filetypes in vifm

You can assign applications to filetypes in vifmrc, eg.

```
filetype *.jpg,*.jpeg,*.png,*.gif feh %f 2>/dev/null &
filetype *.md5 md5sum -c %f

```

Several defaults can be found in vifmrc. These can be edited or added to following the same format.

#### Browse images in current directory with Feh

```
filextype *.jpg,*.jpeg,*.png,*.gif
       \ {View in feh}
       \ feh -FZ %d --start-at %d/%c 2>/dev/null

```

It will display your selected image in feh, but it will enable you to browse all other images in the directory as well, in their default order.

### User commands

You can also create custom commands in vifmrc, eg.

```
command df df -h %m 2> /dev/null
command diff vim -d %f %F

```

#### Creating symbolic links

```
command link ln -s %d/%f %D

```

When you call

```
:link

```

a link of the selected file is made in the other directory (if you are in split view). It even works with multiple files selected with visual (v) or tag (t).

#### Torrent creation

make a .torrent of the current file in the other tab's dir

```
command mkt mktorrent -p -a [your announce url here] -o %D/%f.torrent %d/%f

```

### Marks

Marks can be set same as in vi. To set a mark for current file:

```
m[a-z][A-Z][0-9]

```

Go to a file set for mark:

```
'[a-z][A-Z][0-9]

```

Vifm will remember the marks between the sessions.

### Previews

Provided [poppler](https://www.archlinux.org/packages/?name=poppler) is installed, putting

```
fileviewer *.pdf
  \ pdftotext %c -

```

into vifmrc enables pdf-previewing using pdftotext. The `%c` is a vifm macro for the current file under the cursor. The preview is activated with

```
:view

```

Neat image previewing can be achieved using img2txt from [libcaca](https://www.archlinux.org/packages/?name=libcaca)

```
fileviewer *.png,*.jpeg,*.jpg
 \ img2txt %c 

```

Previewing the contents of tar-archives:

```
fileviewer *.tar,*.tar.gz
 \ tar -tvf %c

```

For previewing html documents suitable programs are text based browsers including [lynx](https://www.archlinux.org/packages/?name=lynx), [links](https://www.archlinux.org/packages/?name=links) or [w3m](https://www.archlinux.org/packages/?name=w3m)

```
fileviewer *.html
 \ w3m %c

```

For printing text instead of previewing the file (for binary files for example):

```
fileviewer *.exe
 \ echo Binary file: no preview available. %i

```

`%i` is there because `%c` is implicitly used if no other macro is used. In this case, `%i` is ignored.

For handling filetypes not handled by anything else, put `fileviewer * <your command>` as the last fileviewer option in your config file.

Further useful programs for previews include

*   [tree](https://www.archlinux.org/packages/?name=tree) for directory previews
*   [mp3info](https://www.archlinux.org/packages/?name=mp3info) for viewing information about mp3 files
*   [libmediainfo](https://www.archlinux.org/packages/?name=libmediainfo) for the mediainfo program (audio and video information)

## Tips and tricks

### Useful key mappings

Single stroke to access command line

```
nmap ; :

```

### Non-vim Users

`vifm` assumes that you are using `vim` and will throw errors if it doesn't find it. If you are using `vi` or `nvim` ([Neovim](/index.php/Neovim "Neovim")), you need to edit your `~/.vifm/vifmrc` file. Comment out the line `set vicmd=vim` and replace it with `set vicmd=vi` or `set vicmd=nvim`. Note that, just like `.exrc`, comment lines are introduced by double quotes.

### Total size of selected files

To get the total size of selected files change %s to %E in `~/.vifm/vifmrc`, like so:

```
set statusline="  %t%= %A %10u:%-7g %15E %20d  "

```

### Use output of external program in status line

Here's a status line that calls [lsattr](/index.php/File_permissions_and_attributes#chattr_and_lsattr "File permissions and attributes"), passing it the name of the file currently under the cursor:

```
set statusline="%{system('lsattr -l ' . expand('%c'))}"

```

For more, see [expression syntax](https://vifm.info/manual.shtml#Expression%20syntax) and available [functions](https://vifm.info/manual.shtml#Functions).