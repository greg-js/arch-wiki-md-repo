Related articles

*   [List of applications/Documents#Vi text editors](/index.php/List_of_applications/Documents#Vi_text_editors "List of applications/Documents")

[Vim](https://en.wikipedia.org/wiki/Vim_(text_editor) is a terminal text editor. It is an extended version of [vi](https://en.wikipedia.org/wiki/vi "wikipedia:vi") with additional features, including syntax highlighting, a comprehensive help system, native scripting (vimscript), a visual mode for text selection, and comparison of files (vimdiff).

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
    *   [3.1 Clipboard](#Clipboard)
    *   [3.2 Syntax highlighting](#Syntax_highlighting)
    *   [3.3 Indentation](#Indentation)
    *   [3.4 Visual wrapping](#Visual_wrapping)
    *   [3.5 Using the mouse](#Using_the_mouse)
    *   [3.6 Traverse line breaks with arrow keys](#Traverse_line_breaks_with_arrow_keys)
*   [4 Merging files](#Merging_files)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Line numbers](#Line_numbers)
    *   [5.2 Spell checking](#Spell_checking)
    *   [5.3 Saving runtime state](#Saving_runtime_state)
        *   [5.3.1 viminfo files](#viminfo_files)
        *   [5.3.2 Session files](#Session_files)
        *   [5.3.3 Saving cursor position](#Saving_cursor_position)
    *   [5.4 Replace vi command with Vim](#Replace_vi_command_with_Vim)
    *   [5.5 DOS/Windows carriage returns](#DOS/Windows_carriage_returns)
    *   [5.6 Empty space at the bottom of gVim windows](#Empty_space_at_the_bottom_of_gVim_windows)
    *   [5.7 Vim as a pager](#Vim_as_a_pager)
*   [6 Plugins](#Plugins)
    *   [6.1 Installation](#Installation_2)
        *   [6.1.1 Using the built-in package manager](#Using_the_built-in_package_manager)
        *   [6.1.2 Using a plugin manager](#Using_a_plugin_manager)
        *   [6.1.3 From Arch repositories](#From_Arch_repositories)
    *   [6.2 cscope](#cscope)
    *   [6.3 Taglist](#Taglist)
*   [7 See also](#See_also)
    *   [7.1 Official](#Official)
    *   [7.2 Tutorials](#Tutorials)
        *   [7.2.1 Videos](#Videos)
        *   [7.2.2 Games](#Games)
    *   [7.3 Configuration](#Configuration_2)
        *   [7.3.1 Colors](#Colors)

## Installation

[Install](/index.php/Install "Install") one of the following packages:

*   [vim](https://www.archlinux.org/packages/?name=vim) — with Python 2/3, Lua, Ruby and Perl interpreters support but without GTK/X support.
*   [gvim](https://www.archlinux.org/packages/?name=gvim) — which also provides the same as the above `vim` package with GTK/X support.

**Note:**

*   The [vim](https://www.archlinux.org/packages/?name=vim) package is built without [Xorg](/index.php/Xorg "Xorg") support; specifically the `+clipboard` feature is missing, so Vim will not be able to operate with the *primary* and *clipboard* [selection buffers](/index.php/Clipboard "Clipboard"). The [gvim](https://www.archlinux.org/packages/?name=gvim) package provides also the CLI version of Vim with the `+clipboard` feature.
*   The unofficial repository [herecura](/index.php/Unofficial_user_repositories#herecura "Unofficial user repositories") also provides a number of Vim/gVim variants: `vim-cli`, `vim-gvim-common`, `vim-gvim-gtk`, `vim-gvim-qt`, `vim-rt` and `vim-tiny`.

## Usage

For a basic overview on how to use Vim, follow the vim tutorial by running either *vimtutor* (for the terminal version) or *gvimtutor* (for the graphical version).

Vim includes a broad help system that can be accessed with the `:h *subject*` command. Subjects include commands, configuration options, key bindings, plugins etc. Use the `:h` command (without any subject) for information about the help system and jumping between subjects.

## Configuration

Vim's user-specific configuration file is located in the home directory: `~/.vimrc`, and Vim files of current user are located inside `~/.vim/`. The global configuration file is located at `/etc/vimrc`. Global Vim files are located inside `/usr/share/vim/`.

**Note:** Commonly expected behavior such as syntax highlighting is enabled in `defaults.vim`, which is loaded when no `~/.vimrc` is present. Add `let skip_defaults_vim=1` to `/etc/vimrc` to disable loading of `defaults.vim` completely. [[1]](https://github.com/vim/vim/issues/1033)

### Clipboard

Vim commands such as `:yank` or `:paste` operate with the unnamed register, which by default corresponds to the `"*` register. If the `+clipboard` feature is available, the `"*` register is reflected to the `PRIMARY` buffer in X.

To change the default register, you can `:set clipboard=unnamedplus` to use the `"+` register instead. The `"+` register corresponds to the `CLIPBOARD` buffer in X.

For more information, see `:help 'clipboard'`.

**Tip:** Custom shortcuts for copy and paste operations can be created. See e.g. [[2]](http://superuser.com/a/189198) for binding `Ctrl+c`, `Ctrl+v` and `Ctrl+x`.

### Syntax highlighting

To enable syntax highlighting for many programming languages:

```
:filetype plugin on
:syntax on

```

### Indentation

The indent file for specific file types can be loaded with:

```
:filetype indent on

```

### Visual wrapping

The `wrap` option is on by default, which instructs Vim to wrap lines longer than the width of the window, so that the rest of the line is displayed on the next line. The `wrap` option only affects how text is displayed, the text itself is not modified.

The wrapping normally occurs after the last character that fits the window, even when it is in the middle of a word. More intelligent wrapping can be controlled with the `linebreak` option. When it is enabled with `set linebreak`, the wrapping occurs after characters listed in the `breakat` string option, which by default contains a space and some punctuation marks (see `:help breakat`).

Wrapped lines are normally displayed at the beginning of the next line, regardless of any indentation. The [breakindent](https://retracile.net/wiki/VimBreakIndent) option instructs Vim to take indentation into account when wrapping long lines, so that the wrapped lines keep the same indentation of the previously displayed line. The behaviour of `breakindent` can be fine-tuned with the `breakindentopt` option, for example to shift the wrapped line another four spaces to the right for Python files (see `:help breakindentopt` for details):

```
autocmd FileType python set breakindentopt=shift:4

```

### Using the mouse

Vim has the ability to make use of the mouse, but it only works for certain terminals:

*   [xterm](/index.php/Xterm "Xterm")/[urxvt](/index.php/Urxvt "Urxvt")-based terminal emulators
*   Linux console with [gpm](https://www.archlinux.org/packages/?name=gpm) (see [Console mouse support](/index.php/Console_mouse_support "Console mouse support") for details)
*   [PuTTY](/index.php/PuTTY "PuTTY")

To enable this feature, add this line into `~/.vimrc`:

```
set mouse=a

```

The `mouse=a` option is set in `defaults.vim`.

**Note:** Copy/paste will use the `"*` register if there is access to an X server, see the [#Clipboard](#Clipboard) section. The xterm handling of the mouse buttons can still be used by keeping the `shift key` pressed.

### Traverse line breaks with arrow keys

By default, pressing `←` at the beginning of a line, or pressing `→` at the end of a line, will not let the cursor traverse to the previous, or following, line.

The default behavior can be changed by adding `set whichwrap=b,s,<,>,[,]` to your `~/.vimrc` file.

## Merging files

Vim includes a diff editor (a program that shows differences between two or more files and aids to conveniently merge them). Use *vimdiff* to run the diff editor — just specify some couple of files to it: `vimdiff *file1* *file2*`. Here is the list of *vimdiff*-specific commands.

| Action | Shortcut |
| next change | `]c` |
| previous change | `[c` |
| diff obtain | `do` |
| diff put | `dp` |
| fold open | `zo` |
| fold close | `zc` |
| rescan files | `:diffupdate` |

## Tips and tricks

### Line numbers

To show the line number column, use `:set number`. By default absolute line numbers are shown, relative numbers can be enabled with `:set relativenumber`.

Jumping to a specific line is possible with `:*line number*` or `*line number*gg`. Jumps are remembered in a jump list, see `:h jump-motions` for details.

### Spell checking

Vim has the ability to do spell checking, enable by entering:

```
set spell

```

By default, only English language dictionaries are installed. More dictionaries can be found in the [official repositories](/index.php/Official_repositories "Official repositories") by searching for `vim-spell`. Additional dictionaries can be found in the [Vim's FTP archive](http://ftp.vim.org/vim/runtime/spell/). Additional dictionaries can be put in the folder `~/.vim/spell/` and enabled with the command: `:setlocal spell spelllang=*en_us*` (replacing the `*en_us*` with the name of the needed dictionary).

| Action | Shortcut |
| next spelling | `]s` |
| previous spelling | `[s` |
| spelling suggestions | `z=` |
| spelling good, add | `zg` |
| spelling good, session | `zG` |
| spelling wrong, add | `zw` |
| spelling wrong, session | `zW` |
| spelling repeat all in file | `:spellr` |

**Tip:**

*   To enable spelling in two languages (for instance English and German), add `set spelllang=*en,de*` into your `~/.vimrc` or `/etc/vimrc`, and then restart Vim.
*   You can enable spell checking for arbitrary file types (e.g. *.txt*) by using the FileType plugin and a custom rule for file type detection. To enable spell checking for any file ending with *.txt*, create the file `/usr/share/vim/vimfiles/ftdetect/plaintext.vim`, and insert the line `autocmd BufRead,BufNewFile *.txt setfiletype plaintext` into that file. Next, insert the line `autocmd FileType plaintext setlocal spell spelllang=*en_us*` into your `~/.vimrc` or `/etc/vimrc`, and then restart Vim. Alternatively, one can simply insert the line `autocmd BufRead,BufNewFile *.txt setlocal spell` into their `~/.vimrc` or `/etc/vimrc`, and then restart Vim. Be sure to edit this line (specifically `*.txt`) to include the filetype(s) intended for spell checking.
*   To enable spell checking for LaTeX (or TeX) documents only, add `autocmd FileType **tex** setlocal spell spelllang=*en_us*` into your `~/.vimrc` or `/etc/vimrc`, and then restart Vim.

### Saving runtime state

Normally, exiting `vim` discards all unessential information such as opened files, command line history, yanked text etc. Preserving these information can be configured in the following ways.

#### viminfo files

The `viminfo` file may also be used to store command line history, search string history, input-line history, registers' content, marks for files, location marks within files, last search/substitute pattern (to be used in search mode with `n` and `&` within the session), buffer list, and any global variables you may have defined. For the `viminfo` modality to be available, the version of `vim` you installed must have been compiled with the `+viminfo` feature.

Configure what is kept in your `viminfo` file, by adding (for example) the following to your `~/.vimrc` file:

```
set viminfo='10,<100,:100,%,n~/.vim/.viminfo

```

where each parameter is preceded by an identifier:

```
 'q  : q, number of edited file remembered
 <m  : m, number of lines saved for each register
 :p  : p, number of  history cmd lines remembered
 %   : saves and restore the buffer list
 n...: fully qualified path to the viminfo files (note that this is a literal "*n*")

```

See the official [viminfo documentation](http://vimdoc.sourceforge.net/htmldoc/options.html#'viminfo') for particulars on how a pre-existing `viminfo` file is modified as it is updated with current session information, say from several buffers in the current session you are in the process of exiting.

#### Session files

Session files can be used to save the state of any number of particular sessions over time. One distinct session file may be used for each session or project of your interest. For that modality to be available, the version of `vim` you installed must have been compiled with the `+mksession` feature.

Within a session, `:mksession[!] [*my_session_name.vim*]` will write a vim-script to `*my_session_name.vim*` in the current directory, or `Session.vim` by default if you choose *not* to provide a file name. The optional `!` will clobber a pre-existing session file with the same name and path.

A `vim` session can be resumed either when starting *vim* from terminal:

```
$ vim -S [*my_session_name.vim*]

```

Or in an already opened session buffer by running the vim command:

```
:source *my_session_name.vim*

```

Exactly what is saved and additional details on session files options are extensively covered in the [vim documentation](http://vimdoc.sourceforge.net/htmldoc/usr_21.html#21.4). Commented examples are found [here](http://vim.wikia.com/wiki/Go_away_and_come_back).

#### Saving cursor position

See [Restore cursor to file position in previous editing session](http://vim.wikia.com/wiki/Restore_cursor_to_file_position_in_previous_editing_session) on the Vim wiki.

### Replace vi command with Vim

Create an [alias](/index.php/Alias "Alias") for `vi` to `vim`.

Alternatively, if you want to be able to type `sudo vi` and get `vim`, install [vi-vim-symlink](https://aur.archlinux.org/packages/vi-vim-symlink/) which will remove `vi` and replace it with a symlink to `vim`.

### DOS/Windows carriage returns

If there is a `^M` at the end of each line then this means you are editing a text file which was created in MS-DOS or Windows. This is because in Linux only a single line feed character (LF) used for line break, but in Windows/MS DOS systems they are using a sequence of a carriage return (CR) and a line feed (LF) for the same. And this carriage returns are displayed as `^M`.

To remove all carriage returns from a file do:

```
:%s/^M//g

```

Note that there `^` is a control letter. To enter the control sequence `^M` press `Ctrl+v,Ctrl+m`.

Alternatively install the package [dos2unix](https://www.archlinux.org/packages/?name=dos2unix) and run `dos2unix *file*` to fix the file.

**Note:** Another simple way is by changing `fileformat` setting. `set ff=unix` to convert files with DOS/Windows line ending to Unix line ending. To do the reverse, just issue `set ff=dos` to convert files with Unix line ending to DOS/Windows line ending.

### Empty space at the bottom of gVim windows

When using a [window manager](/index.php/Window_manager "Window manager") configured to ignore window size hints, gVim will fill the non-functional area with the GTK theme background color.

The solution is to adjust how much space gVim reserves at the bottom of the window. Put the following line in `~/.vimrc`:

```
set guiheadroom=0

```

**Note:** If you set it to zero, you will not be able to see the bottom horizontal scrollbar.

### Vim as a pager

Using scripts Vim can be used as a [terminal pager](/index.php/Terminal_pager "Terminal pager"), so that you get various vim features such as color schemes.

Vim comes with the `/usr/share/vim/vim81/macros/less.sh` script, for which you can create an [alias](/index.php/Alias "Alias").

Alternatively there is also the [vimpager](https://www.archlinux.org/packages/?name=vimpager) Vim script. To change the default pager, [export](/index.php/Export "Export") the `PAGER` environment variable.

## Plugins

Adding plugins to Vim can increase your productivity. Plugins can alter Vim's UI, add new commands, code completion support, integrate other programs and utilities with Vim, add support for additional languages and more.

**Tip:** For a list of popular plugins, see [Vim Awesome](http://vimawesome.com/)

### Installation

#### Using the built-in package manager

Vim 8 added the possibility to load natively third-party plugins. It is possible to use this functionality by storing third-party packages in `~/.vim/pack/foo`.

#### Using a plugin manager

A plugin manager installs and manages Vim plugins in a similar way independent of which platform on you are running Vim. It is a plugin that acts as a package manager for other Vim plugins.

*   [Vundle](https://github.com/gmarik/Vundle.vim) is currently the most popular plugin manager for Vim.
*   [Vim-plug](https://github.com/junegunn/vim-plug) is a minimalist Vim plugin manager with many features like on-demand plugin loading and parallel updating.
*   [pathogen.vim](https://github.com/tpope/vim-pathogen) is a simple plugin for managing Vim's runtimepath.
*   [Dein.vim](https://github.com/Shougo/dein.vim) is a plugin manager replacing [NeoBundle](https://github.com/Shougo/neobundle.vim), available as [vim-dein-git](https://aur.archlinux.org/packages/vim-dein-git/).

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

Create a file which contains the list of files you wish cscope to index (cscope can handle many languages but this example finds *.c*, *.cpp* and *.h* files, specific for C/C++ project):

```
cd */path/to/project/dir*
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
*   [Vim Scripts](http://www.vim.org/scripts/)

### Tutorials

*   [vim Tutorial and Primer](https://danielmiessler.com/study/vim/)
*   [vi Tutorial and Reference Guide](http://usalug.org/vi.html)
*   [Graphical vi-Vim Cheat Sheet and Tutorial](http://www.viemu.com/a_vi_vim_graphical_cheat_sheet_tutorial.html)
*   [Vim Introduction and Tutorial](http://blog.interlinked.org/tutorials/vim_tutorial.html)
*   [Open Vim](http://www.openvim.com/) — collection of Vim learning tools
*   [Learn Vim Progressively](http://yannesposito.com/Scratch/en/blog/Learn-Vim-Progressively/)
*   [Learning Vim in 2014](http://benmccormick.org/learning-vim-in-2014/)
*   [Seven habits of effective text editing](http://www.moolenaar.net/habits.html)
*   [Basic Vim Tips](http://bencrowder.net/files/vim-fu/)
*   [HOWTO Vim](http://www.gentoo-wiki.info/HOWTO_VIM)

#### Videos

*   [Vimcasts](http://vimcasts.org/) — screencasts in *.ogg* format.
*   [Vim Tutorial Videos](http://derekwyatt.org/vim/tutorials/) — covering the basics up to advanced topics.

#### Games

*   [Vim Adventures](http://vim-adventures.com/)
*   [VimGolf](http://vimgolf.com/)

### Configuration

*   [nion's](https://web.archive.org/web/20131020125020/http://nion.modprobe.de/setup/vimrc)
*   [A detailed configuration from Amir Salihefendic](https://web.archive.org/web/20170222115910/http://amix.dk/vim/vimrc.html)
*   [Bart Trojanowski](https://web.archive.org/web/20131004071740/http://www.jukie.net/~bart/conf/vimrc)
*   [Steve Francia's Vim Distribution](https://github.com/spf13/spf13-vim)
*   [Vim Awesome](http://vimawesome.com/) - Vim Plugins
*   [W4RH4WK's Vim configuration](https://github.com/W4RH4WK/dotVim)
*   [Fast vimrc/colorscheme from askapache](https://www.askapache.com/linux/fast-vimrc/)
*   [Basic vimrc](https://gist.github.com/anonymous/c966c0757f62b451bffa)
*   [Usevim](http://www.usevim.com/)

#### Colors

*   [Vivify](http://bytefluent.com/vivify/)
*   [Vim colorscheme customization](https://linuxtidbits.wordpress.com/2014/10/14/vim-customize-installed-colorschemes/)