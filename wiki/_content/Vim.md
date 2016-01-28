# Vim

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [List of applications/Documents#Vi_text_editors](/index.php/List_of_applications/Documents#Vi_text_editors "List of applications/Documents")

[Vim](https://en.wikipedia.org/wiki/Vim_(text_editor) "wikipedia:Vim (text editor)") is a [terminal](https://en.wikipedia.org/wiki/Computer_terminal#Text_terminals "wikipedia:Computer terminal") text editor, an extended version of [vi](https://en.wikipedia.org/wiki/vi "wikipedia:vi") with additional features. To primarily help with editing source code some of Vim's added features include syntax highlighting, a comprehensive help system, native scripting (vimscript), a visual mode for text selection, and comparison of files (vimdiff).

Vim's focus is keyboard-centric and is not a simple text editor like nano or pico—it requires time to learn, and a lifetime to master.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Basic editing](#Basic_editing)
    *   [2.2 Moving around](#Moving_around)
    *   [2.3 Repeating commands](#Repeating_commands)
    *   [2.4 Deleting](#Deleting)
    *   [2.5 Undo and redo](#Undo_and_redo)
    *   [2.6 Visual mode](#Visual_mode)
    *   [2.7 Search and replace](#Search_and_replace)
    *   [2.8 Saving, quitting, and opening](#Saving.2C_quitting.2C_and_opening)
    *   [2.9 Additional commands](#Additional_commands)
*   [3 Configuration](#Configuration)
    *   [3.1 Syntax highlighting](#Syntax_highlighting)
    *   [3.2 Visual wrapping](#Visual_wrapping)
    *   [3.3 Using the mouse](#Using_the_mouse)
    *   [3.4 Traverse line breaks with arrow keys](#Traverse_line_breaks_with_arrow_keys)
    *   [3.5 Example ~/.vimrc](#Example_.7E.2F.vimrc)
*   [4 Merging files](#Merging_files)
*   [5 Tips and recommendations](#Tips_and_recommendations)
    *   [5.1 Help system](#Help_system)
    *   [5.2 Line numbers](#Line_numbers)
    *   [5.3 Spell checking](#Spell_checking)
    *   [5.4 Save cursor position](#Save_cursor_position)
    *   [5.5 Replace vi command with Vim](#Replace_vi_command_with_Vim)
    *   [5.6 DOS/Windows carriage returns](#DOS.2FWindows_carriage_returns)
    *   [5.7 Empty space at the bottom of gVim windows](#Empty_space_at_the_bottom_of_gVim_windows)
*   [6 Plugins](#Plugins)
    *   [6.1 Installation](#Installation_2)
        *   [6.1.1 Using a plugin manager](#Using_a_plugin_manager)
        *   [6.1.2 From Arch repositories](#From_Arch_repositories)
    *   [6.2 cscope](#cscope)
    *   [6.3 Taglist](#Taglist)
*   [7 See also](#See_also)
    *   [7.1 Official](#Official)
    *   [7.2 Tutorials](#Tutorials)
        *   [7.2.1 Videos](#Videos)
        *   [7.2.2 Games](#Games)
    *   [7.3 Example configurations](#Example_configurations)
    *   [7.4 Other](#Other)

## Installation

[Install](/index.php/Install "Install") one of the following packages:

*   [vim](https://www.archlinux.org/packages/?name=vim) — with Python 2/3, Lua, Ruby and Perl interpreters support but without GTK/X support.
*   [gvim](https://www.archlinux.org/packages/?name=gvim) — which also provides the same as the above `vim` package with GTK/X support.

**Note:**

*   The CLI Vim packages are built with **no** X.org display server support; these builds are missing the `+clipboard` feature so Vim will not be able to operate with the X.org _primary_ and _clipboard_ buffers. For X.org clipboard support install a GUI package will also install the CLI version with this extended feature.
*   The unofficial repository [herecura-stable](/index.php/Unofficial_user_repositories#herecura-stable "Unofficial user repositories") also provides a number of Vim/gVim variants: `vim-cli`, `vim-gvim-common`, `vim-gvim-gtk`, `vim-gvim-qt`, `vim-rt` and `vim-tiny`.

## Usage

This is a basic overview on how to use Vim. Alternately, running _vimtutor_/_gvimtutor_ will launch the embedded tutorial.

Vim has four different modes:

*   Command mode: keystrokes are interpreted as commands.
*   Insert mode: keystrokes are entered into the text.
*   Visual mode: keystrokes select, cut, or copy text.
*   [Ex](https://en.wikipedia.org/wiki/Ex_(text_editor) "wikipedia:Ex (text editor)") mode: input mode for additional commands (e.g. saving a file, replacing text and so on).

### Basic editing

If you start Vim with:

```
$ vim _somefile.txt_

```

you will see a blank document (providing that `_somefile.txt_` does not exist; if it does, you will see what is in there). You will not be able to edit right away — you are in Command mode. In this mode you are able to issue commands to Vim with the keyboard.

**Note:** Vim is an example of classic Unix-style ware. It has a difficult learning curve, but once you get started, you will find that it is extremely powerful. Also, all commands are case sensitive. Sometimes the uppercase versions are "blunter" versions (i.e. `s` will replace a character, while `S` will replace a whole line). Other times they are completely different commands (`j` will move down, while `J` will join two lines).

You insert text (stick it before the cursor) with the `i` command. Uppercase `I` inserts text at the beginning of the line. You append text with `a`. Typing `A` will place the cursor at the end of the line. And you return to command mode at any time by pressing `Esc`.

### Moving around

You can move the cursor with the arrow keys, but this isn't the **Vim way**. You'd have to move your right hand all the way from the standard typing position all the way to the arrow keys, and then back. Not fun.

To move down press `j`; to move the cursor back up press `k`. Left is `h`, and right is `l` (lowercase `L`).

`^` will put the cursor at the beginning of the line, and `$` will place it at the end.

**Note:** `^` and `$` are commonly used in regular expressions to match the beginning and ending of the line. Regular expressions are very powerful and are commonly used in *nix environment, so maybe it is a little bit tricky now, but later you will notice "the idea" behind the use of most of these key mappings.

To advance a word, press the `w` key. `W` will include more characters in what it thinks is a word (e.g. underscores and dashes as a part of a word). To go back a word, `b` is used. Once again, `B` will include more characters in what Vim considers a word. To advance to the end of a word, use `e`, `E` includes more characters.

To advance to the beginning of a sentence, `(` will get the job done. `)` will do the opposite, moving to the end of a sentence. For an even bigger jump, `{` will move the the beginning a whole paragraph. `}` will advance to the end of a whole paragraph.

To advance to the header (top) of the screen, `H` will get the job done. `M` will advance to the middle of the screen, and `L` will advance to the last (bottom). `gg` will go to the beginning of the file, `G` will go to the end of the file.

### Repeating commands

If a command is prefixed by a number, then that command will be executed that number of times over (there are exceptions, but they still make sense, like the `s` command). For example, pressing `3i` then `Help!` then `Esc` will print `Help! Help! Help!`. Pressing `2}` will advance you two paragraphs. This comes in handy with the next few commands.

### Deleting

The `x` command will delete the character under the cursor. `X` will delete the character before the cursor. This is where those number functions get fun. `6x` will delete 6 characters. Pressing `.` (dot) will repeat the previous command. So, lets say you have the word `foobar` in a few places, but after thinking about it, you'd like to see just `foo`. Move the cursor under the `b` and hit `3x`. Now move to the `b` symbol of the next `foobar` and hit `.` (dot).

The `d` will tell Vim that you want to delete something. After pressing `d`, you need to tell Vim what to delete. Here you can use the movement commands. `dW` will delete up to the next word. `d^` will delete up unto the beginning of the line. Prefacing the delete command with a number works well too: `3dW` will delete the next three words. `D` (uppercase) is a shortcut to delete until the end of the line (basically `d$`). Pressing `dd` will delete the whole line.

To delete then replace the current word, place the cursor on the word and execute the command `cw`. This will delete the word and change to insert mode. Use `s` to replace a single letter and go into insert mode. `S` will erase the whole line and place you in insert mode. To just replace a single letter use `r`, `R` will put you in replace mode.

### Undo and redo

Vim has a built-in clipboard (also known as a buffer). Actions can be undone with `u` and redone with `Ctrl+r`.

### Visual mode

Pressing `v` will put you in visual mode. Here you can move around to select text, when you're done, you press `y` to yank the text into the buffer (copy), or you may use `c` to cut. `p` pastes after the cursor, `P` pastes before. `V`, Visual Line mode, is the same for entire lines. `Ctrl+v` is for blocks of text.

**Note:** Whenever you delete something, that something is placed inside a buffer and is available for pasting.

### Search and replace

To search for a word or character in the file, simply use `/` and then the characters your are searching for and press `Enter`. To view the next match in the search press `n`, press `N` for the previous match.

To [search and replace](http://vim.wikia.com/wiki/Search_and_replace) use the substitute `:s/` command. The syntax is: `_[range]_s///_[arguments]_`. For example:

```
Command         Outcome
:s/xxx/yyy/     Replace xxx with yyy at the first occurrence
:s/xxx/yyy/g    Replace xxx with yyy at every occurrence in the current line
:s/xxx/yyy/gc   Replace xxx with yyy at every occurrence in the current line, with confirm
:%s/xxx/yyy/g   Replace xxx with yyy global in the whole file
:#,#s/xxx/yyy/g Replace xxx with yyy line number range

```

You can use the global `:g/` command to search for patterns and then execute a command for each match. The syntax is: `_[range]_:g//_[cmd]_`.

Command Outcome

g/^#/d Delete all lines that begins with #

g/^$/d Delete all lines that are empty

### Saving, quitting, and opening

To save and/or quit, you will need to use Ex mode. Ex mode commands are preceded by a `:`. To write a file use `:w` or if you wish to create a new file `:w _filename_`. Quitting is done with `:q`. If you choose not to save your changes, use `:q!`. To save and quit type `:x`. To open a new file use `:e _filename_`, type just `:e` to reload the file.

### Additional commands

1.  `dd` will delete the current line (`ddp` for quick line switching).
2.  `cc` will delete the current line and place you in insert mode.
3.  `o` will create a newline below the line and put you insert mode, `O` will create a newline above the line and put you in insert mode.
4.  `yy` will yank an entire line to the buffer
5.  `*` will highlight the current word and `n` will search it

## Configuration

Vim's user-specific configuration file is located in the home directory: `~/.vimrc`, and Vim files of current user are located inside `~/.vim/`. The global configuration file is located at `/etc/vimrc`. Global Vim files are located inside `/usr/share/vim/`.

To get some commonly expected behaviors (such as syntax highlighting), add the Vim example configuration to `/etc/vimrc`:

 `/etc/vimrc/` 

```
...

runtime! vimrc_example.vim

```

### Syntax highlighting

To enable syntax highlighting (Vim supports a huge list of programming languages):

```
:filetype plugin on
:syntax on

```

### Visual wrapping

The `wrap` option is on by default, which instructs Vim to wrap lines longer than the width of the window, so that the rest of the line is displayed on the next line. The `wrap` option only affects how text is displayed, the text itself is not modified.

The wrapping normally occurs after the last character that fits the window, even when it is in the middle of a word. More intelligent wrapping can be controlled with the `linebreak` option. When it is enabled with `set linebreak`, the wrapping occurs after characters listed in the `breakat` string option, which by default contains a space and some punctuation marks (see `:help breakat`).

Wrapped lines are normally displayed at the beginning of the next line, regardless of any indentation. The [breakindent](https://retracile.net/wiki/VimBreakIndent) option instructs Vim to take indentation into account when wrapping long lines, so that the wrapped lines keep the same indentation of the previously displayed line. The behaviour of `breakindent` can be fine-tuned with the `breakindentopt` option, for example to shift the wrapped line another four spaces to the right for Python files (see `:help breakindentopt` for details):

```
autocmd FileType python set breakindentopt=shift:4

```

### Using the mouse

Vim has the ability to make use of the mouse, but it only works for certain terminals (on Linux it is [xterm](/index.php/Xterm "Xterm") and Linux console with [gpm](https://www.archlinux.org/packages/?name=gpm), see [Console mouse support](/index.php/Console_mouse_support "Console mouse support") for details).

To enable this feature, add this line into `~/.vimrc`:

```
set mouse=a

```

**Note:**

*   This even works in PuTTY over SSH.
*   In PuTTY, the normal highlight/copy behavior is changed because Vim enters visual mode when the mouse is used. To select text with the mouse normally, hold down the `Shift` key while selecting text.

### Traverse line breaks with arrow keys

By default, pressing `←` at the beginning of a line, or pressing `→` at the end of a line, will not let the cursor traverse to the previous, or following, line.

The default behavior can be changed by adding `set whichwrap=b,s,<,>,[,]` to your `~/.vimrc` file.

### Example ~/.vimrc

See [Vim/.vimrc](/index.php/Vim/.vimrc "Vim/.vimrc").

## Merging files

Vim includes a diff editor (a program that shows differences between two or more files and aids to conveniently merge them). Use _vimdiff_ to run the diff editor — just specify some couple of files to it: `vimdiff _file1_ _file2_`. Here is the list of _vimdiff_-specific commands. For basic `vim` editing, read the tutorial in the [#Usage](#Usage) section.

<table class="wikitable">

<tbody>

<tr>

<th>Action</th>

<th>Shortcut</th>

</tr>

<tr>

<td>next change</td>

<td>`]c`</td>

</tr>

<tr>

<td>previous change</td>

<td>`[c`</td>

</tr>

<tr>

<td>diff obtain</td>

<td>`do`</td>

</tr>

<tr>

<td>diff put</td>

<td>`dp`</td>

</tr>

<tr>

<td>fold open</td>

<td>`zo`</td>

</tr>

<tr>

<td>fold close</td>

<td>`zc`</td>

</tr>

<tr>

<td>rescan files</td>

<td>`:diffupdate`</td>

</tr>

<tr>

<td>switch windows</td>

<td>`Ctrl+w+w`</td>

</tr>

</tbody>

</table>

## Tips and recommendations

Some tips and recommendations that may help a user with Vim's workflow.

### Help system

Vim includes a broad help system that can be accessed by typing `:h` or `:h _subject_`; subjects include basic usage to configuration options. Other subjects that are highlighted and can be jumped to by placing the cursor on them and typing `Ctrl-]`, use `Ctrl-T` to go back. Type `:q` to close the help window.

### Line numbers

Show line number column with `:set number`; show relative line number column with `:set relativenumber`; and jump to a line number with `:_line number_` or `_line number_gg`.

### Spell checking

Vim has the ability to do spell checking, enable by entering:

```
set spell

```

By default, only English language dictionaries are installed. More dictionaries can be found in the [official repositories](/index.php/Official_repositories "Official repositories") by searching for `vim-spell`. Additional dictionaries can be found in the [Vim's FTP archive](http://ftp.vim.org/vim/runtime/spell/). Additional dictionaries can be put in the folder `~/.vim/spell/` and enabled with the command: `:setlocal spell spelllang=_en_us_` (replacing the `_en_us_` with the name of the needed dictionary).

<table class="wikitable">

<tbody>

<tr>

<th>Action</th>

<th>Shortcut</th>

</tr>

<tr>

<td>next spelling</td>

<td>`]s`</td>

</tr>

<tr>

<td>previous spelling</td>

<td>`[s`</td>

</tr>

<tr>

<td>spelling suggestions</td>

<td>`z=`</td>

</tr>

<tr>

<td>spelling good, add</td>

<td>`zg`</td>

</tr>

<tr>

<td>spelling good, session</td>

<td>`zG`</td>

</tr>

<tr>

<td>spelling wrong, add</td>

<td>`zw`</td>

</tr>

<tr>

<td>spelling wrong, session</td>

<td>`zW`</td>

</tr>

<tr>

<td>spelling repeat all in file</td>

<td>`:spellr`</td>

</tr>

</tbody>

</table>

**Tip:**

*   To enable spelling in two languages (for instance English and German), add `set spelllang=_en,de_` into your `~/.vimrc` or `/etc/vimrc`, and then restart Vim.
*   You can enable spell checking for arbitrary file types (e.g. _.txt_) by using the FileType plugin and a custom rule for file type detection. To enable spell checking for any file ending with _.txt_, create the file `/usr/share/vim/vimfiles/ftdetect/plaintext.vim`, and insert the line `autocmd BufRead,BufNewFile *.txt setfiletype plaintext` into that file. Next, insert the line `autocmd FileType plaintext setlocal spell spelllang=_en_us_` into your `~/.vimrc` or `/etc/vimrc`, and then restart Vim.
*   To enable spell checking for LaTeX (or TeX) documents only, add `autocmd FileType **tex** setlocal spell spelllang=_en_us_` into your `~/.vimrc` or `/etc/vimrc`, and then restart Vim.

### Save cursor position

If you want the cursor to [appear in its previous position](http://vim.wikia.com/wiki/Restore_cursor_to_file_position_in_previous_editing_session) after you open a file, add the following to your `~/.vimrc`:

```
augroup resCur
  autocmd!
  autocmd BufReadPost * call setpos(".", getpos("'\""))
augroup END

```

### Replace vi command with Vim

Create an [alias](/index.php/Alias "Alias") for `vi` to `vim`.

Alternatively, if you want to be able to type `sudo vi` and get `vim`, install [vi-vim-symlink](https://aur.archlinux.org/packages/vi-vim-symlink/)<sup><small>AUR</small></sup> which will remove `vi` and replace it with a symlink to `vim`.

### DOS/Windows carriage returns

If there is a `^M` at the end of each line then this means you are editing a text file which was created in MS-DOS or Windows. This is because in Linux only a single line feed character (LF) used for line break, but in Windows/MS DOS systems they are using a sequence of a carriage return (CR) and a line feed (LF) for the same. And this carriage returns are displayed as `^M`.

To remove all carriage returns from a file do:

```
:%s/^M//g

```

Note that there `^` is a control letter. To enter the control sequence `^M` press `Ctrl+v,Ctrl+m`.

Alternatively install the package [dos2unix](https://www.archlinux.org/packages/?name=dos2unix) and run `dos2unix _file_` to fix the file.

### Empty space at the bottom of gVim windows

When using a [window manager](/index.php/Window_manager "Window manager") configured to ignore window size hints, gVim will fill the non-functional area with the GTK theme background color.

The solution is to adjust how much space gVim reserves at the bottom of the window. Put the following line in `~/.vimrc`:

```
set guiheadroom=0

```

**Note:** If you set it to zero, you will not be able to see the bottom horizontal scrollbar.

## Plugins

Adding plugins to Vim can increase your productivity. Plugins can alter Vim's UI, add new commands, code completion support, integrate other programs and utilities with Vim, add support for additional languages and more.

### Installation

#### Using a plugin manager

A plugin manager allows to install and manage Vim plugins in a similar way independently on which platform you are running Vim. It is a plugin that acts as a package manager for other Vim plugins.

*   [Vundle](https://github.com/gmarik/Vundle.vim) is currently the most popular plugin manager for Vim.
*   [Vim-plug](https://github.com/junegunn/vim-plug) is a minimalist Vim plugin manager with many features like on-demand plugin loading and parallel updating.
*   [pathogen.vim](https://github.com/tpope/vim-pathogen) is a simple plugin for managing Vim's runtimepath.

#### From Arch repositories

The [vim-plugins](https://www.archlinux.org/groups/x86_64/vim-plugins/) group provides many various plugins. Use `pacman -Sg vim-plugins` command to list available packages which you can then [install](/index.php/Install "Install") with pacman.

### cscope

[Cscope](http://cscope.sourceforge.net/) is a tool for browsing a project. By navigating to a word/symbol/function and calling cscope (usually with shortcut keys) it can find: functions calling the function, the function definition, and more.

[Install](/index.php/Install "Install") the [cscope](https://www.archlinux.org/packages/?name=cscope) package.

Copy the cscope default file where it will be automatically read by Vim:

```
mkdir -p ~/.vim/plugin
wget -P ~/.vim/plugin [http://cscope.sourceforge.net/cscope_maps.vim](http://cscope.sourceforge.net/cscope_maps.vim)

```

**Note:** You will probably need to uncomment these lines in `~/.vim/plugin/cscope_maps.vim` in order to enable cscope shortcuts in Vim 7.x:

```
set timeoutlen=4000
set ttimeout
```

Create a file which contains the list of files you wish cscope to index (cscope can handle many languages but this example finds _.c_, _.cpp_ and _.h_ files, specific for C/C++ project):

```
cd _/path/to/project/dir_
find . -type f -print | grep -E '\.(c(pp)?|h)$' > cscope.files

```

Create database files that cscope will read:

```
cscope -bq

```

**Note:** You must browse your project files from this location or set and export the `$CSCOPE_DB` variable, pointing it to the `cscope.out` file.

Default keyboard shortcuts:

```
 Ctrl-\ and
      c: Find functions calling this function
      d: Find functions called by this function
      e: Find this egrep pattern
      f: Find this file
      g: Find this definition
      i: Find files #including this file
      s: Find this C symbol
      t: Find assignments to

```

Feel free to change the shortcuts.

```
#Maps ctrl-c to find functions calling the function
nnoremap <C-c> :cs find c <C-R>=expand("<cword>")<CR><CR>

```

### Taglist

[Taglist](http://vim-taglist.sourceforge.net/) provides an overview of the structure of source code files and allows you to efficiently browse through source code files in different programming languages.

[Install](/index.php/Install "Install") the [vim-taglist](https://www.archlinux.org/packages/?name=vim-taglist) package.

Useful options to be put in `~/.vimrc`:

```
let Tlist_Compact_Format = 1
let Tlist_GainFocus_On_ToggleOpen = 1
let Tlist_Close_On_Select = 1
nnoremap <C-l> :TlistToggle<CR>

```

## See also

### Official

*   [Homepage](http://www.vim.org/)
*   [Documentation](http://vimdoc.sourceforge.net/)
*   [Vim Wiki](http://vim.wikia.com)

### Tutorials

*   [vim Tutorial and Primer](http://www.danielmiessler.com/study/vim/)
*   [vi Tutorial and Reference Guide](http://usalug.org/vi.html)
*   [Graphical vi-Vim Cheat Sheet and Tutorial](http://www.viemu.com/a_vi_vim_graphical_cheat_sheet_tutorial.html)
*   [Vim Introduction and Tutorial](http://blog.interlinked.org/tutorials/vim_tutorial.html)
*   [Open Vim](http://www.openvim.com/) — collection of Vim learning tools
*   [Learn Vim Progressively](http://yannesposito.com/Scratch/en/blog/Learn-Vim-Progressively/)
*   [know vim](http://www.knowvim.com/) <sup>[[dead link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot") 2014-10-29]</sup>
*   [Learning Vim in 2014](http://benmccormick.org/learning-vim-in-2014/)
*   [Seven habits of effective text editing](http://www.moolenaar.net/habits.html)

#### Videos

*   [Vimcasts](http://vimcasts.org/) — screencasts in _.ogg_ format.
*   [Vim Tutorial Videos](http://derekwyatt.org/vim/tutorials/) — covering the basics up to advanced topics.

#### Games

*   [Vim Adventures](http://vim-adventures.com/)
*   [VimGolf](http://vimgolf.com/)

### Example configurations

*   [nion's](http://nion.modprobe.de/setup/vimrc)
*   [A detailed configuration from Amir Salihefendic](http://amix.dk/vim/vimrc.html)
*   [Bart Trojanowski](http://www.jukie.net/~bart/conf/vimrc)
*   [Steve Francia's Vim Distribution](https://github.com/spf13/spf13-vim)
*   [W4RH4WK's Vim configuration](https://github.com/W4RH4WK/dotVim)
*   [Fast vimrc/colorscheme from askapache](http://www.askapache.com/linux/fast-vimrc.html)
*   [Basic vimrc](https://gist.github.com/anonymous/c966c0757f62b451bffa)

### Other

*   [HOWTO Vim](http://www.gentoo-wiki.info/HOWTO_VIM) — Gentoo wiki article which this article was based on (author unknown).
*   [Vivify](http://bytefluent.com/vivify/) — a colorscheme editor for Vim
*   [Usevim](http://www.usevim.com/) — frequently updated blog highlighting plugins, tips, etc
*   [Vim Awesome](http://vimawesome.com/) — a website that lists and ranks Vim plugins by popularity among GitHub users.
*   [Basic Vim Tips](http://bencrowder.net/files/vim-fu/) — a reference chart for Vim, primarily aimed at beginners.
*   [Vim colorscheme tailoring](https://linuxtidbits.wordpress.com/2014/10/14/vim-customize-installed-colorschemes/) — override installed colorscheme to try-out or permanently alter.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Vim&oldid=417505](https://wiki.archlinux.org/index.php?title=Vim&oldid=417505)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Development](/index.php/Category:Development "Category:Development")
*   [Text editors](/index.php/Category:Text_editors "Category:Text editors")

Hidden category:

*   [Pages with dead links](/index.php/Category:Pages_with_dead_links "Category:Pages with dead links")